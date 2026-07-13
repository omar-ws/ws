# JAM Encontre a mensagem secreta escondida na fila SQS!

que fiquei na duvida querendo saber por que que e entrada do endpoint e um lambda, por que? o lambda na verdade nao e o que processa?

vpc endpoint sg com entrada para o sg do lmabda https, por que?

![image.png](image%2038.png)

task 1:

```wasm
Encontre a mensagem secreta escondida na fila SQS!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
EndpointSecurityGroup
sg-0e3bb1dc5e58564e2

LambdaSecurityGroup
sg-0102eb3204efe492f

PublicSubnet1
subnet-0528cc8346245903f

PublicSubnet2
subnet-0f8849b8e0d7fbcf1

PublicSubnets
subnet-0528cc8346245903f,subnet-0f8849b8e0d7fbcf1

QueueARN
arn:aws:sqs:us-west-2:990713862188:Jam-Challenge-Queue

QueueName
Jam-Challenge-Queue

QueueURL
https://sqs.us-west-2.amazonaws.com/990713862188/Jam-Challenge-Queue

VPC
vpc-03ad762ee0a2fd4b9

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Por que a função lambda está atingindo o tempo limite?
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
40
Verifique meu progresso

Tarefas e pistas
Antecedentes
A equipe de aplicativos reclamou que eles estão recebendo tempos limite da função Lambda. Você verificou que o lambda foi implantado na VPC pelo seu colega. Mas, quando você testa a função Lambda via console, a execução falha com um erro Task timed out after 3.01 seconds. Você suspeita de um problema com a configuração do VPC Endpoint criada para interagir com o AWS SQS.

Tarefa
Verifique o VPC Endpoint e aplique a configuração de segurança apropriada, seguindo o princípio de privilégio LEAST.

Inventário
Os seguintes recursos foram provisionados para que você possa enfrentar o desafio com sucesso: — AWS Lambda (Jam-Challenge-Lambda) — AWS VPC (desafio JAM)

Endpoint SQS VPC
Grupo de segurança da AWS
Grupo de segurança para o endpoint SQS VPC (endpoint-sg)
Grupo de segurança para a função Lambda (lambda-sg)
***Nota: O grupo de segurança do endpoint deve permitir o tráfego de rede da função Lambda. Ele não deve permitir o tráfego do VPC CIDR. ***

Começando
Entenda sobre o VPC endpoint
Como criar endpoints VPC de interface
Como configurar uma função do Lambda em uma VPC para acessar os serviços da AWS
Comece a usar o AWS Lambda
Como testar a função do AWS Lambda usando o AWS Console **Nota: **
**1. Para executar e testar a função lambda, crie um evento de teste de amostra. **

**2. Após a configuração adequada das permissões do grupo de segurança, a execução do Lambda resultará em uma mensagem de erro explícita em vez de um tempo limite. A resolução desse erro está planejada para a Tarefa #2. **

Validação
A tarefa será concluída automaticamente quando você encontrar a solução. Você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Pistas
Quem pode acessar meu endpoint VPC?
4Pontos de penalidade
Desbloqueie o Clue
Como acessar meu endpoint VPC?
5Pontos de penalidade
Desbloqueie o Clue
```

fiz rapido da segunda pois lmebrava da solucao

task 2:

```wasm
Encontre a mensagem secreta escondida na fila SQS!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
EndpointSecurityGroup
sg-0e3bb1dc5e58564e2

LambdaSecurityGroup
sg-0102eb3204efe492f

PublicSubnet1
subnet-0528cc8346245903f

PublicSubnet2
subnet-0f8849b8e0d7fbcf1

PublicSubnets
subnet-0528cc8346245903f,subnet-0f8849b8e0d7fbcf1

QueueARN
arn:aws:sqs:us-west-2:990713862188:Jam-Challenge-Queue

QueueName
Jam-Challenge-Queue

QueueURL
https://sqs.us-west-2.amazonaws.com/990713862188/Jam-Challenge-Queue

VPC
vpc-03ad762ee0a2fd4b9

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: A função lambda da função AWS tem permissões suficientes para acessar o SQS?
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
40
Verifique meu progresso

Tarefas e pistas
Antecedentes
Depois de atualizar com sucesso a configuração de segurança da VPC, executamos o lambda, mas agora está falhando com um erro when calling the GetQueueUrl operation: The specified queue does not exist or you do not have access to it. O aplicativo (função lambda) pesquisa (recebe) mensagens da fila SQS (Jam-Challenge-Queue) e as processa.

Tarefa
Para concluir essa tarefa, você precisa garantir que a função do IAM anexada à função lambda seja suficiente permissões para realizar operações básicas na fila SQS e obter detalhes sobre a fila SQS. Lembre-se de seguir o princípio de privilégio LEAST ao adicionar/atualizar quaisquer permissões à política existente.

**Nota: **

Para validar a função do AWS Lambda, depois de fazer as alterações necessárias na política do IAM, execute-a.
Se a política Least privilage não for fornecida, a validação da tarefa falhará.
A política do IAM anexada à função AWS Lambda pode ser atualizada para adicionar permissões adicionais.
Inventário
Os seguintes recursos foram provisionados para que você tente com sucesso o desafio:

Função AWS Lambda (Jam-Challenge-Lambda)
Fila Amazon SQS (fila Jam-Challenge-Queue)
Função do IAM (função Jam-Challenge-Role)
Começando
Verifique as permissões do IAM anexadas à função do IAM Jam-Challenge-Role.
Consulte como usar políticas baseadas em identidade com o Amazon SQS.
Validação de tarefas
A tarefa será concluída automaticamente quando você encontrar a solução. Você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Nota:

Revise o código da função lambda e adicione somente as permissões necessárias conforme usadas na função.
Para concluir a tarefa, você precisa executar a função AWS Lambda usando um exemplo de evento de teste.
Siga a política de IAM com menos privilégios.
Ignore os erros relacionados ao IAM Access Analyzer no console do AWS IAM ao atualizar a política do IAM.
A política baseada em recursos do SQS está fora do escopo desse desafio.
Pistas
Quais permissões do IAM permitem o acesso ao serviço Amazon SQS?
4Pontos de penalidade
Desbloqueie o Clue
Atualize a política em linha anexada à função do IAM.
5Pontos de penalidade
Desbloqueie o Clue
```

codigo que estava no lambda:

```python
import json
import boto3
import os

def lambda_handler(event, context):
    #This function will poll the message from SQS queue and insert the message into the another SQS queue for validation.
    print(event)
    queue_name = os.environ['QUEUE_NAME']
    result_queue = os.environ['RESULT_QUEUE']
    region = os.environ['AWS_REGION']
    print(queue_name)

    #Resource with Endpoint
    endpoint = f'https://sqs.{region}.amazonaws.com'
    sqs = boto3.resource('sqs', endpoint_url=endpoint)
    queue = sqs.get_queue_by_name(QueueName=queue_name)

    messages = queue.receive_messages(
            MessageAttributeNames=['All']
    )
    
    for msg in messages:
        print(f"Received message is : {msg.body}")
    if messages:
    	return_msg = msg.body
    else:
    	return_msg = ''

    final_queue = sqs.get_queue_by_name(QueueName=result_queue)
    for msg in messages:
        response = final_queue.send_message(MessageBody=json.dumps(msg.body))

    return {
        'statusCode': 200,
        'body': json.dumps(return_msg)
    }

```

eu ja sabia o que fazer entao foi facil so coloquei as permissoes