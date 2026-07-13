# AWS Network Firewall

e uma protecao adicional de subrede, adicionarmos mais um subrede apenas para ela:

IGW ⇒ subrede firewall ⇒ subrede publica

uma subnet firewall por AZ, ou seja, 3 az 1 firewall em cada uma

SG/NACL bloqueiam IPS especificos

Network Firewall bloqueia Url especificas (.maliciosos.com) padroes de trafego packet inspection

- E um firewall a nivel de VPC, fica na borda da VPC, ele consegue:
- Inspecional conteudo de pacote
- Bloquear dominios especificos (SITES MALICIOSOS)
- Detectar padroes de ataque (IDS/IPS)
- Filtrar por protocolo de forma mais granular

Anunciado: 

Inspecao de trafego

IDS/IPS

Bloquear dominios maliciosos

caminho:

interenet ⇒ network firewall ⇒ subnets ⇒ ec2