# JAM NECESSIDADE DE VELOCIDADE!!!

VISAO GERAL 

```jsx
A Speedy Corp contratou consultores externos para criar um aplicativo de back-end. Os consultores são bons em testes unitários, mas terríveis em escrever código legível. Eles estão reclamando que a compilação está levando muito tempo quando verificações adicionais são realizadas durante a fase de compilação

```

TASK 1

```jsx
Antecedentes
Alguém em sua empresa já criou um CodePipeline que cria o código do seu aplicativo. O CodePipeline tem três estágios:

Fonte: CodeCommit tem o código-fonte
Analise: CodeBuild com análise de código
Construção: CodeBuild com artefato armazenado no bucket S3
Sua tarefa
Você foi contratado como engenheiro de DevOps para aplicar práticas de linting sem aumentar o tempo de construção. O CodePipeline atual não tem verificação de linting, então sua tarefa é adicionar uma para que o tempo de construção não aumente.

Recursos criados neste desafio que estão prontos para uso:
CodeCommit Repo: armazena o código do aplicativo e os arquivos buildspec que acionam o pipeline
Buckets S3: armazena artefatos do CodePipeline
Função do IAM para CodePipeline
Política embutida para a função IAM do CodePipeline
CodePipeline
Projetos CodeBuild
Como sei que concluí o desafio com sucesso?
A execução do CodePipeline marcará automaticamente o desafio como bem-sucedido.

Pistas
Pense em etapas paralelas no CodePipeline
8Pontos de penalidade
Mostrar pista
Passos a fazer
10Pontos de penalidade

```

a