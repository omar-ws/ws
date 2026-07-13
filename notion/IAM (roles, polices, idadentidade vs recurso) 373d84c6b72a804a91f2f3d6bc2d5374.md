# IAM (roles, polices, idadentidade vs recurso)

[AWS Organizations](AWS%20Organizations%20373d84c6b72a805aa2d1fa5114f42d02.md)

[AWS Control Tower](AWS%20Control%20Tower%20374d84c6b72a80cfb680ec07b7ac6035.md)

[Criptografia de Dados em Repouso](Criptografia%20de%20Dados%20em%20Repouso%20374d84c6b72a8009808fc84d89053005.md)

IAM Identity Center: voce cria uma um IAM que acessar varias contas AWS ao inves de usar um IAM em cada conta

baundary: permissao principal da conta aws

scp: permissao universal do servico AWS Organizations

se o SCP bloqueia a conta nao consegue fazer nem desabilitar

## IN:Boundary ou PT:Limite de permissao

baundary ou LIMITE DE PERMISSAO: bloqueia permissao de um usuario IAM, se no meu usuario IAM eu tenho

```jsx
allow iam:createuser iam:createrole iam:deleteuser
```

e no limite de permissoes

```jsx
allow iam:createuser iam:createrol
```

porem nao esta o delete user, entao o delete user e negado e como se fosse uma negacao, mas antes uma confirmacao com o limite de permissao, nao necessariamente um deny explicito

lim

AWS IAM: criar usuarios manualemnte

amazon Cognito: criar credenciais temporarias para usuarios acessarem servicos da AWS, exemplo uma aplicacao de uma S3

    ::USUARIO (quero acessar aplicacao de fotos)⇒HTTPS ⇒ CLOUDFRONT ⇒ S3 ⇒ COGNITO (usa STS por baixo dos panos) ⇒ credencial temporaria para S3 bucket fotos ⇒ acessa fotos

AWS Security Token Service (AWS STS): API que permite solicitar credenciais temporarias

[ABAC vs RBAC - estrategias de controle de acesso](ABAC%20vs%20RBAC%20-%20estrategias%20de%20controle%20de%20acesso%20373d84c6b72a80878c67ca975d4d2a39.md)