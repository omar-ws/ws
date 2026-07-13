# RDS Tradicional (MySQL, PostgreeSQL, SQL Server, Oracle)

# (So faca o que o anunciado pedir)

single-AZ se nao pedir “tolerancia a falhas, altamente disponivel, sem intervencao manual, resiliencia contra desestres naturais”

Database (banco de dados)
     └── Table (tabela)
             └── Columns (colunas)  ← estrutura/esquema
                      └── Rows (linhas)  ← os dados em si

****é tipo um computador comum rodando o banco****

| Mult-AZ | Opcional | Manualmente |
| --- | --- | --- |
| Replicas de Leitura | Opcional | P/ aliviar consultas, replica em cascata |
| FailOver | 60 a 120s |  |

Para adicionar outro banco relacional tradicional multi-AZ voce deve apenas mudar a configuracao:

Modify>caixa:Multi-AZ deployment e salva.

(a AWS ja cria e sincroniza).

## EXEMPLO DE CONSULTA COMPLEXA:

JOIN (juntar)= combina duas tabelas em uma so

consulta complexa: buscar dados cruzados em varias tabelas ao mesmo tempo.

![image.png](image%2051.png)

como criar uma maquina RDS com disponibilidade RDS 

1. cria o RDS Master
2. botao sim/nao deplyment options (criar ums instancia de bancos de dados Multi AZ)

Um banco RDS tradicional o banco reserva (standby) nao serve para leitura como o AURORA faz (serve mais para se a AZ principal cair, ainda esteja disponivel) FAILOVER

MULTI-AZ SERVE PARA SEGURANCA E UPGRADE SEM QUEDAS LONGAS

NO AURORA AS RESERVAS SAO ATIVAS PARA LEITURAS MESMO COM A MUDANCA

# CRIACAO DO RDS (MySQL):

UM PRECISA DO OUTRO: ⇒

grupo de sub-redes: VOCE PERMITE PARA A AWS QUE ELA CRIE UMA INSTANCIA NA ZONA QUE VOCE COLOCOU
opçoes de implementacao (ex: single-AZ): VOCE QUER PAGAR POR MAIS DE UMA INSTANCIA?

Single-AZ: Uma unica instancia (MASTER)

Multi-AZ:Cria copias (MASTER/STANDBY)

![image.png](image%2052.png)

A AWS escolher onde a instancia MASTER ficara:

Nome do banco de dados:                                                        Nome do primeiro Databases:

![image.png](image%2053.png)

Adicionar isso para ter isso:

![image.png](image%2054.png)

![image.png](image%2055.png)

![image.png](image%2056.png)

## Se o Banco de dados nao esta criptografato e ja foi criado faz tempo faca:

1. tirar snapshot
2. copiar o snapshot e durante a copiar clicar na caixinha “Enable Encryption”
3. Clica no Snapshot novo e clica em “Restore” para criar ums intanci nova

Criado com o “Habilitar criptografia’ ja funciona em repouco e em Transito ja vem pronto.

como funciona a descriptografia com o dado criptografado:

![image.png](image%2057.png)

criar um snapshot da instancia:

1. dados do banco de dados
2. aba Manutencao de Backups

o Banco nao fica indiponivel com backup, geralmente em producao voce faz o backup do standby (copia que no caso do RDS tradicional so recebe leitura)

VPC security group e o crupo de seguranca do RDS