# JAM ARM64 seus bancos de dados

VISAO GERAK

```jsx
Você é engenheiro de nuvem na Unicorn Company, que usa a AWS para seu site essencial de aluguel de unicórnios.

Seu cliente tem o objetivo de reduzir os custos operacionais. Seu gerente desafiou você a reduzir os custos de seus bancos de dados que atualmente são executados no Amazon RDS. Seus bancos de dados são usados intensamente em todos os momentos, portanto, qualquer alteração deve envolver um tempo mínimo de inatividade.

Você analisou os preços do RDS e percebeu que as instâncias Graviton poderiam economizar custos com a mesma quantidade de CPU e memória. Você não tem certeza se pode adotar essas instâncias em seu ambiente com segurança.

Você também consultou sua equipe de CCOE, que administra suas políticas de controle de serviços do AWS Organizations, e eles confirmam que as instâncias do Graviton2 são permitidas. As instâncias de Graviton3 (por exemplo, r7g) ainda não foram permitidas.

Esse desafio será resolvido usando o console da AWS
```

task 1 e 2 e 3 e 4

```jsx
Plano de fundo
Em sua pesquisa, você descobriu que as instâncias do Graviton são suportadas apenas em versões específicas do motor. Você deve verificar se o mecanismo de banco de dados atual que você usa é compatível com instâncias de graviton. Você precisará atualizar o motor se o Graviton não for suportado.

Sua tarefa
Obtenha a versão atual do mecanismo que está sendo usada para verificar se ela está na lista de bancos de dados suportados

Inventário
Um cluster Amazon Aurora RDS pré-provisionado - Veja as propriedades de saída
Serviços que você deve usar
Amazon RDS
Validação de tarefas
Insira o número da versão do motor na caixa Resposta, que será validada

task 2
Plano de fundo
O processo de Controle de Mudanças em sua organização estipula que um método de reversão deve estar em vigor antes de iniciar as mudanças. Caso o processo de modificação cause um problema, você precisa ter um backup para ativar a reversão.

Sua tarefa
Crie um backup do banco de dados, que pode ser restaurado, se necessário

Inventário
Um cluster Amazon Aurora RDS pré-provisionado - Veja as propriedades de saída
Serviços que você deve usar
Amazon RDS
Validação de tarefas
Essa tarefa será concluída automaticamente. Clique em Verificar meu progresso para acionar a tarefa de validação

task 3
Plano de fundo
Você está pronto para alterar sua primeira instância de banco de dados. Você foi autorizado a alterar o tipo de instância, desde que não haja impacto na criação de aplicativos. Seu gerente também lembra que você não deve aumentar ou diminuir o número de CPUs ou a quantidade de memória atribuída.

Sua tarefa
Modifique uma das instâncias para usar CPUs Graviton

Inventário
Um cluster Amazon Aurora RDS pré-provisionado - Veja as propriedades de saída
Serviços que você deve usar
Amazon RDS
Validação de tarefas
Essa tarefa será concluída automaticamente. Clique em Verificar meu progresso para acionar a tarefa de validação

task 4
Plano de fundo
Agora você tem uma instância do Graviton como parte do seu cluster Amazon Aurora. A equipe de aplicativos relatou que as operações de leitura no endpoint do leitor estão funcionando conforme o esperado e agora querem testar as operações de gravação. É importante que as operações de gravação sejam testadas no Graviton, mas possam ser imediatamente revertidas para x86 se houver algum problema

Sua tarefa
Reconfigure o cluster Amazon Aurora para que as operações de gravação sejam atendidas pela sua instância do Graviton

Inventário
Um cluster Amazon Aurora RDS pré-provisionado - Veja as propriedades de saída
Serviços que você deve usar
Amazon RDS
Validação de tarefas
Essa tarefa será concluída automaticamente. Clique em Verificar meu progresso para acionar a tarefa de validação
```

a