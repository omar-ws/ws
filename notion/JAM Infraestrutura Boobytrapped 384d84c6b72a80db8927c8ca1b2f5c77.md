# JAM Infraestrutura Boobytrapped

```jsx
Você é especialista em InfoSec na XYZ Corp e sua equipe identificou que uma de suas contas da AWS foi comprometida. Eles ainda não sabem a extensão dos danos infligidos e isolaram a conta do resto da sua organização. O agente mal-intencionado criou algum tipo de aplicativo sem servidor que continua interrompendo as instâncias do EC2 à medida que são iniciadas. Você deve investigar a infraestrutura e identificar o recurso que impede a inicialização da instância do EC2.
```

task 1 e 2

```jsx
Infraestrutura Boobytrapped
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Inicie o registro do CloudTrail
Pontos possíveis
16
Penalidade por pista
0
Pontos disponíveis
16
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Sua equipe isolou uma conta da AWS que suspeita ter sido comprometida. As instâncias do EC2 não podem ser iniciadas com êxito e precisam da sua ajuda para identificar o recurso responsável.

Sua tarefa
Como analista da InfoSec, você é responsável por investigar o que está impedindo a instância. Para fazer isso, você precisará capturar os registros da API. Felizmente, uma trilha do CloudTrail já foi configurada na conta por padrão. Você só precisa iniciar o registro.

Começando
Para começar, acesse o serviçoCloudTrail no AWS console e localize a trilha jam-management-events-trail.
Comece a registrar. Se precisar de assistência adicional, confira este link na documentação da AWS:
https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-turning-off-logging.html

Inventário
AWS CloudTrail
Serviços que você deve usar
AWS CloudTrail
Validação de tarefas
Essa tarefa será concluída automaticamente quando o registro do CloudTrail for iniciado.

Princípio do menor privilégio
Este desafio Jam foi desenvolvido seguindo o princípio do menor privilégio. O princípio do menor privilégio se refere à melhor prática de segurança de conceder aos usuários, sistemas ou processos somente os níveis mínimos de acesso ou permissões necessários para executar as funções necessárias.

Durante o desafio, você pode encontrar AccessDeniedException. Isso é intencional. Sua conta tem o acesso necessário para concluir o desafio. Se você não conseguir continuar devido a uma AccessDeniedException, tente uma solução diferente para realizar a tarefa.

Pistas
Comece a registrar o passo a passo
1Pontos de penalidade
Desbloqueie o Clue

task 2

WS PR 2026 - LDB - Training 5
Tabela de classificação

Desafios

Infraestrutura Boobytrapped
Visão geral
Propriedades de saída
Tarefa 1
Tarefa 2

Quem bagunçou os dados no meu cluster de banco de dados?

3 níveis de dor!!

ARM64 seus bancos de dados

Luzes, câmera, segurança!

AWS Config verificará problemas de segurança de compilação de código

NECESSIDADE DE VELOCIDADE!!!

CodePipeline não funciona

A magia da CI/CD da AWS é lançada

Desenvolvendo implantações
Equipe
Feedback
Mensagens
AWS Jam
WS PR 2026 - LDB - Training 5
AWS Jam
WS PR 2026 - LDB - Training 5
Infraestrutura Boobytrapped
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Identifique o recurso malicioso
Pontos possíveis
64
Penalidade por pista
0
Pontos disponíveis
64

Tarefas e pistas
Enviar resposta
Plano de fundo
Agora que o CloudTrail está registrando eventos no CloudWatch, você está pronto para capturar as chamadas de API, fazendo com que as instâncias do EC2 parem. Você só precisa replicar o problema para gerar o evento e os registros.

Sua tarefa
Continue investigando o que está impedindo a instância e identifique o recurso para concluir esse desafio. **O nome do recurso é a resposta para esse desafio. **

Começando
Iniciar uma instância do EC2
Acesse o serviço Amazon EC2 no Console da AWS e selecioneInstâncias no menu de navegação à esquerda.
A partir daí, você verá uma instância do EC2 no estado stopped. Tente iniciar a instância escolhendo a instância e selecionando Estado da instância > Iniciar instância e veja o que acontece.
Analise dados de log com o CloudWatch Log Insights
Em seguida, abra o console CloudWatch em https://console.aws.amazon.com/cloudwatch/
No painel de navegação, escolha Logs e, em seguida, escolha Logs Insights. Na página Logs Insights, o editor de consultas contém uma consulta padrão que retorna os 20 eventos de registro mais recentes.
No menu suspenso **Selecionar grupo (s) de registros **, escolha o grupo de registros /aws/cloudtrail/jam-management-events a ser consultado.
Consulte o grupo de logs e identifique o userIdentity.principalId do recurso que está interrompendo a instância do EC2. Consulte o link abaixo para saber como executar e modificar uma consulta de amostra. https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_AnalyzeLogData_RunSampleQuery.html
NOTA IMPORTANTE
O userIdentity.principalId terá duas partes separadas por dois pontos (:) e estruturado como: AROAXXXXXXXXXXXXXXXXX:function-name. Para resolver esse desafio, insira onome da função que você identificou nos registros. A resposta começará com “jam-”.

**Dica: ** Um de seus colegas recomendou adicionar um filtro para um campo relacionado, como filter eventSource = "ec2.amazonaws.com".

Se precisar de assistência adicional, confira estes links na documentação da AWS:

https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_AnalyzeLogData_RunSampleQuery.html

Inventário
Amazon EC2
Logs do Amazon CloudWatch
Serviços que você deve usar
Amazon EC2
Logs do Amazon CloudWatch
Validação de tarefas
Para concluir essa tarefa, insira o nome do usuário, agente ou recurso que está impedindo a inicialização da instância.

Pistas
Use filtros em suas consultas
6Pontos de penalidade
Desbloqueie o Clue
Passo a passo da solução
8Pontos de penalidade
Desbloqueie o Clue
```

p