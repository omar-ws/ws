# JAM Bloqueio de tráfego malicioso na web #3 (fui avisado que essa ta com problema vou pular para fazer amanha) (na verdede vou hoje, sou eu do  futuro, o professro mandou eu fazer paraa ver se vai dar erro dnv)

> Sua empresa tem uma página de status extremamente importante. Os desenvolvedores incluíram uma página de status do sistema que fornece um nível inadequado de detalhes em uma página pública. Devido à rápida iteração, a exclusão da página não funcionará, pois ela será substituída apenas na próxima versão. Seu CISO solicitou que você restringisse o acesso a esta página de visitantes externos.
> 

task 1:

```jsx
Plano de fundo
Sua empresa publica uma página de informações indicando a integridade dos serviços essenciais. Os desenvolvedores permitiram, por engano, que uma página de status destinada a testes fosse enviada para o ambiente de produção. A equipe de desenvolvimento precisará de tempo para remover a página de seu fluxo de trabalho, testar e publicar o repositório de código-fonte. Até que ela seja removida do repositório, a exclusão da página não funcionará, pois novas instâncias são constantemente provisionadas do repositório. Seu CISO está preocupado com o nível de detalhes que esta página fornece

Sua tarefa
Você foi encarregado pelo CISO de encontrar uma maneira de bloquear o acesso público a esta página da web. Usando os serviços nativos da AWS, você precisará impedir que essa página seja veiculada sem afetar nenhum outro conteúdo regular que sua empresa fornece

.
Começando
Veja as propriedades de saída para obter a URL do Application Load Balancer que está configurado para os servidores web. Veja as páginas da web acessíveis a partir dele. A página do problema é info.php. Anote também o nome do ALB. Você vai precisar disso.

Inventário

Instância EC2
ALB VPC
Serviços que você deve usar
Firewall de aplicativos da Web (WAF)

Validação de tarefas
Essa tarefa pode ser validada automaticamente por meio do script de validação. Você também pode verificar seu progresso verificando manualmente se a página ofensiva

está visível.
Nota
Se você receber um erro “WAFunavailableEntityException” ao resolver o desafio, precisará esperar cinco minutos para que o status seja atualizado. Se o problema persistir, exclua o recurso que você criou e repita as etapas.

Pistas
Camada 7
8Pontos de penalidade
Desbloqueie o Clue
Versões do firewall
10Pontos de penalidade
Desbloqueie o Clue
A solução
12Pontos de penalidade
Desbloqueie o Clue
```

o que seria uma pagina de status? no contexto da aws

como assim constantemente provisionadas?

o que seria o WAF como usar esse servico

nao sei como usar o WAF mas sei que tenho que bloquear a URL especifica /info.php

se aprofudnar no servico WAF entender como configurar

aprender sobre o WAF como funciona o que da pra fazer e etc

eu tive que fazer o passo a passo: (tive que pegar a pista)

```jsx
Pistas
Camada 7
8Pontos de penalidade
Ocultar pista
Você deve considerar bloquear o tráfego perigoso na camada de aplicativo, não na camada de rede. Bloquear o tráfego na camada de rede envolveria impedir todo o tráfego da web, mas o objetivo é impedir o acesso a apenas uma única página.

Versões do firewall
10Pontos de penalidade
Ocultar pista
Use o serviço WAF & Shield para concluir o desafio

A solução
12Pontos de penalidade
Ocultar pista
Vá para WAF & Shield.

Clique em “Criar ACL da web”

Dê à nova Web ACL um nome como “SecJamChallenge”

clique em “Adicionar recursos da AWS”

Selecione o tipo de recurso do “Application Load Balancer”

Selecione o balanceador de carga “SecjaMalb”, clique em “Adicionar” e, em seguida, clique em “Avançar”

Selecione “Adicionar regras” e depois “Adicionar minhas próprias regras e grupos”

Em “Construtor de regras”, dê à regra um nome como “Block-Web-Page”

Em “Declaração”, selecione “Caminho do URI” para o campo “Selecionar”

O “Tipo de correspondência” deve ser definido como “Contém string”

Digite "info.php" para “String to match”

Clique em “Adicionar regra” e depois em “Avançar”

Na página “Definir prioridade da regra”, clique em “Avançar”

Na página “Configurar métricas”, clique em “Avançar”

Na página final, clique em “Criar ACL da web”

Observação: Se você recebeu um erroWAFunavailableEntityException ao criar a Web ACL, acesse Web ACLs, exclua a Web ACL que você criou e repita as etapas acima para criar uma nova Web ACL. Você pode ler mais sobre esse erro aqui: https://docs.aws.amazon.com/waf/latest/APIReference/API_CreateWebACL.html#API_CreateWebACL_Errors

Nota: Se o ALB não estiver incluído nos Recursos da AWS associados para a ACL quando você o criar, aguarde alguns minutos e adicione-o manualmente.

A página da web agora deve estar bloqueada
```

documentacao:

[https://docs.aws.amazon.com/waf/latest/APIReference/API_CreateWebACL.html#API_CreateWebACL_Errors](https://docs.aws.amazon.com/waf/latest/APIReference/API_CreateWebACL.html#API_CreateWebACL_Errors)