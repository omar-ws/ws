# COLINHA 3 — DEVOPS, ARQUIVOS DE DEPLOY, GIT, CLI, PYTHON DE JAM
> Abrir em RAW e usar Ctrl+F pelas palavras-chave da linha `##` de cada bloco.

---

## FAMÍLIA CODE | CodeCommit CodeBuild CodeDeploy CodePipeline | quem faz o quê
- **CodeCommit** = repositório git (almoxarifado) | **CodeBuild** = RODA comandos do buildspec, gera artefato (linha de montagem) | **CodeDeploy** = INSTALA artefato em EC2/Lambda/ECS via appspec (instalador com agente+hooks) | **CodePipeline** = esteira que ORQUESTRA os outros (gerente) | **CodeArtifact** = repositório de pacotes/libs
- Artifacts = envelope/correio entre estágios (ficam num S3; estágios são execuções separadas)
- **O arquivo pertence a quem LÊ**: buildspec→CodeBuild | appspec→CodeDeploy | deployspec→ação EC2 do CodePipeline | imagedefinitions→ação ECS do CodePipeline | taskdef→ECS
- Fórmula de pesquisa: `<serviço> <arquivo> example` (ex: `codebuild buildspec example`, `codedeploy ecs appspec example`, `codepipeline ec2 deploy action deployspec`)

## BUILDSPEC | buildspec.yml | ECR docker push | imagedefinitions
```yaml
version: 0.2
phases:
  pre_build:
    commands:
      - aws ecr get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $ECR_URI
  build:
    commands:
      - docker build -t $ECR_URI:latest .
      - docker tag $ECR_URI:latest $ECR_URI:$CODEBUILD_RESOLVED_SOURCE_VERSION
  post_build:
    commands:
      - docker push $ECR_URI:latest
      - printf '[{"name":"NOME-DO-CONTAINER","imageUri":"%s"}]' $ECR_URI:latest > imagedefinitions.json
artifacts:
  files: imagedefinitions.json
```
- `env:` CRIA variável; `$` USA ("cifrão é buraco, env é massa") — não misturar 2 exemplos da doc
- `artifacts` = lista de empacotamento (não cria nada; o printf cria o bilhete)
- **imagedefinitions.json usa o nome do CONTAINER** (não da task definition!)
- Fonte: tutorial `codepipeline ecs tutorial imagedefinitions`

## CONTAINER NAME 3 LUGARES | consistency ECS CodePipeline
O nome do container DEVE ser IGUAL em: (1) task definition `containerDefinitions[].name`, (2) `imagedefinitions.json`, (3) serviço ECS (`--load-balancers containerName=`) — divergiu = recriar o serviço

## APPSPEC EC2 | zip raiz | hooks | estrutura do pacote
```
source.zip
├── appspec.yml          ← NA RAIZ do zip (não dentro de pasta!)
└── deploy/
    ├── applicationstop.sh
    ├── beforeinstall.sh
    └── applicationstart.sh
```
- ⚠️ Windows: NÃO zipar a pasta-mãe — selecionar os itens (Ctrl+clique) → Enviar para → Pasta compactada
- Hooks: ApplicationStop, BeforeInstall, ApplicationStart (location = caminho do .sh dentro do zip)

## APPSPEC LAMBDA | blue green | alias | TargetVersion
- Deployment Group vinculado ao ALIAS da Lambda (não à função)
- AppSpec mapeia: `FunctionName` + `Alias` (ex: LIVE) + `CurrentVersion` + `TargetVersion`
- Fluxo: atualizar código → publicar VERSÃO nova → CodeDeploy faz traffic shifting do alias
- Alias = ponteiro nomeado pra versão específica

## DEPLOYSPEC | ação de deploy EC2 do CodePipeline | BeforeDeploy AfterDeploy
- `deployspec.yml` na RAIZ do pacote + scripts .sh referenciados nos hooks **BeforeDeploy** (instala servidor) / **AfterDeploy** (inicia servidor)
- Empacotar TUDO junto (html/css/js + deployspec + .sh) → enviar pro bucket de origem do pipeline
- Pesquisa: `codepipeline ec2 deploy action deployspec`

## TASK DEFINITION | taskdef | register-task-definition | Fargate
- Campos-chave: `family`, `containerDefinitions[].name` + `image` + `portMappings`, `cpu`/`memory` (256 = 0.25 vCPU!), `executionRoleArn` = ECSTaskExecutionRole, `taskRoleArn` = ECSTaskRole, `networkMode: awsvpc` (Fargate), `requiresCompatibilities: ["FARGATE"]`
- CLI: `aws ecs register-task-definition --cli-input-json file://taskdef.json`
- Doc com exemplos: `ecs task definition examples` — "no final da documentação tem exemplos"
- Hierarquia: Cluster → Service → Task → Container | Criar: Cluster → Task Definition → Service
- Ler notação da doc: `"campo": string` = valor com aspas | `integer` = sem aspas | Required: No = pode omitir | valid values = enum EXATO

## CODEPIPELINE CONFIGS DE PROVA | aprovação manual | canary | deploy ECS
- **Aprovação manual**: ação DENTRO da stage de Prod (não stage separada!), run order ANTES do deploy
- **Canary/traffic shifting Lambda**: editar a ação de deploy → Action provider = **AWS CodeDeploy** (application + deployment group + deployment config LambdaCanary...)
- **Deploy ECS**: ação "Amazon ECS" com cluster + service + imagedefinitions.json; **Input artifact = BuildArtifact** (nunca SourceArtifact!)
- **Deploy EC2**: ação precisa do TARGET GROUP do ALB (controle de tráfego/drain)
- Paralelo = mesmo run order | Pipeline aponta pra UMA branch (main vs master!)
- Pegadinha do console: ao salvar Source sem mexer, marcar "Nenhuma atualização de recursos necessária"
- Pipeline se EDITA, não se exclui | "Liberar alteração / Release change" roda na mão
- Troubleshooting de build: pular pro FIM do log → achar o comando que falhou → subir → ler o relatório → corrigir

## GIT | comandos | CodeCommit | branch master main
```bash
git config --global user.name "dev" && git config --global user.email "d@d"   # 1ª vez na máquina
git clone <url>                    # baixar repo
pip install git-remote-codecommit  # helper p/ CodeCommit
git clone codecommit::us-east-1://NomeRepo
git status                         # usar TODA HORA
git add .                          # mala: tudo que mudou
git commit -m "mensagem"
git push origin master             # CONFERIR o nome da branch antes!
git branch                         # em qual estou (asterisco)
git checkout -b nova               # criar e mudar
git remote -v                      # endereços | set-url origin <url> troca
```
Pegadinhas vividas: pasta vazia é INVISÍVEL | "nothing to commit" = faltou add | "src refspec main does not match any" = branch é master OU sem commit | 403 no push = sem identidade IAM | pipeline não dispara = push na branch errada

## CLI ANATOMIA | aws comando | 3 formatos de nome
- `aws <serviço> <ação> --flag valor` | flags globais: `--region --output --query --filters`
- Nome da ação em 3 letras: doc/API = `ValidatePolicy` (PascalCase) | boto3 = `validate_policy` (snake_case) | CLI = `validate-policy` (kebab-case)
- `--query "Functions[0].FunctionName"` filtra saída | `--cli-input-json file://arquivo.json` passa JSON
- ⚠️ JSON complexo no PowerShell QUEBRA (come as aspas) → usar CMD com `\"` ou file://
- Fluxo: pesquisar `aws <serviço> <ação>` → CLI Command Reference → Synopsis + Examples no FIM da página
- `aws s3 cp` (upload/download) | `aws s3 sync` (pasta↔bucket) | `aws s3 presign s3://bucket/arq --expires-in 300` (URL temporária de arquivo privado)
- root do Linux ≠ identidade IAM — quem assina a CLI é a ROLE da instância (sudo não resolve AccessDenied)

## CLOUDFORMATION | YAML vs JSON | GetAtt Ref Sub | erros cfn-lint
- Atalhos `!Ref !GetAtt !Sub` são SÓ do YAML — JSON usa `{"Ref": ...}`, `{"Fn::GetAtt": ["Recurso","Arn"]}`, `{"Fn::Sub": ...}`
- `Ref` = ID/nome do recurso (⚠️ Ref de SNS Topic = ARN; Ref de Events::Rule = NOME) | `GetAtt` = atributo específico (ex: `.Arn`) | `Sub` = string com variáveis | `ImportValue` = Output de outra pilha
- Nome LÓGICO (o que você escreveu no template, usado em Ref/GetAtt) vs nome FÍSICO (propriedade Name/gerado)
- `ManagedPolicyArns` anexa política gerenciada a `AWS::IAM::Role`:
```json
"ManagedPolicyArns": [{ "Fn::Sub": "arn:${AWS::Partition}:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole" }]
```
- DeletionPolicy: Delete (padrão) | Retain | Snapshot — mesmo nível do Type
- Conditions = if/else (1 template, 2 ambientes) | Change Set = preview antes de aplicar
- **cfn-lint**: exit codes SOMAM (2 erro + 4 warning = 6) → WARNING TAMBÉM DERRUBA | **cfn_nag**: só FAIL derruba (F1000 = SG sem egress explícito → escrever `SecurityGroupEgress`)
- Erros clássicos: `GetAtt` sem `!` = vira texto literal | `Fn::GetAttr` NÃO existe (é GetAtt) | Runtime é enum exato (`python3.14`, sem espaço)
- "Em JAM, o código do lab é o SUSPEITO, não a referência"

## PYTHON DE JAM | lambda handler | contrato proxy | 403 | return
- Campo **Manipulador/Handler** = `arquivo.função` (ex: `lambda_function.lambda_handler`) — def e campo têm que BATER
- Contrato do proxy (API Gateway): return SEMPRE `{'statusCode': N, 'body': json.dumps(...)}` — chave errada (ex: `message`) = 502
```python
import json

def lambda_handler(event, context):
    print(event)                          # print → CloudWatch Logs
    if event.get("usuario") == "admin":   # == compara (=== NÃO existe em Python)
        return {"statusCode": 200, "body": json.dumps("Bem-vindo!")}
    return {"statusCode": 403, "body": json.dumps("Acesso negado")}
```
- Regras que já me pegaram: `:` só em linha que ABRE bloco (def/if/else/for) | return SEMPRE encerra a função | indentação = paredes | nome se COPIA da ficha, não se deduz (telemtry!) | `json.dumps` com s | import sem usar = pista falsa
- `event` = a requisição em JSON (ficha do ônibus HTTP) | `context` = metadados da execução — os dois são ENTRADAS
- `os.environ["X"]` = lê env var (KeyError = env var não configurada!) | Ctrl+F `environ`/`process.env` acha as chaves que o código lê
- `objeto.metodo(...)` COM () = AÇÃO | `objeto.atributo` sem () = VALOR
- boto3: `client = boto3.client("sns")` → nome = serviço do endpoint | `client.publish(TopicArn=..., Message=...)` — Message obrigatório, Subject opcional
- Ordem dos ifs = prioridade (critical ANTES de warn)

## MAPA DE ERROS API | 500 502 403 | log group diagnóstico
- **500** = API GW nem invocou a Lambda (permissão/integração) — log group da Lambda NEM EXISTE
- **502** = Lambda invocada mas contrato quebrado (erro no código OU return errado) — log group EXISTE
- **403** = resposta PROPOSITAL (Lambda saudável negando)
- **200 no método + "statusCode: 500" no CORPO** = transporte ok, a APLICAÇÃO falhou no elo SEGUINTE → ir no log
- Regra de ouro: a EXISTÊNCIA do log group já é diagnóstico
- 3 jeitos de testar: aba Testar do Lambda (só a função) | aba Testar do API GW (sem deploy, ignora autorização) | Invoke URL (ponta a ponta)

## CRON 3 DIALETOS | EventBridge SSM crontab
| Onde | Campos | "a cada 5 min" |
|---|---|---|
| Linux crontab | 5 | `*/5 * * * *` |
| EventBridge | 6 | `cron(0/5 * * * ? *)` |
| SSM Maintenance Window | **7 (SEGUNDOS na frente)** | `cron(0 0/5 * * * ? *)` |
- Um dos 2 campos de dia TEM que ser `?` | horário em UTC | "todo dia" simples = `rate(1 day)`
- Truque: imitar o EXEMPLO que a própria tela mostra | "rodar em 2 min" → `0/1` a cada minuto (sem conta de fuso)
- EventBridge **Scheduler** (Cronogramas) = assume ROLE (pode dar erro iam:CreateRole em lab) | **Rule clássico** (Regras) = resource policy na Lambda, SEM role → preferir em lab

## REDSHIFT SQL | COPY | GRANT ROLE | query
```sql
COPY nome_tabela
FROM 's3://bucket/pasta/'
IAM_ROLE 'arn:aws:iam::CONTA:role/NomeDaRole'
DELIMITER '|'
IGNOREHEADER 1;

CREATE USER cook PASSWORD 'Senha123!';
CREATE ROLE captain;
GRANT ROLE captain TO cook;

SELECT COUNT(*) FROM sailors WHERE s_segment = 'DIAMOND' AND s_onboard = true;
SELECT * FROM sys_load_error_detail ORDER BY start_time DESC LIMIT 10;  -- erros de carga
```
- Pegadinhas: `iam_role` com ARN COMPLETO (não `credentials`) | apontar pra PASTA (não .tar.gz) | pipe `|` não vírgula
- Doc: `redshift copy syntax`

## MYSQL | mysqldump | migração | macete das setas
```bash
mysqldump --databases loja -u root -p > dump.sql     # > EXPORTA
mysql -u admin -p --ssl --host <ENDPOINT> < dump.sql # < IMPORTA
mysql -u admin -p --host <ENDPOINT>                  # conectar (é --host, não --endpoint)
```
- SG do RDS: entrada 3306 origem = SG da EC2 | `nmap -Pn <endpoint>` testa a porta
- Hierarquia: instância (prédio) → database (andar) → tabela (planilha) — console cria só o SERVIDOR

## LINUX | chmod | logs | systemd | serviços
- `chmod 775` (dono rwx, grupo rwx, outros r-x) | r=4 w=2 x=1 | 644 arquivo normal, 755 pasta pública
- Logs: `sudo tail /var/log/...` | Bitnami: `sudo tail /opt/bitnami/apache/logs/error_log` + `sudo /opt/bitnami/ctlscript.sh restart apache` | normal: `systemctl restart nginx`
- systemd unit em `/etc/systemd/system/nome.service`: `[Unit]` deps, `[Service]` ExecStart= (único obrigatório) + WorkingDirectory (default `/`!), `[Install]` WantedBy — depois `daemon-reload` → `enable` → `start`
- `sudo su` (root) | `su ec2-user` | nano: Ctrl+O salva, Enter, Ctrl+X sai
- Amazon Linux: `sudo yum/dnf install -y` | Ubuntu: `sudo apt install -y`
- SSM Session Manager entra como `ssm-user`

## LOGS INSIGHTS | CloudWatch query | fields filter stats
```
fields @timestamp, @message
| filter eventSource = "ec2.amazonaws.com"
| filter @message like /ERROR/
| sort @timestamp desc
| stats count(*) as total by bin(5m)
| limit 20
```
- Forense CloudTrail: resposta em `userIdentity.principalId` (formato `AROAXXX:nome-da-funcao` — parte DEPOIS dos dois-pontos)
- Trilha pode EXISTIR com logging DESLIGADO → Start logging primeiro


## SQL BÁSICO | select where count insert update | comandos de banco | qual cliente
- Ler tudo: `SELECT * FROM tabela;` | só colunas: `SELECT nome, preco FROM tabela;`
- Filtrar: `SELECT * FROM tabela WHERE coluna = 'valor' AND outra > 10;`
- Contar: `SELECT COUNT(*) FROM tabela WHERE ...;` | ordenar: `ORDER BY coluna DESC` | limitar: `LIMIT 10`
- Inserir: `INSERT INTO tabela (col1, col2) VALUES ('a', 1);`
- Atualizar: `UPDATE tabela SET col = 'novo' WHERE id = 1;` ⚠️ SEM WHERE = altera a tabela INTEIRA
- Apagar: `DELETE FROM tabela WHERE id = 1;`
- Explorar: `SHOW DATABASES;` → `USE banco;` → `SHOW TABLES;` (MySQL) | texto entre 'aspas simples', número sem aspas, `;` no final
- **QUAL CLIENTE PRA QUAL BANCO:** MySQL/MariaDB/Aurora-MySQL = `mysql` no terminal | **SQL Server = RDP + SSMS (gráfico)** (terminal seria sqlcmd) | PostgreSQL = `psql` | Redshift = Query Editor V2 no console
- Pesquisa: `sql select where examples` / `<banco> connect ec2 windows`

## BEDROCK | 3 endpoints | agente | knowledge base | alias | guardrails | preparar
- **3 endpoints:** `bedrock` = CONFIGURAR | `bedrock-runtime` = invocar MODELO | `bedrock-agent-runtime` = invocar AGENTE. Truque: `boto3.client('X')` no código = nome do serviço do endpoint
- Modelo = a IA em si | Agente = orquestra (consulta KB, chama Lambda via action group)
- **FLUXO DO AGENTE (ordem sagrada):** mexeu em QUALQUER coisa → **Preparar (Prepare Agent)** → criar VERSÃO nova → apontar o **ALIAS** pra versão nova. Alias = ponteiro nomeado (igual alias de Lambda). Esquecer o Preparar/alias = mudança não vale
- **KNOWLEDGE BASE:** adicionou/mudou data source → **SINCRONIZAR (Sync)** e ESPERAR concluir — sem sync o agente não acha nada
- **ACTION GROUP:** Agent Builder → Grupos de ação → aqui troca a Lambda invocada; parâmetro exige nome válido + descrição não vazia
- **GUARDRAILS:** se as Output Properties têm um pronto (ex: SecurityGuardrail) = ANEXAR o existente ao agente (+ Preparar + versão + alias)
- ARN de modelo: `arn:aws:bedrock:<região>::foundation-model/<model-id>` (conta VAZIA = `::` duplo) — modelo vai no RESOURCE, Action = verbo limpo (endpoint policy pronta na colinha 1)
- Model ID: catálogo de modelos no console | CLI: `aws bedrock list-foundation-models`
- Pesquisa: `bedrock agent prepare alias` / `bedrock knowledge base sync data source`
