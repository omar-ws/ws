# VPC Flow Logs

anota o trafego de rede da VPC quem entrou quem saiu, de onde veio, para onde foi se foi aceito ou bloqueado pelo SG

- IP de origem e destino
- porta
- protocolo
- bytes transferidos
- Acao como ACCEPT ou REJECT

Você ativa no nível de VPC, subnet ou ENI, e manda os logs para o CloudWatch Logs ou S3.

usado mais para troubleshooting “por que minha ec2 nao consegue se conectar?”

seguranca “quem acessou?”

FERRAMENTAS PARA SOLUCAO DE PROBLEMAS DA VPC: