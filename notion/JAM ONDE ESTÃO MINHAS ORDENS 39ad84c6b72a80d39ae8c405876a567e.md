# JAM ONDE ESTÃO MINHAS ORDENS

```verilog
Visão geral
Um arquiteto de soluções (SA), em sua equipe, projetou um sistema de gerenciamento de pedidos para um restaurante que aceita pedidos de clientes. Esses pedidos são enviados ao chefe de cozinha e ele os redireciona com base em alimentos e bebidas. O chefe de cozinha saiu e o dono do restaurante entrou em contato com a SA para obter uma maneira de redirecionar esses pedidos com base em alimentos e bebidas por meio do próprio sistema. A SA decidiu introduzir as funções do AWS Lambda para as solicitações a serem processadas no sistema usando as regras do Amazon EventBridge para filtrar com base no tipo de pedido. Você, como consultor, recebeu essa tarefa para automatizar o redirecionamento manual de pedidos.

A arquitetura do JAM é fornecida no link. https://aws-jam-challenge-resources.s3.amazonaws.com/eventrule-filtering-lambda/order-management-system.drawio.png

Leia menos

Tarefa 1: CONFIGURAR MEU ÔNIBUS (REGRAS DO EVENTO)
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes:
Você se lembrou da necessidade de automatizar o redirecionamento manual de pedidos usando as funções do AWS Lambda. Você descobriu o uso das regras de eventos do Amazon EventBridge para acionar essas funções lambda.

**Nota: **

O barramento de eventos personalizado Amazon EventBridge foi criado para você chamado OrderEventBus
Duas funções do AWS Lambda são criadas
a. um para pedidos de Food. O nome da função Lambda conteria FoodOrdersLambdaFunction em seu nome
b. um para pedidos de Beverage. O nome da função Lambda conteria BeverageOrdersLambdaFunction em seu nome
Sua tarefa:
Seu Amazon EventBridge não está configurado com regras de eventos para processar pedidos de Food e Beverage. Crie regras de eventos e configure suas respectivas funções do AWS Lambda. Note - Crie regras de eventos no OrderEventBus

Encontre o ônibus de eventos Amazon EventBridge que foi criado para esse desafio e crie regras de eventos para o determinado barramento de eventos Amazon EventBridge.

**Dica: ** use o padrão de evento { "detail": { "OrderType": ["Food"] } } para pedidos Food. Além disso, Creation method deve ser de Custom pattern e não Use schema ou Use pattern form

Começando:
Navegue até o serviço Amazon EventBridge no console de gerenciamento da AWS e encontre o barramento de eventos com o nome OrderEventBus criado sem regras de eventos. Você precisa descobrir como criar regras de eventos e configurar suas funções lambda para os pedidos.

Inventário:
Ônibus de eventos Amazon EventBridge
Verifique o arquivo de propriedades de saída para obter os valores apropriados.
Serviços que você deve usar:
Amazon EventBridge
Validação de tarefas:
Clique no botão verificar meu progresso, um script automatizado será validado para verificar se o desafio foi concluído, verificando se as regras do evento Amazon Event Bridge foram criadas.

Tarefa 2: ENDEREÇAR MINHAS CONFIGURAÇÕES
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes:
Sua configuração de função do AWS Lambda precisa ser atualizada de acordo com as funções recém-introduzidas do Amazon EventBridge e do AWS Lambda que foram introduzidas.

Sua tarefa:
Encontre as funções do AWS Lambda que foram criadas para esse desafio e configure o Environment Variables exigido examinando o código de cada função lambda.

Começando:
Navegue até o serviço AWS Lambda no console de gerenciamento da AWS. As funções do Lambda que foram criadas conteriam os nomes OrdersLambdaFunction, FoodOrdersLambdaFunction e BeverageOrdersLambdaFunction.

Inventário:
Funções do AWS Lambda.
Verifique o arquivo de propriedades de saída para obter os valores apropriados.
Serviços que você deve usar:
AWS Lambda
Validação de tarefas:
Clique no botão verificar meu progresso, um script automatizado será validado para verificar se o desafio foi concluído, verificando se suas funções do AWS Lambda estão configuradas corretamente.

Tarefa 3: RESOLVER O PROBLEMA
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes:
Seu aplicativo está configurado e os testes foram iniciados para diferentes pedidos. Infelizmente, os pedidos ainda não foram recebidos. Você precisa testar o aplicativo usando Amazon API Gateway com as cargas fornecidas para pedidos Food e Beverage.

Sua tarefa:
Teste o método da API com as cargas fornecidas abaixo. Verifique se os pedidos estão armazenados nas tabelas do Amazon DynamoDB.

Começando:
Navegue até o serviço Amazon API Gateway no console de gerenciamento da AWS. Navegue até a seção API Resource, selecione o método POST API e teste as cargas fornecidas abaixo. Verifique as tabelas do Amazon DynamoDB para ver os pedidos recebidos.

Inventário:
API Rest do Amazon API Gateway
Tabela Amazon DynamoDB
Serviços que você deve usar:
Amazon API Gateway
Amazon DynamoDB
verifique a seção Propriedades de saída do desafio
Validação de tarefas
Clique no botão Verificar meu progresso, um script automatizado será validado para verificar se o desafio foi concluído, verificando se suas tabelas do Amazon DynamoDB receberam pedidos.

Carga útil de solicitação de API para pedidos de comida:
{ "ItemName": "Noodles", "OrderType": "Food", "ItemType": "Chinese" }

Carga útil de solicitação de API para pedidos de bebidas:
{ "ItemName":"Coke", "OrderType":"Beverage", "ItemType": "Soft drinks" }

```

s