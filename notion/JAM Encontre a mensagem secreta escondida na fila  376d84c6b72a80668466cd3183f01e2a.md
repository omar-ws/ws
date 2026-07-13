# JAM Encontre a mensagem secreta escondida na fila SQS!

```wasm
Visão geral
Você é engenheiro de DevOps em uma empresa multinacional, a ABC Limited. Recentemente, houve uma auditoria de segurança e o auditor descobriu que algumas das funções do AWS Lambda não estão implantadas em uma VPC. De acordo com as diretrizes de segurança da sua organização, todas as funções do AWS Lambda devem estar em um ambiente seguro. Portanto, é uma violação de segurança e sua equipe de especialistas da AWS precisa reconfigurar e implantar todas as funções do Lambda em uma VPC. Além disso, precisamos garantir que nenhuma funcionalidade existente seja interrompida, pois haverá uma demonstração para clientes na próxima semana.

Essa tarefa foi atribuída a um membro da sua equipe e reconfigurou as funções do Lambda na AWS VPC. No entanto, devido a uma emergência, o membro da sua equipe precisa se despedir antes de testar totalmente o aplicativo. A equipe de aplicativos está se preparando para a demonstração e, durante a execução, encontrou problemas com a função Lambda. Seu gerente entrou em contato com você para obter ajuda para concluir essa tarefa antes da demonstração para o cliente. Pronto para mergulhar?]
Encontre a mensagem secreta escondida na fila SQS!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
EndpointSecurityGroup
sg-0d2c0a51da5e2aafd

LambdaSecurityGroup
sg-03b93927a170b0ac4

PublicSubnet1
subnet-066968a2813d05968

PublicSubnet2
subnet-06b09b9f2ae585b8b

PublicSubnets
subnet-066968a2813d05968,subnet-06b09b9f2ae585b8b

QueueARN
arn:aws:sqs:us-east-1:294028244101:Jam-Challenge-Queue

QueueName
Jam-Challenge-Queue

QueueURL
https://sqs.us-east-1.amazonaws.com/294028244101/Jam-Challenge-Queue

VPC
vpc-08a8ae788d758ba8b

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Por que a função lambda está atingindo o tempo limite?
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
0

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

TASK 2:

Encontre a mensagem secreta escondida na fila SQS!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
EndpointSecurityGroup
sg-0d2c0a51da5e2aafd

LambdaSecurityGroup
sg-03b93927a170b0ac4

PublicSubnet1
subnet-066968a2813d05968

PublicSubnet2
subnet-06b09b9f2ae585b8b

PublicSubnets
subnet-066968a2813d05968,subnet-06b09b9f2ae585b8b

QueueARN
arn:aws:sqs:us-east-1:294028244101:Jam-Challenge-Queue

QueueName
Jam-Challenge-Queue

QueueURL
https://sqs.us-east-1.amazonaws.com/294028244101/Jam-Challenge-Queue

VPC
vpc-08a8ae788d758ba8b

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

# **Funções** (34) **Informações**

**Excluir**

**Criar perfil**

Um perfil do IAM é uma identidade que você pode criar que tem permissões específicas com credenciais válidas por curtos períodos. Os perfis podem ser assumidos por entidades em que você confia.

- 
- **1**
- 2
- 

|  | **Nome da função** | **Entidades confiáveis** | **Última atividade** |
| --- | --- | --- | --- |

|  | **Nome da função** | **Entidades confiáveis** | **Última atividade** |
| --- | --- | --- | --- |
|  | [aws_jams_lab_monitoring](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/aws_jams_lab_monitoring) | Serviço da AWS: lambda | - |
|  | [aws-codestar-service-role](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/aws-codestar-service-role) | Serviço da AWS: codestar | - |
|  | [aws-opsworks-cm-service-role](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/aws-opsworks-cm-service-role) | Serviço da AWS: opsworks-cm | - |
|  | [aws-opsworks-ec2-role](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/aws-opsworks-ec2-role) | Serviço da AWS: ec2 | - |
|  | [AWSCloudFormationStackSetExecutionRole](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSCloudFormationStackSetExecutionRole) | Conta: 693965310126 | - |
|  | [AWSJamAdminAccessRole](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSJamAdminAccessRole) | Conta: 030316276660 | - |
|  | [AWSJamTaskValidationLambdaRole](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSJamTaskValidationLambdaRole) | Serviço da AWS: lambda | - |
|  | [AWSLabs-LabFunction-LabAdmin-v1-BeuZgQuaVhM](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-LabFunction-LabAdmin-v1-BeuZgQuaVhM) | Serviço da AWS: lambda | - |
|  | [AWSLabs-LabFunction-LabAdmin-v2-BqztPLLHXkv](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-LabFunction-LabAdmin-v2-BqztPLLHXkv) | Serviço da AWS: lambda | - |
|  | [AWSLabs-LabFunction-ReadOnly-v1-iFlpBUZaZfE](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-LabFunction-ReadOnly-v1-iFlpBUZaZfE) | Serviço da AWS: lambda | - |
|  | [AWSLabs-LabFunction-ReadOnly-v2-mADAxiuxnnT](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-LabFunction-ReadOnly-v2-mADAxiuxnnT) | Serviço da AWS: lambda | - |
|  | [AWSLabs-Provisioner-v1-DwAEAwsNCww](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-Provisioner-v1-DwAEAwsNCww) | Conta: 684652433853 | - |
|  | [AWSLabs-Provisioner-v2-CjDTNtCaQDT](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-Provisioner-v2-CjDTNtCaQDT) | Conta: 684652433853 | - |
|  | [AWSLabs-Reaper-v1-BggBBwMBCww](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-Reaper-v1-BggBBwMBCww) | Conta: 230749523606, [e mais 1.](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-Reaper-v1-BggBBwMBCww?section=trust_relationships) | - |
|  | [AWSLabs-Reaper-v2-DhoSFxRTulp](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-Reaper-v2-DhoSFxRTulp) | Serviço da AWS: global.prod.reaper.bunsen.aws.internal, [e mais 1.](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-Reaper-v2-DhoSFxRTulp?section=trust_relationships) | - |
|  | [AWSLabs-Teardown-v1-CwMNCwEMAAg](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-Teardown-v1-CwMNCwEMAAg) | Conta: 684652433853 | - |
|  | [AWSLabs-Teardown-v2-TcRIkjDpIdp](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabs-Teardown-v2-TcRIkjDpIdp) | Conta: 684652433853 | - |
|  | [AWSLabsController](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabsController) | Serviço da AWS: prod.accountsmanager.bunsen.aws.internal, [e mais 1.](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabsController?section=trust_relationships) | - |
|  | [AWSLabsServiceRole](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabsServiceRole) | Conta: 693965310126 | - |
|  | [AWSLabsUser-dKKhdkkSjAWNgduZ6T66cg](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/details/AWSLabsUser-dKKhdkkSjAWNgduZ6T66cg) | Conta: 684652433853 | - |

{
"Version": "2012-10-17",
"Statement": [
{
"Action": [
"kms:GenerateDataKey",
"kms:Decrypt",
"kms:Encrypt",
"kms:DescribeKey",
"kms:ReEncrypt*"
],
"Resource": "arn:aws:kms:us-east-1:294028244101:key/30311398-bbbf-49d2-b5ca-9ef1dedf0e83",
"Effect": "Allow"
}
]
}