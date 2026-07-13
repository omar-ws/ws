# JAM Proteja os marinheiros

esse deu errado peguei todas as dicas, tentei fazer apenas pela documentacao mas falhei pois nao consegui escrever da maneira certa, nao entendi como usar isso:

task 1:

aprender tudo desde o coemco por falha nesse JAM a primeira task tava com defeito entao nao passei da primeira, vou anotar apenas para trabalharmos domingo:

task1:

```wasm
Proteja os marinheiros
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
NamespaceName
seabird-nm

RedshiftRoleName
Redshiftgamesrole

RedshiftRoleNameArn
arn:aws:iam::855285956549:role/Redshiftgamesrole

RedshiftServerlessEndpoint
seabird-wg.855285956549.us-east-1.redshift-serverless.amazonaws.com:5439

Workgroupname
seabird-wg

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Todos a bordo
Pontos possíveis
24
Penalidade por pista
5
Pontos disponíveis
19
Verifique meu progresso

Tarefas e pistas
Enviar resposta
Nesta tarefa, você criará uma tabela de marinheiros e carregará os dados. Além disso, você criará diferentes funções e usuários, conforme descrito no resumo do desafio.

Um data warehouse Redshift Serverelss (seabird-wg) foi pré-criado para você na conta.

Etapa 1: Vá para o console Redshift. Expanda o painel de navegação esquerdo e clique em Editor de consultas V2.

Conecte-se ao armazenamento de dados do Redshift Server (seabird-wg) usando a opção “Nome de usuário e senha do banco de dados”.

username: awsuser
password: Retrieve the password from RedshiftServerlessSecret-* secret in AWS Secrets Manager.
database: dev
Etapa 2: Crie uma tabela sailors e carregue-a em s3://redshift-demos/data/gamejam/sailors/ usando o comando COPY.

Consulte CREATE TABLE para obter a sintaxe. A seguir estão os nomes das colunas e os tipos de dados a serem usados.

_id bigint, s_name varchar (25), s_address varchar (40), s_phone varchar (15), s_acctbal numérico (12,2), s_segment varchar (10), s_dietrestrictions varchar (20), booleano s_onboard

Etapa 3: Crie usuários e funções abaixo.

Nomes de usuário: cook, cuddy, cashking Nomes dos papéis: capitão, tripulação, finanças

Etapa 4: conceder funções aos usuários.

papel de capitão para usuário cozinheiro
Função crew para usuário cuddy
Papel de finance para usuário de sacar
Qn: Quantos marinheiros embarcaram com status de diamante na viagem atual?

Pistas
Solução
2Pontos de penalidade
Ocultar pista
-- Criar tabela

CREATE TABLE sailors (
    s_id bigint,
    s_name varchar(25),
    s_address varchar(40),
    s_phone varchar(15),
    s_acctbal numeric(12,2),
    s_segment varchar(10),
    s_dietrestrictions varchar(20),
    s_onboard boolean 
);
-- Tabela de carga

copy sailors from 's3://redshift-demos/data/gamejam/sailors/' 
iam_role 'replace with arn of Redshiftgamesrole from output properties' 
delimiter '|' 
region 'us-east-1';
-- Crie usuários e funções

CREATE USER cook PASSWORD 'Welcome123';
CREATE USER cuddy PASSWORD 'Welcome123';
CREATE USER cashking PASSWORD 'Welcome123';

CREATE ROLE captain;
CREATE ROLE crew;
CREATE ROLE finance;
-- Atribuir funções aos usuários

GRANT ROLE captain TO cook;
GRANT ROLE crew TO cuddy;
GRANT ROLE finance TO cashking;
Responda
3Pontos de penalidade
Ocultar pista
Execute a consulta abaixo para obter a resposta
select count(*) from sailors
where s_onboard='true'
and s_segment='DIAMOND'

```

usei todas as dicas e pedi ajuda pra ia aprendi anda que ta ai

as proximas taslk apenas pra mostrar vou ate pegar as dicas mas nem cheguei nelas por erro da plataforma mandei para o professor:

descrobri que nao da pra ver as outras task se nao fez a primeira, entao nao olhei

docmentacao que usei:

https://docs.aws.amazon.com/pt_br/redshift/latest/dg/t_role_assignment.html

[https://docs.aws.amazon.com/pt_br/redshift/latest/dg/r_CREATE_USER.html](https://docs.aws.amazon.com/pt_br/redshift/latest/dg/r_CREATE_USER.html)

[https://docs.aws.amazon.com/pt_br/redshift/latest/dg/r_CREATE_ROLE.htm](https://docs.aws.amazon.com/pt_br/redshift/latest/dg/r_CREATE_ROLE.html)l

https://docs.aws.amazon.com/pt_br/redshift/latest/dg/r_COPY.html#r_COPY-syntax

[https://docs.aws.amazon.com/pt_br/redshift/latest/dg/r_CREATE_TABLE_NEW.html](https://docs.aws.amazon.com/pt_br/redshift/latest/dg/r_CREATE_TABLE_NEW.html)