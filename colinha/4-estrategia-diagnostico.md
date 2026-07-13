# COLINHA 4 — ESTRATÉGIA DE PROVA, DIAGNÓSTICO E SERVIÇOS RÁPIDOS
> Abrir em RAW e usar Ctrl+F. LER ESTE ARQUIVO NO CAFÉ DA MANHÃ DO DIA 1.

---

## REGRA DO TEMPO | timer | loop | quando pegar dica | quando pular
- **Timer de 15 min por task** (DuckDuckGo: pesquisar `timer 15 minutes`). Tocou → pergunta única: *"produzi informação NOVA?"*
  - SIM → renova 15 min e segue
  - NÃO (loop) → DICA (é barata: 2-20 pts vs 150 da task travada)
  - Tocou 2x na MESMA task (30 min) → dica OBRIGATÓRIA ou pula, sem negociar
- **LOOP vale mais que relógio: mesmo erro 2x = para NA HORA**
- Fluxo do campeão mundial (validado em prova): tentar → pesquisar (doc/Google, 2 buscas reformuladas) → dica
- Pular = mudar de JAM (tasks do mesmo JAM podem ser encadeadas; dica destrava pré-requisito)
- Conta: 3h/período ÷ 3 JAMs = 1h por JAM ≈ 20-25 min por task. Fácil fecha em 5-10 → gera sobra pra voltar na travada

## ORDEM DO PERÍODO | estratégia dos campeões
1. LER os 3 JAMs antes de começar qualquer um (5 min)
2. Mais FÁCIL primeiro (2 médios antes do hard)
3. Travou → próximo | Voltar depois com a sobra e a cabeça fria
4. Negociar pontos: JAM quase 100% > dois pela metade
5. NÃO olhar pontuação/tempo de adversário ("pode ter feito com dica")

## ANTES DE MEXER | 2 min de mapa | erro de processo
- **2 min de mapa ANTES de agir**: qual serviço → qual fluxo → onde está o log ("leio o enunciado, acho que sei e ignoro o básico" = meu erro conhecido)
- **LER ATÉ O FINAL** — a validação diz ONDE mexer ("quando a POLÍTICA estiver correta" = mexe na política, não no código; o código pode ser só referência!)
- O VERBO do enunciado manda: "excluir"≠"editar" | "atualize"=Update no existente | "crie"=novo | "fornecida"=usa a que existe
- **Ritual dos 2 min antes de enviar: conferir NÚMEROS de conta e NOMES contra o enunciado** (policy perfeita com conta errada = reprovada; já passou batido 2x)
- Backup de 10s: antes de editar política, copiar o JSON original num bloco de notas
- Nomes EXATOS do enunciado (validação é literal) | valor literal com `/*` no enunciado = copiar literal

## MAPA DE SINTOMAS | qual camada | diagnóstico rápido
| Sintoma | Camada / 1ª suspeita |
|---|---|
| Timeout | REDE: SG, subnet, rota, VPC endpoint |
| AccessDenied / not authorized | IAM: ler QUEM + AÇÃO + RECURSO + POR QUÊ (identity vs SCP) |
| 500 (API GW) | nem invocou a Lambda — log group NEM EXISTE |
| 502 (API GW) | Lambda rodou, contrato quebrado — log group EXISTE |
| 200 + "500" no corpo | app falhou no elo SEGUINTE → log |
| KeyError: 'X' (Python) | env var X não configurada |
| Alarme "Dados insuficientes" | namespace OU estatística não batem com o put-metric do código |
| "Configurei e nada acontece, sem erro" | permissão ENTRE serviços faltando (resource policy) |
| 403 atrás de CloudFront | bucket policy da origem (OAI/OAC) |
| "Tudo ativo mas não conecta" | rota mais específica interceptando OU TGW RT vazia |
| Task ECS não inicia | Execution Role | App ECS roda mas não acessa serviço → Task Role |
| Site não muda após fix no CloudFront | propagação "Deploying" — ESPERAR |
| Erro nomeia uma ação (`iam:PassRole`...) | adicionar EXATAMENTE essa ação na política de quem agiu |
- CloudWatch Logs = ferramenta #1. Anotação/log do Config = ler e PESQUISAR a mensagem

## PEGADINHAS | tradução | placeholders | IDs
- **Tradução automática**: "ERA O OBJETIVO"/"eu sou"/"VISAM" na lista de serviços = **IAM** | "NOME_DA_IMAGEM" = IMAGE_NAME (placeholder tem que bater LETRA POR LETRA) — na dúvida, ler o enunciado em INGLÊS
- Traduzir TEXTO em aba separada (página inteira quebra o app React = tela preta)
- Colou exemplo da doc → Ctrl+F "function"/"bucket"/"example" e trocar TUDO
- Todo ID AWS tem prefixo que diz o tipo: `i-` instância, `sg-` SG, `mw-` maintenance window, `pl-` prefix list, `eigw-`, `pcx-`, `tgw-` — ler a DESCRIÇÃO do campo antes de colar
- Console cria permissões escondidas (trigger de Lambda) — em CFN/CLI é na mão
- Guardrails do lab: erro em recurso INTERNO do lab (AwsJamsLab...) = criar recurso NOVO com seu nome, não brigar
- Validador que conta pacotes (ping) → deixar rodando 5-10 min

## ORDEM IMPORTA | sequências que já erraram
- S3 Batch Operations: criptografia padrão do bucket ANTES do job; operação = COPIAR; clicar "Executar trabalho" (não roda sozinho)
- AWS Backup: backup CONCLUÍDO antes de terminar/restaurar
- Permissões: Allow ANTES de remover Deny
- EBS: tags ANTES do modify (validador checa os dois); 6h de espera entre modifies do mesmo volume — capricho na 1ª
- Bedrock KB: SYNC do data source ANTES de usar o agente; agente → Preparar → nova versão → alias
- Aurora Graviton: Modify = instância (com reboot) | trocar WRITER imediato/reversível = **Failover** (target = um reader)

## SERVIÇOS RÁPIDOS | regras de ouro | fatos que caem
- **EBS**: gp3 na quase totalidade | modify NÃO estende partição no SO (Disk Management no Windows) | **EC2**: T2 NUNCA, usar T3
- **S3**: bucket público quase nunca é resposta — CloudFront + OAC + bucket privado
- **Lambda**: timeout máx = 15 min (900s) | env vars = suspeito nº1 | versões+alias | criptografia env vars: repouso KMS + trânsito
- **DynamoDB**: case-sensitive (`Key ≠ key`) | RCU/WCU: arredonda tamanho pra cima (RCU bloco 4KB, WCU 1KB) × qtd/s; eventual = metade; transacional = 2x | GSI = padrão (PK diferente, qualquer hora); LSI = SÓ na criação + mesma PK
- **RDS criptografia**: não ativa direto → snapshot → COPIAR criptografado → restaurar
- **Bedrock 3 endpoints**: `bedrock` = configurar | `bedrock-runtime` = invocar MODELO | `bedrock-agent-runtime` = invocar AGENTE — truque: `boto3.client('X')` do código diz o endpoint
- **SSM Maintenance Window**: prioridade MENOR roda primeiro (iguais = paralelo) | diagnóstico = aba Histórico | cron de 7 campos
- **SQS**: 1 msg → 1 consumidor | Long Polling (Wait Time 20s) corta resposta vazia | Visibility Timeout > tempo de processamento evita duplicata | DLQ sempre
- **SNS fan-out**: 1 tópico → N assinantes (email + filas SQS) | 1 evento → 5 apps = SNS → 5 SQS
- **Config vs CloudTrail**: Config = ESTADO do recurso (compliant?) | CloudTrail = AÇÕES (quem fez o quê) | Config: Reavaliar força checagem | remediação automática = SSM Automation doc
- **CloudWatch alarme custom metric**: alarme e código no MESMO namespace; estatística tem que bater com como o código emite (1 por erro → Soma/Contagem; Média dilui e falha)
- **Route 53**: Failover = primário+secundário c/ health check | Alias pra recursos AWS | NÃO é CDN (isso é CloudFront)
- **ElastiCache** = leitura intensa no RDS (não Multi-AZ, que é só HA)
- **PrivateLink** = VPCs com CIDR sobreposto | **Peering** = poucas VPCs, barato | **TGW** = muitas
- **Cognito** = usuários de APLICAÇÃO | **IAM Identity Center** = funcionários/SSO | **STS** = credenciais temporárias por baixo
- **WAF** = L7 (URI path, SQL injection, associa a ALB/CloudFront) | SG = L4
- **Macie** = PII no S3 | **GuardDuty** = ameaças tempo real | **Inspector** = vulnerabilidades EC2 | **Detective** = investigação | **Security Hub** = painel central
- **Step Functions**: waitForTaskToken = pausar até retorno externo (aprovação por email)
- **DB single-AZ primeiro** (endpoint em ~8 min) → converter Multi-AZ em background (macete de prova, se o enunciado permitir)
- **DB Subnet Group** = lista de subnets ≥2 AZs onde o banco pode subir (criar antes do RDS) | Acesso público: NÃO

## GUARD CONFIG RULE | regra custom Config | DSL
```
let ipv4 = '0.0.0.0/0'
let ipv6 = '::/0'

rule conferir when
    resourceType == "AWS::EC2::SecurityGroup" {
    configuration.ipPermissions empty or
    configuration.ipPermissions[*] {
        ipv6Ranges empty or ipv6Ranges[*].cidrIpv6 != %ipv6
        ipv4Ranges empty or ipv4Ranges[*].cidrIp != %ipv4
    }
}
```
- NÃO é JSON — cola direto na caixa Rule content | avalia o CI (configuration item) do recurso, não template
- Caminho vazio FALHA ("No entries for path") → `empty or` | regra que PASSA = recurso conforme
- `!=` diferente (`===` não existe) | ipPermissions = ENTRADA, ipPermissionsEgress = saída | nomes dos campos: COPIAR do exemplo de CI do enunciado
- Pesquisa: `aws config custom policy guard example security group`

## PROTOCOLO PESSOAL | prova | café | dica de ouro
- Dia 1: SEM cafeína (adrenalina natural) | Dia 2: 200mg + L-teanina no CAFÉ DA MANHÃ (~7h) — dose ÚNICA, NUNCA à tarde, nunca empilhar
- Abafador de ouvido: PERMITIDO ✅ — usar
- Pesquisa: DuckDuckGo (sem IA — nenhuma IA permitida) | doc AWS = fonte nº1
- Se der crise: beber água, respirar. "Os outros também estão nervosos." Não olhar o placar dos outros
- Contra-fato oficial: quinta 0/8 nas piores condições → sábado 5 fechados 48h depois. Circunstância ≠ capacidade
- "Descansar também é preparo: chegar lá e fazer o que já sabe"
