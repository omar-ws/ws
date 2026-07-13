# JAM Foundational Serverless: conectando eventos do S3 #7

> 
> 
> 
> Como engenheiro de software em uma equipe de desenvolvimento de aplicativos, você recebeu a tarefa de experimentar uma solução baseada em nuvem para saber como sua organização pode automatizar o processamento de imagens e documentos.
> 
> O processamento de imagens e documentos é um processo comercial essencial para sua organização, mas o software atual é anterior à computação em nuvem. Esse software não usa modelos modernos gerados por aprendizado de máquina para processar os arquivos e não é escalável para suportar suas cargas de trabalho atuais.
> 
> Um dos membros da sua equipe escreveu um código para trabalhar com o serviço [Amazon Rekognition](https://aws.amazon.com/rekognition/) e o implantou como uma função AWS Lambda sem servidor. [Ao manter a solução sem servidor, sua equipe espera que o experimento demonstre uma solução que não só seja escalável para atender a diferentes cargas de trabalho, mas também seja econômica.](https://aws.amazon.com/lambda/)
> 
> [!](https://aws.amazon.com/lambda/) [Arquitetura do desafio](https://aws-jam-challenge-resources.s3.amazonaws.com/s-3-events/2.0.0/question-lambda-rekog.png)
> 
> Sua tarefa é determinar como os arquivos enviados podem invocar automaticamente essa função, evitando a necessidade de outro processo para monitorar o armazenamento de novas imagens.
> 

[https://aws.amazon.com/pt/rekognition/](https://aws.amazon.com/pt/rekognition/)

o que e amazon rekognition?

task 1:

```jsx
Plano de fundo
Sua equipe concordou que o Amazon S3 seria o melhor serviço de armazenamento para as imagens e documentos ingeridos. O S3 pode suportar um grande número de objetos, cada um com até 5 TB de tamanho, o que é muito maior do que você espera processar.

Espera-se que a arquitetura final ao concluir este desafio seja:

! Arquitetura

Sua tarefa
Nessa primeira tarefa, você precisará criar um bucket do S3 onde ingerirá imagens para processamento.

Inventário
Observe a região em que esse desafio está ocorrendo.

Começando
Navegue até o console do Amazon S3 pesquisando por S3 na caixa de pesquisa do console AWS.

Serviços que você deve usar
Amazon S3

Validação de tarefas
Para concluir essa tarefa, digite o nome do bucket que você criou.
```

apenas criei um bucket

task 2:

```jsx
Plano de fundo
Um dos benefícios que você espera demonstrar com essa arquitetura é que o upload de arquivos no bucket do Amazon S3 invocará automaticamente a função AWS Lambda.

Sua tarefa
Configure uma notificação automática quando um novo objeto for criado em seu bucket e teste-o fazendo o upload de kitten.jpg ou box.jpg em seu bucket para que a imagem seja processada.

Inventário
Bucket S3 criado na tarefa anterior
A função AWS Lambda com RekogLambda em seu nome
Dois arquivos de imagem kitten.jpg ou box.jpg podem ser usados para acionar o processo. Baixe-os para o seu desktop, esses arquivos podem ser enviados mais de uma vez.
Começando
Volte para o bucket do S3 que você criou na tarefa anterior para configurar as propriedades dessa tarefa.

Serviços que você deve usar
Amazon S3

Serviços opcionais que você pode explorar
Opcionalmente, explore a função RekogLambda Lambda para ver sua implementação, configuração, permissões e a saída gerada ao processar uma imagem. Isso não é necessário para concluir o desafio.

AWS Lambda -> Funções -> função com RekogLambda em seu nome
Código para ver a implementação.
Configuração para ver como ela é configurada, incluindo a função de execução e as permissões da política de recursos.
Monitor -> Exibir os registros do CloudWatch -> selecione o stream de log mais recente e a saída do Amazon Rekognition.
Validação de tarefas
A tarefa será concluída automaticamente quando uma imagem for carregada e processada, mas você pode pressionar o botão Verificar meu progresso na tela Detalhes do desafio a qualquer momento para receber dicas sobre o que ainda precisa fazer para concluir a tarefa.
```

eu bati a cabeca fui em outro servico e no final das contas era so adicionar uma notificacao para o lambda

eu questione demaius o anunciado tenho que aprender a ler mais o anunciado

vou para outro jam ja que terminei