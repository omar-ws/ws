# JAM Corte o cabo da Internet!

```bash
Bem-vindo à JAS Corporate! Você foi contratado como engenheiro de segurança. Sua função é identificar quaisquer lacunas de segurança dentro da organização e tomar medidas corretivas. Sua primeira tarefa é garantir que as conexões entre o AWS Lambda e o Amazon DynamoDB sejam seguras, utilizando o princípio do privilégio mínimo e evitando a transmissão pela Internet.
```

```bash
Tarefa 1: Conceda acesso de gravação ao Lambda!
Pontos possíveis
50
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
A segurança é nossa maior prioridade. Como engenheiro de segurança, é fundamental que você siga as melhores práticas de segurança e configure as permissões corretas para os serviços da AWS. Há uma política gerenciada pelo IAM que permite acesso de leitura e gravação à tabela do DynamoDB. No entanto, seu Lambda não tem acesso à tabela. Como você pode garantir que seu Lambda tenha acesso?

Sua tarefa
Dê ao seu AWS Lambda acesso à tabela do Amazon DynamoDB.

Inventário
_Os seguintes recursos foram pré-criados para esse desafio: _

Lambda chamado InternetCordJamLambda
Função de execução do Lambda chamada InternetCordJamRole
Política gerenciada do IAM chamada InternetCordJamManagedPolicy
Tabela do DynamoDB chamada InternetCordJamTable
Serviços que você deve usar
Política gerenciada do IAM
Começando
O Lambda já tem uma função de execução associada a ele. Você deve editar a função para receber crédito por esse desafio.
O Lambda exigirá um evento de teste para que você possa executá-lo. Você pode usar o seguinte evento:
{"key": "test"}
Validação
A tarefa será concluída automaticamente quando você encontrar a solução.
Você sempre pode verificar seu progresso clicando no botão --Verificar meu progresso-- na tela de detalhes do desafio.
Fatores que devem ser verdadeiros para que a tarefa seja bem-sucedida
A função do Lambda IAM deve ter acesso à tabela do Amazon DynamoDB. Você deve editar a função existente para receber crédito por esse desafio.

Tarefa 2: Proteja o Lambda!
Pontos possíveis
50
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Recentemente, você tomou conhecimento das preocupações da JAS Corporate em relação aos riscos de privacidade e segurança associados à transmissão de dados pela Internet pública. Como resultado, para mitigar riscos e garantir um ambiente seguro, foi determinado que o aplicativo deve ser executado em uma Amazon VPC e que seu Lambda só se comunica com o Amazon DynamoDB por meio de uma conexão privada.

Sua tarefa
Configure seu AWS Lambda para acessar o Amazon DynamoDB por meio de uma conexão privada.

Inventário
_Os seguintes recursos foram pré-criados para esse desafio: _

Lambda chamado InternetCordJamLambda
Função de execução do Lambda chamada InternetCordJamRole
Tabela do DynamoDB chamada InternetCordJamTable
VPC chamada InternetCordJamVpc
2 sub-redes privadas com tabelas de rotas
1 grupo de segurança chamado InternetCordJamSecurityGroup
Serviços que você deve usar
AWS Lambda
Amazon VPC
Começando
Configure seu Lambda para se comunicar por meio da VPC
Garanta que o Lambda só possa se comunicar com o DynamoDB de dentro da sua VPC
Um endpoint do DynamoDB Gateway roteia o tráfego do DynamoDB de sua VPC por meio da rede privada da AWS em vez da Internet.
Validação de tarefas
A tarefa será concluída automaticamente quando você encontrar a solução.
Você sempre pode verificar seu progresso clicando no botão Check my progress na tela de detalhes do desafio.
Fatores que devem ser verdadeiros para que a tarefa seja bem-sucedida
O Lambda deve estar na VPC fornecida
O Lambda deve se comunicar com o DynamoDB de dentro da VPC
É necessário usar um endpoint do tipo Gateway para esse desafio.

Tarefa 3: Bloqueie a conexão!
Pontos possíveis
50
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Parabéns, a JAS Corporate está feliz que sua conexão entre o AWS Lambda e o Amazon DynamoDB seja somente privada! No entanto, você, como engenheiro de segurança, sabe que deve estreitar ainda mais a conexão de rede do Lambda.

Você precisará garantir que seu AWS Lambda permita apenas a comunicação com o Amazon DynamoDB e nada mais, para permanecer em conformidade com o princípio do menor privilégio.

Sua tarefa
Atualize a comunicação do Lambda para permitir acesso somente ao Amazon DynamoDB.

Inventário
_Os seguintes recursos foram pré-criados para esse desafio: _

Lambda chamado InternetCordJamLambda
VPC chamada InternetCordJamVpc
1 grupo de segurança chamado InternetCordJamSecurityGroup
Serviços que você deve usar
AWS Lambda
Amazon VPC
Começando
Garantir que o Lambda só possa se comunicar com o Amazon DynamoDB por meio da configuração de rede
Observe que os endpoints do Amazon DynamoDB usam o protocolo HTTP/HTTPS para conexão de API
Validação de tarefas
A tarefa será concluída automaticamente quando você encontrar a solução.
Você sempre pode verificar seu progresso clicando no botão Check my progress na tela de detalhes do desafio.
Fatores que devem ser verdadeiros para que a tarefa seja bem-sucedida
O AWS Lambda só deve permitir acesso estrito ao Amazon DynamoDB
```

a