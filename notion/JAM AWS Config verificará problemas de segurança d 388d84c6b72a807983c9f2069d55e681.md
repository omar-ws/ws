# JAM AWS Config verificará problemas de segurança de co...

VISAO GERAL;

```jsx
A equipe de DevOps criou projetos de construção de código da AWS para vários projetos diferentes.

Como membro da equipe de segurança, você é responsável por garantir que todos os projetos do AWS CodeBuild estejam em conformidade com os padrões organizacionais. Em particular, você precisa garantir que nenhum projeto do AWS CodeBuild tenha exposto as credenciais da AWS e que nenhum projeto do AWS CodeBuild esteja sendo executado no modo privilegiado.

Você está pronto para o desafio?
```

TASK 1 E 2

```jsx
Plano de fundo
Sua equipe de DevOps desenvolveu vários projetos do AWS CodeBuild. Eles contam com você para validar se todos os projetos estão em conformidade com os requisitos de acesso privilegiado e para corrigir quaisquer projetos que não estejam em conformidade.

Sua tarefa
Todos os projetos do AWS Codebuild devem ter a verificação privilegiada desativada. Descubra os projetos não compatíveis com o AWS Codebuild e corrija-os adequadamente.

Navegue até o serviço AWS Config no AWS Console, que monitora e registra a configuração dos recursos em sua conta.

Encontre o nome da regra que começa com Labstack para identificar o projeto CodeBuild que não está em conformidade e corrigir o mesmo.

Começando
Navegue até a configuração da AWS e comece com a seção Regras. Nas Regras, você já tem uma regra existente para verificar a verificação de acesso privilegiado (o nome começa com Labstack).

Nota: Por favor, uncheck Allow AWS CodeBuild to modify this service role para que ele possa ser usado com este projeto de construção ao salvar.

Inventário
O AWS Config está habilitado na conta e os recursos necessários já foram descobertos. Se você não conseguir encontrar os recursos do codebuild, aguarde alguns minutos antes que os recursos apareçam e comece com a regra existente.

Serviços que você deve usar
AWS Codebuild e AWS Config

Validação de tarefas
A tarefa será concluída automaticamente quando você remediar o Não compatível Projeto CodeBuild. Como alternativa, você pode clicar em Verificar meu progresso para validar.

TASK 2

AWS Config verificará problemas de segurança de compilação de código
Selecione um desafio abaixo para começar.

Reiniciar o desafio
Tarefa 2: Crie uma nova regra do AWS Config para verificação de credenciais da AWS em projetos do AWS Codebuild
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Agora que você corrigiu os problemas de acesso privilegiado, você precisa identificar os projetos do AWS CodeBuild que expuseram as credenciais da AWS. Crie uma regra de configuração da AWS para verificar quais projetos de desenvolvimento de código da AWS têm credenciais da AWS expostas e quantos projetos do AWS CodeBuild não estão em conformidade.

Sua tarefa
Crie uma regra de configuração da AWS para verificar quais projetos de criação de código da AWS têm credenciais da AWS expostas e quantos projetos de construção de código da AWS não estão em conformidade.

Começando
Navegue até a configuração da AWS e comece com a seção Regras. Na seleção de regras, comece com as regras gerenciadas pela AWS.

Inventário
O AWS Config está habilitado na conta e os recursos já devem estar disponíveis e detectados. Se você não conseguir encontrar os recursos do AWS Codebuild, aguarde alguns minutos antes de começar a criar as regras.

Serviços que você deve usar
AWS Codebuild e AWS Config

Validação de tarefas
Digite o nome do projeto AWS Codebuild que não está em conformidade.
```

a