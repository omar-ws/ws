# JAM Chega de criar cliques, por favor!

diferenca

![image.png](image%2042.png)

nao consegui terminar

```bash
Visão geral
Uma equipe de desenvolvimento da AnyCompany está criando recursos por meio do AWS Management Console, mas o CTO recentemente pediu que a equipe começasse a usar a infraestrutura como código, mais especificamente o serviço AWS CloudFormation. À medida que a equipe de desenvolvimento está aprendendo sobre o serviço AWS CloudFormation, eles começam com uma arquitetura simples que usa um tópico do Amazon SNS que deveria invocar uma função do AWS Lambda, algo que eles criaram várias vezes no console. Enquanto isso, uma equipe de DevOps configurou um pipeline usando o serviço AWS CodePipeline para garantir uma implantação segura. No entanto, a equipe de desenvolvimento não consegue executar o pipeline com sucesso. Você pode ajudá-los a solucionar o problema como consultor de nuvem experiente?

Arquitetura
! arquitetura

Leia menos
```

```bash
Propriedades de saída
JamChallengeCodeCommitRepoName
jam-repo-e7848140-7aeb-11f1-bb5b-0affed5920e3

JamChallengeCodePipelineName
Jam-Pipeline-e7848140-7aeb-11f1-bb5b-0affed5920e3

JamChallengeLambdaExecutionRoleName
LabStack-prewarm-f9bc8c49-33-JamLambdaExecutionRole-gRWhl76b4wvd

JamChallengeLambdaFunctionName
Jam-Function-04078bf0-7aec-11f1-8850-0affee47f7cd

Chega de criar cliques, por favor!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Redefinir ambiente de laboratório
Propriedades de saída
JamChallengeCodeCommitRepoName
jam-repo-e7848140-7aeb-11f1-bb5b-0affed5920e3

JamChallengeCodePipelineName
Jam-Pipeline-e7848140-7aeb-11f1-bb5b-0affed5920e3

JamChallengeLambdaExecutionRoleName
LabStack-prewarm-f9bc8c49-33-JamLambdaExecutionRole-gRWhl76b4wvd

JamChallengeLambdaFunctionName
Jam-Function-04078bf0-7aec-11f1-8850-0affee47f7cd

JamChallengeSnsTopicName
Jam-SNS-Topic-04078bf0-7aec-11f1-8850-0affee47f7cd

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Adicionar permissão do Lambda
Pontos possíveis
53
Penalidade por pista
11
Pontos disponíveis
0

Tarefas e pistas
Antecedentes:
Carlos, da equipe de desenvolvimento, explica que foi muito fácil para a equipe adicionar gatilhos às funções do Lambda no Management Console. Eles simplesmente acessariam o serviço Lambda, escolheriam uma função, clicariam em Adicionar acionador, selecionariam SNS (ou outro serviço) como origem em Configuração do acionador e escolheriam um tópico do SNS no menu suspenso.

Com base nessa experiência, a equipe escreveu e implantou um modelo do CloudFormation que definiu uma função do Lambda e um tópico do SNS, adicionando a função do Lambda ao tópico do SNS como um endpoint. Para sua surpresa, no entanto, publicar uma mensagem no tópico não é invocar a função Lambda. Eles claramente estão faltando alguma coisa no modelo. Além disso, a equipe de DevOps configurou um pipeline usando o AWS CodePipeline que valida o modelo. Portanto, a menos que a equipe de desenvolvimento adicione um recurso adequado, o pipeline falhará e não implantará o modelo atualizado.

Sua tarefa:
Você pode ajudar Carlos e a equipe a descobrir qual recurso está faltando no modelo? O modelo é armazenado em um repositório CodeCommit. Faça a atualização do modelo no repositório do CodeCommit diretamente pelo console do CodeCommit.

Inventário:
(Observação: consulte as Propriedades de saída para obter os nomes dos recursos abaixo)

Tópico do SNS
Função lambda
Repositório CodeCommit
Pipeline do CodePipeline
Serviços que você deve usar:
Amazon SNS
AWS Lambda
AWS CodeCommit
AWS CodePipeline
Validação de tarefas:
A tarefa será marcada como concluída quando oVerificationAction1 no LambdaVerificationStage do pipeline for bem-sucedida. O pipeline é iniciado automaticamente quando uma atualização é detectada no repositório CodeCommit. Se necessário, você pode executar manualmente o pipeline clicando no botãoLiberar alteração.

Referências:
Edite um arquivo usando o console do CodeCommit: https://docs.aws.amazon.com/codecommit/latest/userguide/how-to-edit-file.html#how-to-edit-file-console
Conceda acesso às funções e camadas do Lambda: https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html
Referência da função intrínseca do CloudFormation: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html
Seção de recursos no modelo do CloudFormation: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resources-section-structure.html
Pistas
Política baseada em recursos do Lambda
5Pontos de penalidade
Ocultar pista
Você pode usar políticas baseadas em recursos para conceder permissões a outras contas e serviços da AWS para acessar seus recursos do Lambda. Como você adiciona uma política baseada em recursos para uma função do Lambda em um modelo do CloudFormation?

Passo a passo completo
6Pontos de penalidade
Ocultar pista
Navegue até o console do CodeCommit e selecione o repositório cujo nome começa com jam-repo-, seguido por um UUID (por exemplo, jam-repo-60a13d10-46fb-11ef-8dac-0e76f521cad7).

Clique no arquivo denominadoincomplete_template.json.

Clique no botãoEditar.

Substitua todo o conteúdo do arquivo pelo seguinte:

{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "Creates a Lambda function and an SNS topic",
    "Resources": {
        "JamSnsTopic": {
            "Type": "AWS::SNS::Topic",
            "Properties": {
                "TopicName": {
                    "Fn::Sub": [
                        "Jam-SNS-Topic-${UUID}",
                        {
                            "UUID": {
                                "Fn::Select": [
                                    2,
                                    {
                                        "Fn::Split": [
                                            "/",
                                            {
                                                "Ref": "AWS::StackId"
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                },
                "DisplayName": "Jam SNS Topic",
                "Subscription": [
                    {
                        "Endpoint": {
                            "Fn::GetAtt": [
                                "JamLambdaFunction",
                                "Arn"
                            ]
                        },
                        "Protocol": "lambda"
                    }
                ]
            }
        },
        "JamLambdaFunctionLayer": {
            "Type": "AWS::Lambda::LayerVersion",
            "Properties": {
                "CompatibleRuntimes": [
                    "python3.11"
                ],
                "Content": {
                    "S3Bucket": {
                        "Fn::Sub": "aws-jam-challenge-resources-${AWS::Region}"
                    },
                    "S3Key": "click-building-to-iac/jam_layer.zip"
                }
            }
        },
        "JamLambdaFunctionLogGroup": {
            "DeletionPolicy": "Delete",
            "UpdateReplacePolicy": "Delete",
            "Type": "AWS::Logs::LogGroup",
            "Properties": {
                "LogGroupName": {
                    "Fn::Sub": [
                        "/aws/lambda/Jam-Function-${UUID}",
                        {
                            "UUID": {
                                "Fn::Select": [
                                    2,
                                    {
                                        "Fn::Split": [
                                            "/",
                                            {
                                                "Ref": "AWS::StackId"
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                },
                "RetentionInDays": 3
            }
        },
        "JamLambdaFunction": {
            "Type": "AWS::Lambda::Function",
            "DependsOn": "JamLambdaFunctionLogGroup",
            "Properties": {
                "FunctionName": {
                    "Fn::Sub": [
                        "Jam-Function-${UUID}",
                        {
                            "UUID": {
                                "Fn::Select": [
                                    2,
                                    {
                                        "Fn::Split": [
                                            "/",
                                            {
                                                "Ref": "AWS::StackId"
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                },
                "Description": "Jam Lambda Function",
                "Runtime": "python3.11",
                "Handler": "index.lambda_handler",
                "MemorySize": 256,
                "ReservedConcurrentExecutions": 1,
                "Layers": [
                    {
                        "Ref": "JamLambdaFunctionLayer"
                    }
                ],
                "Role": {
                    "Fn::GetAtt": [
                        "JamLambdaExecutionRole",
                        "Arn"
                    ]
                },
                "Timeout": 30,
                "Code": {
                    "ZipFile": "import jam\n\ndef lambda_handler(event, context):\n    jam.give_me_answer()\n"
                }
            }
        },

        "JamLambdaPermissionForSnsTopic": {
            "Type": "AWS::Lambda::Permission",
            "Properties": {
                "FunctionName": {
                    "Ref": "JamLambdaFunction"
                },
                "Principal": "sns.amazonaws.com",
                "Action": "lambda:InvokeFunction",
                "SourceArn": {
                    "Ref": "JamSnsTopic"
                }
            }
        },

        "JamLambdaExecutionRole": {
            "Type": "AWS::IAM::Role",
            "Properties": {
                "Description": "Lambda Execution Role",
                "Tags": [
                    {
                        "Key": "Event",
                        "Value": "JAM"
                    }
                ],
                "AssumeRolePolicyDocument": {
                    "Version": "2012-10-17",
                    "Statement": [
                        {
                            "Effect": "Allow",
                            "Principal": {
                                "Service": "lambda.amazonaws.com"
                            },
                            "Action": "sts:AssumeRole",
                            "Condition": {
                                "StringEquals": {
                                    "aws:SourceAccount": {
                                        "Ref": "AWS::AccountId"
                                    }
                                }
                            }
                        }
                    ]
                }

            }
        }
    },
    "Outputs": {
        "JamSnsTopicName": {
            "Description": "The name of the Jam SNS topic",
            "Value": {
                "Fn::GetAtt": [
                    "JamSnsTopic",
                    "TopicName"
                ]
            }
        },
        "JamLambdaFunctionName": {
            "Description": "The name of the Jam Lambda function",
            "Value": {
                "Ref": "JamLambdaFunction"
            }
        },
        "JamLambdaExecutionRoleName": {
            "Description": "The name of the Jam Lambda execution role",
            "Value": {
                "Ref": "JamLambdaExecutionRole"
            }
        },
        "JamStackName": {
            "Description": "The name of the Jam stack",
            "Value": {
                "Ref": "AWS::StackName"
            }
        }
    }
}
Forneça o nome do autor e o endereço de e-mail e clique no botãoConfirmar alterações.

Navegue até o console do CodePipeline e selecione o pipeline cujo nome começa com Jam-Pipeline-, seguido por um UUID (por exemplo, JAM-Pipeline-60A13D10-46FB-11EF-8DAC-0E76F521CAD7).

Assista ao funcionamento do oleoduto. O segundo estágio (LambdaVerificationStage) tem duas ações definidas. Quando oVerificationAction1 for bem-sucedida, a tarefa será concluída.

Chega de criar cliques, por favor!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Redefinir ambiente de laboratório
Propriedades de saída
JamChallengeCodeCommitRepoName
jam-repo-e7848140-7aeb-11f1-bb5b-0affed5920e3

JamChallengeCodePipelineName
Jam-Pipeline-e7848140-7aeb-11f1-bb5b-0affed5920e3

JamChallengeLambdaExecutionRoleName
LabStack-prewarm-f9bc8c49-33-JamLambdaExecutionRole-gRWhl76b4wvd

JamChallengeLambdaFunctionName
Jam-Function-04078bf0-7aec-11f1-8850-0affee47f7cd

JamChallengeSnsTopicName
Jam-SNS-Topic-04078bf0-7aec-11f1-8850-0affee47f7cd

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Permissão ausente na função de execução do Lambda
Pontos possíveis
45
Penalidade por pista
9
Pontos disponíveis
0

Tarefas e pistas
Antecedentes:
Ótimo trabalho ao concluir a Tarefa 1!

Carlos, no entanto, percebe que a açãoverificationAction2 no pipeline ainda está falhando. Ele pede sua ajuda novamente, para ver o que mais pode estar errado ou faltando no modelo.

Sua tarefa:
Parece que a função de execução da função Lambda não pode fazer upload de registros para o CloudWatch Logs. Você pode ajudar Carlos e a equipe a adicionar as permissões ausentes usando uma política gerenciada pela AWS? Use o mesmo modelo armazenado em um repositório CodeCommit. Faça a atualização do modelo no repositório do CodeCommit diretamente pelo console do CodeCommit. Algumas linhas de espaços em branco são fornecidas no modelo sob o nome do recurso lógico de JamLambdaExecutionRole.

Inventário:
(Observação: consulte as Propriedades de saída para obter os nomes dos recursos abaixo)

Tópico do SNS
Função lambda
Repositório CodeCommit
Pipeline do CodePipeline
Serviços que você deve usar:
Amazon SNS
AWS Lambda
AWS CodeCommit
AWS CodePipeline
Validação de tarefas:
A tarefa será marcada como concluída quando oVerificationAction2 no LambdaVerificationStage do pipeline for bem-sucedido. O pipeline é iniciado automaticamente quando uma atualização é detectada no repositório CodeCommit. Se necessário, você pode executar manualmente o pipeline clicando no botãoLiberar alteração.

Referências:
Edite um arquivo usando o console do CodeCommit: https://docs.aws.amazon.com/codecommit/latest/userguide/how-to-edit-file.html#how-to-edit-file-console
Acesso ao CloudWatch Logs: https://docs.aws.amazon.com/lambda/latest/operatorguide/access-logs.html
Políticas gerenciadas pela AWS para o AWS Lambda: https://docs.aws.amazon.com/lambda/latest/dg/security-iam-awsmanpol.html
AWS: :IAM: :Role: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html
Referência da função intrínseca do CloudFormation: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html
Pistas
Use o ManagedPolicyArns
4Pontos de penalidade
Ocultar pista
Como você adiciona uma política gerenciada a uma função em um modelo do CloudFormation?

Passo a passo completo
5Pontos de penalidade
Ocultar pista
Navegue até o console do CodeCommit e selecione o repositório cujo nome começa com jam-repo-, seguido por um UUID (por exemplo, jam-repo-60a13d10-46fb-11ef-8dac-0e76f521cad7).

Clique no arquivo denominadoincomplete_template.json.

Clique no botãoEditar.

Substitua todo o conteúdo do arquivo pelo seguinte:

{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "Creates a Lambda function and an SNS topic",
    "Resources": {
        "JamSnsTopic": {
            "Type": "AWS::SNS::Topic",
            "Properties": {
                "TopicName": {
                    "Fn::Sub": [
                        "Jam-SNS-Topic-${UUID}",
                        {
                            "UUID": {
                                "Fn::Select": [
                                    2,
                                    {
                                        "Fn::Split": [
                                            "/",
                                            {
                                                "Ref": "AWS::StackId"
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                },
                "DisplayName": "Jam SNS Topic",
                "Subscription": [
                    {
                        "Endpoint": {
                            "Fn::GetAtt": [
                                "JamLambdaFunction",
                                "Arn"
                            ]
                        },
                        "Protocol": "lambda"
                    }
                ]
            }
        },
        "JamLambdaFunctionLayer": {
            "Type": "AWS::Lambda::LayerVersion",
            "Properties": {
                "CompatibleRuntimes": [
                    "python3.11"
                ],
                "Content": {
                    "S3Bucket": {
                        "Fn::Sub": "aws-jam-challenge-resources-${AWS::Region}"
                    },
                    "S3Key": "click-building-to-iac/jam_layer.zip"
                }
            }
        },
        "JamLambdaFunctionLogGroup": {
            "DeletionPolicy": "Delete",
            "UpdateReplacePolicy": "Delete",
            "Type": "AWS::Logs::LogGroup",
            "Properties": {
                "LogGroupName": {
                    "Fn::Sub": [
                        "/aws/lambda/Jam-Function-${UUID}",
                        {
                            "UUID": {
                                "Fn::Select": [
                                    2,
                                    {
                                        "Fn::Split": [
                                            "/",
                                            {
                                                "Ref": "AWS::StackId"
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                },
                "RetentionInDays": 3
            }
        },
        "JamLambdaFunction": {
            "Type": "AWS::Lambda::Function",
            "DependsOn": "JamLambdaFunctionLogGroup",
            "Properties": {
                "FunctionName": {
                    "Fn::Sub": [
                        "Jam-Function-${UUID}",
                        {
                            "UUID": {
                                "Fn::Select": [
                                    2,
                                    {
                                        "Fn::Split": [
                                            "/",
                                            {
                                                "Ref": "AWS::StackId"
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                },
                "Description": "Jam Lambda Function",
                "Runtime": "python3.11",
                "Handler": "index.lambda_handler",
                "MemorySize": 256,
                "ReservedConcurrentExecutions": 1,
                "Layers": [
                    {
                        "Ref": "JamLambdaFunctionLayer"
                    }
                ],
                "Role": {
                    "Fn::GetAtt": [
                        "JamLambdaExecutionRole",
                        "Arn"
                    ]
                },
                "Timeout": 30,
                "Code": {
                    "ZipFile": "import jam\n\ndef lambda_handler(event, context):\n    jam.give_me_answer()\n"
                }
            }
        },

        "JamLambdaPermissionForSnsTopic": {
            "Type": "AWS::Lambda::Permission",
            "Properties": {
                "FunctionName": {
                    "Ref": "JamLambdaFunction"
                },
                "Principal": "sns.amazonaws.com",
                "Action": "lambda:InvokeFunction",
                "SourceArn": {
                    "Ref": "JamSnsTopic"
                }
            }
        },

        "JamLambdaExecutionRole": {
            "Type": "AWS::IAM::Role",
            "Properties": {
                "Description": "Lambda Execution Role",
                "Tags": [
                    {
                        "Key": "Event",
                        "Value": "JAM"
                    }
                ],
                "AssumeRolePolicyDocument": {
                    "Version": "2012-10-17",
                    "Statement": [
                        {
                            "Effect": "Allow",
                            "Principal": {
                                "Service": "lambda.amazonaws.com"
                            },
                            "Action": "sts:AssumeRole",
                            "Condition": {
                                "StringEquals": {
                                    "aws:SourceAccount": {
                                        "Ref": "AWS::AccountId"
                                    }
                                }
                            }
                        }
                    ]
                },
                "ManagedPolicyArns": [
                    {
                        "Fn::Sub": "arn:${AWS::Partition}:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole"
                    }
                ]
            }
        }
    },
    "Outputs": {
        "JamSnsTopicName": {
            "Description": "The name of the Jam SNS topic",
            "Value": {
                "Fn::GetAtt": [
                    "JamSnsTopic",
                    "TopicName"
                ]
            }
        },
        "JamLambdaFunctionName": {
            "Description": "The name of the Jam Lambda function",
            "Value": {
                "Ref": "JamLambdaFunction"
            }
        },
        "JamLambdaExecutionRoleName": {
            "Description": "The name of the Jam Lambda execution role",
            "Value": {
                "Ref": "JamLambdaExecutionRole"
            }
        },
        "JamStackName": {
            "Description": "The name of the Jam stack",
            "Value": {
                "Ref": "AWS::StackName"
            }
        }
    }
}
Forneça o nome do autor e o endereço de e-mail e clique no botãoConfirmar alterações.

Navegue até o console do CodePipeline e selecione o pipeline cujo nome começa com Jam-Pipeline-, seguido por um UUID (por exemplo, JAM-Pipeline-60A13D10-46FB-11EF-8DAC-0E76F521CAD7).

Assista ao funcionamento do oleoduto. O segundo estágio (LambdaVerificationStage) tem duas ações definidas. Quando oVerificationAction2 for bem-sucedida, a tarefa será concluída.
```

```bash
Tarefa 3: Pegue o hash secreto!
Pontos possíveis
52
Penalidade por pista
0
Pontos disponíveis
52
Verifique meu progresso

Tarefas e pistas
Enviar resposta
Antecedentes:
Ótimo trabalho ao concluir a Tarefa 2!

Até agora, o pipeline deveria ter passado por todos os estágios e o modelo atualizado do CloudFormation deveria ter sido implantado. Isso significa que o serviço Amazon SNS pode invocar a função Lambda quando uma mensagem é publicada no tópico SNS, e a função Lambda tem permissões para fazer login no grupo de logs do CloudWatch Logs associado à função. Vamos testá-lo para ter certeza de que funciona conforme o esperado.

Sua tarefa:
Publique uma mensagem no tópico do SNS para recuperar a resposta dessa tarefa.

Inventário:
(Observação: consulte as Propriedades de saída para obter os nomes dos recursos abaixo)

Tópico do SNS
Função lambda
Repositório CodeCommit
Pipeline do CodePipeline
Serviços que você deve usar:
Amazon SNS
AWS Lambda
Logs do Amazon CloudWatch
AWS CodeCommit
AWS CodePipeline
Validação de tarefas:
A tarefa será marcada como concluída se a resposta corresponder ao valor esperado.

Referências:
Publique mensagens nos tópicos do Amazon SNS no console: https://docs.aws.amazon.com/sns/latest/dg/sns-publishing.html#sns-publishing-messages
Veja os registros de funções do Amazon CloudWatch Lambda: https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs-view.html
Pistas
Você verificou os registros?
5Pontos de penalidade

```

a