# JAM Automatizando a categorização de produtos de comércio eletrônico com o Amazon Rekognition e o AWS Lambda (FACIL)

visao geral

```verilog
Você tem a tarefa de aprimorar o sistema de categorização de produtos de uma plataforma de comércio eletrônico. Seu desafio é criar uma solução automatizada que classifique com eficiência as imagens de novos produtos à medida que elas são carregadas, aproveitando os serviços em nuvem para analisar e categorizar cada item sem intervenção humana. Esse processo simplificado revolucionará a forma como a plataforma gerencia seu catálogo de produtos cada vez maior.
```

task 1:

```verilog
Tarefa 1: Solução de problemas de gatilhos do AWS Lambda para categorização automatizada de imagens de comércio eletrônico
Pontos possíveis
24
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
! Categorização de produtos de comércio eletrônico

Plano de fundo
A Acme Online, uma empresa de comércio eletrônico, está implementando uma solução automatizada para categorizar suas imagens de produtos usando os serviços da AWS. Esse sistema visa substituir seu processo de categorização manual, que é demorado e propenso a inconsistências.

Tarefa
Sua empresa de comércio eletrônico, a Acme Online, configurou os componentes iniciais de um sistema automatizado de categorização de imagens de produtos usando os serviços da AWS. Os principais componentes dessa solução incluem:

Bucket Amazon S3 (com o prefixo “categorização do produto”) para armazenar todas as imagens do produto
Função AWS Lambda denominada “função de categorização de produtos” projetada para processar e categorizar imagens
Amazon Rekognition para classificação de imagens
Amazon DynamoDB para armazenar os resultados da categorização
No entanto, o sistema não está funcionando conforme o esperado. Os usuários estão fazendo upload de arquivos para o bucket do Amazon S3, mas a função AWS Lambda não está sendo acionada automaticamente. Como engenheiro, você precisa garantir que, quando os arquivos forem enviados para o S3, a função Lambda seja acionada automaticamente para processar essas imagens.

Serviços a serem usados
Amazon S3
AWS Lambda
Inventário
A função do AWS Lambda chamada product-categorization-function já foi criada.
Um bucket do S3 com o prefixo “categorização do produto” está configurado para receber imagens do produto.
Fluxo de trabalho:
O usuário carrega a imagem para o bucket S3
O bucket S3 deve acionar a função Lambda (mas atualmente não está acontecendo)
A função Lambda deve processar a imagem
O Amazon Recognition categorizará o item
A tabela do DynamoDB será preenchida com o novo item junto com os detalhes da categorização.
**Observação: ** Você tem permissões para modificar as configurações do bucket do S3 e das funções do Lambda, mas não pode modificar o código da função do Lambda ou as políticas do IAM.

Começando
Analise a configuração existente de S3 bucket (com o prefixo “categorização do produto”) e as configurações de Lambda function. Identifique por que o Lambda function não está sendo acionado quando new files é carregado para S3. Implemente uma solução para garantir que a função Lambda seja acionada automaticamente pelos uploads do S3. Teste a solução atualizada fazendo o upload de novas imagens do produto para S3 bucket e verificando se o Lambda function foi acionado.

Validação
A tarefa será concluída automaticamente quando você encontrar uma solução. Você sempre pode verificar seu progresso clicando no botão Check my progress na tela de detalhes do desafio.
```

task 2:

```verilog
Tarefa 2: Depuração de erros de função do AWS Lambda no pipeline de classificação de imagens de comércio eletrônico
Pontos possíveis
24
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
! Categorização de produtos de comércio eletrônico

Plano de fundo
A Acme Online, uma empresa de comércio eletrônico, está implementando uma solução automatizada para categorizar suas imagens de produtos usando os serviços da AWS. Esse sistema visa substituir seu processo de categorização manual, que é demorado e propenso a inconsistências.

Tarefa
Sua empresa de comércio eletrônico, a Acme Online, configurou os componentes iniciais de um sistema automatizado de categorização de imagens de produtos usando os serviços da AWS. Os principais componentes dessa solução incluem:

Bucket Amazon S3 (com o prefixo “categorização do produto”) para armazenar todas as imagens do produto
Função AWS Lambda denominada “função de categorização de produtos” projetada para processar e categorizar imagens
Amazon Rekognition para classificação de imagens
Amazon DynamoDB para armazenar os resultados da categorização
À medida que o cenário do comércio eletrônico continua evoluindo, a Acme Online deve garantir que nosso sistema automatizado de categorização de produtos possa lidar com a grande variedade de imagens em nosso crescente catálogo. Algumas fotos de produtos podem exigir mais tempo de processamento do que outras, especialmente para nossos itens mais complexos.

Ao analisar o desempenho da função Lambda, considere avaliar as configurações de tempo limite atuais. Aumentar o tempo máximo de execução permitido para a função pode ajudar a garantir que ela possa processar totalmente todas as imagens, mesmo as mais complexas, sem expirar prematuramente. The product team have advised to adjust the lambda timeout to it's maximum value.

Ao alinhar a janela operacional de nossa função Lambda com as necessidades de nosso portfólio de produtos, podemos aprimorar a confiabilidade e a precisão de nosso processo automatizado de categorização. Isso, por sua vez, levará a um banco de dados de produtos mais preciso e abrangente — uma vantagem crítica no espaço competitivo de comércio eletrônico.

Lembre-se de que os recursos de nuvem oferecem a flexibilidade de escalar nossas soluções à medida que nossos negócios crescem. A otimização dos parâmetros da função Lambda pode gerar eficiências operacionais significativas para o Acme Online.

Serviços para usar
AWS Lambda
Inventário
A função do AWS Lambda chamada product-categorization-function já foi criada.
Um bucket do S3 com o prefixo “categorização do produto” está configurado para receber imagens do produto.
Fluxo de trabalho:
O usuário carrega a imagem para o bucket S3
O bucket S3 deve acionar a função Lambda (mas atualmente não está acontecendo)
A função Lambda deve processar a imagem
O Amazon Recognition categorizará o item
A tabela do DynamoDB será preenchida com o novo item junto com os detalhes da categorização.
**Observação: ** Você tem permissões para modificar as configurações do bucket do S3 e das funções do Lambda, mas não pode modificar o código da função do Lambda ou as políticas do IAM.

Começando
Analise a função existente do AWS Lambda chamada “função de categorização de produtos” e suas definições de configuração.
Analise os registros do CloudWatch associados à função Lambda para identificar a natureza dos erros que causam o encerramento prematuro.
Validação
A tarefa será concluída automaticamente quando você encontrar uma solução. Você sempre pode verificar seu progresso clicando no botão Check my progress na tela de detalhes do desafio.
```

task 3:

```verilog
Tarefa 3: Configurando eventos de teste para o AWS Lambda: otimizando a classificação de imagens acionadas pelo S3
Pontos possíveis
32
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
! Categorização de produtos de comércio eletrônico

Plano de fundo
A Acme Online, uma empresa de comércio eletrônico, implementou uma solução automatizada para categorizar suas imagens de produtos usando os serviços da AWS. O sistema foi projetado para agilizar o processo de categorização do produto, melhorando a eficiência e a consistência.

Tarefa
Sua empresacomércio eletrônico, a Acme Online, configurou um sistema automatizado de categorização de imagens de produtos usando os serviços da AWS. Os principais componentes dessa solução incluem:

Um balde Amazon S3 para armazenar todas as imagens do produto
Uma funçãoAWS Lambda acionada quando novas imagens são carregadas no bucket do S3
Amazon Rekognition para classificação de imagens
Amazon DynamoDB para armazenar os resultados da categorização
O sistema agora está acionando a função Lambda quando novos arquivos são enviados para o S3. Você deve validar se o Amazon Rekognition criou uma categoria correta para o item mais recente que foi carregado no bucket do Amazon S3.

Inventário
A função do AWS Lambda chamada product-categorization-function já foi criada.
As notificações de eventos do bucket do S3 são configuradas para acionar a função Lambda.
**FLUXO DE TRABALHO: **

O usuário carrega a imagem para o bucket S3
O bucket S3 deve acionar a função Lambda (mas atualmente não está acontecendo)
A função Lambda deve processar a imagem
O Amazon Recognition categorizará o item
A tabela do DynamoDB será preenchida com o novo item junto com os detalhes da categorização.
**Observação: ** Você tem permissões para visualizar e modificar a configuração da função Lambda e os eventos de teste, mas não pode modificar o código real da função Lambda ou as políticas do IAM.

Começando
1. Faça upload de uma nova imagem no bucket do Amazon S3 começando com o prefixo product-categorization.

2. Analise os registros do cloudwatch selecionando o grupo de registros associado à função lambda para ERRORS/INFO.

3. Valide que você tem a categorização esperada na tabela Amazon DynamoDB. Insira o item mais recente categorizado pelo Amazon Rekognition no campo da solicitação de validação “Insira a resposta aqui”.

Validação
A tarefa será concluída automaticamente quando você encontrar uma solução. Você sempre pode verificar seu progresso clicando no botão Check my progress na tela de detalhes do desafio.
```

a