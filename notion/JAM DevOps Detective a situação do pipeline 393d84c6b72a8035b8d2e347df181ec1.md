# JAM DevOps Detective: a situação do pipeline

```jsx
Visão geral
Você é engenheiro de DevOps na TechCorp, uma empresa de software em crescimento. Recentemente, sua equipe de desenvolvimento configurou um pipeline de CI/CD usando o AWS CodePipeline para implantar seu aplicativo web em uma frota de instâncias do EC2. No entanto, as implantações estão falhando e a equipe está se esforçando para identificar a causa raiz. Sua tarefa é investigar e corrigir os problemas com o pipelin
```

```jsx
Tarefa 1: Validação de configuração
Pontos possíveis
75
Penalidade por pista
7
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Como engenheiro de DevOps recém-nomeado na TechCorp, você foi encarregado de investigar uma falha no pipeline de CI/CD. A equipe de desenvolvimento relatou falhas em suas implantações de aplicativos web em instâncias do EC2. Sua primeira etapa é examinar a configuração existente do CodePipeline e identificar se as implantações estão sendo configuradas corretamente em instâncias do EC2 que fazem parte de um grupo-alvo do AWS ALB.

Sua tarefa
Sua jornada começa no AWS Management Console, onde você precisará navegar pelo cenário digital para encontrar o serviço CodePipeline. O centro de sua investigação gira em torno da ação de implantação do EC2 no estágio “Implantação”. Você precisa garantir que a ação do estágio “Implantar” do CodePipeline seja direcionada às instâncias presentes no grupo-alvo do AWS ALB.

Inventário:
AWS CodePipeline: devops-detective-pipeline
Instâncias EC2:2 instâncias em um grupo-alvo do AWS ALBjam-codepipeline-target-group
Bucket S3 de artefatos: devops-detective-jam-artifact-store-<>
Fonte do bucket S3: devops-detective-jam-source-bucket-<>
Serviços que você deve usar:
AWS CodePipeline
Amazon EC2
Amazon S3
Cuidado
! Pipeline de código

Ao salvar o funil, se NÃO estiver fazendo nenhuma alteração no estágio “Origem” do funil, certifique-se de marcar a caixa “Nenhuma atualização de recursos necessária para esta alteração da ação de origem”

Validação de tarefas:
Para concluir essa tarefa, você precisa identificar corretamente o elemento ausente na configuração da ação de implantação do EC2. Depois de adicionar o elemento ausente, clique em “Verificar meu progresso” na função de validação para verificar se você identificou corretamente o problema.

Pistas
Verifique a configuração
7Pontos de penalidade
Mostrar pista
Passo a passo completo
9Pontos de penalidade
Desbloqueie o Clue

Tarefa 2: Investigação de dutos
Pontos possíveis
75
Penalidade por pista
16
Pontos disponíveis
59
Verifique meu progresso

Tarefas e pistas
Enviar resposta
Antecedentes
Agora que o grupo-alvo do ALB foi adicionado ao estágio de implantação do pipeline, as alterações do aplicativo podem ser implantadas diretamente por meio do CodePipeline em instâncias do EC2 que estão atendendo ao tráfego por trás do balanceador de carga. No entanto, o pipeline ainda está em um estado de “Falha” porque os arquivos necessários não foram encontrados na fonte. A TechCorp decidiu também implantar arquivos de configuração do servidor web por meio do mesmo pipeline para seguir as melhores práticas de CI/CD em vez de executar manualmente os scripts de implantação do servidor web.

Sua tarefa
Suas tarefas são as seguintes:

NOTA: CERTIFIQUE-SE DE QUE OS NOMES DOS ARQUIVOS SEJAM EXATAMENTE OS MESMOS

Baixe os seguintes arquivos localmente:
https://aws-jam-challenge-resources.s3.amazonaws.com/code-pipeline-ec2/index.html
https://aws-jam-challenge-resources.s3.amazonaws.com/code-pipeline-ec2/styles.css
https://aws-jam-challenge-resources.s3.amazonaws.com/code-pipeline-ec2/script.js
Você pode abrir os links no seu navegador -> Clique com o botão direito -> Selecione “Exibir código-fonte da página” para copiar o conteúdo

Crie o arquivo deployspec.yml. Certifique-se de que ele faça referência a 2 scripts: um script “BeforeDeploy” (arquivo.sh) e um script “AfterDeploy” (arquivo.sh).

O script “BeforeDeploy” será usado para instalar o servidor web, suas dependências e quaisquer outros pacotes necessários.

O script “AfterDeploy” será usado para iniciar o servidor web.

Você pode consultar o documento aqui sobre a implantação de um servidor web: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateWebServer.html

Você pode fazer login nas instâncias para solucionar problemas por meio do Systems Manager selecionando a instância relevante no console do EC2 -> Conectar -> Gerenciador de sistemas -> Conectar

Seu objetivo é empacotar todos os arquivos: index.html, styles.css, script.js, deployspec.yml e os 2 scripts (beforeDeploy e afterDeploy) e enviá-los para o bucket de origem no S3 para acionar uma execução bem-sucedida do pipeline.
OBSERVAÇÃO: Nenhuma mudança de rede é necessária para concluir esse desafio. Além disso, NÃO faça alterações nos nomes ou no conteúdo dos arquivos index.html, styles.css ou script.js para uma validação bem-sucedida

Inventário:
AWS CodePipeline: devops-detective-pipeline
Instâncias EC2:2 instâncias em um grupo-alvo do AWS ALBjam-codepipeline-target-group < account_id>* Fonte do bucket S3: devops-detective-jam-source-bucket-<>
Serviços que você deve usar:
AWS CodePipeline
Amazon EC2
Amazon S3
Validação de tarefas:
Para concluir essa tarefa, você precisa empacotar todos os arquivos e garantir que o pipeline seja executado com êxito. Uma vez feito isso, navegue até o nome DNS do Application Load Balancer “devops-detective-lb” e certifique-se de que a página HTML seja carregada com êxito.

Insira o nome DNS do Application Load Balancer “devops-detective-lb” na caixa de resposta e clique em “Enviar resposta” para verificar o desafio.

Pistas
Criando os scripts de implantação antes e depois
7Pontos de penalidade
Mostrar pista
arquivo deployspec.yml
9Pontos de penalidade
Mostrar pista

```

nao conclui a tarefa 2 pois tive q sair, rever documentaçao