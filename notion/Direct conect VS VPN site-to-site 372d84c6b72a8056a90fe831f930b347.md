# Direct conect VS VPN site-to-site

direct conect e uma maneira de conectar um servidor on-promisses a os servicos da aws sem passsar pela internet, via CABO, do data center on-promisses ate o data certer da AWS

VIF: divisoes logicas

VIF Publico: servicos da aws como S3, dynamo que sao servicos fora de uma VPC

VIF Privado: servicoes de dentro de um VPC (EC2, Lambda, RDS)

VIF Transito: acessa varias VPC travez do Transit Gataway

VPN site-to-site: é uma meneira mais facil nao precisando de cabos, sendo uma maneira mais economica e mais idemeditava, usa um tunel criptografado 

Virtual Private Gataway: e basicamente a ponte que conecta o servico da aws e o o datacenter on-promisses