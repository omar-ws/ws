# Migracao de banco de dados

comandos que usei:

sudo su = for root

su ec2-user = entrar como user da ec2

service mariadb status

mysqldump —databases cafe_db -uroot -p > CafeDbDump.sql

mysqldump —databases  -uroot -p > nome do arquivo final.sql

mysqldump ⇒ banco de dados menores

DMS ⇒ migrar sem downtime

Snow ⇒ para volumes gigantes (terabytes), manda o HD fisico para AWS

erro com o usuario ec2-user:

bash: CafeDbDump.sql permission denied

solucao, nao estava na pasta correta /home/ec2-user

## Se conectar com o banco de Dados em uma EC2

mysql -u (usuarioRDS) -p —host (endpoint rds)

sg de rds aceitando entrada da ec2

## Comando para scanear as postar

Nmap -Pn (ip or endpoint)

-Pn ignore ping e ve as portas mesmo assim

## Problema “ —require_secure_transport=ON”

resolucao: flag —ssl + —host (—ssl)

# Outras maneiras:

—ssl

—ssl-mode

—ssl-mode=REQUIRED

pense no > como uma seta

>envia                      <recebe

Para o banco de dados funcionar preciso trocar as variaveis do secret manager

## Variaveis do banco de dados

dburl = endpoint do banco de dados

dbname = nome do banco de dados

dbpassword = senha do RDS 

dbuser = usuario (admin, root)

TROCAR AS VARIAVEIS DO SECRET MANAGER

dbuser = de root para admin

dbpassword = antiga do on-promisses para o RDS

## Ver status de das aplicacoes:

sudo service (nameservice) status

sudo service (nameservico) restart

sudo service (nameservice) stop

sudo service (nameservice) start

EX: httpd, nginx

erros acess denios for admin geralmente:

senha errada 

dados nao importados