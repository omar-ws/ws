# JAM Gateway de aprendizagem ao gateway de trânsito

```json
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

Tarefa 1: Remova os blocos de firewall virtual para os pacotes!!!
Pontos possíveis
38
Penalidade por pista
0
Pontos disponíveis
0

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

Tarefa 2: Mostre aos pacotes um caminho a percorrer!!!
Pontos possíveis
38
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Agora que você pode fazer login na instância privada (10.0.2.x) da VPC1 por meio do bastion host (10.0.1.x), o roteamento é necessário para executar ping na instância na sub-rede privada da VPC2 (192.168.2.x). Identifique uma forma de atender a esse requisito.

Coisas que você deve CONSIDERAR fazer:

Use o CIDR da VPC, o CIDR da sub-rede ou os endereços IP privados da instância nas entradas da tabela de rotas.
Coisas que você deve EVITAR fazer:

De acordo com as melhores práticas, é proibido usar Zero-CIDR (0.0.0.0/0) nas entradas de rota de todas as tabelas de rotas. O script de validação automática de tarefas verificará essa condição durante todo o desafio. Qualquer não conformidade resultará na avaliação da tarefa como incompleta.
Instruções SSH
Use as informações abaixo para acessar a instância EC2 do Bastion Host usando seu endereço IP público. Você pode encontrar o endereço IP público do Bastion Host na guia Propriedades de saída à esquerda dessas instruções.

Credenciais
Nome de usuário: participante
Senha: tgw123
Para usuários de Mac
Para acessar o host Bastion via SSH, abra o aplicativo Terminal e conecte-se ao host bastion usando o seguinte comando SSH. Observação: você deve substituir bastion_host_public_ip pelo IP público do bastion host.

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

Começando
A documentação da AWS que pode ajudar a realizar as etapas necessárias para essa tarefa está no link abaixo.

Adicionar e remover rotas de uma tabela de rotas
Adicione rotas entre o gateway de trânsito e suas VPCs
Inventário
Tabelas de rotas VPC1 e VPC2

Serviços que você deve usar
Amazon VPC

Validação de tarefas
Para concluir essa tarefa, você deve atualizar duas tabelas de rotas com as entradas de rota apropriadas.

Depois de encontrar a solução, a tarefa será concluída automaticamente. No entanto, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes da tarefa.

Nota: De acordo com as melhores práticas de segurança, as tabelas de rotas não devem ter entradas CIDR zero como destino para o tráfego interno. Portanto, é proibido usar Zero-CIDR como destino nas entradas de rota. A função de validação automática de tarefas verificará a conformidade com esse requisito. Além disso, o script de validação automática de tarefas verificará suas entradas de rota antes de marcar a tarefa como concluída.

Dica: atualizar as tabelas de rotas da VPC com as entradas de rota necessárias é suficiente para concluir essa tarefa. O uso de outros serviços não é obrigatório.

Pistas
Adicionar rotas às tabelas de roteamento
3Pontos de penalidade
Desbloqueie o Clue
Passo a passo detalhado
4Pontos de penalidade
Desbloqueie o Clue

Tarefa 3: Obter os pacotes indo!!!
Pontos possíveis
74
Penalidade por pista
7
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Depois de adicionar com êxito as entradas de rota necessárias, você deve encontrar uma maneira de executar ping com êxito na instância EC2 na sub-rede privada VPC2 (192.168.2.x) a partir da instância EC2 da sub-rede privada VPC1 (10.0.2.x) por meio do gateway de trânsito. Descubra uma maneira de cumprir esse requisito.

Essa tarefa habilitará a conectividade entre a VPC1 e a VPC2 por meio do AWS Transit Gateway. Depois de concluída, sua prova de conceito no AWS Transit Gateway estará pronta para a análise da equipe de liderança da sua empresa.

**Nota: ** Não crie uma rota estática para fazer isso.

Para concluir o desafio, você deve fazer o seguinte:

Faça ping do IP privado da instância de sub-rede privada VPC2 a partir da instância de sub-rede privada VPC1.
**Observação: você NÃO precisa fazer login na instância de sub-rede privada VPC2 para concluir esse desafio. **

Começando
Você pode usar esses links de documentação para aprender sobre os conceitos de gateway de trânsito.

Conceitos de gateway de trânsito
Como funcionam os gateways de trânsito
Você pode usar a Etapa 4 neste link de documentação para obter mais informações sobre como testar o Transit Gateway.

Antes de iniciar um comando ping na instância EC2 da sub-rede privada VPC2 (192.168.2.x), verifique se você está na instância EC2 da sub-rede privada VPC1 (10.0.2.x) antes de iniciar um comando ping na instância da sub-rede privada VPC2 (192.168.2.x).

Instruções SSH
Use as informações abaixo para acessar a instância EC2 do Bastion Host usando seu endereço IP público. Você pode encontrar o endereço IP público do Bastion Host na guia Propriedades de saída à esquerda dessas instruções.

Credenciais
Nome de usuário: participante
Senha: tgw123
Para usuários de Mac
Para acessar o host Bastion via SSH, abra o aplicativo Terminal e conecte-se ao host bastion usando o seguinte comando SSH. Observação: você deve substituir bastion_host_public_ip pelo IP público do bastion host.

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

Inventário
Gateway de trânsito VPC
Anexos do VPC Transit Gateway
Tabelas de rotas do VPC Transit Gateway
Serviços que você deve usar
Amazon VPC
AWS Transit Gateway
Validação de tarefas
Depois de descobrir a solução, faça o SSH no VPC1 Bastion Host. Em seguida, faça o SSH na instância de sub-rede privada VPC1 (10.0.2.x) usando as credenciais locais fornecidas nas instruções SSH. Em seguida, você emitirá um comando ping para a instância EC2 da sub-rede privada VPC2 (192.168.2.x) a partir da instância EC2 da sub-rede privada VPC1 (10.0.2.x). Se sua solução estiver correta, você poderá enviar com êxito o tráfego ICMP da VPC1 para a VPC2 por meio do Transit Gateway. Continue fazendo ping na instância por pelo menos 5 a 10 minutos.

O script de validação automática de tarefas levará aproximadamente de 5 a 10 minutos para analisar o número de pacotes que saem do Transit Gateway para avaliar a exatidão de sua solução.

Depois de fazer ping na instância da sub-rede privada VPC2 a partir da sub-rede privada VPC1, a tarefa será concluída automaticamente. No entanto, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes da tarefa.

Pistas
Crie a proposta de rota na tabela de rota do gateway de trânsito
7Pontos de penalidade
Mostrar pista
Passo a passo detalhado
9Pontos de penalidade
Desbloqueie o Clue

```

a