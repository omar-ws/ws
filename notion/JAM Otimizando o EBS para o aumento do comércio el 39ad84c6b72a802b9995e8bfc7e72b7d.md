# JAM Otimizando o EBS para o aumento do comércio eletrônico

```verilog
Visão geral
Na AnyCompany, líder em comércio eletrônico, a próxima promoção da época festiva promete ser o maior aumento de tráfego do ano. Os riscos são altos e a equipe está se esforçando para garantir que sua infraestrutura possa lidar com a enxurrada de clientes. Um dos componentes mais críticos é uma instância**Amazon Elastic Compute Cloud (Amazon EC2) ** que hospeda a lógica principal do aplicativo. O desempenho do servidor é fundamental para garantir que a venda ocorra sem problemas, mas benchmarks recentes mostram que a configuração atual do disco pode não ser suficiente para lidar com os picos de tráfego esperados.

O líder de sua equipe, John, forneceu a configuração de disco necessária para melhorar o IOPS, a taxa de transferência e o tamanho dos volumes do EBS anexados. Faltando apenas algumas horas para o lançamento da venda, você foi encarregado de analisar esses requisitos e fazer os ajustes necessários nos volumes do EBS da instância crítica do EC2. O sucesso da venda e a reputação da empresa dependem da sua capacidade de otimizar o sistema para obter o máximo desempenho. Deixar de agir com rapidez e precisão pode levar a um período de inatividade desastroso durante a época mais lucrativa do ano.

Leia menos

Tarefa 1: Modificar a configuração do volume raiz do EBS
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Benchmarks recentes de uma instância**Amazon Elastic Compute Cloud (Amazon EC2) ** mostram que a configuração atual do disco pode não ser suficiente para lidar com os picos de tráfego esperados para a próxima promoção da temporada festiva.

A instância EC2 em questão precisa de configuração de disco para melhorar IOPS, throughput e size para o volume EBS anexado. Após uma análise minuciosa e a realização de vários testes de benchmarking, concluiu-se que o volume do EBS deve ter a seguinte configuração:

Tipo de volume | SSD de uso geral (** gp3 **)
Tamanho do volume (GiB) | ** 100 **
Volume IOPS | ** 5000 **
Taxa de transferência (MiB/s) | ** 150 *
Modifique o volume do EBS em questão anexado à determinada instância do EC2 com base nas configurações acima.

** NOTE: ** Qualquer modificação subsequente do volume do EBS é permitida após ** 6 hours **, portanto, você deve modificar cuidadosamente os atributos na primeira tentativa, caso contrário encontrará o seguinte erro:

Modify Volume Request Failed for volume vol-xxxxxxxxxxxxxxx.
You've reached the maximum modification rate per volume limit. 
Wait at least 6 hours between modifications per EBS volume.
Além disso, antes de modificar o volume raiz do EBS, você deve marcá-lo com os dois pares de valores-chave a seguir:

Chave: ** Name ** | Valor: ** Production-Volume **
Chave: ** challenge ** | Valor: ** extend-windows-disk **
Sua tarefa
Sua tarefa é:

Marque o volume raiz do EBS anexado à determinada instância do EC2, conforme explicado acima.
Modifique o volume do EBS para aplicar as configurações mencionadas acima.
Começando
Vá para o console Amazon EC2 e selecione a instância EC2 chamada Production-Server e, na guia Storage, escolha o volume raiz com o nome do dispositivo como ** \dev\sda1 **.
Marque esse volume raiz do EBS com os seguintes dois pares de valores-chave:
Chave: ** Name ** | Valor: ** Production-Volume **
Chave: ** challenge ** | Valor: ** extend-windows-disk **
Em seguida, modifique o volume do EBS com base nas configurações explicadas acima.
Inventário
Instância do Amazon EC2 chamada Production-Server.
Para IDs de recursos, consulte a seção Propriedades de saída deste desafio.
Serviços que você deve usar
Nuvem de computação elástica da Amazon (Amazon EC2)
Amazon Elastic Block Store (Amazon EBS)
Validação de tarefas
Depois de modificar com êxito a configuração do volume do EBS conforme mencionado acima, essa tarefa será automaticamente marcada como concluída. Além disso, você sempre pode verificar seu progresso pressionando o botãoVerificar meu progresso na tela de detalhes do desafio.

Tarefa 2: Habilitar o acesso à instância do EC2
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Depois de modificar o volume do EBS, é muito importante observar que, se você aumentou o tamanho de um volume do EBS, também deverá estender a partição do volume no nível do sistema operacional para usar a capacidade de armazenamento adicional.

Para estender o sistema de arquivos no sistema operacional de determinada instância Windows do Amazon EC2, você descobriu que a instância do EC2 não pode ser acessada por meio da Conexão de Área de Trabalho Remota (RDP). Para acessar a instância do seu local de origem, você precisa definir as configurações de rede que habilitarão o RDP e permitirão o acesso à Internet à determinada instância do EC2.

Você deve verificar o Grupo de Segurança anexado à determinada instância Production-Server se ela permitir tráfego de RDP e Internet em sua regra de entrada e saída definida.

Sua tarefa
Sua tarefa é:

Identifique a instância do Windows do EC2 Production-Server
Habilite o RDP e o acesso à Internet a partir do grupo de segurança da instância
Conecte a instância do EC2 via RDP
Começando
Identifique a instância do EC2 - No EC2 Management Console, identifique a instância EC2 Production-Server consultando o ID da instância fornecido na seção Propriedades de saída.

Habilitar RDP e acesso à Internet - Certifique-se de que o acesso RDP à instância do EC2 seja permitido em sua rede de origem adicionando a regra de entrada em questão ao grupo de segurança associado (especifique Fonte como "Meu IP"). Além disso, verifique se o tráfego da Internet é permitido na regra de saída do mesmo grupo de segurança.

**Conecte a instância EC2 por meio da conexão RDP (Remote Desktop Protocol) ** - Depois de ativar o RDP e o acesso à Internet, conecte a instância EC2 Windows via cliente RDP de sua máquina Windows de origem (para macOS, baixe o aplicativo Microsoft Remote Desktop na AppStore) usando seu endereço IPv4 público, que pode ser determinado no console de gerenciamento do EC2 consultando o ID da instância EC2 fornecido e as credenciais de login do usuário nas Propriedades de saída seção.

Inventário
Instância do Amazon EC2 (Windows) chamada Servidor de produção.
Grupo de segurança anexado à instância do EC2 chamado Production-SecurityGroup.
Verifique a seção Propriedades de saída para obter a ID da instância do EC2, a ID do grupo de segurança e as credenciais de login.
Serviços que você deve usar
Nuvem de computação elástica da Amazon (Amazon EC2)
Acesso via cliente Remote Desktop Protocol (RDP)
Validação de tarefas
Depois de ativar o RDP e o acesso à Internet para uma determinada instância do EC2, conecte a mesma via RDP usando as credenciais de login fornecidas pelo seu endereço de origem permitido. Se você conseguir se conectar com sucesso, continue validando essa tarefa inserindo seu endereço IPv4 público de origem no campo de entrada, para o qual você permitiu o acesso RDP no grupo de segurança da instância.

Você pode obter o endereço IP de origem na regra de entrada do grupo de segurança. Na regra de entrada, procure por Source coluna e você deve encontrar o endereço IP no padrão 76.182.14.60/32.

Digite "your-public-ipv4-address/32" no campo de entrada desta tarefa, como: 76.182.14.60/32

NOTES!

O endereço IPv4 de origem inserido no campo de entrada da tarefa deve ser aquele para o qual você permitiu acesso RDP no grupo de segurança da instância.
Se você estiver conectado a uma conexão VPN, certifique-se de que o endereço IPv4 escolhido pela opçãoFonte como Meu IP no Grupo de Segurança da instância esteja correto.
Se você encontrar algum problema de RDP, desconecte-se da VPN, modifique a regra de entrada novamente para escolher a opção Fonte como Meu IP e tente novamente a conexão RDP.
Depois que essa tarefa for validada com sucesso, a instância do EC2 será reinicializada automaticamente. Portanto, reconecte-se se sua conexão RDP cair.

Tarefa 3: Estender partição de disco
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Finalmente, depois de obter acesso à determinada instância do Amazon EC2, conecte-a usando a conexão de desktop remoto (RDP) e estenda a partição do disco usando o utilitárioGerenciamento de disco.

Sua tarefa
Sua tarefa é:

Conecte a determinada instância do Amazon EC2 via RDP.
Estenda o sistema de arquivos usando o utilitárioGerenciamento de disco.
Começando
Conecte a instância do EC2 chamada Production-Server usando a conexão de desktop remoto.
No utilitárioGerenciamento de disco, estenda o Disco 0 para alocar o tamanho aumentado do volume do EBS para torná-lo um volume** 100 GB **.
Inventário
Instância do Amazon EC2 chamada Production-Server.
Para IDs de recursos, consulte a seção Propriedades de saída deste desafio.
Serviços que você deve usar
Nuvem de computação elástica da Amazon (Amazon EC2)
Amazon Elastic Block Store (Amazon EBS)
Validação de tarefas
Depois de estender com sucesso o sistema de arquivos para ter o novo tamanho como ** 100 GB ** volume paraDisco 0, essa tarefa será automaticamente marcada como concluída. Além disso, você sempre pode verificar seu progresso pressionando o botãoVerificar meu progresso na tela de detalhes do desafio.

```

a