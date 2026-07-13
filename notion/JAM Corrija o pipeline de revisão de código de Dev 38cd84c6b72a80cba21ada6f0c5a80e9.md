# JAM Corrija o pipeline de revisão de código de DevOps quebrado (medio) nao fiz

esse eu nao coseguir fazer eu vou so anotar para estudar ferozmente esse JAM, eu preciso entender esses conceitos novos

VISAL GERAL:

```verilog
Você é engenheiro de DevOps na BananaCode, uma empresa peculiar de desenvolvimento de software conhecida por seus aplicativos inovadores e espaços de escritório com tema amarelo. Sua equipe está experimentando um sistema de revisão de código baseado em IA para acelerar o desenvolvimento e, ao mesmo tempo, manter a qualidade do código. Ontem, o engenheiro-chefe saiu de férias depois de fazer “pequenos ajustes” no sistema. Esta manhã, os desenvolvedores estão relatando que as revisões automatizadas de código pararam completamente de funcionar e que as implantações críticas agora estão paralisadas.

O CTO está em pânico porque uma grande demonstração para clientes está agendada para amanhã. O pipeline quebrado usa o Amazon Bedrock Agent para analisar o código, um fluxo de trabalho do LangGraph para tomar decisões inteligentes e o CodePipeline para implantar as alterações aprovadas. Você precisa diagnosticar e corrigir rapidamente os componentes desconectados antes da demonstração.

Neste desafio, você reparará o pipeline de DevOps baseado em IA corrigindo erros de configuração, depurando a lógica do fluxo de trabalho, corrigindo instruções de processamento de arquivos e restaurando a automação da implantação, tudo isso enquanto aprende como os agentes de IA podem aprimorar seus processos de DevOps.

! Diagrama de pipeline
```

task 1:

```verilog
Tarefa 1: Corrigir a configuração do Bedrock Agent
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Plano de fundo
O pipeline de revisão de código baseado em IA da BananaCode parou de funcionar repentinamente. O sistema automatizado que estava processando as revisões de código ontem agora está falhando completamente. A investigação inicial mostra que o Amazon Bedrock Agent responsável por iniciar as revisões de código está enfrentando falhas ao tentar executar suas ações configuradas.

Sua tarefa
Como engenheiro de DevOps da BananaCode, você precisa investigar e resolver os problemas de execução de ações que impedem o Bedrock Agent de processar com êxito as solicitações de revisão de código. O agente parece estar configurado com “grupos de ação”, mas a execução da lógica de negócios está falhando.

Começando
Nessa tarefa, você solucionará e corrigirá a configuração do Bedrock Agent. O agente parece ter problemas de configuração que estão impedindo a execução bem-sucedida das operações de revisão de código. Você precisará investigar a configuração atual do agente e identificar o que está causando as falhas

Inventário
Os seguintes serviços são provisionados:

Base da Amazônia
Agente Amazon Bedrock
Função AWS Lambda (fluxo de trabalho LangGraph)
Serviços que você deve usar
Base da Amazônia
AWS Lambda
Validação de tarefas
Depois de concluir a tarefa, o Bedrock Agent deve invocar com êxito a função Lambda correta do fluxo de trabalho sem erros de conexão. O parâmetro de validação agentInvocationSuccess rastreará se o agente faz chamadas de API bem-sucedidas para o sistema de fluxo de trabalho de back-end.

Pistas
Primeiros passos
4Pontos de penalidade
Desbloqueie o Clue
Etapas de configuração detalhadas
5Pontos de penalidade
Desbloqueie o Clue
```

task 2:

```verilog
Propriedades de saída
ApprovedCodeStatus
Code approved and uploaded successfully

BedrockAgentId
ZXBWKJM748

CodeFilesBucketName
jam-code-files-885638421653-us-west-2

CorrectLambdaArn
arn:aws:lambda:us-west-2:885638421653:function:LabStack-prewarm-67417169--LangGraphWorkflowLambda-UM1VDrvSTJWd

OldCodeBucketName
bananacode-old-code-885638421653-us-west-2

PipelineName
BananaCode-Deployment-Pipeline

ReviewedCodeBucketName
bananacode-reviewed-code-885638421653-us-west-2

SampleFiles
sample.py, test.py, example.js, app.js

WrongLambdaArn
arn:aws:lambda:us-west-2:885638421653:function:LabStack-prewarm-67417169-75f4-DummyLambdaFunction-tWTWOfns7z1Z

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Depurar a lógica da máquina de estado LangGraph
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Plano de fundo
O fluxo de trabalho LangGraph do BananaCode é o cérebro do sistema de revisão de código, projetado para executar uma sequência de estados: buscar → analisar → validar → aprovar/rejeitar. No entanto, o fluxo de trabalho está atualmente interrompido e ignora o estado crítico de “análise”, encaminhando todo o código diretamente para aprovação sem a devida revisão. A partir de agora, o sistema aprova automaticamente todo o código enviado, independentemente da qualidade, mas deve rejeitar de forma inteligente o código de baixa qualidade e aprovar somente o código que atenda aos padrões de qualidade de produção.

Sua tarefa
Como engenheiro de DevOps do BananaCode, você precisa corrigir a lógica do fluxo de trabalho do LangGraph (execute_workflow ()) na função Lambda. Você deve restaurar a transição de estado adequada de “buscar” para “analisar” e implementar uma lógica condicional que direcione o código para “aprovar” ou “rejeitar” com base nos resultados da análise.

Começando
Sua missão é corrigir um fluxo de trabalho de máquina de estado quebrado no AWS Lambda. O fluxo de trabalho serve para analisar a qualidade do código e tomar decisões automatizadas, mas não está funcionando corretamente.

Requisitos:
Encontre e depure a função Lambda relevante

Corrija as transições de estado interrompidas na função de fluxo de trabalho:

Garanta transições de estado de “busca” para “analisar”

Implemente uma lógica de controle de qualidade que direcione o código para “aprovar” ou “rejeitar” com base no ['analysis_score'] para que:

Processa automaticamente código de alta qualidade

Encaminha código de baixa qualidade para revisão manual (ou seja, rejeição)

Usa o benchmark do setor de 0,7 (70%) para a tomada de decisões

Consulte a documentação a seguir para obter mais informações sobre o LangGraph:

Por que LangGraph?

Crie filiais

Conceitos de baixo nível

Gráfico de estado

Inventário
Os seguintes serviços são provisionados:

AWS Lambda (função de fluxo de trabalho LangGraph)
Biblioteca LangGraph (pré-instalada na camada Lambda)
Serviços que você deve usar
AWS Lambda
Registros do Amazon CloudWatch
Validação de tarefas
Depois de concluir a tarefa, todos os 4 estados do fluxo de trabalho (buscar, analisar, validar, aprovar/rejeitar) devem ser executados em sequência. O parâmetro de validação workflowStatesExecuted contará quantos estados do fluxo de trabalho são executados corretamente durante uma revisão de código.

Pistas
Primeiros passos
4Pontos de penalidade
Desbloqueie o Clue
Etapas detalhadas de depuração
5Pontos de penalidade
Desbloqueie o Clue
```

task 3:

```verilog
Corrija o pipeline de revisão de código de DevOps quebrado
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
ApprovedCodeStatus
Code approved and uploaded successfully

BedrockAgentId
ZXBWKJM748

CodeFilesBucketName
jam-code-files-885638421653-us-west-2

CorrectLambdaArn
arn:aws:lambda:us-west-2:885638421653:function:LabStack-prewarm-67417169--LangGraphWorkflowLambda-UM1VDrvSTJWd

OldCodeBucketName
bananacode-old-code-885638421653-us-west-2

PipelineName
BananaCode-Deployment-Pipeline

ReviewedCodeBucketName
bananacode-reviewed-code-885638421653-us-west-2

SampleFiles
sample.py, test.py, example.js, app.js

WrongLambdaArn
arn:aws:lambda:us-west-2:885638421653:function:LabStack-prewarm-67417169-75f4-DummyLambdaFunction-tWTWOfns7z1Z

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 3: Instruções corretas do agente e processamento de arquivos
Pontos possíveis
15
Penalidade por pista
0
Pontos disponíveis
15
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Até agora, você restaurou com sucesso a conexão do Bedrock Agent com o fluxo de trabalho do LangGraph e corrigiu a lógica da máquina de estados. Agora que o agente pode se comunicar com o sistema de fluxo de trabalho e executar todos os estados necessários, há mais um problema crítico que impede análises de código bem-sucedidas.

O Bedrock Agent é configurado de uma forma que lhe diz como identificar e processar arquivos de código para análise. No entanto, a configuração atual está impedindo que o agente analise adequadamente o código Python. Além disso, as instruções precisam lidar adequadamente com os arquivos JavaScript. Esse problema de configuração significa que arquivos de código legítimos estão sendo ignorados pelo sistema de revisão. Portanto, mesmo que seu fluxo de trabalho esteja funcionando corretamente, nenhum código real está sendo processado.

Sua tarefa
Como engenheiro de DevOps do BananaCode, você precisa concluir a restauração do pipeline corrigindo a configuração do agente. Você deve corrigir a configuração para garantir que o agente possa identificar e processar adequadamente os arquivos Python e JavaScript para que o código possa fluir pelo sistema de fluxo de trabalho recém-reparado.

Começando
Nessa tarefa, você investigará e corrigirá os problemas de configuração do agente. A configuração do agente precisa ser corrigida para garantir que ele possa identificar adequadamente os arquivos para análise. Você precisará localizar e resolver os problemas de configuração para garantir que o pipeline completo funcione de ponta a ponta.

Inventário
Os seguintes serviços são provisionados:

Agente Amazon Bedrock
Bucket Amazon S3 com arquivos de código de amostra
Arquivos de teste: sample.py, example.js, test.py, app.js
Serviços que você deve usar
Base da Amazônia
Amazon S3
Validação de tarefas
Depois de concluir a tarefa, o agente deve reconhecer e processar com êxito os arquivos Python e JavaScript.

Pistas
Primeiros passos
1Pontos de penalidade
Desbloqueie o Clue
Etapas de configuração detalhadas
1Pontos de penalidade
Desbloqueie o Clue
Complete Solution
2Pontos de penalidade
Desbloqueie o Clue
```

task 4:

```verilog
Propriedades de saída
ApprovedCodeStatus
Code approved and uploaded successfully

BedrockAgentId
ZXBWKJM748

CodeFilesBucketName
jam-code-files-885638421653-us-west-2

CorrectLambdaArn
arn:aws:lambda:us-west-2:885638421653:function:LabStack-prewarm-67417169--LangGraphWorkflowLambda-UM1VDrvSTJWd

OldCodeBucketName
bananacode-old-code-885638421653-us-west-2

PipelineName
BananaCode-Deployment-Pipeline

ReviewedCodeBucketName
bananacode-reviewed-code-885638421653-us-west-2

SampleFiles
sample.py, test.py, example.js, app.js

WrongLambdaArn
arn:aws:lambda:us-west-2:885638421653:function:LabStack-prewarm-67417169-75f4-DummyLambdaFunction-tWTWOfns7z1Z

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 4: Restaurar a integração com o CodePipeline
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Agora, você restaurou com sucesso a conexão do Bedrock Agent, corrigiu a lógica do fluxo de trabalho do LangGraph e atualizou as instruções de processamento de arquivos do agente. No entanto, falta uma peça final no pipeline de implantação automatizada do BananaCode. No momento, o CodePipeline que deveria implantar o código aprovado está falhando em ser executado corretamente. Mesmo quando o código passa pelo sistema de revisão de IA com sucesso, o pipeline de implantação não está pegando o código aprovado para implantação.

Sua tarefa
Como engenheiro de DevOps da BananaCode, você precisa concluir a automação de ponta a ponta corrigindo a configuração do CodePipeline. O pipeline deve implantar automaticamente o código que foi reviewed pelo sistema de revisão de IA, mas atualmente não está acessando a fonte correta do código revisado.

Começando
Nessa tarefa, você investigará e reparará os problemas de configuração do CodePipeline. O pipeline precisa ser configurado para acessar adequadamente o código revisado do sistema de revisão e acionar as implantações automaticamente. Lembre-se de que, em um fluxo de trabalho de CI/CD adequado, os pipelines de implantação devem implantar somente o código que tenha passado com sucesso pelo processo de revisão e aprovação, e não o código desatualizado, não revisado ou antigo

Inventário
Os seguintes serviços são provisionados:

AWS CodePipeline (pipeline de implantação de código Banana)
Baldes Amazon S3
Funções do IAM para execução do pipeline
Serviços que você deve usar
AWS CodePipeline
Amazon S3
Validação de tarefas
Depois de concluir a tarefa, o CodePipeline deve ser executado com êxito quando o código for aprovado pelo sistema de revisão de IA. O parâmetro de validação pipelineExecutionSuccess rastreará as execuções bem-sucedidas do pipeline acionadas pelas revisões de código aprovadas.

Pistas
Primeiros passos
4Pontos de penalidade
Desbloqueie o Clue
Etapas de configuração detalhadas
5Pontos de penalidade
Desbloqueie o Clue
```

que jam absurdo eu nao sabia nem o que tava fazendo eu nao vi isso na academy porem e mt imporatante e provavelmente vai cair vai ter que estar nesses 12 dias de JAM