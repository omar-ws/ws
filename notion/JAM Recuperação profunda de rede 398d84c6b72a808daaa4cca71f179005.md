# JAM Recuperação profunda de rede

```bash
Visão geral
Você é engenheiro de rede na AnySeaCompany, uma empresa de cabos submarinos que mantém o mundo conectado. A configuração incorreta de um ex-colega interrompeu as comunicações internas em sua infraestrutura de Tóquio.

Restaure a conectividade passo a passo: corrija o roteamento interrompido, coloque VPCs isoladas on-line por meio de um Transit Gateway, force todo o tráfego vinculado ao sensor por meio da inspeção do firewall e responda a um incidente de segurança ao vivo usando os registros de alerta do Network Firewall.

“Conectamos as redes do mundo, mas nem conseguimos conectar as nossas?!”

Leia menos

Propriedades de saída
CableManagementServerPrivateIp
10.1.1.50

DashboardServerInstanceId
i-064b8d76f5a6d49ea

FirewallRouteTableId
tgw-rtb-0f3c4c14468c632a1

FirewallTGWAttachmentId
tgw-attach-01a8063211e0ae4d1

FirewallVPCId
vpc-09328096ed5ff1da8

GeneralRouteTableId
tgw-rtb-05cbc43ef68ddb11f

InspectionRouteTableId
tgw-rtb-06c54c1153467efcd

MonitoringVPCId
vpc-01663b531d5e43c1a

NFWAlertLogGroup
/aws/network-firewall/deepsea/alert

SensorServerPrivateIp
10.3.1.50

SensorTGWAttachmentId
tgw-attach-0f244c5206ca93869

SensorVPCId
vpc-043b37633a2ff3ef3

TransitGatewayId
tgw-05569fa99c81b7399

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Restaurar a tabela de rotas quebrada
Pontos possíveis
23
Penalidade por pista
0
Pontos disponíveis
23
Verifique meu progresso

Tarefas e pistas
Plano de fundo
“O servidor do painel não consegue acessar o servidor de gerenciamento de cabos! Estava funcionando ontem...”

A equipe de monitoramento da AnySeaCompany relata que o Tokyo-Dashboard-Server na Monitoring VPC não pode alcançar o Tokyo-CableManagement Server (10.1.1.50) na CableManagement VPC. As duas VPCs estão conectadas ao Transit Gateway e todas as rotas aparecem como “ativas”, portanto, o problema não é óbvio à primeira vista.

Sua tarefa
Investigue a tabela de rotas do Transit Gateway (Deepsea-General-RT) e corrija o roteamento para que o Monitoring VPC possa alcançar o CableManagement VPC (10.1.0.0/16).

Começando
Abra o VPC Console > Tabelas de rotas do Transit Gateway
Selecione DeepSea-General-RT e examine as rotas
Use o Gerenciador de Sessões para conectar-se ao Tokyo-Dashboard-Server para testes
Inventário
**Portal de trânsito: ** Deepsea-Tokyo-TGW
**Tabela de rotas: ** DeepSea-General-RT (associado a monitoramento, gerenciamento de cabos e VPCs de ataque)
**Monitorando VPC: ** 10.2.0.0/16 com Tokyo-Dashboard-Server
** VPC de gerenciamento de cabos: ** 10.1.0.0/16 com servidor de gerenciamento de cabos de Tóquio (10.1.1.50)
Serviços que você deve usar
Amazon VPC (tabelas de rotas do Transit Gateway)
AWS Systems Manager (gerenciador de sessões)
Validação de tarefas
Execute ping 10.1.1.50 -c 4 a partir do Tokyo-Dashboard-Server. O validador verifica se a rota correta (10.1.0.0/16) existe e se a rota de interceptação (10.1.1.0/24) foi removida.

Pistas
Verifique a especificidade da rota
2Pontos de penalidade
Desbloqueie o Clue
Solução completa
2Pontos de penalidade
Desbloqueie o Clue

```

tinha 4 task nao fiz nem essa rimeiro o resto tava bloqueada