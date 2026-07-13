# Git commands

```bash
# GIT — colinha de JAM

## Setup (1ª vez numa máquina nova — SEMPRE pede antes do 1º commit)
git config --global user.name "bruno"
git config --global user.email "b@b"

## Começar
git init                     → cria repo local (branch nasce como MASTER)
git clone <url>              → baixa repo existente (jeito mais comum em JAM)

## CodeCommit (os 2 jeitos)
pip install git-remote-codecommit        → instala o helper (labs)
git clone codecommit::us-east-1://NomeRepo
# ou HTTPS: precisa de credencial Git do IAM (usuário → Credenciais de segurança)

## Ciclo básico (a ordem SEMPRE é essa)
git status                   → o que mudou? (usar TODA HORA, é de graça)
git add .                    → mala: TUDO que mudou (git add arquivo = só um)
git commit -m "mensagem"     → foto local com etiqueta
git push origin master       → envia (conferir nome da branch antes!)
git pull                     → baixa o que mudou no remoto

## Branch
git branch                   → em qual estou? (asterisco marca)
git branch -m master main    → renomear
git checkout -b nova         → criar e mudar pra branch nova
git checkout main            → trocar de branch

## Remote (agenda de endereços)
git remote -v                → lista endereços cadastrados
git remote add origin <url>  → cadastra (origin = apelido padrão)
git remote set-url origin <url> → TROCA o endereço (se errou/mudou de método)

## Pegadinhas que JÁ me pegaram
- pasta vazia é INVISÍVEL pro git → precisa ter arquivo dentro
- "nothing to commit" → esqueceu o git add
- "src refspec main does not match any" → branch é master OU não tem commit
- 403 no push CodeCommit → sem identidade IAM (aws configure / role / credencial Git)
- pipeline não dispara → push foi pra branch que o pipeline NÃO olha

```