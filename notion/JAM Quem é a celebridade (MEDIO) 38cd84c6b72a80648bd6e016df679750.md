# JAM Quem é a celebridade? (MEDIO)

VISAO GERAL

```verilog
Problema de negócios
Você foi recentemente contratado pelo AS-IF Photo Studio como desenvolvedor full-stack. O Photo Studio é famoso por sua enorme coleção de fotos tiradas de celebridades ao longo do século!

Como a única empregadora no departamento de TI, a empresa confia totalmente na sua competência para desenvolver, operar e resolver todas as “coisas relacionadas à tecnologia” dentro da empresa.

Recentemente, sua empresa investiu em um sistema para detectar automaticamente personalidades conhecidas em imagens usando aprendizado de máquina e armazenar as informações em um banco de dados.

A solução foi trazida para resolver o problema com seu arquivo de fotos muito grande com celebridades e nenhum metadado associado às imagens.

O CEO confirma que a solução funcionou perfeitamente bem há um mês.

Ele disse:

“*Acabei de enviar as fotos para o aplicativo e, em seguida, instantaneamente os nomes das celebridades aparecem no banco de dados. *

*Esta solução foi desenvolvida por um estagiário de verão. Não consigo falar com ele, ele não atende minhas ligações ou e-mails. *

*Mas ele me forneceu algumas credenciais para uma conta da AWS. Eu não sei o que é. Mas sim, essa é a única informação que tenho. *”

Sua tarefa é “consertar” os problemas, para que o aplicativo comece a funcionar novamente.

Boa sorte!

Objetivos de aprendizagem
Você trabalhará com serviços como S3, Lambda, Rekognition, IAM e DynamoDB.
```

propriedades de saida:

```verilog
Propriedades de saída
AccountId
076105034722

Bucket
as-if.photo.studio.archive-076105034722

DynamoDBTable
as-if.photo.studio.db

Lambda
as-if-photo-studio-RecognizeFaces

LambdaRole
as-if-photo-studio-RecognizeFaces-lambda_role

Region
ap-northeast-1

```

task 1:

```verilog
Tarefa 1: Acionar a função
Pontos possíveis
38
Penalidade por pista
0
Pontos disponíveis
38
Verifique meu progresso

Tarefas e pistas
Contexto
Você foi recentemente contratado pelo AS-IF Photo Studio como desenvolvedor full-stack. O Photo Studio é famoso por sua enorme coleção de fotos tiradas de celebridades ao longo do século!

Como a única empregadora no departamento de TI, a empresa confia totalmente na sua competência para desenvolver, operar e resolver todas as “coisas relacionadas à tecnologia” dentro da empresa.

Recentemente, sua empresa investiu em um sistema para detectar automaticamente personalidades conhecidas em imagens usando aprendizado de máquina e armazenar as informações em um banco de dados.

A solução foi trazida para resolver o problema com seu arquivo de fotos muito grande com celebridades e nenhum metadado associado às imagens.

O CEO confirma que a solução funcionou perfeitamente bem há um mês.

Ele disse:

“*Acabei de enviar as fotos para o aplicativo e, em seguida, instantaneamente os nomes das celebridades aparecem no banco de dados. *

*Esta solução foi desenvolvida por um estagiário de verão. Não consigo falar com ele, ele não atende minhas ligações ou e-mails. *

*Mas ele me forneceu algumas credenciais para uma conta da AWS. Eu não sei o que é. Mas sim, essa é a única informação que tenho. *”

Sua tarefa é “consertar” os problemas, para que o aplicativo comece a funcionar novamente.

Boa sorte!

Sua tarefa
A função Lambda: (as-if-photo-studio-RecognizeFaces) deve ser acionada sempre que um usuário fizer upload de uma imagem para o S3 Bucket: (as-if.photo.studio.archive-*/Images)

Etapa #1:
Navegue até o S3 Bucket: (as-if.photo.studio.archive-*)

Faça uso das imagens fornecidas no nível raiz

Mova uma das imagens: image*.jpg para (as-if.photo.studio.archive-*/Images)

Navegue até a função Lambda: (as-if-photo-studio-RecognizeFaces)

Clique na guia Monitor e em “Visualizar logs no CloudWatch”

Não há registros. Qual é o problema? Você pode resolver isso?

PS: Você pode mover imagens da raiz para (as-if.photo.studio.archive-*/Images) e vice-versa para verificar se a função Lambda está sendo acionada enquanto você está depurando

Começando
Em primeiro lugar, verifique a guia Propriedades de saída no site do Jam. Ele fornece muitos parâmetros que podem ser usados para esse desafio.

Navegue até o serviço Lambda no Console de Gerenciamento da AWS.

Dedique algum tempo no início para analisar e entender a função Lambda pré-configurada: (as-if-photo-studio-RecognizeFaces)

Inventário
À sua disposição, você tem acesso ao ambiente da AWS da empresa em que a solução de detecção facial é implantada. Entre outros, esse ambiente é provisionado com os seguintes recursos:

**S3 Bucket: ** (as-if.photo.studio.archive-*): Este bucket é usado para fazer upload de fotos de celebridades.
**Função AWS Lambda: ** (as-if-photo-studio-RecognizeFaces): Isso lida com a automação necessária para capturar as imagens de celebridades e reconhecer a pessoa que usa o Amazon Rekognition.
**Função do Amazon IAM: ** (as-if-photo-studio-RecognizeFaces-lambda_role): Essa função do IAM contém as permissões necessárias para a execução adequada da função Lambda.
**Tabela do Amazon DynamoDB: ** (as-if.photo.studio.db): Este é o banco de dados onde os nomes de celebridades reconhecidas são armazenados.
Serviços da AWS que você deve usar
Amazon S3
AWS Lambda
CloudWatch
Validação de tarefas
Depois de corrigir o problema com êxito, a função deve ser acionada e gerar logs no CloudWatch

A tarefa será concluída automaticamente assim que você encontrar a solução, além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Depois que essa tarefa for concluída, você poderá passar para a Tarefa 2.

Pistas
Usar o AWS Lambda com o Amazon S3
3Pontos de penalidade
Desbloqueie o Clue
Usar um gatilho do Amazon S3 para invocar uma função do Lambda
4Pontos de penalidade
Desbloqueie o Clue
```

task 2

```verilog
Tarefa 2: [ERRO] KeyError: 'TABLE_NAME'?!
Pontos possíveis
38
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Viva!!! Fico feliz que você tenha conseguido concluir a tarefa anterior.

Agora você aprendeu que pode usar o Lambda para processar notificações de eventos do Amazon Simple Storage Service.

O Amazon S3 pode enviar um evento para uma função do Lambda quando um objeto é criado ou excluído.

Agora que você resolveu a Tarefa 1, a função: (as-if-photo-studio-RecognizeFaces) é acionada sempre que você adiciona uma imagem a (as-if.photo.studio.archive-*/Images).

Mas há algo errado com o código Lambda.

Sua tarefa
Seu objetivo é corrigir o primeiro problema de código que está causando a falha do Lambda.

Tente executar a função Lambda para ver qual erro ela gera e consulte a resposta de saída em busca de pistas.

Para executar o Lambda:
Visite o console da AWS
Procure por Lambda e clique nele
No painel de navegação à esquerda, em Funções, selecione a função começando com (as-if-photo-studio-RecognizeFaces)
Clique no botão Testar e insira os detalhes abaixo (ignore isso, se você já tiver criado um evento de teste).
Selecione Create new test event
Modelo de evento como hello-world
Nome do evento como testevent
Mantenha o json padrão preenchido intacto
Clique no botão Create ou Save changes
Clique no botão Testar novamente e você poderá ver os resultados na guia Resultados da execução.
PS: Nessa tarefa, você não precisa fazer nenhuma alteração no código Lambda!

Começando
Para concluir essa tarefa, use o AWS Management Console e navegue até a função Lambda.

Inventário
À sua disposição, você tem acesso ao ambiente da AWS da empresa em que a solução de detecção facial é implantada. Entre outros, esse ambiente é provisionado com os seguintes recursos:

**S3 Bucket: ** (as-if.photo.studio.archive-*): Esse bucket é usado para fazer upload de fotos de celebridades.
**Função do AWS Lambda: ** (as-if-photo-studio-RecognizeFaces): trata da automação necessária para capturar as imagens de celebridades e, em seguida, reconhecer a pessoa usando o Amazon Rekognition.
**Função do Amazon IAM: ** (as-if-photo-studio-RecognizeFaces-lambda_role): Essa função do IAM contém as permissões necessárias para a execução adequada da função Lambda.
**Tabela do Amazon DynamoDB: ** (as-if.photo.studio.db): Esse é o banco de dados no qual os nomes de celebridades reconhecidas são armazenados.
Serviços da AWS que você deve usar
AWS Lambda
Validação de tarefas
Depois de corrigir o problema com sucesso, o TABLE_NAME deve ser impresso na guia Resultados da execução.

A tarefa será concluída automaticamente assim que você encontrar a solução. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Depois que essa tarefa for concluída, você poderá passar para a Tarefa 3.

Pistas
Usando variáveis de ambiente do AWS Lambda
3Pontos de penalidade
Desbloqueie o Clue
Adicionar TABLE_NAME como uma variável de ambiente
4Pontos de penalidade
Desbloqueie o Clue
```

task 3:

```verilog
Tarefa 3: FALTANDO ALGUNS PRIVILÉGIOS???
Pontos possíveis
38
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Agora que você cumpriu essa tarefa, você está se saindo maravilhosamente bem. O CEO está muito feliz com seu progresso atual. Mas você ainda não chegou lá. Ainda há algum trabalho a ser feito.

Sua tarefa
Seu objetivo é corrigir o problema de permissão que não permite que o Lambda armazene dados na tabela do DynamoDB.

Mova uma imagem para (as-if.photo.studio.archive-*/Images). Isso acionará a função Lambda.

Use o CloudWatch para verificar os registros gerados pela função.

PS: Certifique-se de seguir o conselho de segurança padrão de conceder acesso com privilégios mínimos.

Conceda somente a permissão necessária para realizar a tarefa.

Começando
Para concluir essa tarefa, use o AWS Management Console e navegue até o serviço Identity and Access Management (IAM).

Inventário
À sua disposição, você tem acesso ao ambiente da AWS da empresa em que a solução de detecção facial é implantada. Entre outros, esse ambiente é provisionado com os seguintes recursos:

**S3 Bucket: ** (as-if.photo.studio.archive-*): Esse bucket é usado para fazer upload de fotos de celebridades.
**Função do AWS Lambda: ** (as-if-photo-studio-RecognizeFaces): trata da automação necessária para capturar as imagens de celebridades e, em seguida, reconhecer a pessoa usando o Amazon Rekognition.
**Função do Amazon IAM: ** (as-if-photo-studio-RecognizeFaces-lambda_role): Essa função do IAM contém as permissões necessárias para a execução adequada da função Lambda.
**Tabela do Amazon DynamoDB: ** (as-if.photo.studio.db): Esse é o banco de dados no qual os nomes de celebridades reconhecidas são armazenados.
Serviços da AWS que você deve usar
Função do Amazon IAM
Balde S3
CloudWatch
Validação de tarefas
Depois de corrigir o problema com sucesso, a função Lambda será autorizada a armazenar dados na tabela do DynamoDB.

A tarefa será concluída automaticamente assim que você encontrar a solução. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Depois que essa tarefa for concluída, você poderá passar para a Tarefa 4.

Pistas
Acesso excessivamente permissivo
3Pontos de penalidade
Desbloqueie o Clue
A declaração de política
4Pontos de penalidade
Desbloqueie o Clue
```

task 4:

```verilog
Quem é a celebridade?
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 4: OHHH!!! Parece que você tem que consertar o código
Pontos possíveis
36
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Essa é a tarefa final que você precisa resolver antes de poder voltar ao CEO com uma boa notícia.

No entanto, o Lambda ainda está falhando com um erro específico.

Sua tarefa
Seu objetivo é corrigir o segundo problema de código que está causando a falha do Lambda.

Tente executar a função Lambda para ver qual erro ela gera e verifique a resposta de saída em busca de pistas.

Etapa #1:
Navegue até o S3 Bucket: (as-if.photo.studio.archive-*)

Use as imagens fornecidas para você na raiz.

Mova uma das imagens: image*.jpg para (as-if.photo.studio.archive-*/Images)

Navegue até a função Lambda: (as-if-photo-studio-RecognizeFaces)

Clique na guia Monitor e em “Exibir registros no CloudWatch”

Encontre o registro de eventos mais recente e copie o objeto de evento JSON de entrada.

Um evento é um documento formatado em JSON que contém dados para uma função do Lambda processar.

Você o encontrará abaixo do texto: The incoming event below:

Deve ser semelhante ao abaixo (o evento abaixo é apenas um exemplo):

OBSERVAÇÃO: NÃO USE O EVENTO ABAIXO PARA DEPURAR SEU LAMBDA. ENCONTRE O EVENTO SEMELHANTE AO ABAIXO EM SEUS REGISTROS DO CLOUD WATCH

{
    "Records": [
        {
            "eventVersion": "2.1",
            "eventSource": "aws:s3",
            "awsRegion": "ap-northeast-1",
            "eventTime": "2022-03-09T21:07:11.828Z",
            "eventName": "ObjectCreated:Copy",
            "userIdentity": {
                "principalId": "AWS:XXXXXXXXXXXXXXXXXXXXX:default"
            },
            "requestParameters": {
                "sourceIPAddress": "xxx.xxx.xxx.xxx"
            },
            "responseElements": {
                "x-amz-request-id": "KY8F8WEM7HAWMXBX",
                "x-amz-id-2": "NjO3UWfnFgXpxaB7aOVPqmSr3+CBRlQaIQXHJJIVPdarPp+VnNo6TEGP1WS/5/J4WiB5XAkTy00Eo7nKrm8YKXZsrvv8KqZJPtTEiMpSFEg="
            },
            "s3": {
                "s3SchemaVersion": "1.0",
                "configurationId": "af7c18e3-fc12-44b5-a7a8-919ebea6b25d",
                "bucket": {
                    "name": "as-if.photo.studio.archive-34266e60",
                    "ownerIdentity": {
                        "principalId": "AB2L4G61011SE"
                    },
                    "arn": "arn:aws:s3:::as-if.photo.studio.archive-34266e60"
                },
                "object": {
                    "key": "Images/image2.jpg",
                    "size": 53785,
                    "eTag": "3af650022f1cd167b9f8fca1d8f02db2",
                    "sequencer": "00622916FFB04A8DF0"
                }
            }
        }
    ]
}
PS: Você está copiando esse evento JSON para facilitar a depuração. Em vez de mover imagens para frente e para trás de e para (as-if.photo.studio.archive-*/Images) para acionar a função Lambda.

Para executar o Lambda:
Visite o console da AWS
Procure por Lambda e clique nele
Na navegação à esquerda, em Funções, selecione a função começando com (as-if-photo-studio-RecognizeFaces)
Clique no botão Testar e insira os detalhes abaixo (ignore isso se você já tiver criado um evento de teste).
Selecione Create new test event
Modelo de evento como hello-world
Nome do evento como debug_lambda
Cole o evento JSON que você copiou do registro de eventos em seu grupo de registros do Cloud Watch
Clique no botão Create ou Save changes
Clique no botão Testar novamente e você poderá ver os resultados na guia Resultados da execução.
Para fazer uma alteração no código do Lambda e implantar:
Visite o console da AWS
Procure por Lambda e clique nele
Na navegação à esquerda, em Funções, selecione a função começando com aws-jam-challenge-*
Visite a guia chamada Código
Abra o arquivo index.py
Faça a alteração necessária no arquivo index.py e clique no botão Implantar na parte superior.
Você pode clicar no botão Testar para testar suas alterações
**PS: Certifique-se de fazer um backup do código existente antes de fazer qualquer alteração. **

Você finalmente conseguiu?!
Depois de resolver o erro e não receber mais nenhuma resposta de erro, navegue até a tabela do DynamoDB

Pesquise o DynamoDB na guia de pesquisa e navegue até Explore items

Selecione a tabela chamada: (as-if.photo.studio.db)

Você deve encontrar um ou vários itens com celebridades reconhecidas.

Quão incrível é isso?

Começando
Para concluir essa tarefa, use o AWS Management Console e, em seguida, navegue até o S3 Bucket.

Inventário
À sua disposição, você tem acesso ao ambiente AWS da empresa em que a solução de detecção facial é implantada. Entre outros, esse ambiente é provisionado com os seguintes recursos:

**S3 Bucket: ** (as-if.photo.studio.archive-*): Este bucket é usado para fazer upload de fotos de celebridades.
**Função AWS Lambda: ** (as-if-photo-studio-RecognizeFaces): trata da automação necessária para capturar as imagens de celebridades e depois reconhecer a pessoa que usa o Amazon Rekognition.
**Função do Amazon IAM: ** (as-if-photo-studio-RecognizeFaces-lambda_role): Essa função do IAM contém as permissões necessárias para a execução adequada da função Lambda.
**Tabela do Amazon DynamoDB: ** (as-if.photo.studio.db): Esse é o banco de dados em que os nomes de celebridades reconhecidas são armazenados.
Serviços da AWS que você deve usar
Amazon S3
AWS Lambda
CloudWatch
DynamoDB
Validação de tarefas
Depois de corrigir o problema com êxito, um item deve ser criado na tabela do DynamoDB.

A tarefa será concluída automaticamente quando você encontrar a solução. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Depois que essa tarefa for concluída, você terá concluído o desafio.

Pistas
Um ou mais valores de parâmetros eram inválidos: falta a chave chave no item
3Pontos de penalidade
Desbloqueie o Clue
tabela.put_item
4Pontos de penalidade
Desbloqueie o Clue
```

eu achei mais ou menos esse gostei sabia de algumas coisas, mas usei o claude no final pois o erro no codigo era um k minusculo do key, codigo do lambda

```verilog
import os
import json
import boto3

TABLE_NAME = os.environ['TABLE_NAME']

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table(TABLE_NAME)
s3 = boto3.resource('s3')
rekognition = boto3.client('rekognition')

def lambda_handler(event, context):

    # Print the Incoming Event
    print(json.dumps(event))

    # Print The Table Name
    print("Table name is:", TABLE_NAME)

    # Get the object from the event
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']

    obj = s3.Object(bucket, key)
    image = obj.get()['Body'].read()
    print('Recognizing celebrities...')
    response = rekognition.recognize_celebrities(Image={'Bytes': image})

    names = []

    for celebrity in response['CelebrityFaces']:
        name = celebrity['Name']
        print('Name: ' + name)
        names.append(name)

    print(names)

    print('Saving face data to DynamoDB table:', TABLE_NAME)
    response = table.put_item(
        Item={
            'Key': key,
            'names': names,
        }
    )
    
    print(json.dumps(response))

    return {
      "ResponseMetadata": response['ResponseMetadata']
    }

```

erro que estava dando

```verilog

2026-06-28T00:32:51.219Z
[ERROR] ClientError: An error occurred (ValidationException) when calling the PutItem operation: One or more parameter values were invalid: Missing the key Key in the item
Traceback (most recent call last):
  File "/var/task/index.py", line 40, in lambda_handler
    response = table.put_item(
  File "/var/lang/lib/python3.12/site-packages/boto3/resources/factory.py", line 581, in do_action
    response = action(self, *args, **kwargs)
  File "/var/lang/lib/python3.12/site-packages/boto3/resources/action.py", line 88, in __call__
    response = getattr(parent.meta.client, operation_name)(*args, **params)
  File "/var/lang/lib/python3.12/site-packages/botocore/client.py", line 606, in _api_call
    return self._make_api_call(operation_name, kwargs)
  File "/var/lang/lib/python3.12/site-packages/botocore/context.py", line 123, in wrapper
    return func(*args, **kwargs)
  File "/var/lang/lib/python3.12/site-packages/botocore/client.py", line 1094, in _make_api_call
    raise error_class(parsed_response, operation_name)
```

z