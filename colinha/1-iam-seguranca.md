# COLINHA 1 — IAM E SEGURANÇA
> Abrir em RAW e usar Ctrl+F pelas palavras-chave da linha `##` de cada bloco.

---

## COMO LER POLÍTICA | policy | Effect Action Resource Condition | verbo limpo
- `Action` = SÓ o verbo `serviço:Ação` — NUNCA grudar recurso nela (`bedrock:InvokeModel/modelo` NÃO existe)
- `Resource` = ARN de quem SOFRE a ação
- `Condition` = "só vale QUANDO chave-operador-valor" — ler: operador → chave → valor
- Deny explícito VENCE qualquer Allow. Sem Allow em lugar nenhum = deny implícito
- Allow só o específico → o resto morre no deny implícito (não precisa escrever Deny)
- ORDEM ao corrigir acesso: adiciona o Allow ANTES de remover o Deny (senão se tranca fora)

## OS DOIS ASTERISCOS | * no Resource vs * no Principal
- `*` no **Resource** de política de IDENTIDADE = "essa role age em tudo" (poder demais, NÃO abre pra outras contas)
- `*` no **Principal** de política de RECURSO = "qualquer um acessa" (esse SIM abre pro mundo)
- Cross-account SEMPRE exige os dois lados concordando (role da conta A + resource policy do recurso na conta B)

## IDENTIDADE vs RECURSO | identity policy vs resource-based policy | PUSH PULL
- Política de identidade (na role) = "o que EU posso fazer"
- Política de recurso (no recurso) = "quem pode me CHAMAR"
- **PUSH** (serviço empurra: SNS→Lambda, S3→Lambda, EventBridge Rule→Lambda) = permissão no RECEPTOR via resource policy
- **PULL** (quem busca: Lambda lendo SQS) = permissão na ROLE de quem puxa (Execution Role: ReceiveMessage/DeleteMessage/GetQueueAttributes)
- Console faz o passo escondido no "Adicionar trigger" — no CloudFormation/CLI é NA MÃO

## LAMBDA PERMISSION | resource-based policy Lambda | AWS::Lambda::Permission | SNS invocar Lambda
Bloco CFN (JSON) — SNS → Lambda:
```json
"JamLambdaPermissionForSnsTopic": {
    "Type": "AWS::Lambda::Permission",
    "Properties": {
        "FunctionName": { "Ref": "JamLambdaFunction" },
        "Principal": "sns.amazonaws.com",
        "Action": "lambda:InvokeFunction",
        "SourceArn": { "Ref": "JamSnsTopic" }
    }
}
```
Variante EventBridge → Lambda (com SourceAccount):
```json
"s3Permission": {
    "Type": "AWS::Lambda::Permission",
    "Properties": {
        "FunctionName": { "Fn::GetAtt": ["RepoSetupFunction", "Arn"] },
        "Action": "lambda:InvokeFunction",
        "Principal": "events.amazonaws.com",
        "SourceAccount": { "Ref": "AWS::AccountId" },
        "SourceArn": { "Fn::GetAtt": ["NewRepoRule", "Arn"] }
    }
}
```
- `FunctionName` aceita `Ref` OU `GetAtt Arn` | `Principal` = quem bate na porta (`sns.amazonaws.com`, `events.amazonaws.com`, `s3.amazonaws.com`, `iot.amazonaws.com`)
- `SourceArn` = trava de menor privilégio (NÃO ignorar). Ref de SNS Topic = ARN; Ref de Events::Rule = NOME (usar GetAtt Arn)
- ⚠️ Colou exemplo da doc → Ctrl+F em "function"/"bucket" e trocar TODOS os placeholders pelo nome lógico do template
- Doc: pesquisar `aws lambda permission cloudformation`

## PASSROLE | iam:PassRole vs AttachRolePolicy vs CreateRole | entregar role
- `iam:CreateRole` = criar role | `iam:AttachRolePolicy` = colocar política numa role | `iam:PassRole` = ENTREGAR role existente pra um serviço (anexar role na Lambda/ECS/EC2)
- PassRole fica na política de QUEM CONFIGURA (o deploy), não na role do serviço. Invisível quando funciona; aparece no AccessDenied
- PassRole com `Resource: *` = ESCALADA DE PRIVILÉGIO (pendura role admin numa Lambda que você controla) — Resource = ARN da role que será passada
- Finding do Access Analyzer: `PASS_ROLE_WITH_STAR_IN_RESOURCE`

## LAMBDA 1 ROLE vs ECS 2 ROLES | Execution Role | Task Role
| | Quem usa | Pra quê | Política típica |
|---|---|---|---|
| ECS **Task Execution Role** | agente ECS | puxar imagem ECR + logs | `AmazonECSTaskExecutionRolePolicy` |
| ECS **Task Role** | código do container | S3, DynamoDB, etc. | conforme o app |
| Lambda **Execution Role** | os DOIS papéis | logs (`AWSLambdaBasicExecutionRole`) + o que o código acessa | conforme o app |
- Regra: app não INICIA/não puxa imagem → Execution Role. App roda mas não ACESSA serviço → Task Role
- Toda role = trust policy (QUEM veste) + políticas anexadas (O QUE pode)
- Trust: `Service` (lambda.amazonaws.com etc.) ou `AWS` (conta/role — p/ switch role). `:root` em trust = "porta da conta", não superpoderes

## IAM BOUNDARY | admin delegado | SJ-Max | Condition PermissionsBoundary | teto
**Modelo:** João (delegado) tem 1 política de PERMISSÃO com Condition. A SJ-Max NÃO vai no João — vai no bolso 2 (boundary) de toda role que ele CRIAR. Efetiva = política ∩ boundary.
- Criar role admin+boundary NÃO dá erro (nasce desarmada) | criar SEM boundary = AccessDenied
- Boundary é campo manual na criação (`--permissions-boundary`) — a Condition só REJEITA quem esquece
Política do delegado (a permissão do João):
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RoleCreationWithPermission",
      "Effect": "Allow",
      "Action": ["iam:CreateRole", "iam:AttachRolePolicy", "iam:PutRolePolicy",
                 "iam:DetachRolePolicy", "iam:DeleteRolePolicy"],
      "Resource": "*",
      "Condition": {
        "StringEquals": { "iam:PermissionsBoundary": "arn:aws:iam::CONTA:policy/SJ-Max" }
      }
    },
    {
      "Sid": "IAMPermission",
      "Effect": "Allow",
      "Action": ["iam:CreatePolicy", "iam:GetRole", "iam:ListRoles",
                 "iam:DeletePolicy", "iam:DeleteRole", "iam:GetRolePolicy"],
      "Resource": "*"
    }
  ]
}
```
SJ-Max (o teto — política solta na conta):
```json
{
  "Version": "2012-10-17",
  "Statement": [{ "Effect": "Allow", "Action": ["ssm:PutParameter", "s3:*"], "Resource": "*" }]
}
```
- Valor da Condition = ARN da política-teto (NÃO lista de ações!)
- 3 passos: (1) criar a política-teto; (2) criar a política do delegado com a Condition; (3) role do delegado com trust nas contas pedidas
- Pesquisa: `iam delegate role creation permissions boundary example`

## KMS KEY POLICY | 3 statements | MalformedPolicyDocument
1. **Admin** (`kms:*`) — TODAS as roles que gerenciam, INCLUINDO a role ativa no momento do PutKeyPolicy (senão `MalformedPolicyDocumentException` e perde a chave!)
2. **Use** (`kms:Encrypt`, `kms:Decrypt`, `kms:GenerateDataKey`...) — quem usa a chave
3. **Grants** (`kms:CreateGrant`) — root + Condition `kms:GrantIsForAWSResource`
- ⚠️ Whitespace/quebra de linha dentro de ARN = ARN inválido
- Lambda env vars: criptografia em repouso (KMS) + auxiliar em trânsito — role precisa de `kms:Decrypt` na CMK

## BUCKET POLICY CROSS-ACCOUNT | S3 outra conta | Principal role
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": { "AWS": "arn:aws:iam::CONTA-DA-ROLE:role/NomeDaRole" },
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::NOME-BUCKET/*"
  }]
}
```
- Principal usa a conta onde a ROLE VIVE (não a do bucket!) — ⚠️ conferir o NÚMERO contra o enunciado 2x
- `GetObject` age no OBJETO → Resource com `/*` | `ListBucket` age no BUCKET → sem `/*`
- Formato conta inteira: `"AWS": "arn:aws:iam::123456789012:root"` = qualquer identidade da conta COM permissão IAM própria
- Bucket de outra conta NÃO aparece no console — acessa por nome (CLI/SDK/URL)

## AÇÕES S3 | listar buckets | ListAllMyBuckets vs ListBucket vs GetObject
- `s3:ListAllMyBuckets` = listar TODOS os buckets da conta (Resource `*`)
- `s3:ListBucket` = listar objetos DENTRO de um bucket (Resource SEM `/*`: `arn:aws:s3:::bucket`)
- `s3:GetObject` = ler/baixar um arquivo (Resource COM `/*`: `arn:aws:s3:::bucket/*`)
- `s3:PutObject` = gravar | par clássico numa policy: ListBucket no bucket + GetObject no bucket/*

## BUCKET POLICY vs IAM vs ACL vs BLOCK PUBLIC ACCESS | quando usar
- MESMA conta, serviço→S3: IAM Role de quem acessa (checar Role primeiro!)
- OUTRA conta ou serviço AWS (CloudFront/logs): bucket policy (resource-based)
- Objeto público pontual: ACL do objeto (legado) | Site público: quase nunca certo — CloudFront+OAC
- Block Public Access = trava mestra: liga/desliga a POSSIBILIDADE de público (vence policy e ACL)
- CORS = browser em domínio DIFERENTE chamando o bucket — AllowedOrigins SÓ o domínio, SEM path:
```json
[{ "AllowedHeaders": ["*"], "AllowedMethods": ["GET"],
   "AllowedOrigins": ["https://meu-site.com"], "ExposeHeaders": [] }]
```

## ENDPOINT POLICY | VPC endpoint | restringir modelo Bedrock | política de recurso do endpoint
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Principal": "*",
    "Effect": "Allow",
    "Action": "bedrock:InvokeModel",
    "Resource": "arn:aws:bedrock:us-east-1::foundation-model/amazon.nova-lite-v1:0"
  }]
}
```
- `Principal: "*"` é NORMAL em endpoint policy (quem restringe "quem" é a IAM role de quem chama)
- ARN de foundation model: conta VAZIA = `::` duplo (modelo é da AWS)
- Allow só o específico → resto cai no deny implícito
- Quando IAM é proibido no enunciado → endpoint policy é O lugar

## DYNAMODB FINE-GRAINED | LeadingKeys | Attributes | PII
- Restringir LINHAS (por partition key): `"Condition": {"ForAllValues:StringEquals": {"dynamodb:LeadingKeys": ["Customer1"]}}`
- Esconder COLUNAS (atributos): Condition `dynamodb:Attributes` listando só os permitidos + `Select = SPECIFIC_ATTRIBUTES`
- ARN de TABELA sem `/*` pra Query (atributo/item não tem ARN próprio)
- Least privilege: só gravar = só `dynamodb:PutItem` + ARN da tabela

## SCP | service control policy | deny explícito | whitelist
- SCP = teto da CONTA (Organizations). Não concede nada, limita. Efetiva = IAM ∩ SCP
- Deny explícito de SCP vence TUDO — se aparecer `explicit deny in a service control policy`, não brigar: é proposital
- Whitelist de SCP rejeita a CONSULTA inteira (List*) → driblar com URL DIRETA do recurso

## ACCESS ANALYZER | validate_policy | finding
- Função 1: acha recurso acessível de FORA da conta (finding = UUID). Fix simples: REMOVER o statement do Allow externo
- Função 2: **ValidatePolicy** = qualidade da política (boto3: `validate_policy`) — retorna findings de sintaxe/segurança
- `aws:PrincipalAccount` = número SEM hífens | `ArnNotLike` usa ARN de PRINCIPAL, não de recurso

## SWITCH ROLE | assumed-role | sessão | SeniorDevelopers/*
- Quem age vestindo role = `assumed-role/<role>/<sessão>` (2 partes) — filtro exato sem `/*` NÃO casa com nenhuma sessão → usar `NomeDaRole/*`
- Console: menu do usuário → Alternar função / Switch role (conta + nome da role)

## FLOW LOGS PERMISSÕES | delivery.logs | VPC Flow Logs destino
- Flow Logs → **S3** = bucket policy com Principal `delivery.logs.amazonaws.com`, Action `s3:PutObject`, Resource `arn:aws:s3:::BUCKET/AWSLogs/*`, Condition `s3:x-amz-acl = bucket-owner-full-control`
- Flow Logs → **CloudWatch** = IAM Role (logs:CreateLogGroup/CreateLogStream/PutLogEvents/Describe*)

## SNS SQS PERMISSÕES | fan-out | tópico publicar na fila
- SNS → SQS: Access Policy NA FILA permitindo o ARN do tópico (Principal `Service: sns.amazonaws.com` + Condition `aws:SourceArn` = ARN do tópico)
- SNS → Lambda: resource policy na Lambda (`sns.amazonaws.com`)
- `aws:SourceArn`/`aws:SourceAccount` = de ONDE veio a requisição | `aws:PrincipalAccount` = de QUEM é a identidade
- Subscription de email precisa CONFIRMAR (checar status)
- Fan-out (1 evento → N consumidores) = SNS → N filas SQS

## PESQUISA DE POLÍTICA | como achar exemplo | doc
1. `<serviço> policy examples` → página com JSON pronto pra adaptar
2. `<serviço> actions resources condition keys` → Service Authorization Reference (nome exato das actions + formato de ARN)
3. CLI: `aws <serviço> help` | boto3: doc do método
- Erro de permissão NOMEIA a ação que falta — ler o AccessDenied: QUEM (role/sessão) + AÇÃO + RECURSO + POR QUÊ (identity policy vs SCP)
- `ecr:GetAuthorizationToken` exige `Resource: "*"` (ação de nível de conta)
- Política GERENCIADA = anexa, não escreve (AWS Backup: `AWSBackupServiceRolePolicyForBackup` + `...ForRestores`; Lambda logs: `AWSLambdaBasicExecutionRole`)
