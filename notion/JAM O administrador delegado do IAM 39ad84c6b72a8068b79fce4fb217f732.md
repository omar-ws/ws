# JAM O administrador delegado do IAM

nao consegui fazer

```verilog
Visão geral
Os desenvolvedores gostam da agilidade para inovar rapidamente. Delegue adequadamente algumas das tarefas de criação de funções do IAM para seus desenvolvedores, mantendo a segurança com barreiras preventivas para que você possa se concentrar em outras áreas da segurança na nuvem. Isso acelerará o desenvolvimento ao desbloquear os desenvolvedores.

Tarefa 1: Untitled Task
Pontos possíveis
150
Penalidade por pista
34
Pontos disponíveis
116

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
Ocultar pista
Crie uma política do IAM que funcionará como um limite de permissão.

Etapas

Abra o console do IAM
Clique em Políticas
Clique no botão Create Policy
Selecione a guia JSON e use a política json abaixo.
{
    "Version": "2012-10-17",
    "Statement": [
        { 
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ssm:PutParameter",
                "s3:*"
            ],
            "Resource": "*"
        }
    ]
}
Nomeie esta política do IAM como SJ-Max
Não se esqueça de copiar o ARN desta política para referência!!!

Criar política de permissão para administrador delegado e com limite de permissão
19Pontos de penalidade
Ocultar pista
O limite de permissão do IAM não fornece permissões por si só, mas é um controle preventivo que restringe as permissões gerais.
Você precisa criar uma política de permissão para que seu administrador delegado do IAM crie as funções.

Etapas
A criação de uma nova política do IAM com permissões para criar a função do IAM será usada pelo administrador delegado.
Atribua o limite de permissão para garantir que a função só possa ser criada quando o limite máximo de permissão estiver presente.

Acesse o console do IAM
Clique em Políticas no painel esquerdo e, em seguida, clique no botão Criar política.
Copie o JSON abaixo e coloque-o na guia JSON
Nomeie essa política como SJ-boundary
Altere o 12345 para o número da sua conta na condição IAM.
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "RoleCreationWithPermission",
            "Effect": "Allow",
            "Action": [
                "iam:DetachRolePolicy",
                "iam:DeleteRolePolicy",
                "iam:CreateRole",
                "iam:AttachRolePolicy",
                "iam:PutRolePolicy"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:PermissionsBoundary": "arn:aws:iam::12345:policy/SJ-Max"
                }
            }
        },
        {
            "Sid": "IAMPermission",
            "Effect": "Allow",
            "Action": [
                "iam:CreatePolicy",
                "iam:GetRole",
                "iam:ListRoles",
                "iam:DeletePolicy",
                "iam:DeleteRole",
                "iam:GetRolePolicy"
            ],
            "Resource": "*"
        }
    ]
} 
Use essa política para criar uma função para seu administrador delegado.

Complete Solution
22Pontos de penalidade
Desbloqueie o Clue

```

peguei dica e nao fiz