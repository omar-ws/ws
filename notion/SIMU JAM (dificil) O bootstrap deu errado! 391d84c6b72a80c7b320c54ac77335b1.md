# SIMU JAM (dificil) O bootstrap deu errado!

```jsx
Visão geral
Você foi contratado como novoAdministrador do Sistema Windows para monitorar e gerenciar milhares de instâncias Windows do EC2 que hospedam dados essenciais para os negócios. Quando uma nova instância do Amazon Elastic Compute Cloud (EC2) é adicionada, ela passa por um processo de bootstrap que automatiza várias tarefas de configuração do sistema operacional, incluindo a adição da instância a um domínio do Active Directory. Anteriormente, essa funcionalidade funcionava conforme o esperado; no entanto, mudanças recentes feitas por um ex-colega interromperam o processo de bootstrap, exigindo uma correção imediata para integrar vários novos servidores críticos.

Você foi encarregado de investigar o problema em uma réplica de teste de instância do Amazon EC2 para identificar a causa raiz e resolver o problema.
```

```jsx
task 1
Propriedades de saída
BootstrapEC2InstanceID
i-0e2ff69d20fe68d7b

BootstrapSecurityGroupID
sg-088fca8ba6e122952

RDPCredentials
Username: Administrator | Password: p@SSword@123

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Identifique a instância EC2 afetada para habilitar o RDP e a conectividade com a Internet
Pontos possíveis
20
Penalidade por pista
2
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Para investigar e solucionar o problema de inicialização, você recebe uma réplica de uma instância de produção do Windows EC2. Para prosseguir com sua investigação, primeiro você deve conseguir conectar a instância via conexão RDP (Remote Desktop Protocol). No entanto, observou-se que a instância não tem conectividade com a Internet, portanto, para conduzir qualquer investigação no nível do sistema operacional, é necessário ativar a conexão RDP restaurando o acesso à Internet para a instância EC2 afetada.

Sua tarefa
Identifique a instância EC2 afetada
Habilite o RDP e o acesso à Internet a partir do grupo de segurança da instância
Conecte a instância EC2 afetada via RDP
Começando
Identifique a instância EC2 afetada - No console de gerenciamento do EC2, identifique a instância do EC2 afetada consultando o ID da instância fornecido na seção Propriedades de saída.

Habilitar RDP e acesso à Internet - Certifique-se de que o acesso RDP à instância afetada seja permitido a partir de sua rede de origem adicionando a regra de entrada em questão ao grupo de segurança associado. Além disso, verifique se o tráfego da Internet é permitido na regra de saída do mesmo grupo de segurança.

Conecte a instância EC2 afetada via RDP - Conecte a instância EC2 Windows via cliente RDP de sua máquina Windows de origem (para macOS, baixe o aplicativo Microsoft Remote Desktop na AppStore) usando seu endereço IPv4 público, que pode ser determinado no console de gerenciamento do EC2 consultando a ID da instância EC2 fornecida na seção Propriedades de saída.

Inventário
Instância do Amazon EC2 (Windows) chamada Bootstrap-Instance.
Credenciais de login do RDP para o usuárioAdministrador.
Grupo de segurança anexado à instância do EC2 chamado Bootstrap-SecurityGroup.
Verifique a seção Propriedades de saída para obter a ID da instância do EC2, a ID do grupo de segurança e as credenciais de login.
Serviços que você deve usar
Instância Amazon EC2 (Windows)
Acesso via cliente Remote Desktop Protocol (RDP).
Validação de tarefas
Você deve habilitar o RDP e o acesso à Internet para determinada instância do EC2. Em seguida, você deve conectar a instância do Windows EC2 depois de determinar seu endereço IPv4 público. Para validar, você deve inserir o endereço IPv4 público no campo de entrada dessa tarefa.

Pistas
Como começar!
2Pontos de penalidade
Mostrar pista
Ajude-me com etapas detalhadas!
2Pontos de penalidade
Desbloqueie o Clue
```

```jsx
task 2
ropriedades de saída
BootstrapEC2InstanceID
i-0e2ff69d20fe68d7b

BootstrapSecurityGroupID
sg-088fca8ba6e122952

RDPCredentials
Username: Administrator | Password: p@SSword@123

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Habilitando a recuperação de metadados de instância do EC2 (IMDS)
Pontos possíveis
60
Penalidade por pista
13
Pontos disponíveis
47
Verifique meu progresso

Tarefas e pistas
Antecedentes
Depois de conseguir conectar com êxito a réplica afetada da instância EC2 de produção, em seguida, você deve verificar se a instância pode recuperar os metadados da instância.

Ao iniciar uma instância do Windows usando o Amazon EC2, você pode passar dados do usuário para a instância, que podem ser usados para realizar tarefas de configuração automatizadas ou executar scripts após o início da instância. A instância recupera o script de dados do usuário passado no console a partir de metadados que devem estar acessíveis. Além disso, o agente de inicialização do EC2 (EC2Config ou EC2Launch) deve ser configurado corretamente para acionar a execução de dados do usuário do EC2 na inicialização/próxima inicialização, se ativado.

Sua tarefa
Verifique se a instância pode recuperar os metadados da instância.
Corrija quaisquer problemas que causem falhas no acesso ao serviço de metadados da instância.
Começando
Conecte-se à instância do Amazon EC2 via RDP e execute o seguinte comando no PowerShell:
PS > iwr -uri 'http://169.254.169.254/latest/meta-data/'

A saída acima deve ser: StatusCode : 200

Verifique os pré-requisitos para a recuperação de dados do usuário do EC2 no sistema operacional da instância.
Certifique-se de que a instância tenha acesso aos dados do usuário do EC2 passados do console de gerenciamento da AWS para o Amazon EC2.
Inventário
Instância do Amazon EC2 (Windows) chamada Bootstrap-Instance.
Credenciais de login do RDP para o usuárioAdministrador.
Verifique a seção Propriedades de saída para obter o ID da instância do EC2 e as credenciais de login.
Serviços que você deve usar
Instância Amazon EC2 (Windows)
Acesso via cliente Remote Desktop Protocol (RDP)
Validação de tarefas
Depois de se conectar à instância, você deve corrigir o acesso à rota de metadados da instância. Essa tarefa validará automaticamente a correção se a instância afetada conseguir recuperar os metadados da instância e, após a execução do comando do PowerShell, resultar em:

PS > iwr -uri 'http://169.254.169.254/latest/meta-data/'

A saída acima deve ser: StatusCode : 200

!IMPORTANT NOTE!: Se depois de obter a saída acima, o progresso da tarefa não marcar essa tarefa como concluída, execute o seguinte comando no PowerShell:

PS > Restart-Service AmazonSSMAgent

Aguarde 10 segundos e tente verificar novamente o progresso no console JAM clicando no botão Verificar o progresso.

Pistas
Por onde começar a procurar se as coisas não estão se movendo?
6Pontos de penalidade
Mostrar pista
Preciso de ajuda com algumas dicas aqui!
7Pontos de penalidade
Mostrar pista
```

consegui fazer certinho tbm igual o laboratorio pediu mas nao foi, essa era a dica aprendi sobre os comandos 

```jsx
Pistas
Por onde começar a procurar se as coisas não estão se movendo?
6Pontos de penalidade
Mostrar pista
Preciso de ajuda com algumas dicas aqui!
7Pontos de penalidade
Ocultar pista
Etapa A | Conectar a instância EC2 afetada via RDP
Depois de selecionar a instância EC2 afetada, vá para a guia Detalhes na parte inferior e, na seção Resumo da instância, procure o valorEndereço IPv4 público.
Em sua máquina Windows de origem (para macOS, baixe o aplicativo Microsoft Remote Desktop na AppStore), pesquise por RDP ou Conexão de Área de Trabalho Remota e especifique o endereço públicoIPv4 no nome do computador e clique em Conectar.
Quando solicitadas as credenciais de login, digite o nome de usuário como Administrador e, para obter a senha, verifique a seção Propriedades de saída.
Etapa B | Adicionar rota de metadados com o gateway correto
Depois de se conectar à instância, abra o PowerShell com privilégios de administrador.
Execute os seguintes comandos, um após o outro:
PS > route DELETE 169.254.169.254

PS > route -p ADD 169.254.169.254 MASK 255.255.255.255 {Subnet default Gateway IP}

Nota: Para obter o IP de gateway padrão, execute o comando route print e veja o IP Gateway do primeiro destino de rede 0.0.0.0

**Exemplo: **

PS > route print

Saída

Active Routes:
Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0       10.0.0.147         10.0.0.9     50
Observe o IP Gateway para o destino da rede0.0.0.0.

Então, execute o comando acima com esse IP de gateway da seguinte forma:

PS > route -p ADD 169.254.169.254 MASK 255.255.255.255 10.0.0.147

Etapa C | Validar a tarefa
Essa tarefa validará automaticamente a correção se a instância afetada conseguir recuperar os metadados da instância e, após a execução do comando do PowerShell, resultar em:

PS > iwr -uri 'http://169.254.169.254/latest/meta-data/'

A saída acima deve ser: StatusCode : 200

!IMPORTANT NOTE!: Se depois de obter a saída acima, o progresso da tarefa não marcar essa tarefa como concluída, execute o seguinte comando no PowerShell:

PS > Restart-Service AmazonSSMAgent

Aguarde 10 segundos e tente verificar novamente o progresso no console JAM clicando no botão Verificar o progresso.
```

a