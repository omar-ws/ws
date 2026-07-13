# VPC e Proteção de Recursos de Rede

[Route 53](Route%2053%2037bd84c6b72a80a6afa2e6b5b1373248.md)

[Monitoramente](Monitoramente%2036dd84c6b72a80ba9ab4f6f020770261.md)

[Cognito + S3 WEB](Cognito%20+%20S3%20WEB%20379d84c6b72a80afa144e958599a3948.md)

[ELB](ELB%2036dd84c6b72a807daafbca28a10df088.md)

[AWS Network Firewall](AWS%20Network%20Firewall%20368d84c6b72a803aa186e572631edb2a.md)

[Well-Architected Framework](Well-Architected%20Framework%2036bd84c6b72a80d09b98db08f6e17e0e.md)

[VPC Endpoints](VPC%20Endpoints%20368d84c6b72a80fa96a3dd251664a349.md)

[Laboratorios](Laboratorios%2036dd84c6b72a80bdad21c2d967cebfa4.md)

## Infraestrutura fisica da AWS:

Nuvem AWS ⇒ Conta AWS ⇒ Região ⇒ AZ ⇒ Amazon VPC.

VPC:

pertence a uma regiao

funciona via CIDR

Enderenco IP-elastico:

ec2 ⇒ IP elastico ⇒ tabela de rotas publica ⇒ IGW

Sub-rede Publica ⇒ o que precisa ser acessado pela internet (ELB, Frontend)

Sub-rede Privada ⇒ o que nao deve ser exposto (Banco de Dados, processamento em lote, Back-end)

recome:serweb:subpriv

instancias de banco de dados ⇒ subrede privada

instancia de processamento em lote ⇒ subrede privada

instancia de aplicativos web ⇒ subrede porp

gataway ou instancia NAT ⇒ subrede publica

sg ⇒ nivel da instancia

acl ⇒ nivel da subrede

sg nao funciona acl

- exemplo (ACL):
    
    INBOUND:
    100 → permite porta 80
    
    - * → nega o resto
    
    OUTBOUND:
    100 → permite porta 80
    
    - * → nega o resto

complience=conformidade com regras, leis, normas, que uma empresa e obrigada a seguir, ex LGDP PSI HIPAA