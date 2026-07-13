# VPC Peering vs VPC Transit Gataway

como usar vpc peering:

VPC peering: criar Conexoes de Emparelhamento ⇒ aceitar (acoes ⇒ aceitar) ⇒ colocar destina da tabela de rotas ⇒ (Conexao de emparelhamento PCX-XXXX) ⇒ configurado.

como ativar logs de fluxo:

usar apenas um NAT gataway

```jsx
Solução — NAT Gateway centralizado:
  VPC 1 ──┐
  VPC 2 ──┼──→ Transit Gateway ──→ VPC Central ──→ NAT Gateway ──→ internet
  VPC 3 ──┘
```

no final das contas, por que usar? comunicacao internet, por exemplo que acessar uma instancia privada que esta na minha VPC 2 e estou na VPC 1, eu adiciono um VPC pering e na rota da subrede privada eu configuro, com isso consigo acessar minha instancia sem acesso a internet e de forma segura

## VPC Peering:

VPC paring conversa com VPC especifica

A⇒B bi-direcional, porem nao consegue falar com C, exemplo A⇒B⇒C (A nao fala com C)

## VPC Transit Gataway

VPC Transit Gataway tem um HUB, ou seja todas as VPCs se comunicam entre si

A⇒ hub ⇒ B ⇒ hub ⇒ D ⇒ hub ⇒ A