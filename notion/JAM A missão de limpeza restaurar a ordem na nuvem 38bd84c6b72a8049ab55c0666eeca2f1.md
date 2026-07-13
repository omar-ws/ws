# JAM A missão de limpeza: restaurar a ordem na nuvem (FACIL)

esse foi manteiga

visao geral:

```jsx
Na cidade de alta tecnologia de CloudHaven, onde a infraestrutura digital é a espinha dorsal de todas as operações, você é Jordan, um talentoso engenheiro de nuvem da AWS na TechSphere Inc., uma empresa conhecida por suas soluções inovadoras e de tecnologia de ponta.

Recentemente, surgiu um problema que ameaça a segurança e a economia do ambiente AWS da TechSphere. Um ex-colega, Alex, criou vários recursos da AWS usando pilhas do CloudFormation, especificando o atributo da política de exclusão como “retenção” para alguns recursos essenciais. Antes de deixar a empresa, Alex excluiu as pilhas do CloudFormation, deixando um rastro de recursos órfãos.

Esses recursos persistentes, identificados como riscos de segurança e possíveis passivos de custo, resistiram aos esforços automatizados de limpeza devido a dependências complexas. Agora, Jordan recebeu uma missão crítica: identificar e excluir manualmente esses recursos retidos, garantindo que a conta da AWS esteja segura e econômica novamente.
```

task 1:

```jsx
Antecedentes
Alex, ex-colega, tinha vários requisitos de **Amazon Virtual Private Cloud (Amazon VPC) ** com comunicação bidirecional habilitada via conexão de emparelhamento VPC para seu projeto. Eles queriam manter a VPC, portanto, ao criar os recursos usando a pilha do CloudFormation, eles definiram a Política de exclusão como Retain para alguns dos recursos. Uma vez que concluíram o projeto, mas se esqueceram de excluir os recursos retidos antes de saírem da empresa. Esses recursos persistentes, identificados como riscos de segurança e possíveis passivos de custo, resistiram aos esforços automatizados de limpeza devido a dependências complexas. Agora, Jordan recebeu a tarefa de identificar e excluir manualmente esses recursos retidos, garantindo que a conta da AWS esteja segura e econômica novamente.

Sua tarefa
Como Jordan, sua tarefa é excluir a VPC emparelhada que Alex criou. Ao realizar a limpeza da VPC, você pode se deparar com um erro de dependência que precisa resolver e, eventualmente, continuar excluindo a VPC.

Começando
Acesse o Console de gerenciamento da AWS | VPC > Suas VPCs.
Procure VPC que tenha sido identificada e marcada para exclusão, consulte a seçãoInventário para verificar seus IDs de recursos.
Continue selecionando as VPCs em questão e exclua-as.
Inventário
Nuvem privada virtual da Amazon (Amazon VPC)
VPC-A-marked-for-deletion consulte Propriedades de saída para obter o ID.
VPC-B-marked-for-deletion consulte Propriedades de saída para obter o ID.
Gateway de Internet
Interfaces de rede
Gateway NAT
Conexão de emparelhamento VPC
Serviços que você deve usar
Nuvem privada virtual da Amazon (Amazon VPC)
Validação de tarefas
A tarefa será concluída automaticamente quando você excluir as VPCs em questão. Além disso, você sempre pode verificar seu avance pressionando o botãoVerificar meu progresso na tela de detalhes do desafio.

Pistas
Algumas dicas, por favor!
4Pontos de penalidade
Desbloqueie o Clue
Ok, me ajude com mais dicas.
5Pontos de penalidade
Desbloqueie o Clue
```

task 2:

```jsx
Tarefa 2: Ainda existe um Grupo de Segurança remanescente
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Após a exclusão bem-sucedida da VPC emparelhada, Jordan é informada sobre umGrupo de segurança que faz parte de outro ambiente de VPC de produção e não é mais necessário, portanto, precisa ser removido. Jordan recebeu as informações sobre o identificador de recursos e solicitou que excluísse o grupo de segurança remanescente.

Sua tarefa
Como Jordan, sua tarefa é excluir o Grupo de Segurança remanescente. Ao realizar a limpeza do Grupo de Segurança, você pode encontrar um erro de dependência que precisa resolver e, eventualmente, prosseguir com a exclusão do Grupo de Segurança.

Começando
Acesse o Console de gerenciamento da AWS | VPC > Rede e Segurança > Grupo de segurança
Procure o Grupo de Segurança que foi identificado e marcado para exclusão, consulte a seçãoInventário para verificar a ID do recurso.
Selecione o Grupo de Segurança em questão e exclua-o.
Inventário
Nuvem privada virtual da Amazon (Amazon VPC)
Grupo de segurança chamado Production-SG-Marked-for-deletion, consulte a seção Propriedades de saída para obter o ID do recurso.
Interfaces de rede
Instância Amazon EC2
Serviços que você deve usar
Nuvem privada virtual da Amazon (Amazon VPC)
Nuvem de computação elástica da Amazon (Amazon EC2)
Validação de tarefas
A tarefa será concluída automaticamente quando você excluir o Grupo de Segurança em questão. Além disso, você sempre pode verificar seu progresso pressionando o botãoVerificar meu progresso na tela de detalhes do desafio.

Pistas
Preso! Posso dar uma dica, por favor?
4Pontos de penalidade
Desbloqueie o Clue
As coisas estão saindo do controle. Ah! Eu preciso de dicas.
5Pontos de penalidade
Desbloqueie o Clue
```