# JAM Você precisa ser um desenvolvedor sênior para aprovar as mudanças no PROD!!

```bash
**Visão geral**
Na Amazon Web Services (AWS), o AWS CodeCommit pode ser usado para hospedar repositórios seguros baseados em Git. O CodeCommit é um serviço de controle de fonte totalmente gerenciado. Recentemente, houve uma interrupção em um dos aplicativos da web hospedados em um desses repositórios. O gerenciamento de mudanças identificou que mudanças não intencionais foram transferidas para a produção.

Sendo engenheiro de DevOps neste projeto, você foi designado para evitar que isso aconteça no futuro.

Além disso, você foi encarregado de mesclar as últimas mudanças de desenvolvimento no ramo de produção, garantindo que somente membros da função de desenvolvedor sênior possam aprovar essas mudanças.

Além disso, você precisa adicionar a etapa de revisão e aprovação a todos os novos repositórios de forma automatizada.
```

```bash
Tarefa 1: Restrinja a aprovação à função de Desenvolvedores Sêniores
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Na Amazon Web Services (AWS), o AWS CodeCommit pode ser usado para hospedar repositórios seguros baseados em Git. O CodeCommit é um serviço de controle de fonte totalmente gerenciado. Recentemente, houve uma interrupção em um dos aplicativos da web hospedados em um desses repositórios. O gerenciamento de mudanças identificou que mudanças não intencionais foram transferidas para a produção. Você foi designado para evitar que isso aconteça no futuro.

Durante sua investigação, você identificou que a base de código para esse aplicativo da web está no repositório de codecommit WebApplicationRepo. Além disso, não há aprovações e controles para a solicitação pull neste repositório, permitindo que qualquer pessoa com acesso a essa conta da AWS aprove e mescle o código na ramificação Prod.

Tarefa
Permita que somente membros da função **SeniorDevelopers/\ *** aprovem quaisquer alterações na ramificação Prod do repositório WebApplicationRepo

Começando
Navegue até o console codecommit do CodeCommit.
Encontre e modifique modelos de regras de aprovação. Esteja ciente de qualquer caractere de espaço em branco
Serviços usados
AWS CodeCommit, função do IAM

Validação de tarefas
Quando configurado corretamente, somente membros do SeniorDevelopers devem ser capazes de aprovar pull requests. A tarefa será automaticamente marcada como concluída em alguns minutos se você for bem-sucedido. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na seção de detalhes do desafio.

Tarefa 2: Combine as mudanças mais recentes na produção
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Um dos recursos do Git é a capacidade de criar e mesclar ramificações com facilidade. A natureza distribuída do Git incentiva os usuários a criar novas ramificações com frequência e a mesclá-las regularmente como parte do processo de desenvolvimento. Isso melhora fundamentalmente o fluxo de trabalho de desenvolvimento para a maioria dos projetos, incentivando confirmações menores, mais focadas e granulares.

Há algumas mudanças de código no ambiente de desenvolvimento feitas pelos membros da sua equipe. Você foi solicitado a mover essas alterações para a produção. As ramificações e o repositório já foram criados para você.

Tarefa
Mescle as últimas alterações Dev na ramificação Prod para WebApplicationRepo

Começando
Navegue até o console codecommit
Envie uma solicitação pull para prod branch para o repositório WebApplicationRepo
Navegue até o console do IAM. Encontre o link de login para mudar de função para SeniorDevelopers
Mude a função para SeniorDevelopers para fornecer aprovações. Caso contrário, você usará sua função padrão fornecida para quaisquer outras atividades.
Execute as atividades conforme mencionado na tarefa
Lembre-se de voltar para o usuário original após concluir a tarefa.
Serviços usados
AWS CodeCommit, função do IAM

Validação de tarefas
Quando configurados corretamente, somente membros deSeniorDevelopers devem poder aprovar pull requests. A tarefa será automaticamente marcada como concluída em alguns minutos se você for bem-sucedido. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na seção de detalhes do desafio.

Tarefa 3: Todos os novos repositórios devem ser associados à regra de aprovação
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
O gerenciamento de mudanças identificou que, para outros repositórios, as mudanças de desenvolvimento ainda estão sendo mescladas à filial de produção sem qualquer revisão/aprovação de código pelos membros seniores da equipe. Na Investigação, você identificou que esses novos repositórios não estão associados a nenhum modelo de aprovação.

Tarefa
Todos os novos repositórios devem ser associados à regra de aprovação, que é criada na Tarefa 1.

Começando
Navegue até o console do EventBridge
Descubra como você pode conseguir isso usando o AWS Lambda e o EventBridge. Para começar, o Lambda Fuction - ApprovalFlowLambdaFunctionForNewRepo e o stub EventBridge Rule - ApprovalFlowEventTriggerForNewRepo já foram criados.
Adicione as alterações necessárias à regra do Eventbridge ApprovalFlowEventTriggerForNewRepo
Exemplo de evento de trilha em nuvem recebido
event = {
    "version": "0",
    "id": "36eb8523-97d0-4518-b33d-ee3579ff19f0",
    "detail-type": "AWS API Call via CloudTrail",
    "source": "aws.codecommit",
    "detail": {
            "eventTime": "2016-02-20T01:09:13Z",
            "eventSource": "codecommit.amazonaws.com",
            "eventName": "CreateRepository",
            "requestParameters": {
               "repositoryName": ""
            },
            "eventType": "AwsApiCall"
        }
    }  
Nota: Não marque a opção**Usar função de execução (recomendada) **

Serviços usados
Regras do AWS Lambda e do Amazon EventBridge

Validação de tarefas
Quando configurado corretamente, todos os novos repositórios devem ser associados aos modelos de regras de aprovação. A tarefa será automaticamente marcada como concluída em alguns minutos se você for bem-sucedido. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na seção de detalhes do desafio.

```

a