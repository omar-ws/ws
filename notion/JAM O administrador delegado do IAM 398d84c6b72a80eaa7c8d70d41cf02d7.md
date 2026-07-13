# JAM O administrador delegado do IAM

```bash
Visão geral
Os desenvolvedores gostam da agilidade para inovar rapidamente. Delegue adequadamente algumas das tarefas de criação de funções do IAM para seus desenvolvedores, mantendo a segurança com barreiras preventivas para que você possa se concentrar em outras áreas da segurança na nuvem. Isso acelerará o desenvolvimento ao desbloquear os desenvolvedores.

Tarefa 1: Untitled Task
Pontos possíveis
150
Penalidade por pista
0
Pontos disponíveis
150

Tarefas e pistas
Enviar resposta
### Antecedentes

Você é o administrador de segurança na nuvem de uma empresa de médio porte. Atualmente, todos os usuários do IAM e a criação de funções do IAM precisam passar pela sua equipe e isso se tornou um gargalo para sua empresa. Os desenvolvedores precisam de mais agilidade e permissões para criar as funções do IAM, que serão assumidas por seus aplicativos. Isso permitirá que os desenvolvedores criem e testem seus aplicativos e inovem rapidamente.

Seu diretor de equipe deseja fornecer permissões para que os desenvolvedores criem usuários do IAM. Eles estão preocupados com as permissões que os desenvolvedores atribuirão aos novos usuários/funções e também com o aumento de privilégios.

Seu diretor atribuiu a você uma tarefa para criar uma solução para atribuir aos desenvolvedores os privilégios para criar usuários/funções, mas essas funções não devem exceder as permissões definidas pela política de segurança da empresa. Seu desafio é criar um sistema em que você delegue desenvolvedores para criar suas próprias funções do IAM para acelerar os ciclos de desenvolvimento e, ao mesmo tempo, manter a segurança. A permissão máxima à qual os desenvolvedores devem ter acesso é s3:* e ssm:PutParameter

### Sua tarefa

Seu trabalho é criar uma função de administrador delegado (função A).

A função A será usada pelos desenvolvedores para provisionar recursos do IAM para aplicativos. A função A só pode criar funções do IAM se o máximo de permissões destacado estiver presente.
A função A deve ser chamada de SJ-DelegatedAdmin e deve confiar em 2 contas (sua conta atual e Conta 681434714655 para verificação de respostas).
Sua política de permissão máxima deve ser chamada de SJ-Max.
**Opcional: ** Você pode testar a criação de uma função de teste (função B) a partir de SJ-DelegatedAdmin (função A) para garantir que sua solução esteja correta. A função B deve ter a mesma relação de confiança que a função A
Serviços que você deve usar
ERA O OBJETIVO
### Validação de tarefas

Etapas para validar a solução

Execute o seguinte comando substituindo 12345 pelo número da conta da AWS

Máquinas Mac ou Linux:

 curl -d '{"account_id":"12345"}' -H "Content-Type: application/json" -X POST https://1b07hvp92b.execute-api.us-east-1.amazonaws.com/prod/validate
Janelas:
 curl -d "{\"account_id\":\"12345\"}" -H "Content-Type: application/json" -X POST https://1b07hvp92b.execute-api.us-east-1.amazonaws.com/prod/validate
Insira o texto da resposta que você recebe após executar um comando curl no campo Enter answer here no console JAM.
Pistas
Crie a política de permissão máxima
15Pontos de penalidade
Desbloqueie o Clue
Criar política de permissão para administrador delegado e com limite de permissão
19Pontos de penalidade
Desbloqueie o Clue
Complete Solution
22Pontos de penalidade
Desbloqueie o Clue
```

nao sabia nem o que fazer, que raiva