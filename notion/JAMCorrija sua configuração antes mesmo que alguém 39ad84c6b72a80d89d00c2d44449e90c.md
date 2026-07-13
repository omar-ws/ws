# JAMCorrija sua configuração antes mesmo que alguém saiba

```verilog
Visão geral
Você lidera uma equipe de arquitetos de rede. Todos na sua organização têm um desempenho excelente e configuram a rede com os melhores controles em vigor. Um dia, você percebe que algumas contas da AWS têm grupos de segurança abertos para a Internet e pensa “Droga! Eu não esperava isso dos meus artistas famosos.” Você decide implementar a automação para poder detectar precocemente e remediar antes que seja tarde demais

Tarefa 1: Analise o (s) grupo (s) de segurança ofensivo
Pontos possíveis
15
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Contexto
Para verificar se seus security groups expõem seu ambiente do EC2 ao tráfego de entrada da Internet pública, você deve analisar as regras do security group.

Tarefa
Visualize as regras de tráfego de entrada e relate as regras de violação.

**NOTA: Por favor, não remove/atualize a regra de violação por causa das próximas tarefas. **

Começando
Saiba mais sobre as regras do security group neste recurso: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-group-rules.html.

Inventário
Grupos de segurança do Amazon EC2
Grupo Ipv4
Grupo Ipv6
Validação de tarefas
Insira o CIDR de origem da (s) regra (s) violadora (s). Se houver mais de uma violação das regras, separe-as com vírgulas ao fornecer sua resposta.

Exemplo de resposta: “0.0.0.0/32,: :/32"

Tarefa 2: Use o AWS Config para monitorar seus grupos de segurança
Pontos possíveis
75
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Você teve a sorte de detectar essa configuração incorreta a tempo, mas nem sempre estará lá para monitorar seus grupos de segurança. Você quer poder implementar um monitor em seus grupos de segurança para alertar sobre configurações incorretas.

Tarefa
Usando o AWS Config, crie uma regra de configuração chamada “restrict-ec2-ingress” para monitorar seus grupos de segurança do EC2. Essa regra deve considerar um grupo de segurança “não compatível” se as regras de entrada permitirem tráfego de entrada irrestrito. A regra do AWS Config deve ser criada usando as políticas do CloudFormation Guard.

**OBSERVAÇÃO: os modelos de Config CI são diferentes dos modelos do Cloudformation, então você não pode criar sua regra com base na sintaxe do Cloudformation. Visite esta página para entender a sintaxe e a estrutura do Config CI. **

Este é um exemplo de Config CI para um grupo de segurança do EC2:

{
  "version": "1.3",
  "accountId": "...",
  "configurationItemCaptureTime": "...",
  "configurationItemStatus": "ResourceDiscovered",
  "configurationStateId": "1652806735496",
  "configurationItemMD5Hash": "",
  "arn": "...",
  "resourceType": "AWS::EC2::SecurityGroup",
  "resourceId": "...",
  "resourceName": "Ipv6Group",
  "awsRegion": "us-east-1",
  "availabilityZone": "Not Applicable",
  "relatedEvents": [],
  "relationships": [
    {
      "resourceType": "AWS::EC2::VPC",
      "resourceId": "...",
      "relationshipName": "Is contained in Vpc"
    }
  ],
  "configuration": {
    "description": "This security group will be used for Ipv6 related tasks during the Jam challenge",
    "groupName": "Ipv6Group",
    "ipPermissions": [
      {
        "fromPort": 0,
        "ipProtocol": "tcp",
        "ipv6Ranges": [
          {
            "cidrIpv6": "::/0"
          }
        ],
        "prefixListIds": [],
        "toPort": 0,
        "userIdGroupPairs": [],
        "ipv4Ranges": [],
        "ipRanges": []
      }
    ],
    "ownerId": "...",
    "groupId": "...",
    "ipPermissionsEgress": [
      {
        "ipProtocol": "-1",
        "ipv6Ranges": [],
        "prefixListIds": [],
        "userIdGroupPairs": [],
        "ipv4Ranges": [
          {
            "cidrIp": "0.0.0.0/0"
          }
        ],
        "ipRanges": [
          "0.0.0.0/0"
        ]
      }
    ],
    "tags": [],
    "vpcId": "..."
  },
  "supplementaryConfiguration": {},
  "resourceTransitionStatus": "None"
}
Inventário
Configuração da AWS
Validação de tarefas
**NOTA: Antes de enviar, verifique se o nome da sua regra é “restrict-ec2-ingress” . **

Quando você criar uma regra que rastreia com êxito seus grupos de segurança (e seus grupos de segurança NÃO ESTÃO EM CONFORMIDADE), essa tarefa será concluída automaticamente e a próxima tarefa estará disponível. Você também pode forçar uma avaliação da sua regra selecionando Reavaliar na guia Ações da sua regra (isso pode ser mais rápido do que esperar pelo preenchimento automático).

Tarefa 3: Corrija manualmente o (s) grupo (s) de segurança não compatíveis
Pontos possíveis
23
Penalidade por pista
2
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Você sabe que a regra Config está rastreando adequadamente a não conformidade. Agora, você quer verificar se ele ainda funciona quando seus grupos de segurança estão em conformidade.

Tarefa
Corrija manualmente a (s) regra (s) ofensiva (s) do grupo de segurança excluindo a (s) regra (s).

Inventário
Grupos de segurança do Amazon EC2
Grupo Ipv4
Grupo Ipv6
Validação de tarefas
Essa tarefa será concluída automaticamente se você corrigir com êxito a (s) regra (s) violadora (s). Você também pode forçar uma avaliação de sua regra depois de corrigir o (s) grupo (s) de segurança selecionando Reavaliar na guia Ações da sua regra (isso pode ser mais rápido do que esperar pelo preenchimento automático).

Tarefa 4: Deixe os computadores fazerem todo o trabalho! Implementar remediação automática
Pontos possíveis
37
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
O objetivo principal dessa solução é corrigir a configuração do seu grupo de segurança antes que alguém perceba, então você deseja implementar a correção automática de regras não compatíveis. Felizmente, o AWS Config tem integração integrada com o AWS Systems Manager para automação.

Tarefa
Seu trabalho é implantar uma tarefa de automação com o AWS Systems Manager. A AWS fornece e gerencia um documento de remediação chamado “AWSConfigRemediation-RemoveUnrestrictedSourceIngressRules” para esse caso de uso. Use este documento ao configurar a tarefa de remediação da sua regra de configuração.

**NOTA: Verifique se o nome da sua regra de configuração é “restrict-ec2-ingress” . **

Inventário
Documento do AWS Systems Manager
Remediação do AWS Config - remova as regras de entrada de origem irrestritas
Função do AWS IAM
SystemsManager_Automation assume a função
Validação
Essa tarefa será concluída automaticamente se a automação corrigir as regras que violam as regras.

```

a