# JAM Proteja os dados de PII

```bash
A ANY Inc., uma empresa líder em comércio eletrônico, migrou recentemente para a nuvem da AWS e começou a usar o Amazon DynamoDB para armazenar pedidos de clientes. A tabela armazena dados do pedido do cliente, incluindo informações confidenciais de identificação pessoal (PII), como nomes, endereços e detalhes de pagamento.

Você, especialista em segurança da ANY INC., foi encarregado de garantir que o acesso à tabela de dados do cliente no Amazon DynamoDB seja rigorosamente controlado usando o princípio do menor privilégio. Você precisa garantir que papéis personalizados sejam criados para cada aplicativo, definindo as permissões precisas que eles teriam na tabela do Amazon DynamoDB. Para aprimorar ainda mais a segurança, você precisa implementar políticas de controle de acesso refinadas no Amazon DynamoDB, permitindo que aplicativos específicos acessem somente os dados necessários com base na função do usuário e no contexto da solicitação.

Ao implementar essas políticas, os clientes da ANY terão a certeza de que suas informações confidenciais estão sendo protegidas por um sistema de controle de acesso abrangente e baseado em funções.
```

```bash
Tarefa 1: CORRIGIR ACESSO NEGADO À CONSULTA DO BANCO DE DADOS
Pontos possíveis
15
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Há uma tabela do Amazon DynamoDB chamada OrderTable com chave primária CustomerID em sua conta da AWS. Uma API está tentando consultar a tabela do Amazon DynamoDB por meio do AWS Lambda chamada AWSLambdaFunction. Esse AWS Lambda recebe uma função do IAM chamada lambda_execution_role com o nome da política jamawsLambdaPolicy anexado a ela. No entanto, essa chamada de API retorna o acesso negado, o AWS Lambda não tem permissão para executar a consulta. Você pode brincar com o AWS Lambda “QueryDynamodBlambdaFunction”, que pode ser invocado e ver os resultados para sua referência

Sua tarefa
Para concluir a tarefa, corrija o problema de acesso negado sempre que esse AWS Lambda estiver tentando consultar a tabela do Amazon DynamoDB.

Começando
O AWS Identity and Access Management (AWS IAM) é um serviço da AWS que ajuda um administrador a controlar com segurança o acesso aos recursos da AWS. Os administradores do AWS IAM controlam quem pode ser autenticado (conectado) e autorizado (ter permissões) para usar os recursos do Amazon DynamoDB.

Um documento detalhado da AWS sobre como usar a política do AWS IAM para acessar o Amazon DynamoDB pode ser encontrado nas documentações públicas da AWS

Inventário
Sua conta da AWS foi provisionada com os seguintes recursos:

AWS Lambda
AWS DynamoDB
Função do AWS IAM
Serviços que você deve usar
ERA O OBJETIVO
Amazon DynamoDB
Validação de tarefas
A tarefa será concluída automaticamente quando a política do AWS IAM for configurada corretamente. Como alternativa, você pode clicar no botão check my progress para verificar o progresso da sua tarefa.

Tarefa 2: Inserir dados no banco de dados do Amazon Dynamo
Pontos possíveis
15
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Há uma tabela do Amazon DynamoDB chamada OrderTable em sua conta da AWS que foi criada para você. A tabela está vazia e a chave primária é CustomerID. Você pode brincar com o AWS Lambda QueryDynamoDBLambdaFunction, que pode ser invocado e ver os resultados para sua referência. Você pode executar esse AWS Lambda antes de concluir essa tarefa e ver que a tabela está vazia e, quando a tarefa for concluída, você poderá ver os itens inseridos.

Sua tarefa
Para concluir a tarefa, você precisa inserir dois itens na tabela vazia chamada OrderTable.

Detalhes abaixo: -

item-1, 
{
 "CustomerID": "Customer1",
 "OrderID": 1,
 "CommonAttribute_OrderTotal": 254,
 "RestrictedAttribute_PII_Data": "No 123, street 15, India"
}
and item-2, 
{
 "CustomerID": "Customer2",
 "OrderID": 2,
 "CommonAttribute_OrderTotal": 334,
 "RestrictedAttribute_PII_Data": "No 456, street 145, NZ"
}
Começando
O Amazon DynamoDB é um serviço de banco de dados NoSQL, sem servidor, totalmente gerenciado, com tempos de resposta de um dígito em milissegundos em qualquer escala, permitindo que você desenvolva e execute aplicativos modernos pagando apenas pelo que usa.

Uma documentação detalhada da AWS sobre como inserir um item no Amazon DynamoDB pode ser encontrada no Amazon DynamoDB

Inventário
Sua conta da AWS foi provisionada com os seguintes recursos:

AWS Lambda
AWS DynamoDB
Função do AWS IAM
Serviços que você deve usar
Amazon DynamoDB
Validação de tarefas
A tarefa será concluída automaticamente quando as linhas forem inseridas corretamente. Como alternativa, você pode clicar no botão check my progress para verificar o progresso da tarefa.

Tarefa 3: Restrinja os resultados da consulta do banco de dados aos dados específicos do cliente
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Agora que você resolveu a tarefa 1, a API retorna resultados para consulta com base em qualquer valor de CustomerID, por exemplo, Customer2 ou Customer1. Um exemplo de consulta usando o AWS Lambda é mostrado abaixo.

response = client.query (tablename="OrderTable”, select="specific_attributes”, keyConditionExpression = 'CustomerID =: CustomerId ', projectionExpression="ID do cliente, commonAttribute_orderTotal, OrderID”, ExpressionAttributeValues= { ':customerId': {'S': 'Cliente2'} })

A tabela do Amazon DynamoDB tem os seguintes atributos

CustomerID (chave primária para a tabela), por exemplo, Cliente1, Cliente2
ID do pedido, por exemplo, 1, 45
CommonAttribute_OrderTotal, por exemplo, 250 INR, 120 INR
RestrictedAttribute_PII_Data, por exemplo, nº 23, rua 15
Sua tarefa
Para concluir a tarefa, adicione restrições baseadas em atributos para que essa API retorne os resultados somente após consulta por CustomerID = “Customer1".

Começando
O AWS Identity and Access Management (IAM) é um serviço da AWS que ajuda um administrador a controlar com segurança o acesso aos recursos da AWS. No DynamoDB, você tem a opção de especificar condições ao conceder permissões usando uma política do AWS IAM e controlar o acesso às ações da API do DynamoDB.

Uma documentação detalhada da AWS sobre o uso das condições da política do AWS IAM para controle de acesso refinado pode ser encontrada nas documentações públicas da AWS

Inventário
Sua conta da AWS foi provisionada com os seguintes recursos:

AWS Lambda
Amazon DynamoDB
Função do AWS IAM
Serviços que você deve usar
ERA O OBJETIVO
Amazon DynamoDB
Validação de tarefas
A tarefa será concluída automaticamente quando a política do AWS IAM for configurada corretamente. Como alternativa, você pode clicar no botão check my progress para verificar o progresso da sua tarefa.

Tarefa 4: Proteja os dados de PII
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Agora você restringiu com sucesso o resultado da consulta a um CustomerID específico, ou seja, Customer1. No entanto, essa consulta retorna todos os atributos dessa linha, ou seja, “RestrictedAttribute_PII_Data”.

Sua tarefa
Para concluir a tarefa, adicione uma restrição baseada em atributos para que essa consulta retorne todos os atributos nessa linha, exceto “RestrictedAttribute_PII_DATA”.

Começando
O AWS Identity and Access Management (IAM) é um serviço da AWS que ajuda um administrador a controlar com segurança o acesso aos recursos da AWS. No DynamoDB, você tem a opção de especificar condições ao conceder permissões usando uma política do IAM. Além de controlar o acesso às ações da API do DynamoDB, você também pode controlar o acesso a itens de dados e atributos individuais. Por exemplo, você pode fazer o seguinte:

Conceda permissões em uma tabela.
Oculte as informações para que somente um subconjunto de atributos fique visível para o usuário.
Uma documentação detalhada da AWS sobre como controlar o acesso a itens e atributos de dados individuais pode ser encontrada nas documentações públicas da AWS

Inventário
Sua conta da AWS foi provisionada com os seguintes recursos:

AWS Lambda
AWS DynamoDB
Função do IAM
Serviços que você deve usar
ERA O OBJETIVO
Amazon DynamoDB
Validação de tarefas
A tarefa será concluída automaticamente quando a política do IAM for configurada corretamente. Como alternativa, você pode clicar no botão check my progress para verificar o progresso da sua tarefa.

```

a