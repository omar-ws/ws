# JAM Perdido em metadados: resolvendo o quebra-cabeça da instância do EC2

TASK 1:

conseguui fazer li a documentacao nao sabia o que era RDP mas consegui fazer pela logica

```wasm
Perdido em metadados: resolvendo o quebra-cabeça da instância do EC2
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
EC2InstanceID
i-086fbf5db6cb9af59

RDPCredentials
Username: Administrator | Password: p@SSword@123

SecurityGroupID
sg-0b6419cf94705289e

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Habilitar o acesso à instância do EC2
Pontos possíveis
24
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Os metadados da instância do Amazon EC2** são dados sobre sua instância que você pode usar para configurar ou gerenciar a instância em execução. Você pode acessar os metadados da instância do EC2 de dentro da própria instância ou do console do EC2, da API, dos SDKs ou da AWS CLI. Existem diferentes agentes da AWS, como o agenteAmazon SSM, o agenteAmazon CloudWatch, AWS CLI etc. que consultam os metadados da instância para recuperar detalhes relacionados à instância para seu funcionamento.

Para acessar as propriedades de metadados da instância de dentro de uma instância em execução, você obtém os dados dos seguintes URIs IPv4 ou IPv6. Esses endereços IP são endereços locais do link e são válidos somente na instância.

IPv4 - http://169.254.169.254/latest/meta-data/
IPv6 - http://[fd00:ec2::254]/latest/meta-data/
Por padrão, a rota para os metadados da instância é adicionada à tabela de rotas do Windows, como pode ser visto na captura de tela a seguir:

! rotas de janelas

Essa rota é adicionada com o IP do gateway da sub-rede VPC configurada. No entanto, quando a AMI (Amazon Machine Image) de uma instância Windows do EC2 é capturada sem Sysprep, essa rota IP do gateway capturada na imagem não é atualizada quando uma nova instância do EC2 é iniciada em uma sub-rede VPC diferente e, por fim, leva a um problema de rota inválida. Com essa rota incorreta existente na tabela de rotas do Windows, os metadados da instância se tornam inacessíveis para a instância, fazendo com que ela gere o seguinte erro, interrompendo as operações de todos os agentes dependentes da AWS e outros:

Waiting for the metadata service.....

Portanto, nesta tarefa desafiadora, como as AMIs (Amazon Machine Images) para instâncias do EC2 são capturadas de uma VPC de conta da AWS diferente e, agora, sendo lançadas em outra sub-rede da VPC, pode ter ocorrido um conflito semelhante por endereço IP de gateway inválido.

Para investigar isso com antecedência, você precisa conectar uma das instâncias EC2 fornecidas, mas descobriu que a instância do EC2 não está acessível por meio da Conexão de Área de Trabalho Remota (RDP). Para acessar a instância do seu local de origem, você precisa definir as configurações de rede que habilitarão o RDP e permitirão o acesso à Internet à determinada instância do EC2.

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
Pistas
Ajude-me a começar!
2Pontos de penalidade
Desbloqueie o Clue
Mais algumas dicas seriam ótimas!
3Pontos de penalidade
Desbloqueie o Clue
```

task 2:

nao consegui, tiver que evr as dicas e mesmo assim fazendo nao consegui tambem

desafio com as dicas ja: fiquei uma hora  10 minutos nele

```wasm
Perdido em metadados: resolvendo o quebra-cabeça da instância do EC2
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
EC2InstanceID
i-086fbf5db6cb9af59

RDPCredentials
Username: Administrator | Password: p@SSword@123

SecurityGroupID
sg-0b6419cf94705289e

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Corrigir problema de recuperação de metadados do EC2
Pontos possíveis
56
Penalidade por pista
12
Pontos disponíveis
44
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Depois de habilitar com êxito o acesso RDP para determinada instância do EC2, conecte-se a ela e revise as rotas do Windows para qualquer rota capturada com IP de gateway inválido da rede anterior. Se sim, exclua a rota e adicione-a novamente com o endereço IP do gateway correto.

Sua tarefa
Sua tarefa é:

Conecte a instância EC2 fornecida via RDP.
Verifique se a instância pode recuperar os metadados da instância.
Corrija quaisquer problemas que causem falhas no acesso ao serviço de metadados da instância.
Começando
Conecte a instância do EC2 chamada Production-Server usando a conexão de desktop remoto.
Usando o PowerShell, execute o seguinte comando para verificar se os metadados da instância estão acessíveis a partir da instância:
PS > ** iwr -uri 'http://169.254.169.254/latest/meta-data/' **

A saída acima deve ser: ** StatusCode: 200 **

Verifique as rotas do Windows e corrija a rota de metadados se ela tiver uma entrada de endereço IP de gateway inválida.
Inventário
Instância do Amazon EC2 chamada Production-Server.
Para IDs de recursos, consulte a seção Propriedades de saída deste desafio.
Serviços que você deve usar
Nuvem de computação elástica da Amazon (Amazon EC2)
Validação de tarefas
Depois de se conectar à instância, você deve corrigir o acesso à rota de metadados da instância. Essa tarefa validará automaticamente a correção se a instância afetada conseguir recuperar os metadados da instância e, após a execução do comando do PowerShell, resultar em:

PS > ** iwr -uri 'http://169.254.169.254/latest/meta-data/' **

A saída acima deve ser: ** StatusCode : 200 **

** NOTE: ** Se depois de obter a saída acima, o progresso da tarefa não marcar essa tarefa como concluída, execute o seguinte comando no PowerShell:

PS > ** Restart-Service AmazonSSMAgent **

Aguarde 10 segundos e tente verificar seu progresso novamente pressionando o botãoVerificar meu progresso na tela de detalhes do desafio.

Pistas
Por onde começar a procurar se as coisas não estão se movendo?
5Pontos de penalidade
Ocultar pista
Verifique se a rota de metadados da instância EC2 169.254.169.254 está configurada corretamente.

PS > route print

Ok, estou preso! Qual é o caminho a seguir?
7Pontos de penalidade
Ocultar pista
SOLUÇÃO
Execute as seguintes etapas para concluir esta tarefa de desafio:

Etapa A | Conectar a instância EC2 afetada via RDP
Acesse EC2 Dashboard e selecioneInstâncias na guia de navegação à esquerda.
Na lista de instâncias do EC2 em execução, escolha a determinada instância do EC2 chamada Servidor de produção e o ID da instância fornecido na seção Propriedades de saída.
Depois de selecionar a instância do EC2, vá para a guia Detalhes na parte inferior e, na seção Resumo da instância, procure o valorEndereço IPv4 público.
Em sua máquina Windows de origem (para macOS, baixe o aplicativo Microsoft Remote Desktop na AppStore), pesquise por RDP ou Conexão de Área de Trabalho Remota e especifique o endereço públicoIPv4 no nome do computador e clique em Conectar.
Quando solicitadas as credenciais de login, digite o nome de usuário como Administrador e, para obter a senha, verifique a seção Propriedades de saída.
Etapa B | Adicionar rota de metadados com o gateway correto
Depois de se conectar à instância, abra o PowerShell com privilégios de administrador.
Execute os seguintes comandos um após o outro:
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
Depois de se conectar à instância, você deve corrigir o acesso à rota de metadados da instância. Essa tarefa validará automaticamente a correção se a instância afetada conseguir recuperar os metadados da instância e, após a execução do comando do PowerShell, resultar em:

PS > ** iwr -uri 'http://169.254.169.254/latest/meta-data/' **

A saída acima deve ser: ** StatusCode : 200 **

** NOTE: ** Se depois de obter a saída acima, o progresso da tarefa não marcar essa tarefa como concluída, execute o seguinte comando no PowerShell:

PS > ** Restart-Service AmazonSSMAgent **

Aguarde 10 segundos e tente verificar seu progresso novamente pressionando o botãoVerificar meu progresso na tela de detalhes do desafio.
```

meu terminar na ec2 com o RDP: usei as dicas antes eu estava tentando no terminar ai fui ver que era powershell tbm mas nem sei o que e route e etc, acho que tenho que aprender

```wasm
PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Install the latest PowerShell for new features and improvements! https://aka.ms/PSWindows

PS C:\Users\Administrator> iwr -url 'http://18.171.142.28/latest/meta-data'
Invoke-WebRequest : A parameter cannot be found that matches parameter name 'url'.
At line:1 char:5
+ iwr -url 'http://18.171.142.28/latest/meta-data'
+     ~~
    + CategoryInfo          : InvalidArgument: (:) [Invoke-WebRequest], ParameterBindingException
    + FullyQualifiedErrorId : NamedParameterNotFound,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

PS C:\Users\Administrator> iwr -uri 'http://18.171.142.28/latest/meta-data'
iwr : Unable to connect to the remote server
At line:1 char:1
+ iwr -uri 'http://18.171.142.28/latest/meta-data'
+ ~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebExc
   eption
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

PS C:\Users\Administrator> iwr -uri 'http://10.0.0.126/latest/meta-data'
iwr : Unable to connect to the remote server
At line:1 char:1
+ iwr -uri 'http://10.0.0.126/latest/meta-data'
+ ~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebExc
   eption
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

PS C:\Users\Administrator> route print
===========================================================================
Interface List
  8...06 10 57 15 5e b1 ......Amazon Elastic Network Adapter
  1...........................Software Loopback Interface 1
===========================================================================

IPv4 Route Table
===========================================================================
Active Routes:
Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0         10.0.0.1       10.0.0.126     20
         10.0.0.0    255.255.255.0         On-link        10.0.0.126    276
       10.0.0.126  255.255.255.255         On-link        10.0.0.126    276
       10.0.0.255  255.255.255.255         On-link        10.0.0.126    276
        127.0.0.0        255.0.0.0         On-link         127.0.0.1    331
        127.0.0.1  255.255.255.255         On-link         127.0.0.1    331
  127.255.255.255  255.255.255.255         On-link         127.0.0.1    331
  169.254.169.123  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.249  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.250  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.251  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.253  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.254  255.255.255.255  123.123.123.123       10.0.0.126     21
        224.0.0.0        240.0.0.0         On-link         127.0.0.1    331
        224.0.0.0        240.0.0.0         On-link        10.0.0.126    276
  255.255.255.255  255.255.255.255         On-link         127.0.0.1    331
  255.255.255.255  255.255.255.255         On-link        10.0.0.126    276
===========================================================================
Persistent Routes:
  None

IPv6 Route Table
===========================================================================
Active Routes:
 If Metric Network Destination      Gateway
  1    331 ::1/128                  On-link
  8     21 fd00:ec2::123/128        On-link
  8     21 fd00:ec2::250/128        On-link
  8     21 fd00:ec2::253/128        On-link
  8     21 fd00:ec2::254/128        On-link
  8    276 fe80::/64                On-link
  8    276 fe80::996e:77d5:a7c7:fab2/128
                                    On-link
  1    331 ff00::/8                 On-link
  8    276 ff00::/8                 On-link
===========================================================================
Persistent Routes:
  None
PS C:\Users\Administrator> route DELETE 169.254.169.254
 OK!
PS C:\Users\Administrator> route DELETE 169.254.169.258
The route deletion failed: The parameter is incorrect.

PS C:\Users\Administrator> route DELETE 169.254.169.254
The route deletion failed: Element not found.

PS C:\Users\Administrator> route -p ADD 169.524.169.254 MASK 255.255.255.255 10.0.0.1
The route addition failed: The parameter is incorrect.

PS C:\Users\Administrator> route -p ADD 169.254.169.254 MASK 255.255.255.255 10.0.0.1
 OK!
PS C:\Users\Administrator> route print
===========================================================================
Interface List
  8...06 10 57 15 5e b1 ......Amazon Elastic Network Adapter
  1...........................Software Loopback Interface 1
===========================================================================

IPv4 Route Table
===========================================================================
Active Routes:
Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0         10.0.0.1       10.0.0.126     20
         10.0.0.0    255.255.255.0         On-link        10.0.0.126    276
       10.0.0.126  255.255.255.255         On-link        10.0.0.126    276
       10.0.0.255  255.255.255.255         On-link        10.0.0.126    276
        127.0.0.0        255.0.0.0         On-link         127.0.0.1    331
        127.0.0.1  255.255.255.255         On-link         127.0.0.1    331
  127.255.255.255  255.255.255.255         On-link         127.0.0.1    331
  169.254.169.123  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.249  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.250  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.251  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.253  255.255.255.255         On-link        10.0.0.126     21
  169.254.169.254  255.255.255.255         10.0.0.1       10.0.0.126     21
        224.0.0.0        240.0.0.0         On-link         127.0.0.1    331
        224.0.0.0        240.0.0.0         On-link        10.0.0.126    276
  255.255.255.255  255.255.255.255         On-link         127.0.0.1    331
  255.255.255.255  255.255.255.255         On-link        10.0.0.126    276
===========================================================================
Persistent Routes:
  Network Address          Netmask  Gateway Address  Metric
  169.254.169.254  255.255.255.255         10.0.0.1       1
===========================================================================

IPv6 Route Table
===========================================================================
Active Routes:
 If Metric Network Destination      Gateway
  1    331 ::1/128                  On-link
  8     21 fd00:ec2::123/128        On-link
  8     21 fd00:ec2::250/128        On-link
  8     21 fd00:ec2::253/128        On-link
  8     21 fd00:ec2::254/128        On-link
  8    276 fe80::/64                On-link
  8    276 fe80::996e:77d5:a7c7:fab2/128
                                    On-link
  1    331 ff00::/8                 On-link
  8    276 ff00::/8                 On-link
===========================================================================
Persistent Routes:
  None
PS C:\Users\Administrator> iwr -uri 'http://18.171.142.28/latest/meta-data'
iwr : Unable to connect to the remote server
At line:1 char:1
+ iwr -uri 'http://18.171.142.28/latest/meta-data'
+ ~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebExc
   eption
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

PS C:\Users\Administrator> route -p ADD 169.254.169.254 MASK 255.255.255.255 10.0.0.147                                  OK!                                                                                                                    PS C:\Users\Administrator> iwr -uri 'http://18.171.142.28/latest/meta-data'                                             iwr : Unable to connect to the remote server                                                                            At line:1 char:1
+ iwr -uri 'http://18.171.142.28/latest/meta-data'
+ ~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebExc
   eption
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

PS C:\Users\Administrator> iwr -uri 'http://169.254.169.254/latest/meta-data'

Security Warning: Script Execution Risk
Invoke-WebRequest parses the content of the web page. Script code in the web page might be run when the page is
parsed.
      RECOMMENDED ACTION:
      Use the -UseBasicParsing switch to avoid script code execution.

      Do you want to continue?

[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Yy
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): yyYY
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y

StatusCode        : 200
StatusDescription : OK
Content           : ami-id
                    ami-launch-index
                    ami-manifest-path
                    block-device-mapping/
                    events/
                    hostname
                    iam/
                    identity-credentials/
                    instance-action
                    instance-id
                    instance-life-cycle
                    instance-type
                    local-hostname
                    local-ipv4
                    mac
                    ...
RawContent        : HTTP/1.1 200 OK
                    Connection: close
                    Accept-Ranges: none
                    Content-Length: 312
                    Content-Type: text/plain
                    Date: Sat, 06 Jun 2026 22:57:20 GMT
                    Last-Modified: Sat, 06 Jun 2026 22:26:38 GMT
                    Server: EC2ws...
Forms             : {}
Headers           : {[Connection, close], [Accept-Ranges, none], [Content-Length, 312], [Content-Type, text/plain]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : System.__ComObject
RawContentLength  : 312

PS C:\Users\Administrator> Restart-Service AmazonSSMAgent
WARNING: Waiting for service 'Amazon SSM Agent (AmazonSSMAgent)' to stop...
WARNING: Waiting for service 'Amazon SSM Agent (AmazonSSMAgent)' to stop...
WARNING: Waiting for service 'Amazon SSM Agent (AmazonSSMAgent)' to stop...
PS C:\Users\Administrator>
```

documantacao que usei:

[https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/instancedata-data-retrieval.html#instancedata-inside-access](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/instancedata-data-retrieval.html#instancedata-inside-access)

nao sabia como pegar os meta dados ainda nao sei mt bem achei que era so dara um curl no lastest-meta/data mas nao

esse mas nao ajudou:

[https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html)

esse pra entender um pouco o servico:

[https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/connect-rdp.html#configure-admin-accounts](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/connect-rdp.html#configure-admin-accounts)

ver com o claude dpa