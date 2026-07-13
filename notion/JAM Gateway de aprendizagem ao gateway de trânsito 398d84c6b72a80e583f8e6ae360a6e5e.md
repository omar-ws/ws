# JAM Gateway de aprendizagem ao gateway de trânsito

```bash
Visão geral
Plano de fundo
Você é administrador de rede da MyTCPPackets Company, que tem várias arquiteturas Amazon Virtual Private Cloud (Amazon VPC). Para comunicação entre VPCs, você estava usando o emparelhamento de VPC. Você aprendeu que o AWS Transit Gateway resolve o problema do peering transitivo (você pode encontrar mais informações sobre peering transitivo neste link) e queria implementar os conceitos do AWS Transit Gateway usando duas VPCs de teste.

Como prova de conceito para a equipe de liderança, você implantou duas VPCs com todos os componentes de rede e o AWS Transit Gateway usando o AWS CloudFormation. Você tem uma instância do Amazon Elastic Compute Cloud (Amazon EC2) implantada nas sub-redes privadas das VPCs e um host bastion implantado na sub-rede pública da VPC1.

Depois de implantar os recursos, você percebeu os seguintes problemas.

Você não pode usar SSH no Bastion Host e depois na instância de sub-rede privada da VPC1.
As instâncias do EC2 nas sub-redes privadas de VPC1 e VPC2 não podem fazer ping umas nas outras.
Você deve resolver os problemas e estabelecer a conectividade entre as duas VPCs usando o AWS Transit Gateway. Você está pronto para o desafio?

Diagrama de arquitetura:
Link para o diagrama de arquitetura
Nota: consulte a seção de inventário de desafios na tarefa 1 para ver o inventário de desafios.

Serviços que você deve usar:
Amazon EC2
Amazon VPC
AWS Transit Gateway
Leia menos

Propriedades de saída
BastionHostEIP
18.208.42.0

BastionHostEIPAllocationId
eipalloc-0857e387b12c57da0

BastionHostInstanceIP
18.208.42.0

BastionHostSGId
sg-0a7f5b201c4baab52

KeyName
AWSLabsKeyPair-qJThbRN6Eeaa6ACdtM4HvF

TGWId
tgw-08ed2fcc618d181c1

Vpc1PvtInstanceIP
10.0.2.214

Vpc1PvtInstanceSGId
sg-0166776da448085b4

Vpc1PvtSubnetRTId
rtb-02d418b0632b6b3bb

Vpc2PvtInstanceIP
192.168.2.191

Vpc2PvtInstanceSGId
sg-0e89a663b4bb219ad

Vpc2PvtSubnetRTId
rtb-0cafea4fd6b7305d3

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Remova os blocos de firewall virtual para os pacotes!!!
Pontos possíveis
38
Penalidade por pista
0
Pontos disponíveis
38
Verifique meu progresso

Tarefas e pistas
Antecedentes:
De acordo com a configuração inicial, você percebeu que algo está impedindo você de acessar instâncias do EC2. Como administrador de rede da MyTcpPackets Company, você deve limpar os blocos para que as instâncias do EC2 possam se comunicar.

Para concluir a tarefa, você precisa atualizar três grupos de segurança. Dois grupos de segurança estarão na VPC1 e o outro na VPC2. Você deve fazer o seguinte:

Faça ping no VPC1 Bastion Host a partir de sua estação de trabalho local. Você pode encontrar o endereço IP público do Bastion Host na guia Propriedades de saída à esquerda dessas instruções.
Faça o SSH no VPC1 Bastion Host usando as credenciais fornecidas na seção Getting Started.
Faça ping na instância de sub-rede privada VPC1 (10.0.2.x) a partir do bastion host (10.0.1.x).
Faça o SSH na instância de sub-rede privada VPC1 (10.0.2.x) a partir do bastion host (10.0.1.x) usando as credenciais fornecidas na seção Getting Started.
Embora você ainda não consiga fazer ping na instância de sub-rede privada na VPC2 (192.168.0.0/16), certifique-se de que o grupo de segurança da instância EC2 da sub-rede privada VPC2 esteja configurado adequadamente para permitir que a instância privada na VPC1 faça ping nessa instância.
Depois de concluída, essa tarefa permitirá que você entre por SSH no host bastion VPC1 na VPC1 usando o IP público do host e, em seguida, na instância de sub-rede privada da VPC1 (10.0.2.x).

Inventário de desafios
VPC1 (10.0.0.0/16):
Sub-rede pública (10.0.1.0/24)
Tabela de rotas de sub-rede pública
Gateway de Internet
Sub-rede privada (10.0.2.0/24)
Tabela de rotas de sub-rede privada
Anfitrião Bastion (10.0.1.x)
Grupo de segurança Bastion host
Instância EC2 de sub-rede privada (10.0.2.x)
Grupo de segurança de instâncias EC2 de sub-rede privada
VPC2 (192.168.0.0/16):
Sub-rede privada (192.168.2.0/24)
Tabela de rotas de sub-rede privada
Instância EC2 de sub-rede privada (192.168.2.x)
Grupo de segurança de instâncias EC2 de sub-rede privada
Gateway de trânsito
Conexão VPC1 Transit Gateway
Anexo ao VPC2 Transit Gateway
Tabela de rotas do Transit Gateway
Diagrama de arquitetura
Link para o diagrama de arquitetura
Começando
Coisas que você deve CONSIDERAR fazer:

Use VPC CIDR, CIDR de sub-rede ou endereços IP privados de instâncias em regras de entrada de grupos de segurança e entradas da tabela de rotas.
Coisas que você deve EVITAR fazer:

De acordo com as melhores práticas, é proibido usar All-Traffic nas regras de entrada de grupos de segurança.
De acordo com as melhores práticas, o uso do Zero-CIDR (0.0.0.0/0) é proibido nas regras de entrada de todos os grupos de segurança.
De acordo com as melhores práticas, é proibido usar Todas as portas TCP nas regras de entrada de todos os grupos de segurança.
O script de validação automática de tarefas verificará a adesão a essas melhores práticas durante todo o desafio. Qualquer não conformidade fará com que a tarefa não seja marcada como concluída.
SSH na instância de sub-rede privada VPC2 (192.168.2.x).
Você pode consultar este link de documentação para descobrir como adicionar regras de entrada aos grupos de segurança.

OBSERVAÇÃO: Você não precisa usar um par de chaves para fazer login em nenhuma instância do EC2 neste desafio. Uma conta local foi criada em todas as instâncias da VPC1. As credenciais podem ser encontradas nas instruções SSH abaixo.

Instruções SSH
Use as informações abaixo para acessar a instância EC2 do Bastion Host usando seu endereço IP público. O endereço IP público do bastion host pode ser encontrado na guia Propriedades de saída à esquerda dessas instruções.

Credenciais
Nome de usuário: participante
Senha: tgw123
Para usuários de Mac
Para acessar o host Bastion via SSH, abra o aplicativo Terminal e conecte-se ao bastion host usando o seguinte comando SSH. Observação: você deve substituir bastion_host_public_ip pelo IP público do bastion host.

ssh participant@{bastion_host_public_ip}

Após o login bem-sucedido no host Bastion, faça o SSH na instância de sub-rede privada VPC1 (10.0.2.x) usando o comando abaixo no terminal bastion host. Observação: você deve substituir vpc1_private_subnet_instance_private_ip pelo IP privado da instância do EC2 na sub-rede privada VPC1 (ou seja, 10.0.2.x).

ssh participant@{vpc1_private_subnet_instance_private_ip}

Para usuários do Windows
Para acessar o bastion host via SSH, você deve usar um cliente como o PuTTY. Se isso não estiver instalado no seu computador, você deve baixar e instalar um. Verifique suas políticas para garantir que isso seja permitido se você usar um computador da empresa.
Depois de baixar e instalar o PuTTY, inicie o aplicativo.
No painel Categoria, escolhaSessão e preencha os seguintes campos:
Insira participant@{bastion_host_public_ip} como host. Observação: você deve substituir obastion_host_public_ip pelo IP público do bastion host.
Certifique-se de que o valorPorta seja 22.
Em Tipo de conexão, selecioneSSH.
Clique no botãoAbrir
Para obter mais detalhes, consulte a seção Conectando-se à sua instância Linux na documentação da AWS.

Após o login bem-sucedido no host Bastion, faça o SSH na instância de sub-rede privada VPC1 (10.0.2.x) usando o comando abaixo do Bastion host. Observação: você deve substituir vpc1_private_subnet_instance_private_ip pelo IP privado da instância do EC2 na sub-rede privada VPC1 (ou seja, 10.0.2.x).

ssh participant@{vpc1_private_subnet_instance_private_ip}

Inventário de tarefas
Grupos de segurança VPC1 e VPC2

Serviços que você deve usar
Amazon VPC

Validação de tarefas
Você deve atualizar três grupos de segurança com as regras de entrada apropriadas para concluir essa tarefa.

A tarefa será concluída automaticamente quando você encontrar a solução. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes da tarefa.

Observação: de acordo com as melhores práticas de segurança, as regras de entrada dos grupos de segurança não devem permitir zero cidr em nenhuma porta. Portanto, usar zero cidr como fonte é estritamente proibido neste desafio, e a tarefa não será transferida para um estado concluído. Além disso, o script de validação automática de tarefas não considerará as regras de entrada do tipo All TCP e All Traffice como soluções corretas.

Dica: Usar portas ICMP (todas ICMP - IPv4) e SSH é suficiente para concluir essa tarefa. Nenhuma outra porta é necessária.

Pistas
Adicionar Regra de Entrada a Grupos de Segurança
3Pontos de penalidade
Desbloqueie o Clue
Passos passo a passo
4Pontos de penalidade
Desbloqueie o Clue

```

eu so fiz um, na verdade nao fiz a primeira nao cosnegui fazer tambem, nao consegui nada