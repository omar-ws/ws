# JAM Introdução às funções de etapa #5

> 
> 
> 
> Como engenheiro recém-designado para um projeto inovador da AWS, você se encontra imerso em uma arquitetura sem servidor de ponta. Para contribuir de forma eficaz com esse projeto, você precisa desenvolver rapidamente sua expertise em serviços sem servidor da AWS e suas capacidades de orquestração.
> 
> Após uma análise cuidadosa, você decidiu estrategicamente começar sua jornada de aprendizado com o AWS Step Functions, um serviço poderoso que permite coordenar vários serviços da AWS em fluxos de trabalho sem servidor por meio de uma interface visual.
> 
> Neste desafio, você dominará os fundamentos do AWS Step Functions criando, configurando e executando máquinas de estado.
> 

duvidas: o que seria uma arquitetura sem servidor, um docker?

o que e aws step functions?

task 1:

```jsx
Propriedades de saída
LambdaFunctionArn
arn:aws:lambda:us-east-1:675214452622:function:LabStack-prewarm-1aaeb2bf-4ec7-4-CheckNameFunction-t3VurlBwf11X

StateMachineArn
arn:aws:states:us-east-1:675214452622:stateMachine:JamStateMachine-AwJPbvkg1wwD

oTeamRoleName
AWSLabsUser-jvZbHhWRg5WPsimne2Xct9

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Coloque Lambda:Invoke Action
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
40
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Como engenheiro recém-designado para um projeto inovador da AWS, você se encontra imerso em uma arquitetura sem servidor de ponta. Para contribuir de forma eficaz com esse projeto, você precisa desenvolver rapidamente sua expertise em serviços sem servidor da AWS e suas capacidades de orquestração.

Após uma análise cuidadosa, você decidiu estrategicamente começar sua jornada de aprendizado com o AWS Step Functions, um serviço poderoso que permite coordenar vários serviços da AWS em fluxos de trabalho sem servidor por meio de uma interface visual.

Compreendendo as funções do Step
O AWS Step Functions é um serviço sofisticado de fluxo de trabalho visual que capacita os desenvolvedores a aproveitar todo o potencial dos serviços da AWS ao:

Criação de aplicativos distribuídos resilientes
Automatização de processos comerciais complexos
Orquestrando microsserviços com precisão
Criação de canais poderosos de processamento de dados e aprendizado de máquina
Um dos recursos mais valiosos da Step Functions é sua integração perfeita com outros serviços da AWS. Essas integrações vêm em duas formas:

Integrações padrão do AWS SDK — Suporte a toda a gama de ações de API
Integrações otimizadas - Fornecendo conexões simplificadas e específicas para serviços populares
Sua tarefa
Sua primeira tarefa prática é configurar uma máquina de estado Step Functions para invocar uma função Lambda, um dos padrões de integração mais comuns e poderosos em arquiteturas sem servidor.

Em seu ambiente da AWS, você encontrará:

Uma máquina de estado pré-criada (chamada algo como JamStateMachine-****)
Uma função Lambda pré-criada (chamada algo como ****-CheckNameFunction-****)
A função Lambda executa uma verificação de validação de segurança, examinando se a palavra “mal” aparece na propriedade name das solicitações recebidas. Isso representa uma versão simplificada dos padrões de validação de entrada comumente usados em aplicativos de produção.

Seu objetivo é modificar a máquina de estado existente para invocar adequadamente essa função do Lambda e processar sua resposta.

Exemplo de formato de entrada
{
  "name": "john tanaka evil"
}
Inventário
Step Functions State Machine - O orquestrador de fluxo de trabalho que você configurará
Função Lambda - O serviço de validação que você integrará
Começando
Siga estas etapas detalhadas para concluir a tarefa:

Acesse o Step Functions Console
Navegue até a página AWS Step Functions no AWS Management Console
Selecione a máquina de estado com um nome como JamStateMachine-****
Clique no botão “Editar” para entrar no editor de fluxo de trabalho
Modifique a máquina de estados
Exclua o estado do Passe chamado "DeleteThisState"
Adicione um novo estado de integração da função Lambda
No painel de configuração de estado, selecione a função Lambda com um nome como ****-CheckNameFunction-****
Teste sua integração
Salve sua configuração de máquina de estado atualizada
Clique em “Iniciar execução” para testar seu fluxo de trabalho
Forneça uma entrada de teste com o formato: {"name": "john tanaka evil"}
Observe os resultados da execução e verifique se a função Lambda foi invocada corretamente
State machine with Lambda integration
Serviços que você deve usar
AWS Step Functions — Para orquestração do fluxo de trabalho e configuração da máquina de estado
AWS Lambda — Para executar a função de validação
Validação de tarefas
Essa tarefa será marcada automaticamente como concluída quando você tiver sucesso:

Removido o estado do Passe
Foi adicionada uma ação Lambda Invoke configurada corretamente
Salvou a máquina de estado atualizada
Executou o fluxo de trabalho com um JSON de entrada contendo o termo “mal”
Além disso, você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela Detalhes do desafio.
```

para que serve esse servico stap functions

aprender mais a fundo sobre o stap functions

eu acho que o step funcitions serve para executar servicos de uma forma visual

foi facil dms, tava explicando o passo a passo

servicos sem servidor sao lambdas, e acho que tambem kubernetes e containers se for naa aws

task 2:

```jsx

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
LambdaFunctionArn
arn:aws:lambda:eu-west-2:064637953217:function:LabStack-prewarm-05677a65-cedc-4-CheckNameFunction-bCL6nYJc5efZ

StateMachineArn
arn:aws:states:eu-west-2:064637953217:stateMachine:JamStateMachine-osQSz4HDROBA

oTeamRoleName
AWSLabsUser-hxDNakkBx17NLVAov93gui

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Put Choice Flow
Pontos possíveis
40
Penalidade por pista
0
Pontos disponíveis
40
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Como engenheiro recém-designado para um projeto inovador da AWS, você se encontra imerso em uma arquitetura sem servidor de ponta. Para contribuir de forma eficaz com esse projeto, você precisa desenvolver rapidamente sua expertise em serviços sem servidor da AWS e suas capacidades de orquestração.

Após uma análise cuidadosa, você decidiu estrategicamente começar sua jornada de aprendizado com o AWS Step Functions, um serviço poderoso que permite coordenar vários serviços da AWS em fluxos de trabalho sem servidor por meio de uma interface visual.

Sua tarefa
Depois de integrar com sucesso uma função do Lambda na Tarefa 1, seu próximo desafio é implementar a lógica de ramificação condicional em sua máquina de estado do Step Functions. Isso permitirá que seu fluxo de trabalho tome decisões inteligentes com base na saída da função Lambda.

Especificamente, você precisa criar um estado de escolha que avalie o resultado da validação da função Lambda e direcione o fluxo de trabalho para caminhos diferentes, dependendo se a entrada é válida ou contém conteúdo proibido.

Requisitos técnicos
Você deve configurar seu fluxo de trabalho para:

Avalie a propriedade $.isValid retornada pela função Lambda
Se $.isValid for igual a true, direcione a execução para um estado de sucesso
Se $.isValid for igual a false, direcione a execução para um estado de falha
Esse padrão representa um fluxo de trabalho de validação comum usado em aplicativos de produção, em que ações diferentes são tomadas com base no fato de a entrada atender a determinados critérios.

Inventário
Step Functions State Machine - O fluxo de trabalho que você aprimorará com a lógica condicional
Começando
Siga estas etapas detalhadas para implementar a lógica de ramificação condicional:

Acesse sua máquina estadual
Navegue até a página AWS Step Functions no AWS Management Console
Localize e selecione sua máquina de estado (chamada de algo como JamStateMachine-****)
Clique no botão “Editar” para entrar no editor de fluxo de trabalho
Adicionar lógica condicional
Depois do estado do Lambda Invoke, adicione um novo estado Choice
Configure o estado Choice com as seguintes regras:
Regra #1: Se $.isValid for igual a true, faça a transição para o estado Succeed
Regra padrão: transição para um estado de falha
Adicione os estados de terminal de sucesso e falha apropriados ao seu fluxo de trabalho
Teste seu fluxo de trabalho aprimorado
Salve sua configuração de máquina de estado atualizada
Execute a máquina de estado com várias entradas de teste:
Entrada válida (sem “mal”): {"name": "john tanaka"}
Entrada inválida (com “mal”): {"name": "john tanaka evil"}
Verifique se seu fluxo de trabalho é direcionado corretamente para os estados de sucesso ou falha com base na entrada
State machine with conditional logic
Comportamento esperado
Quando o nome da entrada NÃO contém “mal”, a função Lambda retorna {isValid: true} e seu fluxo de trabalho deve atingir o estado de sucesso
Quando o nome da entrada contém “evil”, a função Lambda retorna {isValid: false} e seu fluxo de trabalho deve atingir o estado Fail
Serviços da AWS necessários
AWS Step Functions — Para implementar e testar a lógica condicional do fluxo de trabalho
AWS Lambda — A função de validação integrada ao seu fluxo de trabalho
Critérios de validação de tarefas
Essa tarefa será marcada automaticamente como concluída quando você tiver sucesso:

Adicionou um estado de escolha após sua ação Lambda Invoke
Configurei as regras de escolha para avaliar $.isValid e rotear para os estados apropriados
Estados de terminal de sucesso e falha adicionados
Salvou a máquina de estado atualizada
Executou o fluxo de trabalho com entradas de teste para verificar o comportamento adequado de ramificação
Além disso, você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela Detalhes do desafio.

Pistas
Links úteis
4Pontos de penalidade
Desbloqueie o Clue
Solução
5Pontos de penalidade
Desbloqueie o Clue
```

sera que se eu tiver um aba de execucao e um aba de configuracao funciona sem eu ter que abrir a aba varias vezes?

devo aprender mais sobre esse servico 

o que e novo choice?

quando vai colocar um funcao lambda tem que ter o $ e o ponto

```jsx
$.{name} == true
```

entendi como funciona, nao precisa adicionar funcao para o evil

consegui entender o fluxo tudo, o choice o fluxo com falha e o state

parametro de boleano, nome da funcao que ele leva em consideracao no caso do laboratorio o isValida, que tem que adicionar o cifra igual no JS e o ponto

mas nao consgui terminar por erro da plataforma


consegui terminar era mais uma aula do que desafio mesmo