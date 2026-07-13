# JAM CloudFormation Sherlock!!

```verilog
Visão geral
Plano de fundo
Seu amigo travesso, Morty Arty, bloqueou o lançamento de seu importante projeto adicionando uma versão incorreta ao seu modelo do CloudFormation!

Cabe a você, Cloud Detective Sherlock Holmes, deduzir as configurações incorretas e corrigi-las para que sua versão funcione! Morty Arty deixou um cartão telefônico com as palavras: “Detecte os defeitos”. Você consegue encontrar os defeitos e salvar o dia?

Começando
Neste desafio há duas tarefas, cada uma valendo 50% do total de pontos.

Ambas as tarefas são independentes uma da outra.
```

```verilog
CloudFormation Sherlock!!
Selecione um desafio abaixo para começar.

Reiniciar o desafio
Tarefa 1: Conserte meu linting
Pontos possíveis
75
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
O modelo CloudFormation tem um problema de linting presente, o que faz com que ele falhe na ação LintingCheck quando executado pelo AWS CodePipeline. O CodePipeline tem um projeto AWS CodeBuild que realiza as verificações de linting no modelo do CloudFormation.

O pipeline do CodePipeline está sendo obtido de um repositório do AWS CodeCommit. O modelo do CloudFormation reside na pasta src.

Tarefa
Sherlock precisa identificar e corrigir os fiapos. Sherlock pode investigar a saída do AWS CodeBuild a partir do AWS Console. Quando Sherlock identifica o problema, ele pode confirmar as alterações na filial main. O AWS CodePipeline pode ser acionado manualmente usando o botão laranja Release Change, depois de corrigir o modelo e confirmar a alteração no CodeCommit.

Começando
Você pode usar essa documentação para entender as ferramentas do desenvolvedor da AWS e como elas funcionam.

AWS CodePipeline: https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html
AWS CodeBuild: https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html
AWS CodeCommit: https://docs.aws.amazon.com/codecommit/latest/userguide/welcome.html
Inventário
Os seguintes serviços estão envolvidos para concluir a tarefa:

AWS CloudFormation
AWS CodePipeline
CFN-lint: https://github.com/aws-cloudformation/cfn-lint
Serviços da AWS que você deve usar:
AWS CloudFormation
AWS CodePipeline
AWS CodeCommit
Validação de tarefas
Essa tarefa será validada automaticamente quando a ação do AWS CodePipeline LintingCheck for aprovada e ficar Verde.

CloudFormation Sherlock!!
Selecione um desafio abaixo para começar.

Reiniciar o desafio
Tarefa 2: Onde eu estou falhando?
Pontos possíveis
75
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
O modelo do CloudFormation também tem um problema de segurança presente, que está fazendo com que ele falhe em um estágio quando executado pelo AWS CodePipeline. O pipeline do CodePipeline tem uma ação SecurityCheck, que usa um projeto AWS CodeBuild para realizar as verificações de segurança no modelo do CloudFormation.

O pipeline do CodePipeline está sendo obtido de um repositório do AWS CodeCommit. O modelo do CloudFormation reside na pasta src.

Tarefa
Sherlock precisa identificar a vulnerabilidade de segurança que está falhando na verificação de segurança e corrigi-la. Sherlock pode investigar os logs da saída do AWS CodeBuild Security Check do AWS Console. Quando Sherlock identifica o problema, ele pode confirmar as alterações na filial main. O AWS CodePipeline pode ser acionado manualmente usando o botão laranja Release Change.

Começando
Você pode usar esta documentação para entender as ferramentas do desenvolvedor da AWS:

AWS CodePipeline
AWS CodeBuild
AWS CodeCommit
Inventário
Os seguintes serviços estão envolvidos para concluir a tarefa:

AWS CloudFormation
AWS CodePipeline
AWS CodeBuild
AWS CodeCommit
Bolsa CFN: https://github.com/stelligent/cfn_nag
AWS CloudFormation
AWS CodePipeline
AWS CodeCommit
Validação de tarefas
Essa tarefa será validada automaticamente quando a ação do AWS CodePipeline SecurityCheck for aprovada e ficar Verde.
```

logs lighting check

```bash

[Container] 2026/07/04 14:25:39.684611 Running on CodeBuild On-demand
[Container] 2026/07/04 14:25:39.684624 Waiting for agent ping
[Container] 2026/07/04 14:25:39.886269 Waiting for DOWNLOAD_SOURCE
[Container] 2026/07/04 14:25:40.850365 Phase is DOWNLOAD_SOURCE
[Container] 2026/07/04 14:25:40.851702 CODEBUILD_SRC_DIR=/codebuild/output/src1368677360/src
[Container] 2026/07/04 14:25:40.852929 YAML location is /codebuild/output/src1368677360/src/buildspec-linter.yml
[Container] 2026/07/04 14:25:40.856012 Setting HTTP client timeout to higher timeout for S3 source
[Container] 2026/07/04 14:25:40.856098 Processing environment variables
[Container] 2026/07/04 14:25:41.086329 Selecting 'python' runtime version '3.11' based on manual selections...
[Container] 2026/07/04 14:25:41.087323 Running command echo "Installing Python version 3.11 ..."
Installing Python version 3.11 ...

[Container] 2026/07/04 14:25:41.094601 Running command pyenv global $PYTHON_311_VERSION

[Container] 2026/07/04 14:25:41.671635 Moving to directory /codebuild/output/src1368677360/src
[Container] 2026/07/04 14:25:41.671663 Cache is not defined in the buildspec
[Container] 2026/07/04 14:25:41.711679 Skip cache due to: no paths specified to be cached
[Container] 2026/07/04 14:25:41.711945 Registering with agent
[Container] 2026/07/04 14:25:41.746663 Phases found in YAML: 2
[Container] 2026/07/04 14:25:41.746685  INSTALL: 2 commands
[Container] 2026/07/04 14:25:41.746690  BUILD: 2 commands
[Container] 2026/07/04 14:25:41.746993 Phase complete: DOWNLOAD_SOURCE State: SUCCEEDED
[Container] 2026/07/04 14:25:41.747006 Phase context status code:  Message: 
[Container] 2026/07/04 14:25:41.856546 Entering phase INSTALL
[Container] 2026/07/04 14:25:41.895116 Running command apt-get update -y
Hit:1 https://apt.corretto.aws stable InRelease
Get:2 https://cli.github.com/packages stable InRelease [3917 B]
Get:3 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
Get:4 https://dl.google.com/linux/chrome-stable/deb stable InRelease [1825 B]
Hit:5 http://archive.ubuntu.com/ubuntu jammy InRelease
Get:6 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy-backports InRelease [127 kB]
Get:8 https://ppa.launchpadcontent.net/mozillateam/ppa/ubuntu jammy InRelease [24.6 kB]
Get:9 https://cli.github.com/packages stable/main amd64 Packages [355 B]
Get:10 https://dl.google.com/linux/chrome-stable/deb stable/main amd64 Packages [1214 B]
Get:11 http://archive.ubuntu.com/ubuntu jammy-updates/main i386 Packages [1268 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [1613 kB]
Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [7600 kB]
Get:14 http://security.ubuntu.com/ubuntu jammy-security/universe i386 Packages [860 kB]
Get:15 http://security.ubuntu.com/ubuntu jammy-security/main i386 Packages [1044 kB]
Get:16 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [7332 kB]
Get:17 http://archive.ubuntu.com/ubuntu jammy-updates/restricted i386 Packages [64.2 kB]
Get:18 http://archive.ubuntu.com/ubuntu jammy-updates/universe i386 Packages [998 kB]
Get:19 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [1308 kB]
Get:20 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [4083 kB]
Get:21 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [4415 kB]
Get:22 https://ppa.launchpadcontent.net/mozillateam/ppa/ubuntu jammy/main i386 Packages [2376 B]
Get:23 https://ppa.launchpadcontent.net/mozillateam/ppa/ubuntu jammy/main amd64 Packages [43.4 kB]
Fetched 31.0 MB in 3s (10.6 MB/s)
Reading package lists...

[Container] 2026/07/04 14:25:52.754657 Running command pip install cfn-lint
Collecting cfn-lint
  Downloading cfn_lint-1.52.1-py3-none-any.whl.metadata (24 kB)
Requirement already satisfied: pyyaml>=6.0.3 in /root/.pyenv/versions/3.11.15/lib/python3.11/site-packages (from cfn-lint) (6.0.3)
Collecting aws-sam-translator>=1.110.0 (from cfn-lint)
  Downloading aws_sam_translator-1.111.0-py3-none-any.whl.metadata (8.6 kB)
Collecting jsonpatch (from cfn-lint)
  Downloading jsonpatch-1.33-py2.py3-none-any.whl.metadata (3.0 kB)
Collecting networkx<4,>=2.4 (from cfn-lint)
  Downloading networkx-3.6.1-py3-none-any.whl.metadata (6.8 kB)
Collecting sympy>=1.14.0 (from cfn-lint)
  Downloading sympy-1.14.0-py3-none-any.whl.metadata (12 kB)
Collecting regex (from cfn-lint)
  Downloading regex-2026.6.28-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl.metadata (40 kB)
Collecting typing_extensions (from cfn-lint)
  Downloading typing_extensions-4.16.0-py3-none-any.whl.metadata (3.3 kB)
Requirement already satisfied: boto3<2.0.0,>=1.34.0 in /root/.pyenv/versions/3.11.15/lib/python3.11/site-packages (from aws-sam-translator>=1.110.0->cfn-lint) (1.43.33)
Collecting jsonschema<5,>=4.23 (from aws-sam-translator>=1.110.0->cfn-lint)
  Downloading jsonschema-4.26.0-py3-none-any.whl.metadata (7.6 kB)
Collecting pydantic~=2.13.3 (from aws-sam-translator>=1.110.0->cfn-lint)
  Downloading pydantic-2.13.4-py3-none-any.whl.metadata (109 kB)
Requirement already satisfied: botocore<1.44.0,>=1.43.33 in /root/.pyenv/versions/3.11.15/lib/python3.11/site-packages (from boto3<2.0.0,>=1.34.0->aws-sam-translator>=1.110.0->cfn-lint) (1.43.33)
Requirement already satisfied: jmespath<2.0.0,>=0.7.1 in /root/.pyenv/versions/3.11.15/lib/python3.11/site-packages (from boto3<2.0.0,>=1.34.0->aws-sam-translator>=1.110.0->cfn-lint) (1.1.0)
Requirement already satisfied: s3transfer<0.20.0,>=0.19.0 in /root/.pyenv/versions/3.11.15/lib/python3.11/site-packages (from boto3<2.0.0,>=1.34.0->aws-sam-translator>=1.110.0->cfn-lint) (0.19.0)
Requirement already satisfied: python-dateutil<3.0.0,>=2.1 in /root/.pyenv/versions/3.11.15/lib/python3.11/site-packages (from botocore<1.44.0,>=1.43.33->boto3<2.0.0,>=1.34.0->aws-sam-translator>=1.110.0->cfn-lint) (2.9.0.post0)
Requirement already satisfied: urllib3!=2.2.0,<3,>=1.25.4 in /root/.pyenv/versions/3.11.15/lib/python3.11/site-packages (from botocore<1.44.0,>=1.43.33->boto3<2.0.0,>=1.34.0->aws-sam-translator>=1.110.0->cfn-lint) (2.7.0)
Collecting attrs>=22.2.0 (from jsonschema<5,>=4.23->aws-sam-translator>=1.110.0->cfn-lint)
  Downloading attrs-26.1.0-py3-none-any.whl.metadata (8.8 kB)
Collecting jsonschema-specifications>=2023.03.6 (from jsonschema<5,>=4.23->aws-sam-translator>=1.110.0->cfn-lint)
  Downloading jsonschema_specifications-2025.9.1-py3-none-any.whl.metadata (2.9 kB)
Collecting referencing>=0.28.4 (from jsonschema<5,>=4.23->aws-sam-translator>=1.110.0->cfn-lint)
  Downloading referencing-0.37.0-py3-none-any.whl.metadata (2.8 kB)
Collecting rpds-py>=0.25.0 (from jsonschema<5,>=4.23->aws-sam-translator>=1.110.0->cfn-lint)
  Downloading rpds_py-2026.6.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.1 kB)
Collecting annotated-types>=0.6.0 (from pydantic~=2.13.3->aws-sam-translator>=1.110.0->cfn-lint)
  Downloading annotated_types-0.7.0-py3-none-any.whl.metadata (15 kB)
Collecting pydantic-core==2.46.4 (from pydantic~=2.13.3->aws-sam-translator>=1.110.0->cfn-lint)
  Downloading pydantic_core-2.46.4-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.6 kB)
Collecting typing-inspection>=0.4.2 (from pydantic~=2.13.3->aws-sam-translator>=1.110.0->cfn-lint)
  Downloading typing_inspection-0.4.2-py3-none-any.whl.metadata (2.6 kB)
Requirement already satisfied: six>=1.5 in /root/.pyenv/versions/3.11.15/lib/python3.11/site-packages (from python-dateutil<3.0.0,>=2.1->botocore<1.44.0,>=1.43.33->boto3<2.0.0,>=1.34.0->aws-sam-translator>=1.110.0->cfn-lint) (1.17.0)
Collecting mpmath<1.4,>=1.1.0 (from sympy>=1.14.0->cfn-lint)
  Downloading mpmath-1.3.0-py3-none-any.whl.metadata (8.6 kB)
Collecting jsonpointer>=1.9 (from jsonpatch->cfn-lint)
  Downloading jsonpointer-3.1.1-py3-none-any.whl.metadata (2.4 kB)
Downloading cfn_lint-1.52.1-py3-none-any.whl (5.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.0/5.0 MB 87.3 MB/s  0:00:00
Downloading networkx-3.6.1-py3-none-any.whl (2.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.1/2.1 MB 132.8 MB/s  0:00:00
Downloading aws_sam_translator-1.111.0-py3-none-any.whl (440 kB)
Downloading jsonschema-4.26.0-py3-none-any.whl (90 kB)
Downloading pydantic-2.13.4-py3-none-any.whl (472 kB)
Downloading pydantic_core-2.46.4-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.1/2.1 MB 135.8 MB/s  0:00:00
Downloading annotated_types-0.7.0-py3-none-any.whl (13 kB)
Downloading attrs-26.1.0-py3-none-any.whl (67 kB)
Downloading jsonschema_specifications-2025.9.1-py3-none-any.whl (18 kB)
Downloading referencing-0.37.0-py3-none-any.whl (26 kB)
Downloading rpds_py-2026.6.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (371 kB)
Downloading sympy-1.14.0-py3-none-any.whl (6.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.3/6.3 MB 149.9 MB/s  0:00:00
Downloading mpmath-1.3.0-py3-none-any.whl (536 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 536.2/536.2 kB 32.0 MB/s  0:00:00
Downloading typing_extensions-4.16.0-py3-none-any.whl (45 kB)
Downloading typing_inspection-0.4.2-py3-none-any.whl (14 kB)
Downloading jsonpatch-1.33-py2.py3-none-any.whl (12 kB)
Downloading jsonpointer-3.1.1-py3-none-any.whl (7.7 kB)
Downloading regex-2026.6.28-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (799 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 799.9/799.9 kB 68.1 MB/s  0:00:00
Installing collected packages: mpmath, typing_extensions, sympy, rpds-py, regex, networkx, jsonpointer, attrs, annotated-types, typing-inspection, referencing, pydantic-core, jsonpatch, pydantic, jsonschema-specifications, jsonschema, aws-sam-translator, cfn-lint

Successfully installed annotated-types-0.7.0 attrs-26.1.0 aws-sam-translator-1.111.0 cfn-lint-1.52.1 jsonpatch-1.33 jsonpointer-3.1.1 jsonschema-4.26.0 jsonschema-specifications-2025.9.1 mpmath-1.3.0 networkx-3.6.1 pydantic-2.13.4 pydantic-core-2.46.4 referencing-0.37.0 regex-2026.6.28 rpds-py-2026.6.3 sympy-1.14.0 typing-inspection-0.4.2 typing_extensions-4.16.0
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.

[notice] A new release of pip is available: 26.0.1 -> 26.1.2
[notice] To update, run: pip install --upgrade pip

[Container] 2026/07/04 14:26:23.404765 Phase complete: INSTALL State: SUCCEEDED
[Container] 2026/07/04 14:26:23.404789 Phase context status code:  Message: 
[Container] 2026/07/04 14:26:23.445625 Entering phase PRE_BUILD
[Container] 2026/07/04 14:26:23.448018 Phase complete: PRE_BUILD State: SUCCEEDED
[Container] 2026/07/04 14:26:23.448034 Phase context status code:  Message: 
[Container] 2026/07/04 14:26:23.495522 Entering phase BUILD
[Container] 2026/07/04 14:26:23.496863 Running command cd src

[Container] 2026/07/04 14:26:23.503069 Running command cfn-lint template.yaml
E3031 'GetAtt LambdaExecutionRole.Arn' does not match '^arn:(aws[a-zA-Z-]*)?:iam::\\d{12}:role/?[a-zA-Z_0-9+=,.@\\-_/]+$'
template.yaml:68:7

W2531 Runtime 'python3.9' was deprecated on '2025-12-15'. Creation was disabled on '2027-02-01' and update on '2027-03-03'. Please consider updating to 'python3.14'
template.yaml:69:7

E6101 {'Fn::GetAttr': 'JamChallengeLambdaFunction.Arn'} is not of type 'string'
template.yaml:80:5

[Container] 2026/07/04 14:26:27.804075 Command did not exit successfully cfn-lint template.yaml exit status 6
[Container] 2026/07/04 14:26:27.810037 Phase complete: BUILD State: FAILED
[Container] 2026/07/04 14:26:27.810073 Phase context status code: COMMAND_EXECUTION_ERROR Message: Error while executing command: cfn-lint template.yaml. Reason: exit status 6
[Container] 2026/07/04 14:26:27.852131 Entering phase POST_BUILD
[Container] 2026/07/04 14:26:27.855069 Phase complete: POST_BUILD State: SUCCEEDED
[Container] 2026/07/04 14:26:27.855082 Phase context status code:  Message: 
[Container] 2026/07/04 14:26:27.914480 Set report auto-discover timeout to 5 seconds
[Container] 2026/07/04 14:26:27.914583 Expanding base directory path:  .
[Container] 2026/07/04 14:26:27.919249 Assembling file list
[Container] 2026/07/04 14:26:27.919266 Expanding .
[Container] 2026/07/04 14:26:27.921025 Expanding file paths for base directory .
[Container] 2026/07/04 14:26:27.921039 Assembling file list
[Container] 2026/07/04 14:26:27.921043 Expanding **/*
[Container] 2026/07/04 14:26:27.922926 No matching auto-discover report paths found
[Container] 2026/07/04 14:26:27.922944 Report auto-discover file discovery took 0.008463 seconds
[Container] 2026/07/04 14:26:27.922969 Phase complete: UPLOAD_ARTIFACTS State: SUCCEEDED
[Container] 2026/07/04 14:26:27.922986 Phase context status code:  Message: 
```

logs security check

```bash
[Container] 2026/07/04 13:09:39.971036 Running on CodeBuild On-demand
[Container] 2026/07/04 13:09:39.971055 Waiting for agent ping
[Container] 2026/07/04 13:09:40.172721 Waiting for DOWNLOAD_SOURCE
[Container] 2026/07/04 13:09:41.252969 Phase is DOWNLOAD_SOURCE
[Container] 2026/07/04 13:09:41.254042 CODEBUILD_SRC_DIR=/codebuild/output/src3434495681/src
[Container] 2026/07/04 13:09:41.254686 YAML location is /codebuild/output/src3434495681/src/buildspec-security.yml
[Container] 2026/07/04 13:09:41.256543 Setting HTTP client timeout to higher timeout for S3 source
[Container] 2026/07/04 13:09:41.256648 Processing environment variables
[Container] 2026/07/04 13:09:41.504059 Selecting 'ruby' runtime version '3.2' based on manual selections...
[Container] 2026/07/04 13:09:41.505175 Running command echo "Installing Ruby version 3.2 ..."
Installing Ruby version 3.2 ...

[Container] 2026/07/04 13:09:41.512269 Running command rbenv global $RUBY_32_VERSION

[Container] 2026/07/04 13:09:41.888039 Moving to directory /codebuild/output/src3434495681/src
[Container] 2026/07/04 13:09:41.888065 Cache is not defined in the buildspec
[Container] 2026/07/04 13:09:41.929284 Skip cache due to: no paths specified to be cached
[Container] 2026/07/04 13:09:41.932665 Registering with agent
[Container] 2026/07/04 13:09:41.983232 Phases found in YAML: 2
[Container] 2026/07/04 13:09:41.983254  INSTALL: 2 commands
[Container] 2026/07/04 13:09:41.983259  BUILD: 1 commands
[Container] 2026/07/04 13:09:41.983623 Phase complete: DOWNLOAD_SOURCE State: SUCCEEDED
[Container] 2026/07/04 13:09:41.983639 Phase context status code:  Message: 
[Container] 2026/07/04 13:09:42.087893 Entering phase INSTALL
[Container] 2026/07/04 13:09:42.127443 Running command apt-get update -y
Hit:1 https://apt.corretto.aws stable InRelease
Get:2 https://cli.github.com/packages stable InRelease [3917 B]
Get:3 https://dl.google.com/linux/chrome-stable/deb stable InRelease [1825 B]
Get:4 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
Hit:5 http://archive.ubuntu.com/ubuntu jammy InRelease
Get:6 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy-backports InRelease [127 kB]
Get:8 https://ppa.launchpadcontent.net/mozillateam/ppa/ubuntu jammy InRelease [24.6 kB]
Get:9 https://cli.github.com/packages stable/main amd64 Packages [355 B]
Get:10 https://dl.google.com/linux/chrome-stable/deb stable/main amd64 Packages [1214 B]
Get:11 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [4083 kB]
Get:12 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [1308 kB]
Get:13 http://security.ubuntu.com/ubuntu jammy-security/main i386 Packages [1044 kB]
Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/main i386 Packages [1268 kB]
Get:15 http://security.ubuntu.com/ubuntu jammy-security/universe i386 Packages [860 kB]
Get:16 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [7332 kB]
Get:17 http://archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [7600 kB]
Get:18 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [4415 kB]
Get:19 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [1613 kB]
Get:20 http://archive.ubuntu.com/ubuntu jammy-updates/universe i386 Packages [998 kB]
Get:21 http://archive.ubuntu.com/ubuntu jammy-updates/restricted i386 Packages [64.2 kB]
Get:22 https://ppa.launchpadcontent.net/mozillateam/ppa/ubuntu jammy/main i386 Packages [2376 B]
Get:23 https://ppa.launchpadcontent.net/mozillateam/ppa/ubuntu jammy/main amd64 Packages [43.4 kB]
Fetched 31.0 MB in 3s (11.3 MB/s)
Reading package lists...

[Container] 2026/07/04 13:09:51.830367 Running command gem install cfn-nag
Successfully installed optimist-3.0.1
Successfully installed netaddr-2.0.6
Successfully installed multi_json-1.21.1
Successfully installed little-plugger-1.1.4
Successfully installed logging-2.2.2
Successfully installed lightly-0.3.3
Building native extensions. This could take a while...
Successfully installed psych-3.3.4
Successfully installed kwalify-0.7.2
Successfully installed cfn-model-0.6.6
Successfully installed aws-eventstream-1.4.0
Successfully installed aws-sigv4-1.12.1
Successfully installed jmespath-1.6.2
Successfully installed aws-partitions-1.1265.0
Successfully installed aws-sdk-core-3.252.0
Successfully installed aws-sdk-kms-1.129.0
Successfully installed aws-sdk-s3-1.226.0
Successfully installed cfn-nag-0.8.10
Parsing documentation for optimist-3.0.1
Installing ri documentation for optimist-3.0.1
Parsing documentation for netaddr-2.0.6
Installing ri documentation for netaddr-2.0.6
Parsing documentation for multi_json-1.21.1
Installing ri documentation for multi_json-1.21.1
Parsing documentation for little-plugger-1.1.4
Installing ri documentation for little-plugger-1.1.4
Parsing documentation for logging-2.2.2
Installing ri documentation for logging-2.2.2
Parsing documentation for lightly-0.3.3
Installing ri documentation for lightly-0.3.3
Parsing documentation for psych-3.3.4
Installing ri documentation for psych-3.3.4
Parsing documentation for kwalify-0.7.2
Installing ri documentation for kwalify-0.7.2
Parsing documentation for cfn-model-0.6.6
Installing ri documentation for cfn-model-0.6.6
Parsing documentation for aws-eventstream-1.4.0
Installing ri documentation for aws-eventstream-1.4.0
Parsing documentation for aws-sigv4-1.12.1
Installing ri documentation for aws-sigv4-1.12.1
Parsing documentation for jmespath-1.6.2
Installing ri documentation for jmespath-1.6.2
Parsing documentation for aws-partitions-1.1265.0
Installing ri documentation for aws-partitions-1.1265.0
Parsing documentation for aws-sdk-core-3.252.0
Installing ri documentation for aws-sdk-core-3.252.0
Parsing documentation for aws-sdk-kms-1.129.0
Installing ri documentation for aws-sdk-kms-1.129.0
Parsing documentation for aws-sdk-s3-1.226.0
Installing ri documentation for aws-sdk-s3-1.226.0
Parsing documentation for cfn-nag-0.8.10
Installing ri documentation for cfn-nag-0.8.10
Done installing documentation for optimist, netaddr, multi_json, little-plugger, logging, lightly, psych, kwalify, cfn-model, aws-eventstream, aws-sigv4, jmespath, aws-partitions, aws-sdk-core, aws-sdk-kms, aws-sdk-s3, cfn-nag after 15 seconds
17 gems installed

[Container] 2026/07/04 13:10:20.649583 Phase complete: INSTALL State: SUCCEEDED
[Container] 2026/07/04 13:10:20.649606 Phase context status code:  Message: 
[Container] 2026/07/04 13:10:20.692139 Entering phase PRE_BUILD
[Container] 2026/07/04 13:10:20.694953 Phase complete: PRE_BUILD State: SUCCEEDED
[Container] 2026/07/04 13:10:20.694969 Phase context status code:  Message: 
[Container] 2026/07/04 13:10:20.732996 Entering phase BUILD
[Container] 2026/07/04 13:10:20.735545 Running command pwdir=$(pwd)
cfn_nag_scan --input-path $pwdir/src/
------------------------------------------------------------
/codebuild/output/src3434495681/src/src/template.yaml
------------------------------------------------------------------------------------------------------------------------
| WARN W11
|
| Resource: ["LambdaExecutionRole"]
| Line Numbers: [38]
|
| IAM role should not allow * resource on its permissions policy
------------------------------------------------------------
| WARN W58
|
| Resource: ["JamChallengeLambdaFunction"]
| Line Numbers: [60]
|
| Lambda functions require permission to write CloudWatch Logs
------------------------------------------------------------
| WARN W89
|
| Resource: ["JamChallengeLambdaFunction"]
| Line Numbers: [60]
|
| Lambda functions should be deployed inside a VPC
------------------------------------------------------------
| WARN W92
|
| Resource: ["JamChallengeLambdaFunction"]
| Line Numbers: [60]
|
| Lambda functions should define ReservedConcurrentExecutions to reserve simultaneous executions
------------------------------------------------------------
| WARN W28
|
| Resource: ["LambdaExecutionRole"]
| Line Numbers: [38]
|
| Resource found with an explicit name, this disallows updates that require replacement of this resource
------------------------------------------------------------
| WARN W9
|
| Resource: ["LambdaSecurityGroup"]
| Line Numbers: [27]
|
| Security Groups found with ingress cidr that is not /32
------------------------------------------------------------
| FAIL F1000
|
| Resource: ["LambdaSecurityGroup"]
| Line Numbers: [27]
|
| Missing egress rule means all traffic is allowed outbound.  Make this explicit if it is desired configuration
------------------------------------------------------------
| WARN W36
|
| Resource: ["LambdaSecurityGroup"]
| Line Numbers: [27]
|
| Security group rules without a description obscure their purpose and may lead to bad practices in ensuring they only allow traffic from the ports and sources/destinations required.

Failures count: 1
Warnings count: 7

[Container] 2026/07/04 13:10:21.453107 Command did not exit successfully pwdir=$(pwd)
cfn_nag_scan --input-path $pwdir/src/ exit status 1
[Container] 2026/07/04 13:10:21.458491 Phase complete: BUILD State: FAILED
[Container] 2026/07/04 13:10:21.458508 Phase context status code: COMMAND_EXECUTION_ERROR Message: Error while executing command: pwdir=$(pwd)
cfn_nag_scan --input-path $pwdir/src/. Reason: exit status 1
[Container] 2026/07/04 13:10:21.498210 Entering phase POST_BUILD
[Container] 2026/07/04 13:10:21.500974 Phase complete: POST_BUILD State: SUCCEEDED
[Container] 2026/07/04 13:10:21.500988 Phase context status code:  Message: 
[Container] 2026/07/04 13:10:21.549009 Set report auto-discover timeout to 5 seconds
[Container] 2026/07/04 13:10:21.549094 Expanding base directory path:  .
[Container] 2026/07/04 13:10:21.551107 Assembling file list
[Container] 2026/07/04 13:10:21.551122 Expanding .
[Container] 2026/07/04 13:10:21.553060 Expanding file paths for base directory .
[Container] 2026/07/04 13:10:21.553073 Assembling file list
[Container] 2026/07/04 13:10:21.553076 Expanding **/*
[Container] 2026/07/04 13:10:21.555231 No matching auto-discover report paths found
[Container] 2026/07/04 13:10:21.555282 Report auto-discover file discovery took 0.006273 seconds
[Container] 2026/07/04 13:10:21.555295 Phase complete: UPLOAD_ARTIFACTS State: SUCCEEDED
[Container] 2026/07/04 13:10:21.555328 Phase context status code:  Message: 

```

a