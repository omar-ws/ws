# JAM Fundamental: pipeline de implantação sem servidor ...

visao geral:

```jsx
🚀 Comece sua aventura na AWS: criando o país das maravilhas sem servidor na Pipeline Pioneers! 🌟
🎉 Você está preparado para entrar no reino cativante da AWS e despertar seu mágico interior na nuvem? Bem-vindo a bordo da Pipeline Pioneers para o AWS DevOps Challenge — uma iniciação empolgante para iniciantes! 🚀 Embarque em uma aventura na AWS: construa seu país das maravilhas sem servidor! 🌟

🔧 **Sua missão: ** Crie uma terra dos sonhos sem servidor 🏰 Neste desafio, você embarcará em uma missão para criar um pipeline mágico de implantação sem servidor. Sua missão, caso decida aceitá-la, é automatizar o processo de implantação de um aplicativo sem servidor extravagante.

🌈 **O que espera por você nesta jornada épica? ** 🌠
🧙‍♂️ ** AWS CodePipeline ** - Seu livro de feitiços confiável para orquestrar as etapas do pipeline.

🔨 ** AWS CodeBuild ** - A forja encantada onde você cria seus feitiços (código).

💫 ** AWS Lambda ** - Seus assistentes místicos que realizam tarefas com o aceno de sua varinha (funções).

🌟 **Por que você vai adorar essa aventura: ** 🌟
🔮 Aprenda magia, Oops, queremos dizer AWS! Seja você um novato ou um mago iniciante, esse desafio lhe ensinará os segredos da feitiçaria do AWS DevOps!

🎨 **Liberte sua criatividade: ** Crie seu país das maravilhas sem servidor como quiser! Um castelo de conto de fadas, uma cidade futurista ou até mesmo uma floresta cheia de animais falantes - é sua tela da AWS!

💡 **Desafie suas habilidades: ** Teste suas habilidades de resolução de problemas enquanto navega pelas voltas e reviravoltas dos desafios baseados na nuvem.

🌟 Você será a próxima lenda do AWS DevOps? Participe do Pipeline Pioneers AWS DevOps Challenge e embarque em sua jornada mágica hoje mesmo! 🌟

Leia menos
```

task 1:

```jsx
Tarefa 1: Assista ao vídeo e responda à pergunta
Pontos possíveis
16
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Assista ao vídeo O que é computação sem servidor na AWS e responda à pergunta sobre aplicativos sem servidor.

! Teste

**O que torna um serviço ou aplicativo sem servidor? **

A. Sem gerenciamento de servidores

B. Serviços de pagamento por valor

C. Dimensionamento contínuo e tolerância a falhas incorporada

D. Todas as opções acima

**Posso acessar a infraestrutura em que o AWS Lambda é executado? **

R. Sim, o AWS Lambda permite que você acesse a infraestrutura e baixe as ferramentas e os patches necessários para manutenção a qualquer momento.

B. Não. O AWS Lambda opera a infraestrutura computacional em seu nome, permitindo que ele realize verificações de saúde, aplique patches de segurança e faça outras manutenções de rotina.

**Onde você pode encontrar métricas e registros em tempo real das funções do AWS Lambda? **

A. AWS CloudTrail

B. Amazon CloudWatch

C. AWS CloudFormation

D. AWS LogWatch

Observação: para concluir essa tarefa, você não precisa visitar o AWS Console, basta digitar as opções e enviar a resposta. Exemplos de formatos de resposta aceitáveis:

X, Y, Z x, y, z XYZ xyz X. Sua resposta1, Y. Sua resposta2, Z. Sua resposta3 X. Sua resposta1y. Sua resposta2z. Sua resposta3
```

task 2:

```jsx
Tarefa 2: Integração perfeita: AWS Lambda e API Gateway
Pontos possíveis
16
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
O Amazon API Gateway é um serviço totalmente gerenciado que facilita aos desenvolvedores criar, publicar, manter, monitorar e proteger APIs em qualquer escala. As APIs atuam como a “porta de entrada” para que os aplicativos acessem dados, lógica de negócios ou funcionalidades de seus serviços de back-end. Usando o API Gateway, você pode criar APIs RESTful e APIs WebSocket que permitem aplicativos de comunicação bidirecional em tempo real. O API Gateway oferece suporte a cargas de trabalho em contêineres e sem servidor, bem como a aplicativos da web.

O API Gateway lida com todas as tarefas envolvidas na aceitação e processamento de até centenas de milhares de chamadas de API simultâneas, incluindo gerenciamento de tráfego, suporte ao CORS, autorização e controle de acesso, limitação, monitoramento e gerenciamento de versões da API. O API Gateway não tem taxas mínimas nem custos iniciais. Você paga pelas chamadas de API que recebe e pela quantidade de dados transferidos e, com o modelo de preços hierárquicos do API Gateway, você pode reduzir seu custo à medida que o uso da API aumenta.

Documentação Consulte a documentação Amazon API Gateway e Integração do Amazon API Gateway com o AWS Lambda para saber como criar uma API sem servidor e responder às seguintes perguntas.

**Quais tipos de API são compatíveis com o Amazon API Gateway? **

A. API HTTP

B. API REST

C. API WebSocket

D. Todas as opções acima

**Uma API que atualmente recebe 1000 solicitações por segundo. Você quer hospedar isso de forma econômica usando a AWS. Qual das soluções a seguir é mais adequada para isso? **

R. Use o API Gateway com os serviços de back-end do jeito que estão.

B. Use o CloudFront junto com o serviço de back-end da API do jeito que está.

C. Use o API Gateway junto com o AWS Lambda

D. Use o ElastiCache junto com o serviço de back-end da API do jeito que está.

**Qual serviço da AWS ajuda a registrar e monitorar o uso e as alterações da API? **

A. AWS CloudTrail

B. AWS QuickSight

C. AWS Lambda

D. AWS CloudFormation
```

task 3:

```jsx
Tarefa 3: Dominando o AWS CodeCommit e o CodePipeline
Pontos possíveis
24
Penalidade por pista
2
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
A Pipeline Pioneers é uma empresa com experiência em tecnologia que está aproveitando novas tecnologias para criar aplicativos sem servidor com processos de CI/CD. Agora, eles embarcaram em uma nova iniciativa para fazer com que seus aplicativos sem servidor funcionem sem problemas na Amazon Web Services (AWS). Eles estão usando uma linguagem de programação chamada Node.js para seu aplicativo e querem salvar e gerenciar seu código usando um serviço chamado AWS CodeCommit. Além disso, eles querem implantar automaticamente seu código usando o AWS CodePipeline em um serviço chamado AWS Lambda, que é onde o aplicativo realmente será executado. A boa notícia é que eles já configuraram toda a infraestrutura necessária em sua conta da AWS. Eles só precisam que você descubra como transferir o código atualizado para o AWS Lambda por meio do processo de CI/CD.

Tarefa
Acesse o AWS CodeCommit e encontre o repositório chamado “ServerlessApplicationRepo”. Faça upload de dois arquivos específicos, "index.js" e “buildspec.yml”, para a ramificação principal desse repositório. Agora, vá para o AWS CodePipeline, especificamente aquele chamado “ServerlessDeploymentPipeline”. Verifique o status desse pipeline. Se não estiver funcionando conforme o esperado, investigue o motivo e faça os ajustes necessários em sua configuração para garantir que seu código seja implantado corretamente.

index.js

buildspec.yml

Inventário
! Diagrama de infraestrutura

_Os seguintes recursos foram pré-criados para esse desafio: _

Repositório CodeCommit
CodePipeline com estágios de origem e construção
Função IAM usada pelo CodePipeline para acessar o código do repositório CodeCommit
Nota:
Observe também que você não tem permissões para modificar as políticas do IAM. Prepare-se para testar suas habilidades de resolução de problemas e salve o dia!

Serviços que você deve usar
CodeCommit
CodePipeline
Começando
No console da AWS, acesse o AWS CodeCommit para encontrar o repositório criado.
Localize o AWS CodePipeline e procure o problema que precisa ser resolvido.
Validação
A tarefa será concluída automaticamente quando você encontrar a solução.
Você sempre pode verificar seu progresso clicando no botãoVerificar meu progresso na tela de detalhes do desafio.
Fatores que devem ser verdadeiros para que a tarefa seja bem-sucedida:
Os arquivos de código devem ser enviados para o repositório CodeCommit
O pipeline deve ser executado com sucesso.
```

task4:

```jsx
Tarefa 4: DOMINANDO A FUNÇÃO LAMBDA E O GATEWAY DE API
Pontos possíveis
24
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Você implantou seu aplicativo sem servidor na Tarefa 3. Parabéns! Apesar de uma implantação bem-sucedida do código AWS Lambda, o endpoint do API Gateway para esse aplicativo sem servidor é retornando um erro sobre “Resposta malformada”. O sem servidor infraestrutura que a Pipeline Pioneers aproveitou para isso a solução é a integração proxy lambda. Depois de alguns investigação, você percebeu que o problema está relacionado à forma como seu A função Lambda está enviando dados de volta.

Tarefa
O API Gateway não está retornando o código de status 200 adequado que indica uma comunicação bem-sucedida entre os novos função lambda e API Gateway. Você tem a tarefa de descobrir o porquê O API Gateway não está retornando o código de status 200 para garantir a fluidez Comunicação API-Lambda com a nova tecnologia sem servidor da Pipeline Pioneers aplicativo.

Inventário
! Diagrama de infraestrutura

Os seguintes recursos foram pré-criados para esse desafio:

AWS API Gateway
Função AWS Lambda
Todas as infraestruturas da tarefa anterior.
Função do IAM usada pelo API Gateway para acessar o código e a função Lambda.
**Observação: ** Você não tem permissões para modificar as políticas do IAM. Prepare-se para testar suas habilidades de resolução de problemas e salvar o dia!

Serviços que você deve usar
Gateway de API
AWS CodeCommit
Começando
Certifique-se de que a Tarefa 3 seja concluída primeiro!

Abra o AWS Console e descubra por que o endpoint do API Gateway está retornando um erro de resposta malformado.

Validação
A tarefa será concluída automaticamente quando você encontrar a solução. Você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela de detalhes do desafio. Fatores que devem ser verdadeiros para que a tarefa seja bem-sucedida:

O API Gateway está retornando o código de status 200
```

essa foi bem legal aprendi um pouco sobre retorno

return {statusCode: 200, body:”deu certo”} else { statusCode:500, body:”deu erro”} 

aprendi um pouco mas da para aprofundar no skillbiulder vai ajudar mt

documentacao:

https://docs.aws.amazon.com/pt_br/apigateway/latest/developerguide/welcome.html

https://docs.aws.amazon.com/pt_br/apigateway/latest/developerguide/getting-started.html

https://docs.aws.amazon.com/pt_br/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html#api-gateway-simple-proxy-for-lambda-output-format

mesmo que nao tive que fazer na aws, entender esse intregracao, seria uma boa, esse proxy