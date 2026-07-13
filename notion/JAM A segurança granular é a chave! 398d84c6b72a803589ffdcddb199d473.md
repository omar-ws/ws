# JAM A segurança granular é a chave!

```bash
Visão geral
Plano de fundo
Você ingressou recentemente na ABC Corp como engenheiro de segurança. Seu CISO encarregou você de reforçar a segurança dos serviços da AWS. Como parte dessa iniciativa, você será solicitado a criptografar as variáveis de ambiente usando o AWS Key Management Service. Isso deve ser feito para se beneficiar de um controle mais granular sobre o processo de criptografia/descriptografia de dados. Você está pronto para o desafio?

```

```bash
Tarefa 1: Criptografe as variáveis em trânsito e em repouso
Pontos possíveis
50
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Como profissional da AWS e em seu primeiro dia de trabalho, seu gerente solicita que você criptografe variáveis de ambiente de uma função lambda em trânsito e em repouso usando uma chave KMS gerenciada pelo cliente.

Tarefa
Sua tarefa é criptografar todas as variáveis usando uma chave mestra de cliente existente.

Primeiros passos
Abra o Console da AWS. Você pode usar esta documentação para encontrar seu caminho no console: https://docs.aws.amazon.com/lambda/latest/dg/configuration-envvars.html

Inventário
Trabalhe com os seguintes recursos do Lambda e do KMS

Lambda - Função MyLambda
KMS - MyKeyAlias
Serviços que você deve usar
Lambda
KMS
Validação de tarefas
A tarefa será concluída automaticamente assim que você encontrar a solução. Você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Tip: Anote execution role policy para tarefas subsequentes.

Tarefa 2: Descriptografar - permissão
Pontos possíveis
50
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Agora que as variáveis estão criptografadas usando a chave KMS gerenciada pelo cliente, corrija a função de execução da função Lambda para poder chamar a função de descriptografia.

Tarefa
Sua tarefa é corrigir a função usada pelo Lambda e suas permissões de execução.

Referência: https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#inline-policies

Observação: políticas e recursos baseados em “*” não são aceitos como respostas corretas.

Inventário
IAM - MyLambdaFunctionExecutionRole
Lambda - Função MyLambda
Serviços que você deve usar
VISAM
Lambda
CloudWatch Logs (opcional)
Validação de tarefas
A tarefa será concluída automaticamente quando você encontrar a solução. Você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Tarefa 3: Descriptografar - Verificar
Pontos possíveis
50
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
As variáveis são criptografadas usando a chave KMS gerenciada pelo cliente e as permissões são adicionadas ao aplicativo Lambda. No entanto, o aplicativo Lambda não consegue descriptografar a variável e está gerando um erro. Você está aqui para consertá-lo. Corrija a função Lambda para descriptografar as variáveis para que elas possam ser usadas pelo aplicativo. Observe que a função Lambda precisará descriptografar especificamente cada variável de ambiente criptografada necessária.

Tarefa
Sua tarefa é corrigir as políticas que não permitem que o Lambda descriptografe a variável. Observe que você precisa executar a função Lambda por meio do console para encontrar o erro.

Você pode usar essa documentação para encontrar seu caminho dentro do console e invocar a função Lambda com eventos de teste. https://aws.amazon.com/blogs/compute/improved-testing-on-the-aws-lambda-console/

Inventário
IAM - MyLambdaFunctionExecutionRole
KMS - MyKeyAlias
Lambda - Função MyLambda
Serviços que você deve usar
VISAM
KMS
Lambda
CloudWatch Logs (opcional)
Dica profissional: Evite criptografar novamente um valor já criptografado. Se você precisar redefinir e criptografar a variável de ambiente novamente, use a chave original “DatabaseUser” e o valor “admin” para continuar.

Validação de tarefas
A tarefa será concluída automaticamente quando você encontrar a solução. Você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

```

a