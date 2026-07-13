# JAM Negar ataques externos a partir do IPv6

visao geral:

```jsx
Recentemente, você ingressou na ABC Corp como especialista em redes para trabalhar em um novo aplicativo usando o Amazon EC2 e o Amazon VPC. No entanto, você herdou desafios de um ex-funcionário que saiu repentinamente. Um grande problema é o risco de segurança em uma instância do EC2 em uma VPC habilitada para IPv6. Essa instância tem um endereço IPv6 público, o que a torna exposta à Internet por padrão, já que os endereços IPv6 podem ser acessados publicamente mesmo sem atribuir um IP elástico ou configurar um IP público. Para aumentar a segurança, o tráfego de entrada precisa ser bloqueado enquanto somente o tráfego de saída IPv6 permanece aberto.
```

task 1:

```jsx
Tarefa 1: Bloqueie o tráfego de entrada!
Pontos possíveis
80
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Recentemente, você ingressou na ABC Corp como especialista em redes, assumindo a infraestrutura da AWS de um ex-funcionário que saiu repentinamente. Durante sua auditoria de segurança inicial, você descobriu um problema crítico de segurança: uma instância do EC2 na VPC AWS-JAM-FixIPv6 tem acesso público irrestrito via IPv6, criando um risco de segurança significativo.

Tarefa
A equipe de segurança alertou você sobre esse problema e solicitou que você implementasse uma solução abrangente de segurança IPv6 que:

Bloqueia todo o acesso IPv6 público de entrada à instância para mitigar o risco imediato de segurança
Mantém a capacidade da instância de iniciar conexões de saída com a Internet via IPv6
Devido aos requisitos de otimização de custos, o uso do gateway NAT ou da instância NAT não é permitido. Você precisará encontrar uma solução alternativa que permita o tráfego IPv6 de saída e, ao mesmo tempo, bloqueie as conexões de entrada.

Inventário
Os seguintes serviços são provisionados:

Amazon EC2
Amazon VPC
Componentes de rede
Começando
Antes de fazer qualquer alteração, você deve verificar se a porta 3389 (RDP) está aberta atualmente no endereço IPv6 da instância. Você pode fazer isso de várias maneiras:

Use uma ferramenta de verificação de portas on-line:
Visite https://portchecker.co/
Insira o endereço IPv6 e a porta 3389 da instância
Clique em “Verificar” para ver se a porta está aberta
Use o telnet da sua máquina local (se você tiver conectividade IPv6):
Abra um prompt de comando ou terminal
Tipo: telnet [IPv6_address] 3389
Se você conseguir uma conexão, a porta estará aberta
Tente uma conexão RDP:
Use um cliente RDP que ofereça suporte a IPv6
Tente se conectar ao endereço IPv6 da instância
Depois de verificar se a porta 3389 está aberta, continue com a tarefa de bloquear o acesso público IPv6 de entrada e, ao mesmo tempo, manter a conectividade de saída com a Internet IPv6 usando configurações de roteamento de rede.

Serviço que você deve usar
Amazon EC2
Amazon VPC
Validação de tarefas
Depois de implementar a solução de restrição de tráfego de entrada e conectividade de saída, clique em verificar progresso para validar a segurança da rede. A validação verificará se:

A instância não está mais acessível por meio de endereços IPv6 públicos
A instância ainda pode acessar a Internet via IPv6 para conexões de saída.
```

nao conhecia muit bem esse servico, mas configurei suber rapido quando compreendi com a IA, pois nao sabia que existia um servico para isso