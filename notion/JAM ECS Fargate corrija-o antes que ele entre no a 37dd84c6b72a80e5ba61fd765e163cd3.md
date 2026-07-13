# JAM ECS Fargate: corrija-o antes que ele entre no ar

```json
Sua equipe está se preparando para lançar um aplicativo web em execução no ECS Fargate. No entanto, o ambiente criado pela equipe de infraestrutura tem várias configurações incorretas e o aplicativo não está funcionando corretamente.

Antes da ativação, identifique e corrija os problemas com o serviço ECS para colocar o aplicativo em funcionamento.

Neste desafio, você corrigirá a função de execução de tarefas, a função de tarefa e a configuração de escalabilidade de serviços do ECS Fargate.
```

task 1:

```json
ECS Fargate: corrija-o antes que ele entre no ar
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 1: Corrija a função de execução de tarefas do ECS
Pontos possíveis
26
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Um aplicativo web implantado no ECS Fargate não está em execução. As tarefas do serviço ECS falham repetidamente ao serem iniciadas.

Sua tarefa
Corrija a configuração da função de execução de tarefas para que as tarefas do ECS possam ser iniciadas com êxito.

Inventário
Cluster ECS — O cluster em que o aplicativo é executado
Serviço ECS — O serviço que gerencia as tarefas
Função do IAM — A função de execução de tarefas
Serviços que você deve usar
Amazon ECS
OBJETIVO DA AWS
Recursos atuais
Um cluster ECS com um serviço Fargate que está tentando executar tarefas
Uma definição de tarefa referenciando uma imagem de contêiner no ECR
Uma função do IAM configurada como a função de execução de tarefas (atualmente sem as permissões necessárias)
Começando
Clique em Propriedades de saída no painel de navegação esquerdo desta página. Anote os valores dos seguintes itens:
oTaskExecutionRoleName — Nome da função de execução de tarefas do ECS
oAppUrl — URL do aplicativo
Acesse a URL do aplicativo em seu navegador para verificar o estado atual do aplicativo.
Abra o console do ECS e verifique o status das tarefas do serviço. Veja as tarefas interrompidas e suas mensagens de erro.
DICAS:

A tarefa do ECS precisa das permissões apropriadas na função de execução de tarefas para extrair imagens de contêiner do ECR.
Verifique as políticas gerenciadas pela AWS disponíveis para o ECS.
Links para seguir
Função IAM de execução de tarefas do Amazon ECS
Solução de problemas de falhas na inicialização de tarefas do Amazon ECS
Validação de tarefas
Essa tarefa será marcada automaticamente como concluída quando:

A política gerenciada AmazonECSTaskExecutionRolePolicy está anexada à Função de Execução de Tarefas do ECS.
Além disso, você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela Detalhes do desafio.

Pistas
Pistas 1
2Pontos de penalidade
Desbloqueie o Clue
Pistas 2
3Pontos de penalidade
Desbloqueie o Clue
```

task 2:

```json
ECS Fargate: corrija-o antes que ele entre no ar
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 2: Corrija a função de tarefa do ECS
Pontos possíveis
26
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Depois de resolver a Tarefa 1, as tarefas do ECS agora estão em execução. Quando você acessa o URL do aplicativo, o aplicativo está ativo, mas não consegue recuperar o arquivo sinalizador do S3.

**Observação: ** Se o aplicativo ainda não estiver acessível após a conclusão da Tarefa 1, o serviço ECS pode estar esperando para tentar novamente. Acesse o console do ECS, selecione o serviço e clique em Atualizar serviço → Forçar nova implantação para acionar uma reimplantação imediata.

Observação: ** O URL do aplicativo está disponível emPropriedades de saída** no painel de navegação esquerdo desta página. Você não tem permissão para acessar os detalhes de distribuição do CloudFront por meio do AWS Management Console.

Sua tarefa
Conceda as permissões apropriadas à função correta do IAM para que o aplicativo possa ler o arquivo sinalizador do S3.

Inventário
Definição de tarefa do ECS — contém a configuração da função
Funções do IAM — Função de execução de tarefas e função de tarefa
S3 Bucket — O bucket que contém o arquivo de sinalização
Serviços que você deve usar
Amazon ECS
OBJETIVO DA AWS
Amazon S3
Recursos atuais
Uma tarefa do ECS Fargate em execução que atende a um aplicativo web
Uma função do IAM configurada como a função de tarefa (atualmente sem permissões do S3)
Um bucket do S3 contendo um arquivo de sinalização
Começando
Clique em Propriedades de saída no painel de navegação esquerdo desta página e abra o URL oAppUrl em seu navegador. Observe a mensagem de erro.
Abra o console do ECS e inspecione a definição da tarefa para entender a configuração da função.
Identifique qual função o aplicativo usa para acessar os serviços da AWS.
Anexe a política gerenciada AmazonS3ReadOnlyAccess à função correta.
DICAS:

Há duas funções do IAM associadas a uma tarefa do ECS: a função de execução da tarefa e a função da tarefa. Eles servem a propósitos diferentes.
A função de execução de tarefas é usada pelo agente do ECS. A função de tarefa é usada pelo aplicativo em execução dentro do contêiner.
Links para seguir
Função IAM da tarefa do Amazon ECS
Função de execução de tarefas versus função de tarefa
Validação de tarefas
Essa tarefa será marcada como concluída quando:

Você insere a string de sinalização correta exibida na página do aplicativo.
Observação: depois de anexar a política, as tarefas existentes não receberão as novas permissões imediatamente. Acesse o console do ECS, selecione o serviço e clique em Atualizar serviço → Forçar nova implantação para reiniciar as tarefas. Pode levar alguns minutos para que as novas tarefas se tornem saudáveis.

Além disso, você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela Detalhes do desafio.

Pistas
Pistas 1
2Pontos de penalidade
Desbloqueie o Clue
Pistas 2
3Pontos de penalidade
Desbloqueie o Clue
```

task 3:

```json
ECS Fargate: corrija-o antes que ele entre no ar
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 3: Dimensione o serviço ECS para obter alta disponibilidade
Pontos possíveis
28
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
O aplicativo agora está funcionando e você pode recuperar o sinalizador. No entanto, o serviço está sendo executado atualmente com apenas uma tarefa, o que não é suficiente para um ambiente de produção em termos de disponibilidade.

Sua tarefa
Aumente o número de tarefas no serviço ECS para pelo menos 2 para obter alta disponibilidade. Em seguida, acesse o aplicativo e identifique duas IDs de tarefas diferentes.

Inventário
Serviço ECS — Configuração da contagem de tarefas
ALB — Ponto de acesso para o aplicativo
Serviços que você deve usar
Amazon ECS
Balanceamento de carga elástico
Recursos atuais
Um serviço ECS Fargate executando 1 tarefa
Um Application Load Balancer distribuindo tráfego para o serviço
O aplicativo exibe a ID da tarefa de atendimento e a zona de disponibilidade na parte inferior da página
Começando
Abra o console do ECS e verifique a contagem atual de tarefas desejada para o serviço.
Atualize o serviço para executar pelo menos duas tarefas.
Aguarde até que ambas as tarefas atinjam o status Em execução.
Acesse o URL do aplicativo várias vezes e observe o ID da tarefa e o AZ exibidos na parte inferior da página.
Insira as duas IDs de tarefas diferentes separadas por uma vírgula.
DICAS:

Você pode alterar a contagem de tarefas na opção “Atualizar serviço” no console do ECS.
O ALB distribui solicitações em várias tarefas, então você verá IDs de tarefas diferentes ao recarregar a página.
Links para seguir
Atualização de um serviço Amazon ECS
Balanceamento de carga do serviço ECS
Validação de tarefas
Essa tarefa será marcada como concluída quando:

O serviço ECS tem pelo menos duas tarefas no status RUNNING.
Os dois IDs de tarefa que você inseriu correspondem às tarefas reais em execução.
Além disso, você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela Detalhes do desafio.

Pistas
Pistas 1
2Pontos de penalidade
Desbloqueie o Clue
Pistas 2
3Pontos de penalidade
Desbloqueie o Clue
```

achei mais elve consegui resolver, acho que apenas nao sabia se tinha coloca a role certa no lugar certo, teve um tempinho ate atualizar depois de eu suar o read only acess

os dois IDs 

88615d0b2a91480d9d1d3a52ec2c7d9d

827802c4c0564ec6aa53143b8dd5e4cd

documentacoes que estava la mas nao li todas:

https://docs.aws.amazon.com/pt_br/AmazonECS/latest/developerguide/task_definition_parameters.html#task_role_arn

https://docs.aws.amazon.com/pt_br/AmazonECS/latest/developerguide/managed-instances-instance-profile.html

refazendo pela segunda vez:

refiz ela pela segunda vez no domingo, percebi que ainda nao sei a diferenca das 2 roles que a aws cria

outra duvida como eu iria saber que era para escolher aquela poitica ecstask? eu nao saberia escolher

demorei para fazer mesmo sabendo

na segunda task qe era para colocar o s3 ainda nao consegui coloquei nas suas role, nao sei a diferenca e preciso entender isso

a task 3 achei simples e lembrava como fazia tbm

terminei