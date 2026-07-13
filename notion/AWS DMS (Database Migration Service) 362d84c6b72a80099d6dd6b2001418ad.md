# AWS DMS (Database Migration Service)

Quando for PEQUENO poder ter DOWNTIME e for HOMOGENEO ⇒ MySQL-DUMP

Quando for GRANDE deve continuar rodando OU HETEROGENEO ⇒ DMS

DMS PODE FUNCIONAR EM PRODUCAO:

esse servico e para migracao, basicamente ele serve como um intermediador ate o RDS, que tem a permissao de ler seu banco on-promisses como se fosse um usuario, e replica para o banco RDS dentro da AMAZON

EX: On-promisses ⇒ Amazon DMS ⇒ RDS da AMAZON

- Se um banco e igual exemplo MySQL on-promisses e RDS on-promisses = HOMOGENEA
- Se o banco de dadps e diferente exemplo Oracle e RDS mySQL = HETEROGENEA

## Quais servicos usar se for heterogenea:

- 

para conversao:

- **É um serviço gerenciado de migração e replicação.**
- **Ajuda a mover workloads de banco de dados e analytics existentes para e dentro da AWS.**
- **É compatível com a maioria dos bancos de dados comerciais e de código aberto mais usados.**
- **Replica dados sob demanda ou de acordo com uma programação para replicar as alterações realizadas em uma origem.**

Como funciona:

![image.png](image%2079.png)

Ferramentas:

![image.png](image%2080.png)

![image.png](image%2081.png)

Exemplo do Schema Conversion Tool:

![image.png](image%2082.png)

Como funciona a replicacão de Dados:

![image.png](image%2083.png)

![image.png](image%2084.png)

i

Termos:

migracao homogenea exemplo:

mysql on-promisses ⇒ DMS ⇒ mysql RDS (tipos de dados iguais, migracao mais simples)