# JAM Thermal Recall: Pit Stop para IA

```verilog
A frota de veículos elétricos da sua empresa está crescendo — 10.000 veículos hoje, 500.000 até o próximo ano. Cada veículo transmite a telemetria da bateria: temperaturas, deltas de tensão, taxas de carga e resistência interna. Quando esses picos aumentam, ocorre uma fuga térmica — e isso significa fogo.

A liderança quer um AI-powered safety system que monitore a telemetria da bateria em tempo real e intervenha de forma autônoma quando condições perigosas são detectadas. A equipe de engenharia criou um protótipo usando o SDK do Strands Agent e o MCP, mas ele está quebrado e preso em uma única instância do EC2.

**Sua missão: ** Corrigir o pipeline quebrado, equipar o agente com as ferramentas que faltam e implantá-lo no Amazon Bedrock AgentCore, transformando-o de um protótipo frágil em um serviço gerenciado de nível de produção com memória incorporada, observabilidade e capacidade de escalar para milhões de veículos.

Começando
Inventário do Desafio
Amazon VPC e redes
ev-agent-vpc: VPC (10.0.0.0/16)
ev-agent-subnet: Sub-rede (10.0.1.0/24) em AZ1
Amazon EC2 — Servidor de código (código VS no navegador)
ev-agent-codeserver: t3.micro Amazon Linux 2023 executando code-server
Pré-carregado com a base de código do Battery Safety Agent (Strands SDK + MCP + AgentCore)
Acesse via navegador: consulte CodeServerURL e CodeServerPassword em Propriedades de saída
AWS Lambda
ev-battery-safety-agent: função Python 3.12 que classifica a telemetria da bateria como NORMAL, WARN ou CRITICAL e armazena os resultados no DynamoDB/envia alertas de SNS
Amazon DynamoDB
ev-battery-telemetry: armazena o histórico de telemetria do veículo e as decisões do agente (chave de partição: vehicle_id, chave de classificação: timestamp)
Amazon SNS
ev-battery-critical-alerts: tópico para notificações críticas de eventos de bateria
Amazon CloudWatch
EV Battery-HighTemperature: Alarme para monitoramento de temperatura em toda a frota
Funções do AWS IAM
ev-battery-agent-lambda-role: função de execução do Lambda
ev-agent-ec2-role: função de servidor de código EC2 (inclui permissões de IoT, Lambda, DynamoDB, SNS, Bedrock, AgentCore, ECR e CodeBuild)
Acessando o IDE do Code-Server
Encontre CodeServerURL em Propriedades de saída (por exemplo, http://:8080)
Abra no navegador (use http e não https)
Digite a senha de CodeServerPassword
Estrutura do projeto (em servidor de código)
ev-battery-agent/
├── agent/                  # Strands Agent SDK + AgentCore core
│   ├── cli.py             # CLI — Strands Agent with MCP tools
│   ├── core.py            # AgentCore Runtime entry point (ready to deploy)
│   ├── prompts.py         # System prompt
│   └── memory.py          # DynamoDB telemetry history
├── mcp_server/            # MCP server — tools for the Strands agent
│   ├── server.py          # Entry point 
│   └── tools/
│       ├── iot.py         # IoT Core operations
│       ├── battery.py     # Battery telemetry queries
│       ├── sns.py         # SNS tools 
│       └── cloudwatch.py  # CloudWatch metrics
├── lambda_handler/        # Lambda code 
│   └── handler.py
├── run_test.py            # Test script — publishes via IoT Core, queries DynamoDB
└── requirements.txt
**Observação: ** Você pode ver banners de aviso no console da AWS. Isso é esperado devido aos princípios de menor privilégio.

Leia menos
```

```verilog
Tarefa 1: Conecte o sinal
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
O Battery Safety Agent não pode proteger ninguém se nunca receber dados. Os veículos estão transmitindo a telemetria da bateria para o IoT Core, mas não há uma regra para encaminhá-la para a função Lambda — a regra de tópicos da IoT nunca foi criada durante a implantação.

Além disso, a função Lambda não pode enviar alertas do SNS para eventos CRÍTICOS porque uma variável de ambiente crítica está vazia.

Sua tarefa
Crie uma regra de tópico de IoT que escute a telemetria da bateria e invoque o ev-battery-safety-agent Lambda
Veículos publicados em: ev/battery/{vehicle_id}/telemetry
Encontre e corrija a variável de ambiente Lambda ausente que a conecta ao tópico de alerta do SNS
Começando
Explore o console IoT → Roteamento de mensagens → Regras
Você precisa criar uma nova regra com o SQL correto e uma ação do Lambda
Verifique as variáveis de ambiente da função Lambda
O tópico ARN do SNS pode ser encontrado nas saídas da pilha do CloudFormation
Documentação relevante
Referência do AWS IoT SQL
Criação de regras de tópicos de IoT
Variáveis de ambiente Lambda
Inventário
Função Lambda: ev-battery-safety-agent
Tópico do SNS: ev-battery-critical-alerts
Serviços que você deve usar
AWS IoT Core — Crie uma regra de tópico
AWS Lambda — Configurar variáveis de ambiente
Validação de tarefas
Validado por meio da função Lambda:

Existe uma regra de IoT com o padrão de tópico correto direcionado ao Lambda
O Lambda tem ALERT_TOPIC_ARN definido para o ARN correto do tópico SNS
Pistas
O caminho do sinal
6Pontos de penalidade
Desbloqueie o Clue
Passo a passo completo
7Pontos de penalidade
Desbloqueie o Clue

Tarefa 2: Arme o agente
Pontos possíveis
80
Penalidade por pista
18
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
O Battery Safety Agent usa um servidorMCP (Model Context Protocol) ** para interagir com os serviços da AWS. As ferramentas são registradas para IoT, telemetria de baterias e CloudWatch, mas a capacidade de alertaSNS está incompleta**.

Duas coisas estão quebradas:

mcp_server/server.py — A ferramenta SNS não é importada nem registrada
mcp_server/tools/sns.py — O arquivo existe, mas tem somente list_sns_topics. A função crítica da ferramenta send_battery_alert está ausente (marcada com um TODO)
Sem send_battery_alert, o agente não tem como publicar alertas de segurança no SNS ao detectar uma condição CRÍTICA da bateria.

Sua tarefa
Abra o IDE do servidor de código usando a URL e a senha das Propriedades de saída
Adicione a função da ferramenta send_battery_alert em mcp_server/tools/sns.py (siga o TODO)
Registre as ferramentas do SNS em mcp_server/server.py (importe + ligue em create_server())
Começando
Veja como outras ferramentas são estruturadas (por exemplo, mcp_server/tools/iot.py) — cada uma usa o decorador @mcp.tool()
A função send_battery_alert deve publicar no SNS usando boto3
Verifique mcp_server/server.py para ver como outras ferramentas são importadas e registradas
Documentação relevante
Protocolo de contexto do modelo
Registro da ferramenta FastMCP
API de publicação do Amazon SNS
Inventário
IDE de servidor de código: consulte as propriedades de saída para URL e senha
Arquivos para corrigir: mcp_server/tools/sns.py e mcp_server/server.py
Referência: mcp_server/tools/iot.py (para padrão de ferramenta)
Serviços que você deve usar
EC2 (code-server) — Edite o código-fonte no IDE do navegador
Validação de tarefas
Validado por meio da função Lambda (lê arquivos do EC2 via SSM):

sns.py contém a ferramenta send_battery_alert com o decorador @mcp.tool()
server.py importa e registra ferramentas SNS
Pistas
A arma que faltava
8Pontos de penalidade
Mostrar pista
Passo a passo completo
10Pontos de penalidade
Mostrar pista

Tarefa 3: O final!
Pontos possíveis
60
Penalidade por pista
13
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
O pipeline está conectado e o servidor MCP tem todas as suas ferramentas. Dois problemas permanecem:

A classificação Lambda é cega. classify_battery_state verifica apenas temperature — ignorando voltage_delta, charge_rate e resistance. Uma bateria com temperatura normal, mas delta de tensão de 150mV, seria classificada como NORMAL. O ditado THRESHOLDS no código já define todas as quatro métricas.

O agente está preso no EC2. Sem escalabilidade, sem memória, sem observabilidade, sem API. O agent/core.py no servidor de código já está conectado com BedrockAgentCoreApp e memória AgentCore — ele só precisa ser implantado.

Limites
Métrico	NORMAL	AVISAR	CRÍTICO
temperatura	< 45°C	45—60°C	> 60°C
< 50 mV	50—100 mV	>	tensão_delta
< 1.5 C	1.5—2.0 C	>	taxa_de_carga
resistência	< 80 mΩ	80—120 mΩ	> 120 mΩ
Regra: CRÍTICA se ALGUMA métrica exceder a crítica. AVISE se ALGUM exceder o aviso. NORMAL, caso contrário.

Sua tarefa
Parte A: Corrija a classificação Lambda
Abra a função Lambda ev-battery-safety-agent no console
Atualize classify_battery_state para verificar todas as quatro métricas, não apenas a temperatura
Parte B: Implantar no AgentCore
Abra um terminal em code-server (Terminal → Novo terminal) — isso é necessário porque a função EC2 tem as permissões de IAM necessárias
Instale o kit de ferramentas AgentCore CLI e configure o agente
O repositório ECR e as funções de execução serão criados automaticamente pela CLI
Implante e verifique se o tempo de execução atinge o status ATIVO
Parte C: Teste o pipeline completo
Depois que o Lambda for corrigido e o agente implantado, execute o script de teste no terminal do servidor de código:

cd /home/ec2-user/ev-battery-agent
python3.12 run_test.py
O script publica três cenários de teste por meio do IoT Core — isso prova o pipeline completo que você criou:

Publicação da IoT → Regra da IoT (tarefa 1) → Lambda (classificação fixa) → DynamoDB + SNS

O roteiro:

Publica cada carga em ev/battery/{vehicle_id}/telemetry via IoT Core
Espera que a regra de IoT acione o Lambda e grave no DynamoDB
Consulta o DynamoDB e imprime a classificação de cada veículo
Documentação relevante
Edição de código em linha do Lambda
Amazon Bedrock AgentCore
CLI do AgentCore
Cliente de teste IoT MQTT
Inventário
Função Lambda: ev-battery-safety-agent (Parte A)
Referência de código: agent/core.py no servidor de código
Repositório ECR: criado automaticamente pela CLI do agentcore
Ferramenta CLI: agentcore — instale via pip (Parte B)
Script de teste: run_test.py na raiz do projeto code-server (Parte C)
Serviços que você deve usar
AWS Lambda — Corrija a classificação
EC2 (servidor de código) — Execute a CLI do agentcore e o script de teste
Amazon Bedrock AgentCore — Implante o agente
AWS IoT Core — Teste fluxos de dados por meio da regra de IoT
Amazon DynamoDB — Verifique o armazenamento de telemetria
Amazon SNS — O cenário CRÍTICO aciona um alerta
Validação de tarefas
OBRIGATÓRIO: Os dados do teste devem ser publicados executando run_test.py

Execute o comando abaixo no terminal do servidor de código
   agentcore invoke '{"prompt": "Query the DynamoDB ev-battery-telemetry table and tell me the classification for vehicles VH-TEST-ALPHA, VH-TEST-BRAVO, and VH-TEST-CHARLIE. Return only the classification values in order, comma-separated."}'
** (OU) **

Abra o console do AgentCore → Clique em Agent Sandbox em Testar na navegação à esquerda, insira a consulta e execute
Insira as três classificações em ordem (separadas por vírgula) como resposta para cada VH-TEST-ALPHA, VH-TEST-BRAVO, VH-TEST-CHARLIE

Por exemplo, se a resposta do agente fornecer VH-TEST-ALPHA:NORMAL, VH-TEST-BRAVO:CRITICAL, VH-TEST-CHARLIE:WARN

Em seguida, digite a resposta como NORMAL,CRITICAL,WARN (sem espaço)

Mais algumas instruções para jogar com o EV Battery Agent AI:

“prompt”: “você poderia fornecer itens armazenados no dynamodb”
“prompt”: “quais ações você pode realizar para mim?”
“prompt”: “você pode listar todos os tópicos do SNS na conta”
Pistas
O ponto cego
6Pontos de penalidade
Mostrar pista
Passo a passo completo
7Pontos de penalidade
Mostrar pista
```

a