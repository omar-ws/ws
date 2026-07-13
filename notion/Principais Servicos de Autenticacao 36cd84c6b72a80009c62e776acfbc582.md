# Principais Servicos de Autenticacao

Cognito — mais usado
Usuário → Cognito (login) → retorna token → EC2 App valida token

- Gerencia usuários, senhas, MFA
- Login social (Google, Facebook)
- Gera tokens JWT automaticamente

IAM Identity Center — para funcionários/times

- Acesso ao console AWS
- SSO entre contas