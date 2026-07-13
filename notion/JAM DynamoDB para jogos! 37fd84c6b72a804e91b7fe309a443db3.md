# JAM DynamoDB para jogos!

visao geral:

```jsx
Bem-vindo ao Really Awesome Games! A equipe de jogos acaba de lançar um novo título que está se tornando uma sensação global: o número de jogadores está subindo rapidamente e jogadores de todo o mundo estão se juntando a guildas e competindo pelas melhores classificações. Mas com esse crescimento explosivo, surge um desafio: a solução atual de armazenamento em disco para perfis de jogadores e dados de guildas simplesmente não consegue atender à demanda. Como designer de jogos da equipe, você precisará arquitetar uma solução de banco de dados escalável usando o Amazon DynamoDB que possa lidar com milhões de jogadores sem suar a camisa.

O Amazon DynamoDB é um serviço de banco de dados NoSQL totalmente gerenciado que se tornou a melhor escolha para desenvolvedores de jogos em todo o mundo. Ele oferece tempos de resposta de um dígito em milissegundos em qualquer escala — fundamental quando os jogadores esperam atualizações instantâneas em suas estatísticas, inventário e tabelas de classificação. Ao contrário dos bancos de dados tradicionais que exigem planejamento complexo de capacidade e escalabilidade manual, o DynamoDB aumenta e diminui automaticamente para lidar com os padrões de tráfego do seu jogo, independentemente de você ter 100 jogadores ou 100 milhões. Seu esquema flexível o torna perfeito para armazenar diversos dados de jogos, como perfis de jogadores, estados de sessão, configurações de jogos e informações da guilda. Além disso, com a replicação integrada em várias regiões da AWS, você pode oferecer experiências de baixa latência para jogadores em qualquer lugar do mundo.

O que você aprenderá:

Como criar uma tabela do DynamoDB com escalabilidade sob demanda que se ajusta automaticamente ao tráfego do seu jogo Entendendo o modo de capacidade provisionada do
DynamoDB e como calcular as unidades de capacidade de gravação (WCU) e as unidades de capacidade de leitura (RCU) com base nos requisitos específicos do seu jogo Melhores práticas para escolher entre os modos de capacidade
sob demanda e provisionada para diferentes cargas de trabalho de jogos Como criar tabelas que possam armazenar e
recuperar dados de jogadores e guildas com eficiência em escale os principais conceitos do DynamoDB que ajudarão você a criar
soluções responsivas, backends de jogos escaláveis
```

task 1:

```jsx
Tarefa 1: Tabela da guilda
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
As guildas são o coração de qualquer jogo multijogador de sucesso — elas são onde os jogadores formam comunidades, criam estratégias juntos e constroem amizades duradouras. À medida que a base de jogadores da Really Awesome Games explode globalmente, a equipe decidiu lançar a criação de guildas como uma característica principal. Os jogadores já estão pedindo isso, e a equipe de desenvolvimento sabe que isso impulsionará o engajamento e a retenção.

Para oferecer suporte a esse recurso, a equipe de back-end criou uma função Lambda que lida com solicitações de criação de guildas a partir da API do jogo. Agora eles precisam que você crie uma tabela do DynamoDB que armazenará todos os dados da guilda — nomes da guilda, listas de membros, datas de criação e outros metadados. A beleza dessa abordagem? O modo de capacidade sob demanda do DynamoDB significa que você não precisa prever quantas guildas os jogadores criarão. Independentemente de 10 guildas serem criadas em uma hora ou 10.000, o DynamoDB escalará automaticamente para lidar com a carga sem qualquer intervenção manual. Isso é perfeito para cargas de trabalho de jogos imprevisíveis, nas quais a atividade do jogador pode aumentar drasticamente durante eventos, fins de semana ou momentos virais nas redes sociais.

A função Lambda já está configurada com a estrutura de tabela que ela espera, então você precisará criar uma tabela que corresponda a essas especificações. O modo sob demanda é ideal aqui porque a criação de guildas é inerentemente imprevisível — você não pode prever quando os jogadores decidirão formar novas guildas, o que torna difícil provisionar a quantidade certa de capacidade com antecedência.

Dê uma olhada nesta documentação sobre como criar uma tabela do DynamoDB

Você precisará criar uma tabela com os seguintes elementos:

Nome da tabela: guild_data
Chave de partição: id
Chave de classificação: gname
Inventário
DynamoDB
Validação de tarefas
Depois de criar a tabela do DynamoDB, clique no botão Verificar meu progresso acima.

Pistas
Solução
4Pontos de penalidade
Desbloqueie o Clue
```

era so criar por enquanto era facil

task 2:

```jsx
Tarefa 2: Tabela de caracteres
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Com a funcionalidade da guilda instalada e funcionando, a Really Awesome Games está pronta para lidar com a próxima peça crítica: armazenar dados de personagens. Toda vez que um jogador cria um novo personagem — escolhendo sua classe, personalizando sua aparência e definindo seu nome de usuário — essas informações precisam ser salvas de forma confiável e rápida. A equipe de back-end criou uma função do Lambda chamada character_add que lida com solicitações de criação de personagens a partir da API do jogo.

Para esse caso de uso, a equipe decidiu usar o modo de capacidade provisionada em vez de sob demanda. Por quê? A criação de personagens segue padrões previsíveis. Com base nas análises de seus jogos anteriores, a Really Awesome Games sabe que os jogadores normalmente criam personagens em horários específicos: logo após o registro da conta, durante as principais atualizações de conteúdo e quando novas classes de personagens são lançadas. Essa previsibilidade torna a capacidade provisionada a escolha econômica: você pode dimensionar sua capacidade de acordo com o tráfego esperado e pagar um custo menor por solicitação em comparação com o modo sob demanda.

Compreendendo as unidades de capacidade de leitura e gravação

A capacidade provisionada do DynamoDB é medida em duas unidades:

**Unidades de capacidade de leitura (RCUs) **: Uma RCU representa uma leitura fortemente consistente por segundo para itens de até 4 KB de tamanho. Se você usar leituras eventualmente consistentes (que são aceitáveis para muitos cenários de jogos), você obtém o dobro da taxa de transferência — uma RCU fornece duas leituras eventualmente consistentes por segundo.

**Unidades de capacidade de gravação (WCUs) **: Uma WCU representa uma gravação por segundo para itens de até 1 KB.

Para essa tarefa, a função Lambda usa a API transacional do DynamoDB para garantir que a criação do personagem seja atômica — ou todo o registro do personagem seja criado com sucesso ou nada seja escrito. Isso evita que dados parciais de caracteres corrompam seu banco de dados se algo der errado no meio da criação. As transações fornecem garantias ACID, o que é crucial para manter a integridade dos dados em seu jogo.

Calculando seus requisitos de capacidade

A função character_add Lambda tem requisitos específicos que você precisará traduzir em RCUs e WCUs:

**Para capacidade de leitura: **

A função executa 1 transação por segundo
Cada transação lê três itens para validar a criação do personagem (verificar a disponibilidade do nome de usuário, o status da conta e os limites do espaço de caracteres)
Cada item tem 1 KB de tamanho
Você usará leituras fortemente consistentes para garantir que está verificando os dados mais atualizados
As leituras transacionais consomem o dobro das RCUs normais
**Para capacidade de gravação: **

As gravações transacionais exigem capacidade para duas fases:
Fase de preparação: 1 WCU para preparar a transação
Fase de confirmação: 1 WCU para confirmar a transação
Cada item escrito em uma transação consome o dobro das WCUs normais
Você está escrevendo um registro de 1 caractere (1 KB) por transação
Informações sobre os requisitos para APIs transacionais podem ser encontradas aqui.

Você precisará criar uma tabela com os seguintes elementos:

Nome da tabela: character_data
Chave de partição: id
Chave de classificação: username
Modo de capacidade: Provisionado
Unidades de capacidade de leitura: Calcule o número de RCUs a serem usadas aqui
Unidades de capacidade de gravação: Calcule o número de WCUs a serem usadas aqui
Desative o escalonamento automático (para este exercício, queremos que você configure manualmente a capacidade)
Inventário
Lambda chamado character_add
Validação de tarefas
Depois de criar a tabela do DynamoDB com as configurações corretas de capacidade provisionada, clique no botão Verificar meu progresso acima.

Pistas
Mergulhe profundamente no cálculo de RCU/WCU
4Pontos de penalidade
Desbloqueie o Clue
Solução
5Pontos de penalidade
Desbloqueie o Clue
```

sobre esse confesso que nao aprendi absolutamente nada como calculas tabelas do dynamodb, eu tenho que aprender isso nas aulas do omar, achei itneresante mas eu ja tinha feito antes por isso conseui, fazendo pela segunda vez que vi meu erro, eu nao sabia entao rever, nao tinha antoado antes