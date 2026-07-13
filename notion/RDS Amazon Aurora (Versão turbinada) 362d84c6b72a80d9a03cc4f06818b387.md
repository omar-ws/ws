# RDS Amazon Aurora (Versão turbinada)

AMAZON AURORA SERVELESS: escala CPU sozinho e memoria.

AMAZON AURORA PROVISIONADO: escala apenas memoria sozinho, a troca e manual. (ACU’s)

# Estrutura:

Database (banco de dados)
     └── Table (tabela)
              └── Columns (colunas)  ← estrutura/esquema
                       └── Rows (linhas)  ← os dados em si

AURORA NORMAL OU AURORA SERVELESS?

AURORA NORMAL: 24/7. PAGA O TEMPO TODO. VELOCIDADE IMEDIATA SEMPRE. (QUANDO USAR?) APP EM PRODUCAO COM TRAFEGO CONSTANTE

AURORA SERVELESS: LIGA SO QUANDO TEM REQUISICAO. PAGA PELO USO. PODE TER COLDSTART (ALGUNS SEGUNDOS PARA USAR)  (QUANDO USAR?) APP INTERNO, DEV/TEST. TRAFEGO IMPREVISIVEL

Serveless = muda de forma automatica com a aplicacao

serveless v2 otimo para picos

provisionado mais barato, indicado para apliacoes estaveis

![image.png](image%2058.png)

| Mult-AZ | Nativo. Sempre grava 6 copias de dados espalhados em 3 AZ diferentes | Automaticamente |
| --- | --- | --- |
| Replicas de Leitura | Foco em Performance e Velocidade (tira o peso das consultas da maquina principal) | Automaticamente |
| FailOver | 30s |  |

As outras instancias ajudam na leitura, no select

ex 

![image.png](image%2059.png)

leitura vai para as copias

escrita vai para a MASTER

Dados transacionais sao dados que sao criticos e precisam de ordem para fucionar exemplo em um banco de dinheiro, precisa debitar ⇒ enviar ⇒ chegar se um nao acontencer nao acontece nada gracas ao ACID 

no RDS o aumento de CPU/RAM e vertical

para trocar o tipo da instancia sempre entenda se ela ta usando mais CPU ou mais RAM
**APRENDER SOBRE COMPONENTES DE UM PC ENTENDER HARDWARE E COMO ESCOLHER OS TIPOS**

failover = acao de mudar para o reserva

rto = tempo que demora par essa troca

escabilidade = capacidade de crescer com a demanda

desempenho= velocidade e eficiencia

failover = garante que continue funcionando mesmo em caso de falha

o amazon RDS aurora fica disponivel para leitura mesmo off diferente dos RDS normais que ficam off

Quando troca o tipo de instancia a maquina antiga vira reserva no AURORA, tem um tempo de failover de 30 segundos

Quando escolher o serveless v1 e o serveless v2?

![image.png](image%2060.png)

PARA PRODUCAO:

NORMAL = TRAFEGO CONSTANTE

V2 = TRAFEGO IRREGULAR

![image.png](image%2061.png)

No AURORA troque primeiro as replicas depois o mater

# Como funciona a maquina Master e Replica:

MASTER ⇒ NECESSITA TROCA

REPLICA ⇒ TROCA NELA POIS ELA VIRARA MASTER

A ANTIGA MASTER VIRA REPLICA DE LEITURA