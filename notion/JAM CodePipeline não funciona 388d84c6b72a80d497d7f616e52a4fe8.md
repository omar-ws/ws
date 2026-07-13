# JAM CodePipeline não funciona

VISAO GERAL 

```jsx
A APinC Ltd. está tentando fazer um retorno após anos de má gestão. Eles têm curso corrigido agora e estão tentando liberar recursos inovadores para seu principal produto para melhorar sua quota de mercado. Uma das equipes críticas de aplicativos deseja configurar um pipeline de entrega contínua para testar as alterações rapidamente. A equipe configurou o pipeline e criou modelos do CloudFormation para implantar seus aplicativos.

```

TASK 1

```jsx
Detalhes da tarefa
Plano de fundo
Alguém em sua empresa criou um CodePipeline para implantar a infraestrutura da AWS usando o CodePipeline e o CloudFormation. O CodePipeline contém 2 estágios:

Fonte: é um repositório CodeCommit que contém um único modelo do CloudFormation
Implantar: implanta a pilha do CloudFormation.
Sua tarefa
A implantação do CloudFormation não está acontecendo. Você é chamado como consultor de DevOps para solucionar e solucionar o problema.

Começando
Você pode navegar até o serviço CodePipeline no console da AWS e ver que um CodePipeline já foi criado e está no estado “Falha”. Você precisa descobrir o problema e resolvê-lo.

Nota:

Depois de fazer alterações no estágio do funil, ao pressionar o botão final de Salvar, um prompt aparecerá com a mensagem: “Salvar alterações do funil”. Certifique-se de que você check “Nenhuma atualização de recursos é necessária para esta alteração da ação de origem” antes de clicar em Salvar no prompt.
Desmarcar o prompt resultará em um erro que começa com: “Ocorreu um erro não especificado”.
Nesse caso, clique em Salvar novamente e, desta vez, marque a caixa de seleção para dizer “Nenhuma atualização de recursos é necessária para essa alteração da ação de origem”.
Inventário
Repositório CodeCommit: contém o código-fonte do CodePipeline
Baldes S3:
artefatos: armazena artefatos do CodePipeline
Função do IAM para CodePipeline
CodePipeline
Verificação
A execução do CodePipeline será concluída com êxito em pouco tempo. Uma nova pilha do CloudFormation foi implantada com sucesso. O nome da pilha do CloudFormation está presente nas saídas da pilha principal.

Nota: Depois de corrigir o pipeline, se a execução do pipeline não começar depois de algum tempo, você pode selecionar o botão Liberar alteração e, no pop-up subsequente que aparecer, selecionar Liberar

O desafio será automaticamente marcado como concluído quando a execução do CodePipeline for concluída com êxito.

Serviços usados
Serviços usados: CodeCommit, CodePipeline, CloudFormation.
```

a