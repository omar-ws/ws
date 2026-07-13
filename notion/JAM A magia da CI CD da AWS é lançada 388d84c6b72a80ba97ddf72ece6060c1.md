# JAM A magia da CI/CD da AWS é lançada

VISAO GERAL

```jsx
Parabéns! Você conseguiu o emprego dos seus sonhos na TerraTrend Travel, uma startup vibrante que ajuda clientes a reservar hotéis e voos de luxo em todo o mundo. Como engenheiro sênior de DevOps, você é responsável por garantir implantações sistemáticas de software em toda a infraestrutura de nuvem.

```

TASK 1 A 3

```jsx
Antecedentes
Houve um grande problema na empresa há 2 dias. Um código de baixa qualidade foi implantado no site da empresa e impediu que os usuários fizessem reservas. Isso resultou em uma perda estimada de 5,6 milhões de dólares ($). O problema já foi resolvido. Uma investigação interna foi feita e descobriu-se que a empresa não tinha uma estratégia sistemática de implantação de software para implantar código de software no site.

O CTO da empresa deu à sua equipe a tarefa de configurar uma estratégia confiável de implantação de software. Foi criado um AWS CodePipeline básico, que se integra ao AWS CodeBuild. Como você é o líder dessa equipe, eles contam com você para ajudá-los a realizar a tarefa designada. Você será capaz de entregar bons resultados!?

O primeiro requisito é que o site sempre contenha a seguinte string: “O conteúdo desta página é de propriedade da exampleorg. Entre em contato conosco em caso de dúvidas.”

Sua tarefa
Sua tarefa é garantir que o projeto AWS CodeBuild crie o código-fonte com sucesso somente se a string necessária estiver presente no código. Essa sequência de texto, conforme mencionado na seção acima, é: “O conteúdo desta página é de propriedade da exampleorg. Entre em contato conosco em caso de dúvidas.”

Começando
Navegue até o serviço 'CodeBuild' no console da AWS. Você deve conseguir ver o projeto intitulado 'MyBuildProject'. Você precisa revisar e atualizar este projeto para garantir que o requisito acima seja atendido.

Inventário:
Projeto AWS CodeBuild
Serviços que você deve usar:
AWS CodeBuild
Validação de tarefas
A tarefa será marcada automaticamente como concluída após a atualização correta do projeto CodeBuild.

TASK 2

Antecedentes
Trabalho maravilhoso até agora! Agora você foi informado de que seu pipeline do AWS CodePipeline tem quatro estágios. Todas as atualizações de software que serão implantadas no site da empresa no futuro terão que passar por esses quatro estágios com sucesso:

Etapa 1: A primeira etapa recupera o código-fonte
Etapa 2: A segunda etapa é integrada ao projeto CodeBuild que você atualizou na tarefa anterior e garante que o código-fonte contenha a sequência de texto necessária
Etapa 3: a terceira etapa implanta o código na função Lambda do ambiente de desenvolvimento
Etapa 4: A quarta etapa implanta o código na função Lambda do ambiente Prod.
Assim, todo o seu processo de lançamento de software será automatizado! Agora, sua equipe precisa de sua ajuda para refinar o pipeline. Você será capaz de usar sua experiência e ajudá-los?

Como próximo requisito, seu CTO quer garantir que, quando o pipeline estiver em execução, ele aguarde a aprovação manual de um engenheiro antes de implantar o código na função Lambda do ambiente Prod. Isso dá à equipe a oportunidade de revisar e corrigir quaisquer problemas observados no ambiente de desenvolvimento e só então aprovar a implantação no ambiente Prod.

Sua tarefa
Você precisa atualizar o pipeline de forma que ele exija aprovação manual antes de implantar o código na função Lambda do ambiente Prod. A mudança deve ser feita no estágio de pipeline, que implanta o código no ambiente Prod.

(Observação: ao salvar as alterações no pipeline, certifique-se de marcar a caixa “Nenhuma atualização de recursos necessária para essa alteração na ação de origem”, conforme mostrado na imagem abaixo)

!

Começando
Navegue até o serviço 'CodePipeline' no console da AWS. Você deve conseguir ver o pipeline chamado 'myCodePipeline'. Você precisa revisar e atualizar esse funil para garantir que o requisito acima seja atendido. (Você pode ignorar com segurança o status de execução do Pipeline e o estágio 'Fonte', que aparece como Falha)

Inventário:
Pipeline do AWS CodePipeline
Serviços que você deve usar:
AWS CodePipeline
Validação de tarefas
A tarefa será marcada automaticamente como concluída após a atualização correta do pipeline.

TASK 3
Tarefas e pistas
Antecedentes
Ótimo trabalho nas tarefas anteriores! Agora você estava tendo uma discussão com seu CTO. Ele percebeu que o estágio final do pipeline transfere todo o tráfego para a função atualizada do Lambda de uma só vez. Ele teme que, se houvesse algum problema nessa função lambda atualizada, isso afetaria todos os usuários. Em vez disso, ele quer ter cuidado e ter uma estratégia de implantação melhor. Você pode ajudá-lo com esse requisito final?

Sua tarefa
Você precisa atualizar o pipeline de forma que apenas 10% do tráfego seja transferido para a função lambda atualizada no primeiro incremento. O tráfego restante de 90% deve ser alterado 2 minutos depois. Essa atualização precisa ser executada no estágio de pipeline, que implanta o código no ambiente Prod.

(Observação: semelhante à tarefa anterior, ao salvar as alterações no pipeline, certifique-se de marcar a caixa “Nenhuma atualização de recursos necessária para essa alteração na ação de origem”.)

Começando
Você precisa revisar e atualizar o pipeline para garantir que o requisito acima seja atendido.

Inventário:
Pipeline do AWS CodePipeline
Serviços que você deve usar:
AWS CodePipeline
Validação de tarefas
A tarefa será marcada automaticamente como concluída após a atualização correta do pipeline.

```

a