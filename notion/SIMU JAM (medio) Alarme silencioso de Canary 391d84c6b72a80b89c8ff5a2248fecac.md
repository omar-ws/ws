# SIMU JAM (medio) Alarme silencioso de Canary

```jsx
Visão geral
A AnyCompany é uma empresa de comércio eletrônico em rápido crescimento que processa milhões de dólares em transações diariamente. Na semana passada, uma implantação rotineira em seu serviço de checkout causou uma interrupção de 30 minutos durante o horário de pico de compras, resultando em 2,3 milhões de dólares em receita perdida e centenas de pedidos irritados de atendimento ao cliente.

A equipe de engenharia implementou o que eles acreditavam ser uma estratégia robusta de implantação de canários. Sua arquitetura consiste em:

Instâncias do EC2 executando o serviço de checkout por trás de um Application Load Balance
Pipeline AWS CodeDeploy que é implantado primeiro em uma instância canária
Função lambda que processa registros de aplicativos e publica métricas de erro
Alarmes do CloudWatch que monitoram as taxas de erro durante as implantações
Notificações do SNS para alertar a equipe de operações sobre problemas
O sistema foi projetado para implementar alterações gradualmente em 10% do tráfego primeiro, monitorar erros por meio de análise automatizada de registros e reverter automaticamente se problemas fossem detectados. No entanto, o incidente recente revelou que sua “rede de segurança” não estava funcionando conforme o esperado — a implantação do Canary foi concluída com sucesso, apesar de conter bugs críticos que posteriormente afetaram todos os clientes.

Como engenheiro de DevOps, você foi encarregado de investigar por que o sistema de implantação canary deles não conseguiu detectar o código problemático antes que ele atingisse o tráfego de produção. O CTO quer uma solução antes da próxima temporada de compras natalinas, quando até mesmo alguns minutos de inatividade podem custar milhões.

A investigação inicial revela que a infraestrutura existe, mas tem três problemas críticos de configuração que impedem a validação adequada do canário. O pipeline de implantação mostra marcas verdes e relata o sucesso, mas os mecanismos de monitoramento, reversão automática e alerta que deveriam proteger os clientes não estão funcionando corretamente.

Leia menos
```

```jsx
task 1
Propriedades de saída
CanaryInstanceId
i-01541078518bc0067

CodeDeployBucket
anycompany-checkout-artifacts-611515252105

CurrentRegion
us-west-2

LoadBalancerDNS
LabSta-Appli-5NW9qMQAZbKi-329369851.us-west-2.elb.amazonaws.com

ProductionInstanceId
i-07cdab0fafd6a1d50

RegionSupported
Yes

SNSTopicArn
arn:aws:sns:us-west-2:611515252105:anycompany-checkout-alerts

SNSTopicName
arn:aws:sns:us-west-2:611515252105:anycompany-checkout-alerts

SupportedRegions
us-east-1, us-west-2, eu-west-1, ap-southeast-1

UtilityFunction
utility-handler-svc

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Investigue problemas de monitoramento
Pontos possíveis
45
Penalidade por pista
9
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Durante a investigação do incidente, a equipe de operações descobriu que seu sistema de monitoramento não estava detectando erros na implantação do Canary. A função Lambda responsável por processar registros de aplicativos e publicar métricas de erro no CloudWatch estava sendo executada com sucesso, mas o alarme do CloudWatch projetado para acionar altas taxas de erro nunca foi ativado.

A arquitetura de monitoramento consiste em:

Uma função do Lambda (anycompany-checkout-log-processor) que analisa os registros do aplicativo
Métricas do CloudWatch publicadas para rastrear taxas de erro
Um alarme do CloudWatch (anycompany-checkout-error-rate) que deve ser acionado quando os erros excederem o limite
A função Lambda processa registros e publica 8 erros (acima do limite de alarme de 5), mas o alarme não entra no estado “Em alarme” conforme o esperado.

Sua tarefa
Investigue por que o alarme do CloudWatch não consegue encontrar as métricas publicadas pela função Lambda e corrija a configuração para que o monitoramento funcione corretamente.

Começando
Navegue até o console do AWS Lambda e localize a função anycompany-checkout-log-processor
Teste a função com uma carga vazia {} para vê-la publicar métricas
Acesse o console do CloudWatch e verifique o alarme anycompany-checkout-error-rate
Investigue por que o alarme não é acionado apesar da função Lambda publicar métricas
Inventário
**Recursos para investigar: **

Função Lambda: anycompany-checkout-log-processor
Alarme do CloudWatch: anycompany-checkout-error-rate
Métricas do CloudWatch em vários namespaces
Serviços que você deve usar
AWS Lambda: para examinar e modificar a função de processamento de log
Amazon CloudWatch: para visualizar métricas, alarmes e configurar o monitoramento
Validação de tarefas
Depois de fazer suas alterações:

Teste a função Lambda com payload {}
Aguarde de 1 a 2 minutos para que as métricas apareçam
Verifique a transição do alarme do CloudWatch do estado “Ok” para “Em alarme”
Verifique seu progresso no console JAM
Pistas
Compare namespaces
4Pontos de penalidade
Mostrar pista
Instruções passo a passo
5Pontos de penalidade
Mostrar pista
```

task 2

```jsx
Propriedades de saída
CanaryInstanceId
i-01541078518bc0067

CodeDeployBucket
anycompany-checkout-artifacts-611515252105

CurrentRegion
us-west-2

LoadBalancerDNS
LabSta-Appli-5NW9qMQAZbKi-329369851.us-west-2.elb.amazonaws.com

ProductionInstanceId
i-07cdab0fafd6a1d50

RegionSupported
Yes

SNSTopicArn
arn:aws:sns:us-west-2:611515252105:anycompany-checkout-alerts

SNSTopicName
arn:aws:sns:us-west-2:611515252105:anycompany-checkout-alerts

SupportedRegions
us-east-1, us-west-2, eu-west-1, ap-southeast-1

UtilityFunction
utility-handler-svc

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Analise a configuração de implantação
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Plano de fundo
O segundo problema crítico descoberto foi que o CodeDeploy não estava configurado para reverter automaticamente as implantações com falha. Durante o incidente, a implantação do Canary deveria ter sido revertida automaticamente quando o sistema de monitoramento detectou altas taxas de erro, mas, em vez disso, continuou e promoveu o código problemático à produção.

A arquitetura de implantação inclui:

Aplicativo CodeDeploy (anycompany-checkout-service) com um grupo de implantação temporária
Alarme do CloudWatch (anycompany-checkout-error-rate) que deve acionar reversões quando os limites de erro forem excedidos
Configuração de implantação que deve permitir o controle de tráfego e a reversão automática
Atualmente, as implantações são concluídas com êxito mesmo quando erros são detectados porque o mecanismo de reversão automática não está configurado corretamente.

Sua tarefa
Configure o grupo de implantação do CodeDeploy para permitir reversões automáticas em falhas de implantação e acionadores de alarme, garantindo que as implantações problemáticas sejam interrompidas antes de atingirem o tráfego de produção.

Começando
Navegue até o console do AWS CodeDeploy
Encontre o aplicativo anycompany-checkout-service
Examine a configuração do grupo de implantação staging-deployment
Revise o estilo de implantação atual e as configurações de reversão
Inventário
**Recursos para investigar: **

Aplicativo CodeDeploy: anycompany-checkout-service
Grupo de implantação: staging-deployment
Alarme do CloudWatch: anycompany-checkout-error-rate
Serviços que você deve usar
AWS CodeDeploy: para definir grupos de implantação e configurações de reversão
Amazon CloudWatch: para verificar a configuração de alarme para gatilhos de reversão
Validação de tarefas
Depois de fazer suas alterações:

Verifique se o grupo de implantação mostra “Controle de tráfego” ativado
Confirme se a reversão automática está ativada para os dois tipos de falha
Verifique se o alarme do CloudWatch está associado corretamente
Verifique seu progresso no console JAM
Pistas
Verifique as configurações do grupo de implantação
4Pontos de penalidade
Desbloqueie o Clue
Conecte o sistema de implantação aos alarmes
5Pontos de penalidade
Desbloqueie o Clue
Complete Solution
6Pontos de penalidade
Desbloqueie o Clue
```

adicionei o botao

task 3:

```jsx
Alarme silencioso de Canary
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
CanaryInstanceId
i-01541078518bc0067

CodeDeployBucket
anycompany-checkout-artifacts-611515252105

CurrentRegion
us-west-2

LoadBalancerDNS
LabSta-Appli-5NW9qMQAZbKi-329369851.us-west-2.elb.amazonaws.com

ProductionInstanceId
i-07cdab0fafd6a1d50

RegionSupported
Yes

SNSTopicArn
arn:aws:sns:us-west-2:611515252105:anycompany-checkout-alerts

SNSTopicName
arn:aws:sns:us-west-2:611515252105:anycompany-checkout-alerts

SupportedRegions
us-east-1, us-west-2, eu-west-1, ap-southeast-1

UtilityFunction
utility-handler-svc

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 3: Solucionar problemas do sistema de alerta
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
60
Verifique meu progresso

Tarefas e pistas
Plano de fundo
A equipe de operações não estava recebendo notificações quando as implantações falharam ou os alarmes foram acionados. O incidente durou 30 minutos porque a equipe só foi alertada quando os clientes começaram a ligar para o suporte, em vez de receber notificações automáticas imediatas quando o sistema de monitoramento detectou problemas.

A arquitetura de alerta inclui:

Alarme CloudWatch (anycompany-checkout-error-rate) que detecta altas taxas de erro
Tópico do SNS (anycompany-checkout-alerts) configurado para notificações da equipe
Integração entre o tópico de alarme e SNS para alertas automatizados
O alarme detecta corretamente os problemas (após a conclusão da Tarefa 1), mas nenhuma notificação é enviada.

Sua tarefa
Configure o alarme do CloudWatch para enviar notificações ao tópico do SNS quando os limites de erro forem excedidos, garantindo que a equipe de operações receba alertas imediatos sobre problemas de implantação.

Começando
Navegue até o console do Amazon CloudWatch
Vá até “Alarmes” e encontre anycompany-checkout-error-rate
Examine a configuração e as ações atuais do alarme
Verifique o tópico do SNS anycompany-checkout-alerts disponível para receber notificações
Inventário
**Recursos para investigar: **

Alarme do CloudWatch: anycompany-checkout-error-rate
Tópico do SNS: anycompany-checkout-alerts
Serviços que você deve usar
Amazon CloudWatch: para configurar ações de alarme e notificações
Amazon SNS: para verificar a configuração do tópico e as assinaturas
Validação de tarefas
Depois de fazer suas alterações:

Verifique se o alarme mostra o tópico SNS em suas ações
Teste se as notificações são enviadas quando o alarme é acionado
Verifique seu progresso no console JAM
Pistas
Verifique as ações no alarme do Cloudwatch
6Pontos de penalidade
Desbloqueie o Clue
Selecione o tópico do SNS
7Pontos de penalidade
Desbloqueie o Clue
Complete Solution
9Pontos de penalidade
Desbloqueie o Clue
```

foi facil criei o alarme