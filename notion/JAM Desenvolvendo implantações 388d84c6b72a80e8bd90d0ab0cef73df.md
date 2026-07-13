# JAM Desenvolvendo implantações

VISAO GERAL

```jsx
Você é um desenvolvedor que oferece suporte a um aplicativo web muito importante voltado para o cliente. O aplicativo web é hospedado no EC2 usando o Nginx e você precisa ajudar sua equipe a configurar um mecanismo de implantação contínua para fornecer atualizações de forma rápida, segura e confiável. O AWS CodeDeploy é um serviço totalmente gerenciado que automatiza as implantações de software. Seu aplicativo é implantado em um grupo do AWS Auto Scaling e você quer garantir que uma atualização de software seja implantada. Uma implantação também precisará ser executada toda vez que o Auto Scaling lançar uma nova instância do EC2 em seu nome. A boa notícia é que outro desenvolvedor da sua equipe já empacotou o código-fonte do aplicativo para você — sua tarefa é recuperar a fonte e modificar o pacote para que o aplicativo possa ser implantado com o AWS Code Deploy! O código-fonte está localizado na seção Ativos do desafio.

```

TASK 1 A 3

```jsx
Antecedentes
Como engenheiro de DevOps, você decidiu usar o CodeDeploy para implantar alterações de HTML em seu aplicativo.

Seu aplicativo é implantado em um AWS Auto Scaling grupo e você deseja garantir que uma atualização de software seja implantada no atual frota de instâncias do EC2. Uma implantação também precisará ser executada sempre que o Auto Scaling lança uma nova instância do EC2 em seu nome.

A boa notícia é que outro desenvolvedor da sua equipe já empacotou (ZIP) o código HTML do aplicativo. Sua tarefa é para recuperar a fonte e modificar o pacote para que o HTML atualizado possa ser implantado com o AWS Code Deploy.

Tarefa
Sua primeira tarefa é criar um arquivo appspec.yml válido com chaves de localização para os ganchos ApplicationStop, BeforeInstall e ApplicationStart. Consulte: https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file.html

NOTA: Somente o nome padrão é permitido para este arquivo e somente o arquivo ZIP deve ser carregado para o s3 - source.zip

Começando
Faça o download do código-fonte usando o link fornecido abaixo. Para facilitar, uma amostra appspex-FIXME.yml foi adicionada ao ZIP.
source.zip

Descompacte o arquivo source.zip.

Crie um arquivo válido appspec.yml. Certifique-se de dizer ao CodeDeploy que extraia os arquivos para /opt/codedeploy. Outro código depende desse caminho. Usaremos os ganchos Application Stop, BeforeInstall e ApplicationStart para CodeDeploy, não use o gancho Install.

OPCIONAL: atualize o texto UPDATEME no arquivo deploy/index.html para o dia de hoje. Exemplo: Today is Friday

Certifique-se de que a localização dos scripts seja mencionada para cada um dos ganchos no arquivo appspec.yml. Abaixo está um exemplo.

Parada de aplicativos:

localização: deploy/applicationstop.sh tempo limite: 60 runas: root
ZIP do conteúdo. Não altere a estrutura da pasta. Ele deve ter appspec.yml na raiz do ZIP, além da pasta deploy com todos os scripts necessários e index.html
Faça o upload do código-fonte modificado para o bucket do S3. Um bucket foi provisionado com o nome no formato jam-codedeploy--
Copie o URI do S3 para o objeto do S3 - source.zip no bucket.
Inventário
Um bucket do Amazon S3 é provisionado para você, no qual você precisa fazer o upload do arquivo source.zip atualizado. Você pode encontrar o nome do bucket do S3 no Aba output properties no lado esquerdo da página de tarefas do jam.

Serviços
Amazon S3

Validação de tarefas
Depois que o arquivo de origem do S3 for recarregado no Bucket in Outputs, a Jam Platform marcará a tarefa como bem-sucedida.

Pistas
Etapas para preparar o artefato de implantação
2Pontos de penalidade
Desbloqueie o Clue
Guia completo para preparar o artefato de implantação
3Pontos de penalidade

 TASK 2
 
 Tarefa 2: Crie o grupo de aplicativos e implantação do CodeDeploy
Pontos possíveis
24
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Agora você deve configurar o CodeDeploy para sua implantação

Tarefa
Crie um aplicativo CodeDeploy e um grupo de implantação do CodeDeploy.

Começando
Você pode usar o console do AWS CodeDeploy ou o AWS CLI para realizar essa tarefa.

Crie um aplicativo CodeDeploy e um grupo de implantação do CodeDeploy.
Certifique-se de ligar para seu aplicativo jam-app e para o grupo de implantação do CodeDeploy jam. Essa etapa é importante para que o desafio seja validado adequadamente.
Você precisa configurar a implantação “no local” e “uma de cada vez”.
Lembre-se de que, se a implantação falhar, ela deverá ser revertida.
Você não precisará de nenhum balanceador de carga para essa implantação
Inventário
arquivo source.zip que você carregou na Tarefa 1.
A função de serviço CodeDeploy já foi criada para você. É chamado Jam-CodeDeploy.
Você não precisa modificar nenhum recurso do IAM para concluir esse desafio.
Serviços
AWS CodeDeploy

Validação
A plataforma Jam validará para você quando o aplicativo e o grupo de implantação do CodeDeploy forem criados.

Pistas
Guia completo para criar o grupo de aplicativos e implantação do CodeDeploy
2Pontos de penalidade

TASK 3

Tarefa 3: Crie a implantação
Pontos possíveis
32
Penalidade por pista
0
Pontos disponíveis
32
Verifique meu progresso

Tarefas e pistas
Antecedentes
Agora você deve pedir ao CodeDeploy que implante seu código.

Tarefa
Crie uma implantação do CodeDeploy

Começando
Você pode usar o console do AWS CodeDeploy ou o AWS CLI para realizar essa tarefa.

Crie a implantação no jam-app aplicativo e aponte para o Amazon S3 source.zip que você carregou na Tarefa 1.
O comportamento dessa implantação deve sobrescrever o conteúdo.
Inventário
source.zip já deve ter sido enviado
O nome do S3 Bucket está disponível na seção output properties.
Serviços
AWS CodeDeploy
Amazon S3
Validação
O aplicativo Jam validará se a última implantação foi bem-sucedida e abrirá o Grupo de Segurança e verificará o texto correto na página da web. **Aguarde até que a implantação seja bem-sucedida antes de verificar o progresso. **

OPCIONAL: Para validar a página da web por meio de um navegador, pesquise o AWS Systems Manager na barra de pesquisa. No lado esquerdo, escolha Armazenamento de parâmetros em Gerenciamento de aplicativos. Selecione o hiperlink /sj/codedeploy/dns. Copie a string fornecida em Valor e cole-a em um navegador da web para ver a página da web.

Pistas
Guia completo para verificar o status da implantação e a página da Web criada pelo Codedeploy
3Pontos de penalidade

```

a