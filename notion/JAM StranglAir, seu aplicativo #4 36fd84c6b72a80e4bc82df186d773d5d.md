# JAM StranglAir, seu aplicativo #4

> Você é arquiteto sênior de nuvem na Paws & Whiskers, uma adorada empresa de adoção de animais de estimação que conecta famílias com amigos peludos há mais de uma década. A empresa começou como um pequeno abrigo local, mas se transformou em uma rede regional com milhares de adoções bem-sucedidas. Seu site baseado em Java serviu bem a você, mas as expectativas dos clientes evoluíram: eles querem interações inteligentes e conversacionais ao procurar o companheiro perfeito para animais de estimação.…
> 

task 1:  sinto que nao entendi nada que lia:

```jsx
ApplicationURL
http://pawsandwhiskers-alb-1091147746.us-east-1.elb.amazonaws.com/pawsandwhiskers/

InstanceId
i-04808221c88927862

LambdaFunctionName
pawsandwhiskers-bedrock-chatbot

LambdaFunctionURL
https://brlhw33k27bisr7whuih42tfh40eqtte.lambda-url.us-east-1.on.aws/

Tarefa 1: Habilitar a configuração do modelo de IA
Pontos possíveis
20
Penalidade por pista
0
Pontos disponíveis
20
Verifique meu progresso

Tarefas e pistas
Antecedentes
Sua equipe de desenvolvimento implementou com sucesso a infraestrutura padrão Strangler Fig para permitir uma integração perfeita de IA sem interromper os serviços existentes. Eles implantaram uma nova função do Lambda junto com o chatbot legado baseado em regras, criaram os mecanismos de roteamento necessários no servidor de aplicativos e estabeleceram todos os recursos necessários da AWS. No entanto, para concluir a implementação do Strangler Fig e garantir zero interrupção nas operações atuais, o componente de serviço de IA precisa de configuração final. Atualmente, a função Lambda tem um valor reservado para o ID do modelo Bedrock que impede que ela se conecte ao modelo Nova Lite da Amazon Bedrock. Como arquiteto de nuvem, você precisa configurar o identificador de modelo adequado para ativar o recurso de IA e, ao mesmo tempo, manter a confiabilidade do sistema existente. Essa configuração permitirá que o padrão Strangler Fig roteie o tráfego entre serviços legados e de IA com base nas configurações do aplicativo, garantindo que os clientes não tenham nenhuma interrupção do serviço durante o processo de modernização.

Sua tarefa
Configure a variável de ambiente da função Lambda para usar o modelo Nova Lite da Amazon Bedrock. A função precisa do ID de modelo correto para estabelecer comunicação com o serviço Bedrock e processar consultas de linguagem natural dos clientes.

Inventário
Função Lambda: pawsandwhiskers-bedrock-chatbot
Tabela do DynamoDB com metadados de animais de estimação
O Application Load Balancer roteia o tráfego para a instância EC2
Serviços que você deve usar
AWS Lambda
Base da Amazônia
Validação de tarefas
A tarefa será concluída automaticamente quando você configurar o ID correto do modelo Bedrock. Você pode verificar seu progresso usando o botão “Verificar meu progresso”.

Pistas
Pistas 1
2Pontos de penalidade
Desbloqueie o Clue
Pistas 2
2Pontos de penalidade
Desbloqueie o Clue
```

duvidas durante a task:

o que sao variavel de ambiente?

o que e o badrock model

entender tudo do lambda

o que eu deveria colocar bno backrock model ID? como vejo isso?

eu coloquei o id da instancia, tinha aberto o amazon badrock mas nao achei anda e percebi por que deixariam um id da isntancia se teoricamente nao falaram nada? coloquei ent

nao era isso

estava no servico errado

o que e amazon badrock?

o que e strangle fig

eu nao cheguei a conclusao sozinho

mas entrei nos servicos que o jam falou fui em catalogo de modelos e achei o modelo que ele queria que e o amazon nova lite

o site ainda nao funcionou mas consegui completar o desafio, o modelo funcionou e era:

```jsx
amazon.nova-lite-v1:0
```

task 2:

```jsx
ApplicationURL
http://pawsandwhiskers-alb-1091147746.us-east-1.elb.amazonaws.com/pawsandwhiskers/

InstanceId
i-04808221c88927862

LambdaFunctionName
pawsandwhiskers-bedrock-chatbot

LambdaFunctionURL
https://brlhw33k27bisr7whuih42tfh40eqtte.lambda-url.us-east-1.on.aws/

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Atualizar a configuração do servidor de aplicativos
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
40
Verifique meu progresso

Tarefas e pistas
Antecedentes
O servidor de aplicativos Tomcat está atualmente configurado para usar o sistema de chatbot baseado em regras legado. Para implementar o padrão Strangler Fig, você precisa atualizar a configuração do servidor para rotear as solicitações do chatbot para a nova função Lambda alimentada por IA, em vez do sistema legado. Essa alteração redirecionará as consultas dos usuários para o Amazon Bedrock, mantendo o restante do aplicativo inalterado.

Sua tarefa
Conecte-se à instância do EC2 e modifique a configuração do Tomcat para alternar do modo legado para o modo Bedrock. Você precisará atualizar o arquivo de configuração do ambiente e reiniciar o serviço Tomcat para aplicar as alterações.

Como começar
Use o AWS Systems Manager Session Manager para se conectar à instância do EC2. O arquivo de configuração está localizado em /opt/tomcat/bin/setenv.sh e contém a variável CHATBOT_MODE que controla o comportamento do roteamento.

Inventário
Instância EC2 executando o servidor de aplicativos Tomcat
Gerenciador de sessões do Systems Manager para acesso seguro
Arquivos de configuração do serviço Tomcat
Serviços que você deve usar
Amazon EC2
AWS Systems Manager (gerenciador de sessões)
Validação de tarefas
A tarefa será concluída automaticamente quando a configuração do Tomcat for atualizada e o serviço for reiniciado com as novas configurações.

Pistas
Pistas 1
4Pontos de penalidade
Desbloqueie o Clue
Pistas 2
5Pontos de penalidade

```

essa acessei logo ssm entrei no terminal dei um nano na pasta e troquei, vou mandar o que digitei no terminal

treinar sair do nano 

control o e control enter

nao funcionou deu unritable

tinha que ter entrado com sudo, saber quando usar sudo

eu achei que daria um reboot, mas nao dei e funcionou

estudar mais sobre

dei sudo su e com o nano, e deu certo

primeiro coloquei a variavel do lambda segundo tirei do codigo legado

task 3:

```jsx
ApplicationURL
http://pawsandwhiskers-alb-1091147746.us-east-1.elb.amazonaws.com/pawsandwhiskers/

InstanceId
i-04808221c88927862

LambdaFunctionName
pawsandwhiskers-bedrock-chatbot

LambdaFunctionURL
https://brlhw33k27bisr7whuih42tfh40eqtte.lambda-url.us-east-1.on.aws/

Tarefa 3: Valide a integração do AI Chatbot
Pontos possíveis
20
Penalidade por pista
0
Pontos disponíveis
20
Verifique meu progresso

Tarefas e pistas
Antecedentes
Com a função do Lambda e o servidor de aplicativos configurados corretamente, é hora de testar a integração completa da IA. O padrão Strangler Fig permite que você verifique se o novo chatbot alimentado por IA funciona corretamente, mantendo a estrutura do aplicativo existente. As consultas dos clientes agora devem receber respostas inteligentes e personalizadas com base no banco de dados de animais de estimação.

Sua tarefa
Acesse o site Paws & Whiskers e teste a funcionalidade do chatbot com uma consulta em linguagem natural sobre adoção de animais de estimação. Verifique se o sistema responde com recomendações geradas pela IA em vez de respostas genéricas baseadas em regras.

Como começar
Navegue até a URL do aplicativo fornecida nas saídas do desafio. Use a interface do chatbot para fazer uma pergunta como “Estou procurando um cachorro amigável que seja bom com crianças” e observe a qualidade e a personalização da resposta.

Inventário
Aplicativo web acessível por meio do Application Load Balancer
Interface de chatbot com tecnologia de IA
Banco de dados de animais de estimação com metadados para recomendações
Serviços que você deve usar
Balanceador de carga de aplicativos
AWS Lambda (indiretamente por meio da interface da web)
Amazon Bedrock (indiretamente por meio do Lambda)
Validação de tarefas
Acesse o aplicativo usando o 'applicationUrl' em Output Properties. A tarefa será concluída automaticamente quando o chatbot de IA processar com sucesso uma consulta e retornar recomendações personalizadas de animais de estimação usando o Amazon Bedrock.

Pistas
Pistas 1
2Pontos de penalidade
Desbloqueie o Clue
Pistas 2
2Pontos de penalidade
Desbloqueie o Clue
```

nao funcionou e teoricamente nao pediu para fazer nada, por que Deu erro?

deu um erro na task 4, nao consegui testar por completo

falei para o professor, achei que tinha que ir em ingles, mas tambem nao foi, vou ir para a task 3 novamente, ele mandou eu fazer

so deixando claro uma duvida, nas variaveis de ambiente do lambda:

```jsx
Código
Testar
Monitor
Configuração
Aliases
Versões
Configuração
Configuração geral
Gatilhos
Permissões
Destinos
URL da função
Variáveis de ambiente
Tags
VPC
Bancos de dados do RDS
Ferramentas de monitoramento e operações
Detecção de recursão e simultaneidade
Invocação assíncrona
Assinatura de código
Sistemas de arquivos
Máquinas de estado
Variáveis de ambiente (2)
Editar
As variáveis de ambiente a seguir são criptografadas em repouso com a chave de serviço padrão do Lambda.

Chave
Valor
BEDROCK_MODEL_ID
amazon.nova-lite-v1:0
DYNAMODB_TABLE
pawsandwhiskers-pet-table

```

por que tem uma variavel de ambiente do dynamodb? a ia deveria mostrar imagens?

codigo do lambda:

```jsx
import json, boto3, logging, os
from typing import Dict, List, Any
from decimal import Decimal

logger = logging.getLogger()
logger.setLevel(logging.INFO)

# Use current Lambda region for all AWS clients
current_region = os.environ.get('AWS_REGION')
bedrock_runtime = boto3.client('bedrock-runtime', region_name=current_region)
dynamodb = boto3.resource('dynamodb', region_name=current_region)

BEDROCK_MODEL_ID = os.environ.get('BEDROCK_MODEL_ID', 'us.amazon.nova-lite-v1:0')
DYNAMODB_TABLE_NAME = os.environ.get('DYNAMODB_TABLE', 'PetMetadata')

def lambda_handler(event, context):
    try:
        logger.info(f"Chatbot request received - Request ID: {context.aws_request_id}")
        logger.info(f"Current BEDROCK_MODEL_ID: {BEDROCK_MODEL_ID}")
        
        if BEDROCK_MODEL_ID == 'PLACEHOLDER_MODEL_ID_NEEDS_CONFIGURATION':
            logger.warning("Lambda function not configured - placeholder model ID detected")
            return {
                'statusCode': 500,
                'headers': {
                    'Content-Type': 'application/json', 
                    'Access-Control-Allow-Origin': '*',
                    'Access-Control-Allow-Methods': 'POST, OPTIONS',
                    'Access-Control-Allow-Headers': 'Content-Type'
                },
                'body': json.dumps({
                    'response': "🚨 CONFIGURATION REQUIRED: Please set BEDROCK_MODEL_ID environment variable.",
                    'error': True, 'mode': 'bedrock', 'configurationRequired': True
                })
            }
        
        # Handle CORS preflight
        if event.get('requestContext', {}).get('http', {}).get('method') == 'OPTIONS':
            logger.info("Handling CORS preflight request")
            return {
                'statusCode': 200,
                'headers': {
                    'Access-Control-Allow-Origin': '*',
                    'Access-Control-Allow-Methods': 'POST, OPTIONS',
                    'Access-Control-Allow-Headers': 'Content-Type'
                }
            }
        
        body = json.loads(event['body']) if isinstance(event.get('body'), str) else event
        message = body.get('message', '')
        session_id = body.get('sessionId', 'default')
        
        logger.info(f"Processing message: '{message}' for session: {session_id}")
        
        response_text = process_chat_query(message, session_id)
        
        final_response = {
            'statusCode': 200,
            'headers': {
                'Content-Type': 'application/json', 
                'Access-Control-Allow-Origin': '*',
                'Access-Control-Allow-Methods': 'POST, OPTIONS',
                'Access-Control-Allow-Headers': 'Content-Type'
            },
            'body': json.dumps({'response': response_text, 'sessionId': session_id, 'mode': 'bedrock'})
        }
        
        logger.info(f"Returning successful response with mode: bedrock")
        logger.info(f"Final response body: {final_response['body']}")
        
        return final_response
        
    except Exception as e:
        logger.error(f"Lambda function error: {str(e)}")
        logger.error(f"Error type: {type(e).__name__}")
        
        error_response = {
            'statusCode': 500,
            'headers': {
                'Content-Type': 'application/json', 
                'Access-Control-Allow-Origin': '*',
                'Access-Control-Allow-Methods': 'POST, OPTIONS',
                'Access-Control-Allow-Headers': 'Content-Type'
            },
            'body': json.dumps({'response': "Sorry, please try again later.", 'error': True, 'mode': 'bedrock'})
        }
        
        logger.info(f"Returning error response: {error_response['body']}")
        return error_response

def process_chat_query(message: str, session_id: str) -> str:
    try:
        all_pets = get_all_pets_from_dynamodb()
        
        if not all_pets:
            logger.warning("Pet database is empty")
            return "I'm sorry, our pet database seems to be empty. Please try again later."
        
        logger.info(f"Retrieved {len(all_pets)} pets from database")
        response_text = generate_bedrock_response(message, all_pets)
        
        logger.info(f"Bedrock response generated: '{response_text}'")
        logger.info(f"Response length: {len(response_text)} characters")
        
        return response_text
    except Exception as e:
        logger.error(f"Query error: {str(e)}")
        return "I'm sorry, please try again."

def get_all_pets_from_dynamodb() -> List[Dict[str, Any]]:
    try:
        table = dynamodb.Table(DYNAMODB_TABLE_NAME)
        response = table.scan()
        pets = response['Items']
        
        filtered_pets = []
        for pet in pets:
            if pet.get('petType') != 'bunny':
                filtered_pets.append(convert_decimals(pet))
        
        return filtered_pets
    except Exception as e:
        logger.error(f"DynamoDB error: {str(e)}")
        return []

def convert_decimals(obj):
    if isinstance(obj, list):
        return [convert_decimals(item) for item in obj]
    elif isinstance(obj, dict):
        return {key: convert_decimals(value) for key, value in obj.items()}
    elif isinstance(obj, Decimal):
        return float(obj)
    else:
        return obj

def generate_bedrock_response(message: str, all_pets: List[Dict[str, Any]]) -> str:
    try:
        pets_context = json.dumps(all_pets, indent=2)
        
        prompt = f"""Pet adoption assistant. Database: {pets_context}

User: "{message}"

Rules:
- If just "hi/hello": respond "Hi! What pet are you looking for?"
- If mentions "weather/this weather" without specifying: ask "What's your weather like?"
- If clear request (dog, cat, price range, etc.): show 2-3 pets
- Be brief

Response:"""
        
        logger.info(f"Calling Bedrock with model: {BEDROCK_MODEL_ID}")
        logger.info(f"User query: '{message}'")
        
        request_body = {
            "messages": [{"role": "user", "content": [{"text": prompt}]}],
            "inferenceConfig": {"maxTokens": 150, "temperature": 0.7}
        }
        
        response = bedrock_runtime.converse(
            modelId=BEDROCK_MODEL_ID,
            messages=request_body["messages"],
            inferenceConfig=request_body["inferenceConfig"]
        )
        
        bedrock_response = response['output']['message']['content'][0]['text'].strip()
        
        logger.info(f"Bedrock API call successful!")
        logger.info(f"Raw Bedrock response: '{bedrock_response}'")
        
        return bedrock_response
    except Exception as e:
        logger.error(f"Bedrock API error: {str(e)}")
        return "I'm sorry, please try again."

```

o