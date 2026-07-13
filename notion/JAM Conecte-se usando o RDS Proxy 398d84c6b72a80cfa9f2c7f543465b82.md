# JAM Conecte-se usando o RDS Proxy

```bash
Visão geral
Você desenvolveu uma função do Lambda que acessa uma instância do RDS. No entanto, o administrador do banco de dados não permitiu acesso direto ao RDS a partir da função Lambda devido a preocupações com o esgotamento das conexões disponíveis. Em vez disso, o acesso usando o RDS Proxy foi concedido.

Você é responsável por iniciar o proxy do RDS e configurá-lo para que a função Lambda possa acessar a instância do RDS.

Propriedades de saída
oRDSProxyRole
RDSProxyRole

oRDSProxySecurityGroup
sg-080c60ce45d9f4191

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Tarefa 1
Pontos possíveis
150
Penalidade por pista
0
Pontos disponíveis
150

Tarefas e pistas
Enviar resposta
Plano de fundo
O administrador do banco de dados configurou a segurança e a rede para o RDS Proxy. O RDS Proxy ainda não foi criado.

Sua tarefa
Você deve criar um proxy RDS e tornar o banco de dados acessível a partir da função dbClient.

Inventário
O nome da função Lambda é DBClient. Os recursos a serem especificados ao criar um proxy RDS são os seguintes.

Função do IAM: use RDSProxyRole. O proxy usará essa função do IAM para acessar os segredos do AWS Secrets Manager.
Segredos do Secrets Manager: O mesmo segredo usado na função DbClient.
Há outros parâmetros necessários para criar um proxy RDS, portanto, investigue-os em sua conta da AWS.

Serviços que você deve usar
Amazon RDS
AWS Lambda
Amazon VPC
Validação de tarefas
A resposta pode ser encontrada na saída da função DbClient. Entre na caixa de texto no console do Jam.

Pistas
O que você precisa ao criar um proxy RDS
15Pontos de penalidade
Desbloqueie o Clue
Verifique as configurações de rede
19Pontos de penalidade
Desbloqueie o Clue
Solução Completa
22Pontos de penalidade
Desbloqueie o Clue
```

era so uma e nao cosnegui terminar