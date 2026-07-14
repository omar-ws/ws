# COLINHA 2 — REDES (VPC, SG, ENDPOINTS, TGW, CLOUDFRONT, RDS PROXY)
> Abrir em RAW e usar Ctrl+F pelas palavras-chave da linha `##` de cada bloco.

---

## SG CRACHÁ | security group aponta security group | origem = SG | camadas
- SG com ORIGEM = outro SG é um CRACHÁ, não um lugar: "aceito 3306 só de quem VESTE o SG X"
- Padrão de camadas: `[SG-ALB: 80 de 0.0.0.0/0] → ALB → [SG-App: 8080 SÓ do SG-ALB] → App → [SG-DB: 3306 SÓ do SG-App] → DB`
- SG é STATEFUL: resposta volta sozinha — só escrever as regras de ENTRADA, egress padrão liberado já resolve
- `0.0.0.0/0` só aparece UMA vez na cadeia (entrada do ALB externo)
- ⚠️ Crachá SG→SG só funciona DENTRO da mesma VPC. Entre VPCs (via TGW/peering) = origem por CIDR na mão
- ping = ICMP (não é TCP/UDP) — liberar "All ICMP - IPv4" quando validador usa ping

## RDS PROXY | Lambda RDS | DB_ENDPOINT | token IAM | generate_db_auth_token
Cadeia completa: `Lambda (VPC + subnets + DBClientSG) --token IAM--> Proxy (RDSProxySG + secret via RDSProxyRole) --senha do secret--> RDS (SG aceita 3306 do RDSProxySG)`
- **Env var da Lambda: `DB_ENDPOINT` = endpoint do PROXY** (não do RDS!). Porta 3306/nome/usuário ficam iguais
- Código usa `rds.generate_db_auth_token(...)` = autenticação IAM (token ~15min como senha) → role da Lambda precisa de `rds-db:connect`; proxy com autenticação IAM = Obrigatória
- Quem lê o Secrets Manager é O PROXY (via RDSProxyRole) — por isso o código não chama secret
- Só 2 regras de ENTRADA: RDSProxySG aceita 3306 de DBClientSG; SG do RDS aceita 3306 do RDSProxySG
- Por que existe: Lambda escala pra centenas de execuções e afoga o limite de conexões do RDS (proxy = gerente de conexões)
- SG ≠ permissão de secret (SG = rede; secret = IAM)

## SINTOMA DIZ A CAMADA | timeout vs AccessDenied | diagnóstico rede
- **Timeout** = REDE (SG, subnet, rota, endpoint faltando)
- **AccessDenied / não autorizado** = IAM (política, role, trust)
- Lambda em VPC + timeout falando com serviço AWS = falta VPC endpoint OU SG do endpoint sem entrada 443 do SG da Lambda

## VPC ENDPOINTS | Gateway vs Interface | PrivateLink | prefix list
- **Gateway Endpoint**: SÓ S3 e DynamoDB. GRATUITO. Vira ROTA na route table (sem ENI, sem SG)
- **Interface Endpoint**: demais serviços (SSM, Secrets, Bedrock, SQS...). PAGO. Cria ENI com IP privado + SG (entrada TCP 443 do SG de quem chama). DNS privado resolve sozinho — código não muda
- Restringir Lambda→DynamoDB só pela REDE: regra de SAÍDA (egress) no SG da Lambda → destino = **prefix list do DynamoDB (pl-...)**, porta 443. (Mesma peça pra CloudFront em regra de entrada)
- Pesquisa: `security group dynamodb prefix list`

## TRANSIT GATEWAY | TGW route table | propagações | 2 decisões
- 2 decisões em cadeia: (1) route table da SUBNET manda pro `tgw-...`; (2) **TGW route table** (menu próprio: "Tabelas de rotas do gateway de trânsito") escolhe o attachment de saída
- Rotas de IDA E VOLTA nas 2 VPCs apontando pro tgw- (CIDR da VPC destino, nunca 0.0.0.0/0 se proibido)
- **Propagações / Propagations**: attachment anuncia o CIDR da VPC SOZINHO (vs estática = você escreve e mantém). Enunciado proíbe estática → aba Propagações
- Sintoma: "rota da subnet ok + ping não vai" = TGW RT vazia ou SG sem ICMP
- Validador conta pacotes → deixar ping rodando 5-10 min
- Rota aponta pra CIDR da REDE (10.1.0.0/16), não pra IP de instância

## ROTA MAIS ESPECÍFICA | longest prefix match | rota interceptadora
- /24 vence /16; /32 vence tudo. "Tudo ativo mas tráfego some" → procurar rota MAIS ESPECÍFICA sequestrando o destino → remover a interceptadora
- Vale pra route table de VPC, de TGW e do Windows

## ROUTE WINDOWS | route print | metadados 169.254.169.254 | IMDS
```powershell
route print                          # gateway certo = linha do destino 0.0.0.0
route DELETE 169.254.169.254
route -p ADD 169.254.169.254 MASK 255.255.255.255 <gateway>
iwr -uri 'http://169.254.169.254/latest/meta-data/'   # tem que dar StatusCode: 200
Restart-Service AmazonSSMAgent       # se não validar
```
- `-p` = persistente | é `-uri`, não `-url` | 169.254.169.254 = link-local, SÓ de dentro da instância
- RDP = porta 3389, origem "Meu IP"

## NAT | NAT Gateway zonal | route table decide
- NAT vive numa AZ (zonal), fica em subnet PÚBLICA; quem decide quem usa é a ROUTE TABLE da subnet privada (`0.0.0.0/0 → nat-...`)
- Migrar NAT = trocar o alvo da rota | Subnet sem associação explícita cai na MAIN route table
- Lambda em VPC que precisa de internet = subnet PRIVADA + NAT (subnet pública NÃO funciona — Lambda não ganha IP público)
- IPv6 saída-somente = **Egress-Only IGW** (gratuito): `::/0 → eigw-...`

## PEERING vs TGW vs PRIVATELINK | conectar VPCs
- Poucas VPCs = Peering (barato, SEM transitividade, rotas manuais nos 2 lados)
- Muitas VPCs / transitividade = Transit Gateway
- **CIDRs SOBREPOSTOS = PrivateLink** (expõe só 1 serviço via endpoint)

## CLOUDFRONT | OAI | OAC | Origin path | Default root object | 403
- **3 caminhos**: URL já traz o caminho → NADA | esconder pasta da URL → **Origin path** (Edit origin — prefixo escondido em toda requisição) | raiz `/` servir arquivo → **Default root object** (Edit settings)
- **OAI (legado / Identidades antigas)**: bucket policy com Principal pseudo-usuário `arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity <ID>` (ID em CloudFront → Segurança → Acesso à origem)
- **OAC (novo)**: Principal `Service: cloudfront.amazonaws.com` + Condition `AWS:SourceArn` = ARN da distribuição
- Console oferece atualizar a bucket policy sozinho — CONFERIR ("No, I will update" é o defeito clássico)
- **403 atrás de CloudFront → 1ª suspeita = bucket policy da origem**
- **PROPAGAÇÃO**: mudança fica "Implantando/Deploying" por minutos — ESPERAR antes de testar (senão desfaz coisa certa)
- Task de HTTPS: Behavior → Viewer Protocol Policy → Redirect/HTTPS only
- Proteger origem: L4 = SG do ALB com prefix list do CloudFront | L7 = custom header secreto no CloudFront + listener rule no ALB (aceita só com header, default 403)

## ALB NLB | listener rules | dualstack | health check
- ALB = L7 HTTP/HTTPS (path, host, header) | NLB = L4 TCP/UDP (IP/porta, rápido, IP estático)
- Listener rules: prioridade 1 avaliada primeiro; default por último
- Dualstack: EC2 → Load Balancers → editar tipo de IP; target group tem tipo de IP próprio; testar `curl -4` / `curl -6`
- ASG + ALB: habilitar "verificações de integridade do ELB" senão ASG não substitui instância com app quebrado
- Health check: caminho `/health`, código 200 | Target group "unhealthy" → olhar SG da instância (entrada da porta do app SÓ do SG do ALB)

## LAMBDA EM VPC | ENI | subnets | SG da Lambda
- Lambda em VPC ganha ENI nas subnets escolhidas + SG próprio — conferir: VPC certa, subnets certas, **SG "crachá" certo anexado** (config VPC da Lambda)
- Acessar serviço AWS de dentro: VPC endpoint (ver bloco acima) | Acessar internet: subnet privada + NAT
- Env var pertence a quem LÊ (o código da Lambda)

## DELETAR VPC | dependências | ordem de deleção
1. Peering → 2. NAT (esperar Deleted, liberar EIP) → 3. desassociar+deletar IGW → 4. subnets → 5. route tables custom → 6. SGs custom → 7. VPC
- SG que não deleta = algo referencia → EC2 → Network Interfaces → filtrar pelo SG → terminar instância/desassociar ENI

## VPC FLOW LOGS | quando usar
- Metadados de tráfego (IP, porta, ACCEPT/REJECT) — nível VPC/subnet/ENI — destino CloudWatch (via role) ou S3 (via bucket policy)
- Usar quando NÃO acha o erro em SG/NACL/rota — mostra onde o pacote morre


## SSM SEM INTERNET | Fleet Manager vazio | Session Manager | 3 endpoints | instancia nao aparece
Receita EC2 privada acessivel via SSM (Fleet Manager / Session Manager), sem internet:
1. **Role na EC2**: `AmazonSSMManagedInstanceCore` (instance profile)
2. **3 Interface Endpoints**: `ssm` + `ssmmessages` + `ec2messages` (com **DNS privado LIGADO**)
3. **1 SG so pros 3 endpoints**: ENTRADA 443, origem = SG da EC2 (crachá) — NAO precisa 1 SG por endpoint
4. **Paciencia**: instancia que ganhou role/endpoint DEPOIS de criada demora minutos pra aparecer; se demorar, reiniciar o agente (`Restart-Service AmazonSSMAgent` / `sudo systemctl restart amazon-ssm-agent`)
- QUEM INICIA e a EC2 (o agente DENTRO dela liga pra fora perguntando "tem ordem?") — o servico NUNCA disca pra instancia; seu comando pega carona na RESPOSTA da conexao que o agente ja abriu
- **NAO EXISTE regra de volta em SG** (stateful: aonde vai, volta) — saida do endpoint / entrada na EC2 = nao escrever. Regra de volta e coisa de NACL (stateless), nao de SG
- ⚠️ **PEGADINHA: endpoint criado SEM escolher SG pega o SG DEFAULT da VPC** — e o default so aceita entrada de quem TAMBEM veste o default. EC2 com outro SG = bloqueada = Fleet Manager vazio com tudo "parecendo certo"
- Se nao puder CRIAR SG: (a) EDITAR regras de um SG existente (quase sempre permitido), ou (b) por o MESMO SG da EC2 no endpoint + regra de entrada 443 com origem = ele mesmo (auto-referencia)
- Pesquisa: `ec2 private subnet ssm vpc endpoints fleet manager`

## SQL SERVER NA EC2 | RDP + SSMS | select no banco | portas de banco
- Banco **SQL Server** em EC2 Windows: caminho esperado = **RDP na maquina + ferramenta GRAFICA (SSMS / SQL Server Management Studio)** — nao e mysql no terminal! (terminal seria `sqlcmd`, mas o grafico e o caminho)
- `mysql -u admin -p --host <endpoint>` = so MySQL/MariaDB. Cada banco tem seu cliente
- SELECT basico: `SELECT * FROM tabela WHERE coluna = 'valor';` | contar: `SELECT COUNT(*) FROM tabela WHERE ...;`
- Portas pra SG: MySQL/Aurora **3306** | SQL Server **1433** | PostgreSQL **5432** | RDP **3389** | SSH **22** | endpoints/APIs AWS **443**
- Regra universal de SG: quem INICIA so precisa de saida (padrao ja libera); quem RECEBE ganha a regra de ENTRADA com origem = SG de quem chama. **1 regra por elo, sempre de entrada, sempre no lado que recebe**


## WAF E CORS | bloquear caminho URI | erro de CORS no navegador
- **WAF (bloquear /pagina sem afetar o resto):** WAF & Shield → Criar Web ACL → associar recurso (ALB ou CloudFront) → Add rule → **Rule builder** → Inspect: **URI path** | Match: Contains | valor: `/info.php` → Action: **Block**. WAF = L7 (vê URL/payload; SG não vê URL)
- **CORS:** erro que só aparece no NAVEGADOR (console F12: "blocked by CORS policy") quando um site chama recurso de OUTRO domínio → bucket → Permissões → CORS:
```json
[{ "AllowedHeaders": ["*"], "AllowedMethods": ["GET"], "AllowedOrigins": ["https://dominio-que-chama.com"], "ExposeHeaders": [] }]
```
- ⚠️ AllowedOrigins = SÓ o domínio, SEM path e SEM barra no final (`/index.html` no origin = erro clássico)
- Objeto 403 público simples pode ser só ACL do objeto (tornar público), não bucket policy — ler o que a task pede
