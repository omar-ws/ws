# JAM The Broken Chain: Missão de Resgate do Agente (medio)

confesso que nao entendi anda na solucao desse jam

visao geral

```jsx
É dia de lançamento na TechCore, e a implantação de seu produto sem servidor está por um fio! A implantação de um agente crítico de IA falhou e a equipe que a criou deixou a empresa. Com o UpgradeRollout Agent como guia e a documentação técnica como mapa, você deve corrigir o pipeline quebrado e implantar o agente, além de lançar a nova versão do serviço e implementá-la sem problemas. Você pode restaurar a cadeia de implantação, corrigir o código e lançar uma nova atualização?
```

task 1

```jsx
Propriedades de saída
CodeBuildProjectName
UpgradeRollOutBuild

CodeDeployServiceRoleArn
arn:aws:iam::861202889881:role/LabStack-prewarm-d0e5b172-b1d-CodeDeployServiceRole-FmY1A3Agwq18

CustomerOrderProcessorAliasArn
arn:aws:lambda:us-east-1:861202889881:function:CustomerOrderProcessor:LIVE

CustomerOrderProcessorArn
arn:aws:lambda:us-east-1:861202889881:function:CustomerOrderProcessor

KnowledgeBaseArn
arn:aws:bedrock:us-east-1:861202889881:knowledge-base/QVHIH2R8PY

LambdaCodeS3Bucket
aws-jam-challenge-resources-us-east-1

PipelineArtifactsBucket
pipeline-861202889881

UpgradeRollOutAgentRoleArn
arn:aws:iam::861202889881:role/UpgradeRollOutAgentRole

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Missão de recuperação do CodePipeline com o Amazon Q
Pontos possíveis
45
Penalidade por pista
9
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Você é um novoEngenheiro de DevOps na empresa TechCore e precisa implementar uma atualização para algumas correções no código, mas não está ciente das estratégias e configurações de implantação. Portanto, para isso, você precisa da ajuda do UpgradeRollout AI Agent para implementar as atualizações sem problemas. Mas o pipeline que implanta o agente está em estado de falha. Você precisa solucionar esse problema de pipeline, o que ajudará a implantar o Agente. Dada a natureza urgente e a complexidade dos problemas, a solução manual de problemas pode levar horas. Os recursos avançados do Amazon Q podem acelerar significativamente o processo de diagnóstico e resolução, reduzindo o tempo de depuração de horas para minutos e garantindo a identificação precisa do problema e as correções sistemáticas.

Suas tarefas
Anote o ID da conta da AWS e a região da AWS em que você está trabalhando. Use esses valores no desafio.

Acesse o console do CodePipeline e localize o pipeline que falhou.

Use o Amazon Q para analisar os logs de compilação e resolver os erros sequencialmente.

Você também pode depurá-lo manualmente, mas terá acesso ao console Amazon Q para solucionar problemas.

Para usar o Amazon Q, basta clicar no ícone Q no console da AWS no canto direito.

NOTA:

Pode haver várias maneiras de resolver a tarefa e também há vários problemas (no máximo 2 bugs) que você precisa resolver nesta tarefa. Resolver 1 bug também pode resolver a tarefa (depende da abordagem). Depende da abordagem que você adota.
Serviços que você deve usar
Amazon Q
Amazon S3
AWS CodePipeline
ERA O OBJETIVO
Validação de tarefas
Depois de resolver com êxito todas as falhas do CodeBuild e garantir que o CodePipeline seja concluído com êxito, você pode clicar no botão Verificar meu progresso ou simplesmente esperar e ele será validado automaticamente.

Pistas
Pista para corrigir a falha de compilação do CodePipeline com o Amazon Q
4Pontos de penalidade
Mostrar pista
Passo a passo completo da resolução: pista para resolver a falha do pipeline do CodeBuild atualizando a política do IAM anexada à função do CodeBuild IAM
5Pontos de penalidade
Mostrar pista
```

nao vou mentir que usei a dica que estava ali, eu nao epguei mas a dica so no titulo era extremamente explicativa, eu achei que o erro nao tinha nada have com o IAM, cheguei nessa conclusao tipo, eu tentei colocar o que o amazon q falou colocar a origim vindo no s3 e nao do pipeline, entao eu estava colando mas nao tinha permissao para isso, entao dai eu fui atras da role que apreceu no erro, ai eu mandei para o claud eoq ue tem de errado nessa police, e voce disse que tinha um deny, tipo assim

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "logs:CreateLogGroup",
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": "arn:aws:logs:us-east-1:861202889881:log-group:/aws/codebuild/*",
            "Effect": "Allow"
        },
        {
            "Action": [
                "iam:GetRole",
                "iam:PassRole",
                "lambda:CreateFunction",
                "lambda:UpdateFunctionCode",
                "lambda:UpdateFunctionConfiguration",
                "lambda:GetFunction",
                "lambda:ListVersionsByFunction",
                "lambda:PublishVersion",
                "lambda:CreateAlias",
                "lambda:UpdateAlias",
                "lambda:GetAlias",
                "lambda:AddPermission"
            ],
            "Resource": [
                "arn:aws:iam::861202889881:role/*",
                "arn:aws:lambda:us-east-1:861202889881:function:*"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:GetObject",
                "s3:GetObjectVersion",
                "s3:PutObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::pipeline-861202889881",
                "arn:aws:s3:::pipeline-861202889881/*"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::aws-jam-challenge-resources-us-east-1",
                "arn:aws:s3:::aws-jam-challenge-resources-us-east-1/*"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "bedrock:*"
            ],
            "Resource": [
                "*"
            ],
            "Effect": "Deny"
        }
    ]
}
```

ai eu coloquei um allow e foi, mas o amazon q nao me ajudou em nada eu estava tentando corrigir pelo code biuld mas nao foi, entende? nao enendi eu to meio ferrado em varios conteudos

logs quando deu tudo certo no code biulder

```verilog
[Container] 2026/06/27 21:11:29.547015 Running on CodeBuild On-demand
[Container] 2026/06/27 21:11:29.547046 Waiting for agent ping
[Container] 2026/06/27 21:11:29.648493 Waiting for DOWNLOAD_SOURCE
[Container] 2026/06/27 21:11:30.678375 Phase is DOWNLOAD_SOURCE
[Container] 2026/06/27 21:11:30.679661 CODEBUILD_SRC_DIR=/codebuild/output/src2087212488/src
[Container] 2026/06/27 21:11:30.680294 YAML location is /codebuild/output/src2087212488/src/buildspec.yml
[Container] 2026/06/27 21:11:30.682476 Setting HTTP client timeout to higher timeout for S3 source
[Container] 2026/06/27 21:11:30.682598 Processing environment variables
[Container] 2026/06/27 21:11:30.852402 Selecting 'python' runtime version '3.9' based on manual selections...
[Container] 2026/06/27 21:11:30.853615 Running command echo "Installing Python version 3.9 ..."
Installing Python version 3.9 ...

[Container] 2026/06/27 21:11:30.861289 Running command pyenv global  $PYTHON_39_VERSION

[Container] 2026/06/27 21:11:31.136150 Moving to directory /codebuild/output/src2087212488/src
[Container] 2026/06/27 21:11:31.136175 Cache is not defined in the buildspec
[Container] 2026/06/27 21:11:31.173514 Skip cache due to: no paths specified to be cached
[Container] 2026/06/27 21:11:31.173938 Registering with agent
[Container] 2026/06/27 21:11:31.208427 Phases found in YAML: 3
[Container] 2026/06/27 21:11:31.208445  PRE_BUILD: 3 commands
[Container] 2026/06/27 21:11:31.208450  BUILD: 6 commands
[Container] 2026/06/27 21:11:31.208454  INSTALL: 2 commands
[Container] 2026/06/27 21:11:31.208880 Phase complete: DOWNLOAD_SOURCE State: SUCCEEDED
[Container] 2026/06/27 21:11:31.208892 Phase context status code:  Message: 
[Container] 2026/06/27 21:11:31.308225 Entering phase INSTALL
[Container] 2026/06/27 21:11:31.343146 Running command echo Installing dependencies...
Installing dependencies...

[Container] 2026/06/27 21:11:31.351029 Running command pip install boto3
Requirement already satisfied: boto3 in /root/.pyenv/versions/3.9.17/lib/python3.9/site-packages (1.42.59)
Requirement already satisfied: jmespath<2.0.0,>=0.7.1 in /root/.pyenv/versions/3.9.17/lib/python3.9/site-packages (from boto3) (1.1.0)
Requirement already satisfied: s3transfer<0.17.0,>=0.16.0 in /root/.pyenv/versions/3.9.17/lib/python3.9/site-packages (from boto3) (0.16.1)
Requirement already satisfied: botocore<1.43.0,>=1.42.59 in /root/.pyenv/versions/3.9.17/lib/python3.9/site-packages (from boto3) (1.42.97)
Requirement already satisfied: urllib3<1.27,>=1.25.4 in /root/.pyenv/versions/3.9.17/lib/python3.9/site-packages (from botocore<1.43.0,>=1.42.59->boto3) (1.26.20)
Requirement already satisfied: python-dateutil<3.0.0,>=2.1 in /root/.pyenv/versions/3.9.17/lib/python3.9/site-packages (from botocore<1.43.0,>=1.42.59->boto3) (2.9.0.post0)
Requirement already satisfied: six>=1.5 in /root/.pyenv/versions/3.9.17/lib/python3.9/site-packages (from python-dateutil<3.0.0,>=2.1->botocore<1.43.0,>=1.42.59->boto3) (1.17.0)
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
WARNING: You are using pip version 21.3.1; however, version 26.0.1 is available.
You should consider upgrading via the '/root/.pyenv/versions/3.9.17/bin/python3.9 -m pip install --upgrade pip' command.

[Container] 2026/06/27 21:11:48.326757 Phase complete: INSTALL State: SUCCEEDED
[Container] 2026/06/27 21:11:48.326777 Phase context status code:  Message: 
[Container] 2026/06/27 21:11:48.359825 Entering phase PRE_BUILD
[Container] 2026/06/27 21:11:48.361294 Running command echo Pre-build phase started on `date`
Pre-build phase started on Sat Jun 27 21:11:48 UTC 2026

[Container] 2026/06/27 21:11:48.372197 Running command echo Checking AWS credentials...
Checking AWS credentials...

[Container] 2026/06/27 21:11:48.379529 Running command aws sts get-caller-identity
{
    "UserId": "AROA4RA5RHSMQJB6G3QWR:AWSCodeBuild-9e279ffd-06a0-4770-b168-57925eef7970",
    "Account": "861202889881",
    "Arn": "arn:aws:sts::861202889881:assumed-role/LabStack-prewarm-d0e5b172-b1d3-CodeBuildServiceRole-W15w41TAiD1A/AWSCodeBuild-9e279ffd-06a0-4770-b168-57925eef7970"
}

[Container] 2026/06/27 21:11:57.782919 Phase complete: PRE_BUILD State: SUCCEEDED
[Container] 2026/06/27 21:11:57.782936 Phase context status code:  Message: 
[Container] 2026/06/27 21:11:57.817553 Entering phase BUILD
[Container] 2026/06/27 21:11:57.818738 Running command echo Build phase started on `date`
Build phase started on Sat Jun 27 21:11:57 UTC 2026

[Container] 2026/06/27 21:11:57.827171 Running command echo Deploying Action Group Lambda...
Deploying Action Group Lambda...

[Container] 2026/06/27 21:11:57.834265 Running command python3 deploy_action_lambda.py
/root/.pyenv/versions/3.9.17/lib/python3.9/site-packages/boto3/compat.py:89: PythonDeprecationWarning: Boto3 will no longer support Python 3.9 starting April 29, 2026. To continue receiving service updates, bug fixes, and security updates please upgrade to Python 3.10 or later. More information can be found here: https://aws.amazon.com/blogs/developer/python-support-policy-updates-for-aws-sdks-and-tools/
  warnings.warn(warning, PythonDeprecationWarning)
Using pre-created Lambda role: arn:aws:iam::861202889881:role/UpgradeRollOutActionLambdaRole
Updated existing Lambda function
Bedrock permission already exists

[Container] 2026/06/27 21:11:59.160031 Running command echo Deploying UpgradeRollOut Bedrock Agent...
Deploying UpgradeRollOut Bedrock Agent...

[Container] 2026/06/27 21:11:59.167499 Running command python3 deploy_bedrock_agent.py
/root/.pyenv/versions/3.9.17/lib/python3.9/site-packages/boto3/compat.py:89: PythonDeprecationWarning: Boto3 will no longer support Python 3.9 starting April 29, 2026. To continue receiving service updates, bug fixes, and security updates please upgrade to Python 3.10 or later. More information can be found here: https://aws.amazon.com/blogs/developer/python-support-policy-updates-for-aws-sdks-and-tools/
  warnings.warn(warning, PythonDeprecationWarning)
Using pre-created agent role: arn:aws:iam::861202889881:role/UpgradeRollOutAgentRole
Created Bedrock agent: EHFGHWQOML
Created action group: CMA7GOBFGR
Preparing agent...
Agent status: PREPARING
Agent status: PREPARED
Created agent alias: 8PCDKBRJIG
✅ UpgradeRollOut Agent deployed successfully!
Agent ID: EHFGHWQOML
Agent Alias ID: 8PCDKBRJIG
Production Alias: PROD
You can now test the agent using the PROD alias in the AWS Bedrock console!
Deployment completed - Agent ID: EHFGHWQOML, Alias: 8PCDKBRJIG

[Container] 2026/06/27 21:12:26.077405 Running command echo Build phase completed successfully
Build phase completed successfully

[Container] 2026/06/27 21:12:26.084960 Phase complete: BUILD State: SUCCEEDED
[Container] 2026/06/27 21:12:26.084977 Phase context status code:  Message: 
[Container] 2026/06/27 21:12:26.134077 Entering phase POST_BUILD
[Container] 2026/06/27 21:12:26.136843 Phase complete: POST_BUILD State: SUCCEEDED
[Container] 2026/06/27 21:12:26.136867 Phase context status code:  Message: 
[Container] 2026/06/27 21:12:26.230502 Expanding base directory path: .
[Container] 2026/06/27 21:12:26.233873 Assembling file list
[Container] 2026/06/27 21:12:26.233888 Expanding .
[Container] 2026/06/27 21:12:26.236984 Expanding file paths for base directory .
[Container] 2026/06/27 21:12:26.236998 Assembling file list
[Container] 2026/06/27 21:12:26.237002 Expanding **/*
[Container] 2026/06/27 21:12:26.240116 Found 5 file(s)
[Container] 2026/06/27 21:12:26.242573 Set report auto-discover timeout to 5 seconds
[Container] 2026/06/27 21:12:26.242708 Expanding base directory path:  .
[Container] 2026/06/27 21:12:26.245692 Assembling file list
[Container] 2026/06/27 21:12:26.245707 Expanding .
[Container] 2026/06/27 21:12:26.248752 Expanding file paths for base directory .
[Container] 2026/06/27 21:12:26.248767 Assembling file list
[Container] 2026/06/27 21:12:26.248866 Expanding **/*
[Container] 2026/06/27 21:12:26.251896 No matching auto-discover report paths found
[Container] 2026/06/27 21:12:26.251914 Report auto-discover file discovery took 0.009341 seconds
[Container] 2026/06/27 21:12:26.251927 Phase complete: UPLOAD_ARTIFACTS State: SUCCEEDED
[Container] 2026/06/27 21:12:26.251934 Phase context status code:  Message: 

```

task 2:

```json
Propriedades de saída
CodeBuildProjectName
UpgradeRollOutBuild

CodeDeployServiceRoleArn
arn:aws:iam::861202889881:role/LabStack-prewarm-d0e5b172-b1d-CodeDeployServiceRole-FmY1A3Agwq18

CustomerOrderProcessorAliasArn
arn:aws:lambda:us-east-1:861202889881:function:CustomerOrderProcessor:LIVE

CustomerOrderProcessorArn
arn:aws:lambda:us-east-1:861202889881:function:CustomerOrderProcessor

KnowledgeBaseArn
arn:aws:bedrock:us-east-1:861202889881:knowledge-base/QVHIH2R8PY

LambdaCodeS3Bucket
aws-jam-challenge-resources-us-east-1

PipelineArtifactsBucket
pipeline-861202889881

UpgradeRollOutAgentRoleArn
arn:aws:iam::861202889881:role/UpgradeRollOutAgentRole

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: The Wisdom Wire - Unindo inteligência artificial e conhecimento organizacional
Pontos possíveis
38
Penalidade por pista
0
Pontos disponíveis
38
Verifique meu progresso

Tarefas e pistas
Enviar resposta
Plano de fundo
Excelente trabalho na resolução das falhas do CodePipeline na Tarefa 1! Sua solução de problemas bem-sucedida concluiu todas as etapas do CodePipeline e ele implantou o Rollout-Agent (Bedrock Agent). No entanto, resta uma etapa crítica para tornar esse agente Bedrock totalmente operacional: o agente Bedrock implantado está atualmente desconectado do conhecimento organizacional da TechCore — é como ter um consultor brilhante que não sabe nada sobre sua empresa.

Suas tarefas
Anote o ID da conta da AWS e a região da AWS em que você está trabalhando. Use esses valores no desafio.
Encontre a base de conhecimento e sincronize com a fonte de dados (AGUARDE A CONCLUSÃO DA SINCRONIZAÇÃO). Não saia da página antes que a sincronização seja concluída.
Conecte o agente Amazon Bedrock à base de conhecimento.
Você precisa de Prepare Agent e depois disso criar um novo alias e uma nova versão do agente.
Nota
Ao adicionar a Base de Conhecimento ao Agente, adicione a descrição como siga:

“Você tem as informações sobre os lambdas que precisam ser corrigidas, junto com suas configurações de implantação de codedeploys"

Serviços que você deve usar
Base da Amazônia
Amazon S3
Validação de tarefas
Depois de conectar com sucesso o Agente à Base de Conhecimento e criar o alias, você pode enviar o nome do alias e clicar no botão Verificar meu progresso.

Pistas
Pista para conectar o Bedrock Agent à Base de Conhecimento.
3Pontos de penalidade
Desbloqueie o Clue
Passo a passo completo de resolução
4Pontos de penalidade
Desbloqueie o Clue
```

vou comecar a ler as dicas o anunciado sem pegar mt das vezes elas ajudam para caramba mesmo sem pegar olha nesse pistas para conectar no backrock

sinceramente nao sabia nada nem sabia o que estava fazendo no amazon badrock, modelo de IA, vou ter que focar mt nisso e entender isso quando temrinar a academy nesses 12 dias

task 3:

```verilog
Propriedades de saída
CodeBuildProjectName
UpgradeRollOutBuild

CodeDeployServiceRoleArn
arn:aws:iam::861202889881:role/LabStack-prewarm-d0e5b172-b1d-CodeDeployServiceRole-FmY1A3Agwq18

CustomerOrderProcessorAliasArn
arn:aws:lambda:us-east-1:861202889881:function:CustomerOrderProcessor:LIVE

CustomerOrderProcessorArn
arn:aws:lambda:us-east-1:861202889881:function:CustomerOrderProcessor

KnowledgeBaseArn
arn:aws:bedrock:us-east-1:861202889881:knowledge-base/QVHIH2R8PY

LambdaCodeS3Bucket
aws-jam-challenge-resources-us-east-1

PipelineArtifactsBucket
pipeline-861202889881

UpgradeRollOutAgentRoleArn
arn:aws:iam::861202889881:role/UpgradeRollOutAgentRole

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 3: Fuso de tempo de inatividade zero: o agente navega em implantações complexas
Pontos possíveis
67
Penalidade por pista
0
Pontos disponíveis
67
Verifique meu progresso

Tarefas e pistas
Você progrediu com sucesso em sua jornada de transformação da IA resolvendo problemas de pipeline e estabelecendo um assistente inteligente usando os agentes Amazon Bedrock. Agora, você está entrando na fase final: implementar atualizações e implantações automatizadas de código Lambda usando sua infraestrutura de IA.

Nessa tarefa, você aproveitará o UpgradeRollout Agent (Amazon Bedrock Agent), conectado à base de conhecimento de lançamento e upgrade da TechCore, para orquestrar um processo completo de atualização e implantação do Lambda.

Suas tarefas
Seu agente Bedrock entende as estratégias de implantação da base de conhecimento, mas agora ele precisa agir — realmente executar comandos de implantação e tomar decisões em tempo real durante o processo de atualização.

Agora, o código fixo para uma função lambda específica é carregado e mantido no bucket do S3. Você precisa atualizar a função lambda com o novo código que criará uma nova versão do lambda. E você precisa implantar a implantação na nova versão usando uma estratégia de implantação específica mencionada na base de conhecimento do agente.

Antes de consultar o agente, verifique se você está usando a versão do agente que foi anexada à Base de Conhecimento na Tarefa 2. Além disso, verifique se você forneceu a mesma descrição ao anexar a base de conhecimento ao agente, conforme mencionado na Tarefa 2.

Toda a atualização e o lançamento seguem esse fluxo único:

Etapa 1 — Identificar e atualizar o código Lambda
Consulte o Knowledge Base usando o agente:

Você pode me ajudar a encontrar funções lambda que precisam ser corrigidas e implementadas.

Você pode compartilhar comigo todas as configurações para atualizar e implantar Name of the Lambda function, fornecidas no formato adequado.

Substitua o placeholder no local do bucket do S3 pela região onde seu desafio acontece.

Use o agente para update the Lambda code.

code version encontrado na base de conhecimento (⚠️ não é a versão do AWS Lambda)

Anote o novo published Lambda version criado após a atualização.

Etapa 2 — Configurar o CodeDeploy usando o Agent
Peça ao agente que forneça toda a configuração de um lambda específico para lançar sua nova versão usando o codedeploy.
Crie um CodeDeploy application (o nome deve corresponder ao nome presente na base de conhecimento).
Crie um Codedeploy Deployment Group vinculado ao alias do Lambda:
Use ServiceRoleArn nas propriedades de saída do console JAM.
Prepare um AppSpec file que mapeie:
O nome da função Lambda
Alias (ainda apontando para a versão antiga)
Nova versão do Lambda (que você obteve na Etapa 1) para lançar.
Crie CodeDeploy Deployment.
Depois disso, você pode monitorar a implantação no serviço Codedeploy.
FLOW da atualização de RollingOut usando UpgradeRolloutAgent será:

UpdateLambda Code -> CreateDeploymentApplication -> CreateDeploymentGroup -> CreateAppsec -> CreateDeployment

Você pode começar perguntando “Vamos prosseguir para a primeira etapa e quais parâmetros são necessários para isso”.
Confira o Output Properties do console JAM para obter IDs de recursos específicos que são usados nas tarefas (ServiceRoLearn, Knowledgbase).

Depois que todas as 5 etapas forem concluídas, vá para o serviço AWS CodeDeploy no console e, em Implantação, você poderá monitorar a implantação do CodeDeploy do Lambda da versão mais antiga para a nova.

NOTAS:

Names ao implantar a infraestrutura do Codedeploy deve corresponder aos nomes recuperados por meio da base de conhecimento.
Execute essa atualização usando ALIAS e Version apropriados do Agente que você criou na Tarefa 2.
⚠️ Não feche a janela do prompt do Bedrock Agent até que você tenha criado completamente a infraestrutura de implantação do Codedeploy, pois se a sessão for fechada, ela não se lembrará de nada e começará do início.
Tente validar os parâmetros que estão sendo passados para uma ferramenta específica, se você enfrentar algum erro, pois às vezes ela pode tentar detectá-lo sozinha, mas tente ver o Show Trace e solucionar o problema.
Aguarde 5 minutos para que a implantação seja lançada, você pode monitorá-la no CodeDeploy em Implantação e clicar em Check My Progress quando ela for concluída.
Se, por engano, você criou um arquivo appsec com valores errados, você pode executar novamente e criar um novo arquivo Appsec, pois o controle de versão está ativado, ele sempre seleciona o arquivo mais recente. Depois disso, você pode liberar a implantação novamente.
Serviços que você deve usar
Agente Amazon Bedrock
AWS Lambda
AWS CodeDeploy
Validação de tarefas
Você tem permissões para visualizar as implantações no CodeDeploy Service depois de implementadas com configurações específicas usando o UpgradeRollout Agent. E veja a implantação azul/verde que está sendo realizada pelo CodeDeploy. Depois de bem-sucedido, tente clicar em Check My Progress, ele deverá validar e concluir a tarefa. A função de validação também leva em consideração o nome da configuração, então tente fornecer nomes exatos.

Pistas
6Pontos de penalidade
Desbloqueie o Clue

```

nao consegui fazer eu desisti tava mt massante com toda certeza eu vou ter que estudar isso, eu nao entendi absolutamente nada, nada mesmo