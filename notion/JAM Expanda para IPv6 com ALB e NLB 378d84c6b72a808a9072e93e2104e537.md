# JAM Expanda para IPv6 com ALB e NLB

task 1:

```wasm
Expanda para IPv6 com ALB e NLB
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 1: Tipo de endereço IP ALB: dualstack
Pontos possíveis
16
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Seu aplicativo usa o Application Load Balancer (ALB). O ALB chamado Jam-ALB foi criado com o tipo de endereço IP IPv4.

! <a href=” https://aws-jam-challenge-resources.s3.amazonaws.com/ipv-6-alb-nlb/1.0.0/JamArchitecture-Task1.png “ALB IPv4 IP address type"">Tipo de endereço IP IPv4 ALB

Começando
Seu cliente só pode acessar seu aplicativo usando IPv4. Com o IPv6, ele falha.

Você foi solicitado a garantir que seu ALB ofereça suporte a IPv4 e IPv6. Assim, o cliente pode enviar a solicitação com as duas versões IP. Todo o resto já está preparado para que seu ALB também funcione com IPv6, conforme definido nos requisitos de pilha dupla.

Inventário
Dentro desse ambiente, existem:

Um Application Load Balancer (ALB) chamado Jam-ALB.
Serviços que você deve usar
ALB

Sua tarefa
Altere o ALB chamado Jam-ALB para usar o tipo de endereço IP dualstack
Lembre-se: os balanceadores de carga pertencem ao console do EC2.

Você não precisa alterar mais nada, apenas o tipo de endereço IP.

Validação de tarefas
A tarefa será concluída automaticamente quando você realizar a alteração do tipo de endereço IP do ALB. Como alternativa, você sempre pode verificar seu progresso pressionando o botão Check my progress na tela de detalhes do desafio.

Pistas
Detalhes do balanceador de carga
1Pontos de penalidade
Desbloqueie o Clue
Descrição
2Pontos de penalidade
Desbloqueie o Clue
```

task 2:

```wasm
Expanda para IPv6 com ALB e NLB
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 2: Posso usar o IPv4 somente como alvo do meu ALB?
Pontos possíveis
12
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Seu aplicativo usa o Application Load Balancer (ALB). O ALB chamado Jam-ALB está configurado no modo dualstack.

! <a href=” https://aws-jam-challenge-resources.s3.amazonaws.com/ipv-6-alb-nlb/1.0.0/JamArchitecture-Task2.png “ALB IPv4 only target"">Alvo somente IPv4 do ALB

Começando
Você foi solicitado a garantir que seu ALB ofereça suporte a destinos executados com IPv4 em sub-rede somente IPv4.

Inventário
Dentro desse ambiente, existem:

Um Application Load Balancer (ALB) chamado Jam-ALB.
Um grupo-alvo de balanceador de carga chamado Jam-ALB-IPv4-Only
Você pode encontrar o comando curl para testar seu grupo-alvo disponível em Propriedades de saída à esquerda.

O comando de teste ALB IPv4 é chamado Task2IPv4Command.
O comando de teste ALB IPv6 é chamado Task2IPv6Command.
Serviços que você deve usar
ALB

Sua tarefa
Altere o ALB chamado Jam-ALB para usar o grupo-alvo chamado Jam-ALB-IPv4-Only
Conecte-se em uma instância do EC2 chamada Jam-Instance-Test usando o Gerenciador de Sessões
No console Linux, faça a solicitação curl usando IPv4
No console Linux, faça a solicitação curl usando IPv6
Lembre-se: os balanceadores de carga pertencem ao console EC2.

⚠ 👁 Atenção!
Pode levar algum tempo após você alterar o Load Balancer para usar o novo grupo-alvo. Aguarde até 3 minutos para que a alteração seja aplicada e propagada. O Load Balancer ainda pode apontar para o antigo grupo-alvo até que ele seja aplicado!

Você notará que pode acessar seu ALB configurado com o grupo-alvo que responde somente em IPv4 (grupo-alvo Jam-ALB-IPv4-Only), mesmo quando você acessa por meio de IPv6. A ALB é responsável por “traduzir” a comunicação entre IPv4 e IPv6.

O balanceador de carga se comunica com os destinos com base no tipo de endereço IP do grupo de destino.

Validação de tarefas
A tarefa será concluída automaticamente quando você executar a solicitação curl usando IPv4 e IPv6. Como alternativa, você sempre pode verificar seu progresso pressionando o botão Check my progress na tela de detalhes do desafio.

Pistas
Grupo alvo do balanceador de carga
1Pontos de penalidade
Desbloqueie o Clue
Descrição
1Pontos de penalidade
Desbloqueie o Clue
```

task 3:

```wasm
Expanda para IPv6 com ALB e NLB
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 3: Posso usar o IPv6 somente como alvo do meu ALB?
Pontos possíveis
12
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Seu aplicativo usa o Application Load Balancer (ALB). O ALB chamado Jam-ALB está configurado no modo dualstack.

! <a href=” https://aws-jam-challenge-resources.s3.amazonaws.com/ipv-6-alb-nlb/1.0.0/JamArchitecture-Task3.png “ALB IPv6 only target"">Alvo somente IPv6 do ALB

Começando
Você foi solicitado a garantir que seu ALB ofereça suporte a destinos executados com IPv6 em uma sub-rede somente IPv6.

Inventário
Dentro desse ambiente, existem:

Um Application Load Balancer (ALB) chamado Jam-ALB.
Um grupo-alvo de balanceador de carga chamado Jam-ALB-IPv6-Only
Você pode encontrar o comando curl para testar seu grupo-alvo disponível em Propriedades de saída à esquerda.

O comando de teste ALB IPv4 é chamado Task3IPv4Command.
O comando de teste ALB IPv6 é chamado Task3IPv6Command.
Serviços que você deve usar
ALB

Sua tarefa
Altere o ALB chamado Jam-ALB para usar o grupo-alvo chamado Jam-ALB-IPv6-Only
Conecte-se em uma instância do EC2 chamada Jam-Instance-Test usando o Gerenciador de Sessões
No console Linux, faça a solicitação curl usando IPv4
No console Linux, faça a solicitação curl usando IPv6
Lembre-se: os balanceadores de carga pertencem ao console do EC2.

⚠ 👁 Atenção!
Pode levar algum tempo após você alterar o Load Balancer para usar o novo grupo-alvo. Aguarde até 3 minutos para que a alteração seja aplicada e propagada. O Load Balancer ainda pode apontar para o antigo grupo-alvo até que ele seja aplicado!

Você notará que pode acessar seu ALB configurado com o grupo-alvo que responde somente em IPv6 (grupo-alvo Jam-ALB-IPv6-Only), mesmo quando você acessa por meio de IPv4. A ALB é responsável por “traduzir” a comunicação entre IPv4 e IPv6.

O balanceador de carga se comunica com os destinos com base no tipo de endereço IP do grupo de destino.

Validação de tarefas
A tarefa será concluída automaticamente quando você executar a solicitação curl usando IPv4 e IPv6. Como alternativa, você sempre pode verificar seu progresso pressionando o botão Check my progress na tela de detalhes do desafio.

Pistas
Grupo alvo do balanceador de carga
1Pontos de penalidade
Desbloqueie o Clue
Descrição
1Pontos de penalidade
Desbloqueie o Clue
```

task 4:

```wasm
Expanda para IPv6 com ALB e NLB
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 4: Tipo de endereço IP NLB: dualstack
Pontos possíveis
16
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Seu aplicativo usa o Network Load Balancer (NLB). O NLB chamado Jam-NLB foi criado com o tipo de endereço IP IPv4.

! <a href=” https://aws-jam-challenge-resources.s3.amazonaws.com/ipv-6-alb-nlb/1.0.0/JamArchitecture-Task4.png “NLB IPv4 IP address type"">Tipo de endereço IP IPv4 NLB

Começando
Seu cliente só pode acessar seu aplicativo usando IPv4. Com o IPv6, ele falha.

Você foi solicitado a se certificar de que seu NLB oferece suporte a IPv4 e IPv6. Assim, o cliente pode enviar a solicitação com as duas versões IP. Todo o resto já está preparado para que seu NLB funcione também com IPv6, conforme definido nos requisitos de pilha dupla.

Inventário
Dentro desse ambiente, existem:

Um Network Load Balancer (NLB) chamado Jam-NLB.
Serviços que você deve usar
NLB

Sua tarefa
Altere o NLB chamado Jam-NLB para usar o tipo de endereço IP dualstack
Lembre-se: os balanceadores de carga pertencem ao console EC2.

Você não precisa alterar mais nada, apenas o tipo de endereço IP.

Validação de tarefas
A tarefa será concluída automaticamente quando você realizar a alteração do tipo de endereço IP do NLB. Como alternativa, você sempre pode verificar seu progresso pressionando o botão Check my progress na tela de detalhes do desafio.

Pistas
Detalhes do balanceador de carga
1Pontos de penalidade
Desbloqueie o Clue
Descrição
2Pontos de penalidade
Desbloqueie o Clue
```

task 5:

```wasm
Expanda para IPv6 com ALB e NLB
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 5: Posso usar IPv4 somente como destino para meu NLB?
Pontos possíveis
12
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Seu aplicativo usa o Network Load Balancer (NLB). O NLB chamado Jam-NLB está configurado no modo de pilha dupla.

! <a href=” https://aws-jam-challenge-resources.s3.amazonaws.com/ipv-6-alb-nlb/1.0.0/JamArchitecture-Task5.png “NLB IPv4 only target"">Alvo somente IPv4 do NLB

Começando
Você foi solicitado a garantir que seu NLB ofereça suporte a destinos executados com IPv4 em uma sub-rede somente IPv4.

Inventário
Dentro desse ambiente, existem:

Um Network Load Balancer (NLB) chamado Jam-NLB.
Um grupo-alvo de balanceador de carga chamado Jam-NLB-IPv4-Only
Você pode encontrar o comando curl para testar seu grupo-alvo disponível em Propriedades de saída à esquerda.

O comando de teste IPv4 do NLB é chamado Task5IPv4Command.
O comando de teste IPv6 do NLB é chamado Task5IPv6Command.
Serviços que você deve usar
NLB

Sua tarefa
Altere o NLB chamado Jam-NLB para usar o grupo-alvo chamado Jam-NLB-IPv4-Only
Conecte-se em uma instância do EC2 chamada Jam-Instance-Test usando o Gerenciador de Sessões
No console Linux, faça a solicitação curl usando IPv4
No console Linux, faça a solicitação curl usando IPv6
Lembre-se: os balanceadores de carga pertencem ao console do EC2.

⚠ 👁 Atenção!
Pode levar algum tempo após você alterar o Load Balancer para usar o novo grupo-alvo. Aguarde até 3 minutos para que a alteração seja aplicada e propagada. O Load Balancer ainda pode apontar para o antigo grupo-alvo até que ele seja aplicado!

Você notará que pode acessar seu NLB configurado com o grupo-alvo que responde somente em IPv4 (grupo-alvo Jam-NLB-IPv4-Only), mesmo quando você acessa por meio de IPv6. O NLB é responsável por “traduzir” a comunicação entre IPv4 e IPv6.

O balanceador de carga se comunica com os destinos com base no tipo de endereço IP do grupo de destino.

Validação de tarefas
A tarefa será concluída automaticamente quando você executar a solicitação curl usando IPv4 e IPv6. Como alternativa, você sempre pode verificar seu progresso pressionando o botão Check my progress na tela de detalhes do desafio.

Pistas
Grupo alvo do balanceador de carga
1Pontos de penalidade
Desbloqueie o Clue
Descrição
1Pontos de penalidade
Desbloqueie o Clue
```

task 6:

```wasm
Expanda para IPv6 com ALB e NLB
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 6: Posso usar o IPv6 somente como destino para meu NLB?
Pontos possíveis
12
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Seu aplicativo usa o Network Load Balancer (NLB). O NLB chamado Jam-NLB está configurado no modo de pilha dupla.

! <a href=” https://aws-jam-challenge-resources.s3.amazonaws.com/ipv-6-alb-nlb/1.0.0/JamArchitecture-Task6.png “NLB IPv6 only target"">Destino somente IPv6 do NLB

Começando
Você foi solicitado a garantir que seu NLB ofereça suporte a destinos executados com IPv6 em uma sub-rede somente IPv6.

Inventário
Dentro desse ambiente, existem:

Um Network Load Balancer (NLB) chamado Jam-NLB.
Um grupo-alvo de balanceador de carga chamado Jam-NLB-IPv6-Only
Você pode encontrar o comando curl para testar seu grupo-alvo disponível em Propriedades de saída à esquerda.

O comando de teste IPv4 do NLB é chamado Task6IPv4Command.
O comando de teste IPv6 do NLB é chamado Task6IPv6Command.
Serviços que você deve usar
NLB

Sua tarefa
Altere o NLB chamado Jam-NLB para usar o grupo-alvo chamado Jam-NLB-IPv6-Only
Conecte-se em uma instância do EC2 chamada Jam-Instance-Test usando o Gerenciador de Sessões
No console Linux, faça a solicitação curl usando IPv4
No console Linux, faça a solicitação curl usando IPv6
Lembre-se: os balanceadores de carga pertencem ao console EC2.

⚠ 👁 Atenção!
Pode levar algum tempo após você alterar o Load Balancer para usar o novo grupo-alvo. Aguarde até 3 minutos para que a alteração seja aplicada e propagada. O Load Balancer ainda pode apontar para o antigo grupo-alvo até que ele seja aplicado!

Você notará que pode acessar seu NLB configurado com o grupo-alvo que responde somente em IPv6 (grupo-alvo Jam-NLB-IPv6-Only), mesmo quando você acessa por meio de IPv4. O NLB é responsável por “traduzir” a comunicação entre IPv4 e IPv6.

O balanceador de carga se comunica com os destinos com base no tipo de endereço IP do grupo de destino.

Validação de tarefas
A tarefa será concluída automaticamente quando você executar a solicitação curl usando IPv4 e IPv6. Como alternativa, você sempre pode verificar seu progresso pressionando o botão Check my progress na tela de detalhes do desafio.

Pistas
Grupo alvo do balanceador de carga
1Pontos de penalidade
Desbloqueie o Clue
Descrição
1Pontos de penalidade
Desbloqueie o Clue
```

[https://docs.aws.amazon.com/pt_br/elasticloadbalancing/latest/application/application-load-balancers.html#ip-address-type](https://docs.aws.amazon.com/pt_br/elasticloadbalancing/latest/application/application-load-balancers.html#ip-address-type)