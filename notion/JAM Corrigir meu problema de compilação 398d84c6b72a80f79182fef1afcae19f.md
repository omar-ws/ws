# JAM Corrigir meu problema de compilação

```bash
Sua empresa acaba de ser notificada de que a imagem base do nginx tem uma vulnerabilidade e precisa ser corrigida. Você é um engenheiro de DevOps designado para fazer isso!

Alguém tentou fazer isso, e há um CodePipeline que já está construído. Mas o pipeline que constrói a nova imagem está falhando.

Você precisa descobrir o que há de errado com isso e consertá-lo!
```

```bash
Tarefa 1: Corrigir problemas CodeBuild!
Pontos possíveis
150
Penalidade por pista
0
Pontos disponíveis
150
Verifique meu progresso

Tarefas e pistas
Detalhes
Plano de fundo
Alguém em sua empresa criou um CodePipeline para divulgar uma nova imagem do nginx que tem a solução para a vulnerabilidade. O CodePipeline tem dois estágios:

Fonte: é um repositório CodeCommit que contém o Dockerfile atualizado para criar novas imagens
Construção: é feita pelo CodeBuild, em que a imagem é construída e armazenada no ECR
Sua tarefa
A construção está falhando! Você é chamado como consultor de DevOps para solucionar e solucionar o problema.

Começando
Você pode navegar até o serviço CodePipeline no console da AWS e ver que um CodePipeline já foi criado e está no estado “Falha”. Você precisa descobrir o problema e resolvê-lo.

Inventário
CodeCommit
CodePipeline
Projeto CodeBuild
Funções do IAM para os seguintes serviços:
CodePipeline
CodeBuild
Baldes S3:
artefatos: armazena artefatos do CodePipeline
Chave KMS: usada para criptografar artefatos
Repositório ECR: para armazenar imagens do Docker
Serviços que você deve usar
CodePipeline, CodeBuild, IAM

Nota
Você veria o seguinte erro ao atualizar as políticas do IAM:

Usuário: arn:aws:sts: :123456789012:assumed-role/awslabsUser-xxxxxxxxxxxx/default não está autorizado a executar: Access-Analyzer:validatePolicy on resource: arn:aws:access-analyzer:us-east- 1:123456789012: *

Não estamos usando o IAM Access Analyzer neste desafio do Jam. Portanto, as permissões relacionadas estão habilitadas. Você pode ignorar essa mensagem e continuar salvando as alterações do IAM.

Validação de tarefas
A execução do CodePipeline será concluída com êxito e uma nova imagem será enviada ao repositório ECR no final. O desafio será automaticamente marcado como concluído quando a execução do CodePipeline for concluída com êxito.

Pistas
Pistas 1
15Pontos de penalidade
Desbloqueie o Clue
Mais um problema
19Pontos de penalidade
Desbloqueie o Clue
Caminhada completa
22Pontos de penalidade
Desbloqueie o Clue
```

```bash
a
```

a