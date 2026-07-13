# JAM Eleve seu jogo de política de IAM

```jsx
Visão geral
Você é engenheiro de segurança e trabalha na UnicornLimited. Sua empresa adquiriu recentemente a BlackHatUnicorns. Como parte da equipe técnica de due diligence, você precisa auditar (e possivelmente corrigir) algumas das políticas do AWS IAM. Sua tarefa é criar um trabalho em lotes para analisar e relatar as descobertas existentes e remediar quaisquer violações para evitar danos à UnicornLimited.
```

```jsx
Tarefa 1: Crie sua função Lambda de avaliação do IAM
Pontos possíveis
80
Penalidade por pista
18
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
A primeira tarefa é criar uma função do AWS Lambda para usar programaticamente o recurso de validação de políticas do IAM Access Analyzer.

Você pode validar suas políticas usando as verificações de políticas do AWS IAM Access Analyzer. Você pode criar ou editar uma política usando a CLI da AWS, a API da AWS ou o editor de políticas JSON no console do IAM. O Access Analyzer valida sua política em relação à gramática e às melhores práticas do IAM. Você pode ver as descobertas da verificação de validação de políticas que incluem avisos de segurança, erros, avisos gerais e sugestões para sua política. Essas descobertas fornecem recomendações práticas que ajudam você a criar políticas que sejam funcionais e estejam em conformidade com as melhores práticas de segurança.

Inventário
Você tem uma função Lambda jam-validate-iam-policy-with-access-analyzer.

Sua tarefa
Atualize a função do AWS Lambda jam-validate-iam-policy-with-access-analyzer para usar a capacidade de validação de políticas do IAM Access Analyzer.

Por onde começar
No Console de Gerenciamento da AWS, acesse o console do AWS Lambda e revise o código-fonte jam-validate-iam-policy-with-access-analyzer da função Lambda. O desafio será aprovado automaticamente quando você atualizar o código-fonte.

Pistas
Saiba mais sobre a validação da política do IAM Access Analyzer.
8Pontos de penalidade
Mostrar pista
Use o AWS SDK para Python para identificar a chamada da API de validação de políticas do IAM Access Analyzer.
10Pontos de penalidade
Mostrar pista
Solução
12Pontos de penalidade

Tarefa 2: Adicione um gatilho à sua função do Lambda
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Agora você tem uma função do Lambda capaz de avaliar as políticas do IAM usando o IAM Access Analyzer. Você deseja executar essa função periodicamente para garantir que as políticas de IAM novas ou atualizadas sejam avaliadas.

Inventário
Você tem uma função do Lambda jam-validate-iam-policy-with-access-analyzer.

Sua tarefa
Anexe um gatilho à função Lambda para execução todos os dias.

Por onde começar
Você pode começar a explorar AWS Lambda Triggers acessando o console Amazon AWS Lambda. O desafio será validado automaticamente quando o gatilho correto for anexado.

Pistas
Amazon Lambda Triggers em seu socorro
4Pontos de penalidade
Desbloqueie o Clue
Crie um evento de gatilho que seja acionado diariamente
5Pontos de penalidade
Desbloqueie o Clue
Solução
6Pontos de penalidade
Desbloqueie o Clue

Tarefa 3: Corrija as descobertas do IAM Access Analyzer
Pontos possíveis
80
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Agora, você tem uma função do AWS Lambda capaz de avaliar as políticas do AWS IAM usando o IAM Access Analyzer diariamente.

Inventário
Você tem uma função do Lambda jam-validate-iam-policy-with-access-analyzer.

Você tem uma regra de evento agendado do Amazon EventBridge, criada na etapa anterior.

Sua tarefa
Investigue e corrija as descobertas do IAM Access Analyzer geradas após a avaliação das políticas existentes do IAM. A tarefa será aprovada automaticamente quando todos os problemas forem resolvidos.

Por onde começar
Você pode começar executando a função Lambda jam-validate-iam-policy-with-access-analyzer e visualizando suas saídas. O desafio será validado automaticamente quando os resultados da execução de jam-validate-iam-policy-with-access-analyzer não contiverem nenhuma descoberta do IAM Access Analyzer.

Pistas
Crie um evento de teste para executar a função Lambda e investigar as descobertas
8Pontos de penalidade
Desbloqueie o Clue
Use o AWS IAM para corrigir suas políticas de IAM
10Pontos de penalidade
Desbloqueie o Clue
Solução
12Pontos de penalidade
Desbloqueie o Clue

```

a