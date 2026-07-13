# JAM Não estou encontrando meu carro favorito. Me ajude!!

```wasm
Não estou encontrando meu carro favorito. Me ajude!!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
ReadFromDynamoDbCarsApiUrl
https://lj7iefuehb.execute-api.us-east-1.amazonaws.com

VpcId
vpc-03bb9f48e2b2595e1

Tarefa 1: Uso da condição “Limite” do Amazon DynamoDB
Pontos possíveis
80
Penalidade por pista
0
Pontos disponíveis
80
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Sua empresa lançou recentemente um novo modelo Audi “e-tron GT”, que é do estilo de carroceria “Sedan”. Há um total de 36 modelos de carros Audi lançados por sua empresa e os detalhes do carro (marca, modelo e estilo da carroceria) de todos os carros estão armazenados na tabela do Amazon DynamoDB cars. Quando os usuários realizam pesquisas usando o site da sua empresa, o endpoint do API Gateway invoca a função AWS Lambda, e a função lambda consulta os dados da tabela cars do DynamoDB com os critérios de pesquisa especificados para exibir os resultados.
Devido ao recente lançamento da produção, quando os usuários pesquisam carros “Audi” com o estilo de carroceria “Sedan”, os usuários não conseguem encontrar o modelo Audi “e-tron GT” lançado recentemente nos resultados da pesquisa.

Sua tarefa
Determine o motivo pelo qual o modelo Audi “e-tron GT” não está aparecendo nos resultados da pesquisa e corrija-o.

Começando
Navegue até o menu Output Properties do Jam Challenge e obtenha o URL do site na propriedade ReadFromDynamoDbCarsApiUrl.
Ao acessar o site, você não conseguirá encontrar o modelo Audi “e-tron GT” na lista de carros exibida.
Inventário
Para facilitar as tarefas, os seguintes recursos foram configurados nesse ambiente: -

Gateway de API
Função Lambda: jamDynamoDbLimitFunction. Isso consulta o DynamoDB para carros Audi no estilo “Sedan”.
DynamoDB:
Nome da tabela: cars
Colunas:
Chave de partição: make (“Audi” etc.)
Chave de classificação: model (“e-tron GT” etc.)
body_styles (“Sedan” etc.)
Serviços que você deve usar
Amazon API Gateway
AWS Lambda
Validação de tarefas
Para concluir a tarefa, você deve conseguir ver o modelo Audi “e-tron GT” na lista de carros exibida.
Pistas
Verifique os parâmetros de consulta do DynamoDB especificados na função AWS Lambda
8Pontos de penalidade
Desbloqueie o Clue
Instruções passo a passo para a variável de ambiente da função AWS Lambda
10Pontos de penalidade
Desbloqueie o Clue
```

eu apenas troquei essa variavel do lambda, que eu nao sabia o que fazia, mas eu pre supos que era algo importante

```wasm
Variáveis de ambiente (1)
Editar
As variáveis de ambiente a seguir são criptografadas em repouso com a chave de serviço padrão do Lambda.

Chave
Valor
DynamoDbQueryLimit
40

```

estava 12 e eu coloquei 40, o que iso faz?

codigo do lambda

```wasm
exports.handler = async (event) => {  const { DynamoDBClient } = require('@aws-sdk/client-dynamodb'); const { DynamoDBDocumentClient, QueryCommand } = require('@aws-sdk/lib-dynamodb');
const dynamoDbQueryLimit = parseInt(process.env.DynamoDbQueryLimit); const docClient = DynamoDBDocumentClient.from(new DynamoDBClient({}));
const paramsGetFilter = {
  TableName: 'cars',
  KeyConditionExpression: 'make = :make',
  FilterExpression: 'body_styles = :body_styles',
  ExpressionAttributeValues: {
    ':make': 'Audi',
    ':body_styles': 'Sedan',
  },
  Limit: dynamoDbQueryLimit,
};
const dataFilter = await docClient.send(new QueryCommand(paramsGetFilter)); let result = ''; result = result +'The following are the list of cars based on search criteria: ';
for (let i = 0; i < dataFilter.Count; i++) {
  result = result + (i+1) + ') Make - ' + dataFilter.Items[i]["make"] + ', Model - ' + dataFilter.Items[i]["model"] + ', Body Style - ' + dataFilter.Items[i]["body_styles"] + ' ';
}
const response = { statusCode: 200, body: result}; return response; };

```