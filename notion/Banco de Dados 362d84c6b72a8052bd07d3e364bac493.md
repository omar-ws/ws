# Banco de Dados

[Elastic Cache](Elastic%20Cache%20381d84c6b72a804fadedc746aa162f85.md)

### Relacional → quando precisa de transação segura (ACID)
NoSQL → quando precisa de velocidade e escala

## Diferenca de escabilidade do RDS para o RDS AURORA

o RDS tradicional em single az recebe gravacao/leitura na mesma instancia, nao tem alta disponibilidade

RDS tradicional multi az (2 instancia) a instancia MASTER fica para gravacao e leitura e a STANDBY fica apenas para receber dados e em caso da problema na Master ela substitui

RDS tradicional multi az (3 instancia) tem uma instancia MASTER e duas STANDBY com REPLICAS DE LEITURA que ficam em duas az diferentes e ajudam na diminuicao da latencia e na sobrecarga do MASTER

RDS aurora (quando criada multi az) compartilham o mesmo armazenamento ou seja mesmo se tiver apenas um STANDBY ela ja esta com o disco compartilhado

A DIFERENCA DO RDS AURORA E O FATO DE COMPARTILHAR A MEMORIA EM ATE 3AZ MESMO SEM INSTANCIA

- Relacional (RDS) → dados estruturados com relacionamentos via joins
- Grafo (Neptune) → relacionamentos entre entidades
- Documento (DocumentDB) → JSON aninhado, estrutura flexível por documento
- Série temporal (Timestream) → dados ordenados por tempo (métricas, sensores)
- Ledger (QLDB) → histórico imutável de transações

[RDS Tradicional (MySQL, PostgreeSQL, SQL Server, Oracle)](RDS%20Tradicional%20(MySQL,%20PostgreeSQL,%20SQL%20Server,%20O%20362d84c6b72a80dd915cf8bab76d18e6.md)

[RDS Amazon Aurora (Versão turbinada)](RDS%20Amazon%20Aurora%20(Vers%C3%A3o%20turbinada)%20362d84c6b72a80d9a03cc4f06818b387.md)

[Amazon RedShift](Amazon%20RedShift%20362d84c6b72a808db471fa2e0f04dc5a.md)

Nao Relacionais:

[DynamoDB (No-SQL)](DynamoDB%20(No-SQL)%20362d84c6b72a80cfbe32f025daf93d56.md)

[Outros tipos de Bancos de Dados:](Outros%20tipos%20de%20Bancos%20de%20Dados%20362d84c6b72a806eb136d178b733e4c0.md)

Banco de Dados PARA **migrar e replicar dados**

[**AWS DMS** (Database Migration Service)](AWS%20DMS%20(Database%20Migration%20Service)%20362d84c6b72a80099d6dd6b2001418ad.md)

PRATICAS RECOMENDADAS:

[Well-Architected Framework a Camada do Banco de Dados](Well-Architected%20Framework%20a%20Camada%20do%20Banco%20de%20Da%20362d84c6b72a80cb9946f2c2e28cc306.md)

fork = quando alguem pega o opensource e faz o seu proprio

Quando escolher cada banco:

**1. Escolha DynamoDB (Não-Relacional) se o enunciado disser:**
• Dados em formato JSON, chave-valor ou documentos flexíveis.
• Precisa aguentar milhões de acessos por segundo com latência de milissegundos.
• Menção a tabelas globais (Global Tables) ou arquitetura 100% Serverless.

**2.Escolha RDS Tradicional (MySQL, Postgres, SQL Server) se o enunciado disser:**
• Precisa de banco relacional (tabelas, `JOIN`, transações ACID).
• Motores obrigatórios: **SQL Server** ou **Oracle** (Aurora não roda eles).
• Ambiente de **baixo custo**, teste ou desenvolvimento (onde pode usar instâncias baratas tipo `t3.micro`).

**3. Escolha Amazon Aurora se o enunciado disser:**
• Precisa de banco relacional (MySQL ou Postgres) com **altíssima performance** de leitura.
• Exige o **menor tempo de failover possível** (quedas de até 30 segundos).
• O armazenamento precisa crescer sozinho sem intervenção manual e sem downtime.

**4. Amazon Redshift (Data Warehouse / OLAP)** Escolha o **Redshift** se o enunciado disser:
• **Análise**: Consultas complexas em grandes volumes de dados (BI / Business Intelligence).
• **Volume**: Menção a Terabytes (TB) ou Petabytes (PB) de dados históricos.
• **Operação**: Cargas de trabalho analíticas (OLAP) e não transacionais (OLTP).
• **Armazenamento**: Armazenamento colunar (Columnar storage) para acelerar relatórios.

Diferença de VALORES:

| **Banco de Dados** | **Modelo de Cobrança** | **Custo de Entrada** | **Custo de Escala** | **Quando escolher pelo custo?** |
| --- | --- | --- | --- | --- |
| **Banco no EC2** | Paga por hora da máquina ligada + preço fixo do disco EBS. | **Muito Baixo**. Sem taxa de gerenciamento. | Linear (Gasta mais se mudar de máquina). | Orçamentos extremamente apertados ou laboratórios simples. |
| **RDS Tradicional** *(Gerenciado)* | Paga por hora da máquina ligada + tamanho fixo do disco alocado (gp2/gp3). | **Baixo/Médio**. Inclui o custo do gerenciamento AWS. | Médio (Paga pelo tamanho do disco mesmo se estiver vazio). | Projetos de produção padrão com orçamento controlado. |
| **Amazon Aurora** *(Altamente Gerenciado)* | Paga por hora da máquina + espaço em disco usado + **quantidade de requisições de leitura/escrita (I/O)**. | **Alto**. Não tem opção no Free Tier. | Alto (Se o sistema tiver muitos acessos, a cobrança por I/O aumenta a conta). | Grandes empresas onde a performance e a tolerância a falhas importam mais que o preço. |
| **DynamoDB** *(Não-Relacional)* | Paga apenas por dados armazenados + capacidade de leitura/escrita por segundo (ou por requisição no modo On-Demand). | **Zero / Grátis**. Possui uma camada gratuita generosa para sempre. | Excelente (Só escala o custo se o uso real do aplicativo subir). | Aplicações modernas, Serverless ou com picos de acessos imprevisíveis. |

Relacionais:

![image.png](image%2012.png)

Como analisar qual banco escolher:

![image.png](image%2013.png)

Um **schema (ou esquema)** de banco de dados **é a estrutura lógica que define como os dados são organizados, armazenados e relacionados**.