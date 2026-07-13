# JAM Corrija sua configuração antes mesmo que alguém saiba

```bash
Visão geral
Você lidera uma equipe de arquitetos de rede. Todos na sua organização têm um desempenho excelente e configuram a rede com os melhores controles em vigor. Um dia, você percebe que algumas contas da AWS têm grupos de segurança abertos para a Internet e pensa “Droga! Eu não esperava isso dos meus artistas famosos.” Você decide implementar a automação para poder detectar precocemente e remediar antes que seja tarde demais.

IAMRoleID
arn:aws:iam::240782466875:role/SystemsManager_AutomationAssumeRole

Ipv4SecurityGroupID
sg-002cfb3768a6f4528

Ipv6SecurityGroupID
sg-0cb96119da1923cbc

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

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

Pistas
Onde posso encontrar mais informações sobre um grupo de segurança específico?
1Pontos de penalidade
Desbloqueie o Clue
Instruções passo a passo
1Pontos de penalidade
Desbloqueie o Clue

Tarefa 2: Use o AWS Config para monitorar seus grupos de segurança
Pontos possíveis
75
Penalidade por pista
0
Pontos disponíveis
75
Verifique meu progresso

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

Pistas
Não entendo como escrever uma regra de guarda!
7Pontos de penalidade
Desbloqueie o Clue
Regra da Guarda de
9Pontos de penalidade
Desbloqueie o Clue
Instruções passo a passo
11Pontos de penalidade
Desbloqueie o Clue

```

faltou duas task essa segunda nao consegui nao sabia sinto que vou falhar no worldskills