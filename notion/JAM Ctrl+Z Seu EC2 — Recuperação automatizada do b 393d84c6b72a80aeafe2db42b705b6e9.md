# JAM Ctrl+Z Seu EC2 — Recuperação automatizada do backup

```jsx
Visão geral
Imagine isso — são 2 da manhã. Um servidor de produção cai acidentalmente. Desaparecido. Aplicativo inativo, clientes afetados, todo mundo confuso.
Seu engenheiro de automação de nuvem criou uma solução para isso — codinome XYZ Protocol. Um pipeline totalmente automatizado que cria um backup no momento em que um servidor é iniciado e o recupera instantaneamente se ele for destruído. Sem intervenção humana. Sem pânico.

Há apenas um problema — **o protocolo XYZ está quebrado. **

As peças críticas estão mal configuradas, ausentes ou desconectadas. No momento, se esse servidor cair, ele permanecerá inativo. Sem backup. Sem recuperação. Sem segunda chance.

Your mission: Investigate, repair, and activate the XYZ Protocol — then prove it works by triggering a real backup, destroying the server, and watching it come back online, fully restored.

Começando
Inventário de desafios
Os seguintes recursos foram provisionados para você:

Amazon VPC e redes

xyz-vpc: VPC dedicada (10.0.0.0/16) para o ambiente de desafio
xyz-subnet: Sub-rede (10.0.1.0/24) no AZ1 — hospeda a instância EC2
Amazon EC2 e EBS Volume — Recursos de computação

xyz-instance: t3.micro Instância EC2 do Amazon Linux 2023 em xyz-subnet

Volume do Amazon EBS: volume criptografado de 8 GB gp3 anexado a xyz-instance

**AWS Lambda Functions (mecanismo de automação) **

xyz-auto-backup: função Lambda (Python 3.12, tempo limite de 300s)

xyz-auto-recover: função Lambda (Python 3.12, 300s (tempo limite)

Permissões do Lambda: as políticas baseadas em recursos são pré-configuradas em ambas as funções do Lambda, permitindo que o Amazon EventBridge as invoque

**Regras do Amazon EventBridge (acionadores de sinal) **

xyz-auto-backup-rule: regra do EventBridge que escuta as notificações de mudança de estado da instância do EC2
xyz-auto-recover-rule: regra do EventBridge destinada a acionar a recuperação automática quando uma instância é encerrada.
Funções e permissões do AWS IAM

xyz-backup-role: função do IAM para operações do serviço AWS Backup

xyz-auto-backup-lambda-role: função IAM para a função Lambda de backup

xyz-auto-recover-lambda-role: função IAM para a função Lambda de recuperação
```

```jsx
Tarefa 1: Construa o cofre — Carregue as coordenadas
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes

Todo backup precisa de uma casa. No AWS Backup, essa casa é chamada de Backup Vault — um contêiner seguro que armazena pontos de recuperação. Neste momento, sem cofre existe.

Além disso, as duas funções do Lambda estão quebradas. As funções falharão no momento em que forem invocadas.
Sua tarefa

Crie um cofre de backup no AWS Backup. O nome do cofre DEVE ser xyz-backup-vault
Configure as variáveis de ambiente ausentes nas ambas funções do Lambda (xyz-auto-backup e xyz-auto-recover):
Começando

Explore o console AWS Backup para criar um novo cofre de backup com o nome necessário
Investigue o console Lambda para entender quais variáveis de ambiente cada função espera
Use o console IAM ou CloudFormation Outputs para localizar o ARN da função necessário para a configuração
**Documentação relevante da AWS: **

Criação de um cofre de backup
Usando variáveis de ambiente do AWS Lambda
Visualização dos detalhes da função do IAM
Observação: Você pode ver banners de aviso no console da AWS. Esse comportamento é esperado devido à implementação do princípio de menor privilégio da AWS, que garante que você tenha apenas as permissões necessárias para concluir a tarefa.

Inventário

Cofre de backup: xyz-backup-vault
Função Lambda 1: xyz-auto-backup
Função Lambda 2: xyz-auto-recover
Serviços que você deve usar

AWS Backup — Crie um cofre de backup
AWS Lambda — Configurar variáveis de ambiente
AWS IAM — Para obter o BACKUP_ROLE_ARN
Validação de tarefa

Essa tarefa será validada por meio de uma função do Lambda quando você concluir as etapas necessárias. Como alternativa, você pode clicar em “verificar meu progresso” para validar o progresso

O cofre de backup xyz-backup-vault existe.
Ambas as funções do Lambda têm variáveis de ambiente
Pistas
O mapa do tesouro
4Pontos de penalidade
Desbloqueie o Clue
O projeto do Vault
5Pontos de penalidade
Desbloqueie o Clue

Tarefa 2: Corrija a fiação
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes

O protocolo XYZ se baseia em duas regras do Amazon EventBridge para detectar alterações de estado de instâncias do EC2 e encaminhá-las para as funções corretas do Lambda. Pense nessas regras como sinalizadores — quando algo acontece com seu servidor, o respondente certo precisa ser alertado.

No momento, os dois sinalizadores estão cruzados. Sem corrigi-los, nenhum sinal alcançará a função Lambda correta — e todo o pipeline permanecerá inativo.

Sua tarefa

Investigue as regras do EventBridge (xyz-auto-backup-rule e xyz-auto-recover-rule)
Regra 1 (xyz-auto-backup-rule): Adicione a configuração ausente
Regra 2 (xyz-auto-recover-rule): Corrija o padrão do evento — altere-o para apenas o estado terminated
⚠️ Mantenha as duas regras no estado DESATIVADO — você as habilitará em uma tarefa posterior
Começando

Navegue até Amazon EventBridge e inspecione as duas regras — procure o que está faltando ou configurado incorretamente em cada uma
Entenda como as regras do EventBridge conectam os padrões de eventos aos alvos
Certifique-se de que ambas as regras permaneçam desativadas após fazer alterações
**Documentação relevante da AWS: **

Regras do Amazon EventBridge
Adicionar alvos do EventBridge
Padrões de eventos no EventBridge
Eventos de mudança de estado do EC2
Observação: Você pode ver banners de aviso no console da AWS. Esse comportamento é esperado devido à implementação do princípio de menor privilégio da AWS, que garante que você tenha apenas as permissões necessárias para concluir a tarefa.

Inventário

Regra 1 do EventBridge: xyz-auto-backup-rule
Regra 2 do EventBridge: xyz-auto-recover-rule
Função Lambda 1: xyz-auto-backup
Função Lambda 2: xyz-auto-recover
Serviços que você deve usar

Amazon EventBridge — Configure metas de regras e edite padrões de eventos
Validação de tarefa

Essa tarefa será validada por meio de uma função do Lambda quando você concluir as etapas necessárias. Como alternativa, você pode clicar em “verificar meu progresso” para validar o progresso

A regra 1 (xyz-auto-backup-rule) foi configurada corretamente.
O padrão de eventos da regra 2 (xyz-auto-recover-rule) é acionado somente no estado terminated.
Ambas as regras permanecem no estado DESATIVADO.
Pistas
A agulha da bússola
6Pontos de penalidade
Desbloqueie o Clue
O diagrama de fiação
7Pontos de penalidade
Desbloqueie o Clue

Tarefa 3: Arme o Guardião
Pontos possíveis
30
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes

O AWS Backup não opera sozinho — ele precisa de uma função do IAM para realizar operações de backup e restauração em seu nome. O xyz-backup-role é esse papel. Ele já está configurado para ser assumido pelo AWS Backup serviço e tem uma política embutida que concede permissões específicas do EC2, como RunInstances e CreateVolume.

Mas há uma lacuna crítica. O AWS Backup exige duas políticas gerenciadas pela AWS para funcionar

um que concede permissões para criar backups (instantâneos, pontos de recuperação) e
outro que concede permissões para restaurar a partir de esses backups.
Sua tarefa

Investigue a função xyz-backup-role do IAM para ver quais políticas gerenciadas estão atualmente anexadas
Identifique as duas políticas gerenciadas pela AWS que o AWS Backup precisa para operações de backup e restauração
Anexe as duas políticas gerenciadas a xyz-backup-role
Começando

Abra o console IAM e examine as permissões atuais anexadas a xyz-backup-role
Pesquise quais políticas gerenciadas pela AWS foram projetadas para a função do serviço AWS Backup de realizar operações de backup e restauração
Anexe as políticas gerenciadas identificadas à função
**Documentação relevante da AWS: **

Políticas gerenciadas pela AWS para o AWS Backup
Adicionar permissões de identidade do IAM
Funções e permissões do AWS Backup IAM
Observação: Você pode ver banners de aviso no console da AWS. Esse comportamento é esperado devido à implementação do princípio de menor privilégio da AWS, que garante que você tenha apenas as permissões necessárias para concluir a tarefa.

Inventário

Função do IAM: xyz-backup-role (políticas gerenciadas ausentes)
Política em linha existente: xyz-backup-ec2-restore (permissões EC2 — intactas)
Política 1 ausente: política gerenciada pela AWS para operações de backup
Política 2 ausente: política gerenciada pela AWS para operações de restauração
Saída da pilha: BackupRoleName → xyz-backup-role
Serviços que você deve usar

AWS IAM — investigue as permissões de funções e anexe políticas gerenciadas
Validação de tarefa

Essa tarefa será validada por meio de uma função do Lambda quando você concluir as etapas necessárias. Como alternativa, você pode clicar em “verificar meu progresso” para validar o progresso

A função de IAM xyz-backup-role exigiu que ambas as políticas gerenciadas pela AWS fossem anexadas.

Pistas
A dica de arsenal
3Pontos de penalidade
Desbloqueie o Clue
O Arsenal do Guardião
3Pontos de penalidade
Desbloqueie o Clue

Tarefa 4: Acenda o fusível — Recupere o EC2
Pontos possíveis
50
Penalidade por pista
0
Pontos disponíveis
50
Verifique meu progresso

Tarefas e pistas
Antecedentes

Cada componente do protocolo XYZ agora está configurado corretamente, mas o pipeline ainda está off-line. Ambas as regras do EventBridge permanecem desativadas, o que significa que nenhum evento está sendo capturado e nenhuma função do Lambda está sendo acionada.

É hora de dar vida a todo o pipeline. Você habilitará as regras, acionará um backup real reiniciando a instância do EC2, verifique se o backup foi concluído e, em seguida, faça o encerramento intencional do o servidor. Se tudo funcionar, o pipeline de recuperação detectará o encerramento, encontre o backup e crie automaticamente um novo exemplo.

Nota: Enquanto aguarda a conclusão das tarefas de backup e restauração, vá para a Tarefa 5 e resolva o quebra-cabeça.

Sua tarefa

**Fase A — Acenda o backup: **

Ative as duas regras do EventBridge (xyz-auto-backup-rule e xyz-auto-recover-rule)
Pare a instância do EC2 (xyz-instance)
Inicie-o novamente — quando atingir o estado running, o pipeline de backup deve ser acionado automaticamente
Verifique os CloudWatch Logs da função xyz-auto-backup Lambda para confirmar se ela foi acionada
Verifique se uma tarefa de backup aparece no console do AWS Backup
Aguarde até que a tarefa de backup alcance o status CONCLUÍDA
**Fase B — Recuperação do EC2: **

Confirme se existe um ponto de recuperação em xyz-backup-vault

Encerre a instância do EC2 — sim, destrua-a

Verifique os CloudWatch Logs da função xyz-auto-recover Lambda

Verifique se um trabalho de restauração foi iniciado no console do AWS Backup

Aguarde a conclusão da restauração — uma nova instância do EC2 renasce das cinzas

Começando

Ative as duas regras do EventBridge para que o pipeline possa começar a ouvir as mudanças de estado do EC2
Acione o fluxo de backup percorrendo a instância do EC2 por meio de uma sequência de parada e início
Use CloudWatch Logs para confirmar se a função de backup do Lambda foi invocada e monitore o console AWS Backup para concluir o trabalho
Depois que um ponto de recuperação for confirmado no cofre de backup, encerre a instância para acionar o fluxo de restauração
Verifique a restauração do Lambda acionada por meio de seus CloudWatch Logs e monitore o trabalho de restauração no AWS Backup até que uma nova instância apareça
**Documentação relevante da AWS: **

Ativando e desativando as regras do EventBridge
Pare e inicie as instâncias do Amazon EC2
Encerrar instâncias do Amazon EC2
Monitoramento de trabalhos de backup da AWS
Trabalhando com cofres de backup e pontos de recuperação
Visualização do CloudWatch Logs para Lambda
Observação: Você pode ver banners de aviso no console da AWS. Esse comportamento é esperado devido à implementação do princípio de menor privilégio da AWS, que garante que você tenha apenas as permissões necessárias para concluir a tarefa.

Inventário

Regra 1 do EventBridge: xyz-auto-backup-rule
Regra 2 do EventBridge: xyz-auto-recover-rule
Instância EC2: xyz-instance (parar → iniciar → verificar o backup → encerrar)
Lambda Logs: /aws/lambda/xyz-auto-backup e /aws/lambda/xyz-auto-recover
Backup Vault: xyz-backup-vault (verifique o ponto de recuperação)
Trabalhos de backup da AWS: painéis de tarefas de backup e tarefas de restauração
Serviços que você deve usar

Amazon EventBridge — Habilitar regras
Amazon EC2 — Pare, inicie e encerre a instância
Amazon CloudWatch Logs — Verifique a execução do Lambda
AWS Backup — Monitore trabalhos de backup e restauração
Validação de tarefa

Essa tarefa será validada por meio de uma função do Lambda quando você concluir as etapas necessárias. Como alternativa, você pode clicar em “verificar meu progresso” para validar o progresso

As duas regras do EventBridge estão habilitadas.
Uma tarefa de backup foi concluída em xyz-backup-vault.
A instância original do EC2 foi encerrada.
Um trabalho de restauração foi iniciado ou concluído no AWS Backup, resultando em uma nova instância do EC2.
Pistas
A sequência de ignição
5Pontos de penalidade
Desbloqueie o Clue
O manual do protocolo XYZ
6Pontos de penalidade
Desbloqueie o Clue

Tarefa 5: Resolva o quebra-cabeça!
Pontos possíveis
20
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes

Você reparou e ativou com sucesso todo o protocolo XYZ. Mas construindo algo não é o mesmo que entender isso.

Mapeie o exato fluxo de dados e eventos em cada componente. Esta é a sua final desafio: divirta-se entendendo a arquitetura mapeando ambas fluxos de automação usando os blocos de construção do protocolo XYZ.

Sua tarefa

Estude os seis elementos básicos da imagem e mapeie o fluxo correto tanto para a automação de backup quanto para a automação de restauração.

Usando somente os números do bloco, insira a sequência correta para cada fluxo:
**Fluxo de backup: ** Quando o EC2 começa a ser executado, como o backup é criado automaticamente?

**Fluxo de restauração: ** Quando o EC2 é encerrado, como a instância renasce das cinzas?

Inventário

Validação de tarefa

Digite as respostas corretas na caixa em branco

Para Eg:

se o fluxo de backup correto for 1→2→3→6

se o fluxo de restauração for 2→4→3→6→1

Em seguida, digite (sem espaços): Backup_Flow:1,2,3,6|Restore_Flow:2,4,3,6,1

Pistas
Folha de dicas
2Pontos de penalidade
Desbloqueie o Clue

```

a