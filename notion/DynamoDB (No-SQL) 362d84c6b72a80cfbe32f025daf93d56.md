# DynamoDB (No-SQL)

DynamoDB nao faz join (Juntas duas tabelas)

Boas praticas usar o VPC endpoint para nao sair pela internet

o Dynamo e acessado por permissao no IAM

## Como funciona GSI vs LSI:

Gsi ⇒ agrupamento de dados, ja tem um PK unico EX: PK salario = 5000k retornara todos os usuarios que tem esse salario. O PK DO GSI PODE TER DADOS REPETIDO (AGRUPA)

Lsi: ⇒ serve para trazer dados especificos, o sk do LSI pode ser de dados repitidos, MAS NA CRIACAO NAO (DADOS ESPECIFICOS)

- GSI → global, cruza todo mundo, PK pode repetir
- LSI → específico dentro de uma partição, SK pode repetir
- Os dois eliminam a necessidade de Scan ou FilterExpression caro

## Como escolher o banco de dados ideal:

1. necessidades da workload
2. modeo de dados que ele usa
3. os recursos e beneficios do banco de dados
4. em quais casos de uso aquele banco aparece na prática. EX: "Neptune é visto em redes sociais, detecção de fraude, grafos
de conhecimento."

Como funciona:

![image.png](image%2062.png)

DynamoDB:

DynamoDB Table: Produto, Usuario

Table Item (Linha):

Partion Key: atributo especifico (unico) Para dar Query

- Partition Key — atributo único que identifica o item. DynamoDB usa para achar o item rápido
- Sort Key — opcional. Usado junto com a partition key para agrupar e ordenar itens relacionados

![image.png](image%2063.png)

![image.png](image%2064.png)

# Quando usar apenas Partion Key ou Partion Key + Sort Key?

![image.png](image%2065.png)

GSI vs LSI

![image.png](image%2066.png)

**Práticas recomendadas de segurança do DynamoDB
Prevenção:**

**• Use perfis do IAM para autenticar o acesso.**

**• Use políticas do IAM para autorização básica do DynamoDB.**

**• Use as condições de política do IAM para um controle de acesso detalhado.**

**• Use políticas e um endpoint da VPC para acessar o DynamoDB. Detecção**

**• Use o AWS CloudTrail para monitorar o uso de chaves do AWS KMS gerenciadas pela AWS.**

**• Monitore as operações do DynamoDB usando o CloudTrail.**

**• Monitore a configuração do DynamoDB com o AWS Config.**

**• Monitore a conformidade do DynamoDB com as regras do AWS Config.**

![image.png](image%2067.png)

![image.png](image%2068.png)

projection e o filtro