# JAM Portal NAT regional para a simplicidade

```bash
Visão geral
Sua empresa, AnyCompany Innovations, está aproveitando a onda de crescimento explosivo! Sua plataforma de comércio eletrônico de três níveis agora atende clientes em três zonas de disponibilidade, mas a equipe de infraestrutura está mergulhada na complexidade operacional. Toda vez que você expande para uma nova região ou adiciona capacidade, alguém precisa provisionar manualmente os gateways NAT, configurar sub-redes públicas, atualizar tabelas de rotas e rezar para que nada seja interrompido durante a migração.

Na semana passada, seu vice-presidente de engenharia participou do AWS re:Invent e voltou falando sobre um anúncio revolucionário: Gateways NAT regionais. Ela desafiou você a ser o herói que simplifica a arquitetura, reduz a sobrecarga operacional em 70% e prova que alta disponibilidade não precisa significar alta complexidade.

Sua missão: transformar a rede emaranhada de gateways NAT zonais em uma arquitetura de gateway NAT regional elegante e autorecuperável. Mostre à equipe que, às vezes, a melhor solução é a mais simples.

! Arquitetura do estado atual

Leia menos

Propriedades de saída
NATGatewayAZ1Name
jam-nat-az1

NATGatewayAZ2Name
jam-nat-az2

NATGatewayAZ3Name
jam-nat-az3

TestInstanceAZ1Name
jam-test-instance-az1

TestInstanceAZ2Name
jam-test-instance-az2

TestInstanceAZ3Name
jam-test-instance-az3

VPCId
vpc-025915724da9f24b8

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: A Grande Migração
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
É segunda-feira de manhã e seu vice-presidente de engenharia acabou de lhe enviar um e-mail com o assunto: “Vamos simplificar nossa arquitetura NAT - ESTA SEMANA”. Ela está convencida de que o Regional NAT Gateway é a resposta para suas crescentes dores de cabeça. A equipe de infraestrutura está cética: eles já viram recursos “revolucionários” que se revelaram mais exagerados do que úteis.

Seu trabalho? Prove que eles estão errados. Migre o ambiente de produção de três gateways NAT zonais para um único gateway NAT regional sem descartar um único pacote. Sem tempo de inatividade. Sem desculpas. Apenas engenharia elegante.

Sua tarefa
Execute uma migração sem tempo de inatividade da arquitetura atual do gateway NAT zonal para o gateway NAT regional. Você precisa:

Crie um gateway NAT regional em sua VPC
Atualize todas as tabelas de rotas para usar o novo gateway NAT regional
Verifique se a conectividade é mantida em todas as zonas de disponibilidade
Descomissionar os antigos gateways NAT zonais
**Nota importante: ** Enquanto o gateway NAT regional está sendo provisionado (normalmente leva de 2 a 3 minutos), você pode começar a atualizar as tabelas de rotas. No entanto, as rotas que apontam para o Regional NAT Gateway aparecerão como “buraco negro” até que o gateway alcance o estado “disponível”. Esse é o comportamento esperado: aguarde até que o gateway fique disponível antes de testar a conectividade.

Inventário
Seu ambiente inclui:

**VPC: ** jam-regional-nat-vpc (10.0.0.0/16)
**3 gateways NAT zonais: ** jam-nat-gateway-az1, jam-nat-gateway-az2, jam-nat-gateway-az3
**3 tabelas de rotas privadas: ** jam-private-rt-az1, jam-private-rt-az2, jam-private-rt-az3
**3 Instâncias de teste do EC2: ** Executando em sub-redes privadas em todas as AZs
**3 IPs elásticos: ** Atualmente associados a gateways NAT zonais
Serviços que você deve usar
Amazon VPC
Gateway NAT (modo regional)
Tabelas de rotas
EC2 (para testes de conectividade)
Pistas
Estratégia de migração e primeiros passos
6Pontos de penalidade
Desbloqueie o Clue
O passo a passo completo da migração
7Pontos de penalidade
Desbloqueie o Clue

Tarefa 2: Chaos Engineering - Simulação de falhas AZ
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
🛡️ Tarefa 2: Engenharia do Caos - Simulação de falha AZ
Antecedentes
Sua migração foi perfeita! A equipe está impressionada, mas seu engenheiro de confiabilidade de sites (SRE), Marcus, ainda não está convencido. “Claro, funciona quando tudo está perfeito”, diz ele com um sorriso cético. “Mas o que acontece quando uma zona de disponibilidade inteira fica escura? Com nossa configuração antiga, sabíamos exatamente qual gateway NAT falharia. Com essa coisa regional... como sabemos que ela realmente falha?”

Marcus tem razão. Na arquitetura antiga, cada AZ tinha seu próprio gateway NAT — se uma AZ falhasse, somente o tráfego dessa AZ era afetado. Mas com o Regional NAT Gateway, você afirma que é ainda melhor. É hora de provar isso com um pouco de caos controlado.

Sua tarefa
Demonstre que o Regional NAT Gateway fornece alta disponibilidade real simulando uma falha de AZ. Você precisa:

Pare todas as instâncias do EC2 em uma zona de disponibilidade (simulando falha de AZ)
Verifique se as instâncias em outras AZs mantêm a conectividade com a Internet
Confirme se o gateway NAT regional tem interfaces de rede em várias AZs
Reinicie as instâncias interrompidas e verifique a recuperação automática
Inventário
**Gateway NAT regional: ** Seu gateway recém-criado
**3 Instâncias EC2 de teste: ** jam-test-instance-az1, az2, az3
**Interfaces de rede: ** Criadas automaticamente pelo gateway NAT regional em cada AZ
Serviços que você deve usar
Amazon EC2 (gerenciamento de instâncias)
Gateway NAT (monitoramento de ENIs)
VPC (inspeção de interface de rede)
Pistas
Entendendo a arquitetura Multi-AZ
4Pontos de penalidade
Desbloqueie o Clue
Passo a passo completo da simulação de falhas AZ
5Pontos de penalidade
Desbloqueie o Clue

Tarefa 3: O teste definitivo - Expansão automática de AZ
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Plano de fundo
O CEO acaba de anunciar uma grande parceria que triplicará sua base de clientes da noite para o dia! Sua equipe de infraestrutura precisa se expandir imediatamente para uma quarta zona de disponibilidade. No velho mundo, isso significaria:

Provisionamento de uma nova sub-rede pública
Criação de um terceiro gateway NAT
Alocação de outro IP elástico
Configurando novas tabelas de rotas
Testando tudo manualmente
Rezando para que nada quebre
Mas você tem uma arma secreta: a expansão automática do Regional NAT Gateway. Você afirma que tudo o que precisa fazer é lançar recursos no novo AZ, e o Regional NAT Gateway os detectará automaticamente e se expandirá dentro de ** 60 minutos**. Sem configuração manual. Sem gateways NAT adicionais. Simplesmente magia pura e automatizada.

Seu vice-presidente de engenharia está assistindo. É hora de mostrar o que a arquitetura de nuvem moderna pode fazer!

Sua tarefa
Prove que o Regional NAT Gateway se expande automaticamente para novas zonas de disponibilidade ao:

Criação de uma nova sub-rede na 4ª Zona de Disponibilidade com o nome jam-private-subnet-az4 (nome deve começar com jam-)
Criação de uma nova tabela de rotas (nome deve começar com jam-).
Associando a nova tabela de rotas à nova sub-rede.
Configurando o roteamento para usar o gateway NAT regional
Lançamento de uma instância EC2 na nova sub-rede do JAM VPC usando o Amazon Linux 2023 AMI com testInstanceProfile (terá o prefixo LabStack) e o grupo de segurança TestInstanceSecurityGroup (terá o prefixo LabStack)
Aguardando a expansão automática (até 60 minutos, mas geralmente é feita muito mais cedo)
Verificando se o gateway NAT regional criou um ENI no novo AZ
Inventário
**VPC: ** jam-regional-nat-vpc (10.0.0.0/16)
**Gateway NAT regional: ** Seu gateway existente
**CIDR disponível: ** 10.0.13.0/24 (sugerido para nova sub-rede)
**Target AZ: ** jam-private-subnet-az4 (ou o nome fornecido ao criar a nova sub-rede)
**Grupo de segurança: ** Grupo de segurança existente TestInstanceSecurityGroup (terá o prefixo LabStack)
Perfil da instância Perfil de instância existente TestInstanceProfile (terá o prefixo LabStack).
Serviços que você deve usar
Amazon VPC (criação de sub-rede)
Amazon EC2 (lançamento da instância)
NAT Gateway (expansão automática)
Tabelas de rotas
**Observação: ** A expansão pode levar até 60 minutos.

Pistas
Configurando a nova zona de disponibilidade
4Pontos de penalidade
Desbloqueie o Clue
Passo a passo completo da expansão AZ
5Pontos de penalidade
Desbloqueie o Clue

```

nao consiui fazer a 3, que raiva, nao temrinei nenhuma