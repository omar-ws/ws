# SIMU JAM (medio) Mentes silenciosas na nuvem: nenhuma invasão é permitida

```jsx
Visão geral
O Amazon Bedrock é um serviço totalmente gerenciado que fornece acesso a modelos de base (FMs) de alto desempenho das principais empresas de IA, como AI21 Labs, Anthropic etc. Ele simplifica o desenvolvimento de aplicativos de IA generativos e garante privacidade e segurança.

Considere um cenário em que você precise usar o Bedrock em sua nuvem privada virtual (VPC). Você pode usar o Bedrock simplesmente chamando a API, mas em um ambiente de segurança crítica, talvez não consiga conectar o Internet Gateway à VPC. Nesse caso, é possível chamar Bedrock a partir da VPC? Há alguma solução para esse problema?

introduction overview
Neste desafio, você aprenderá a usar o Bedrock de forma privada.
```

```jsx
task 1
Propriedades de saída
LambdaFunctionName
JamVPCLambda

LambdaSecurityGroupId
sg-0c37f8511ff3e11f8

VPCId
vpc-065e786d3e87746c9

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: implantar a função lambda na VPC
Pontos possíveis
30
Penalidade por pista
0
Pontos disponíveis
30
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Você é arquiteto de soluções e deseja usar o Amazon Bedrock para uma carga de trabalho com requisitos de segurança muito rígidos. Isso significa que você não pode colocar um gateway de Internet na VPC. É possível usar o Bedrock de forma privada (sem o Internet Gateway)?

Sua tarefa
Antes de tudo, implante a função lambda em sua VPC.

Use a função lamdba chamada JamVPCLambda, vpc chamada JamVPC.

Inventário
Amazon VPC - JamVPC
Função AWS Lambda - JamVPCLambda
Começando
Abra o AWS Management Console e navegue até o console do AWS Lambda.
Você encontrará a função lambda chamada JamVPCLambda.
Você deve implantar essa função na VPC chamada JamVPC.
Você deve usar o grupo de segurança chamado JamVPCLambdaSG.
Serviços que você deve usar
Amazon VPC
AWS Lambda
Validação de tarefas
Essa tarefa será marcada automaticamente como concluída quando:

A função Lambda é implantada em sua VPC.
Além disso, você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela Detalhes do desafio.

Pistas
Alguns links úteis
3Pontos de penalidade
Desbloqueie o Clue
Soluções
3Pontos de penalidade
Desbloqueie o Clue
```

ja sabia fiz rapido por que ja tinha feito ontem

```jsx
task 2
Propriedades de saída
LambdaFunctionName
JamVPCLambda

LambdaSecurityGroupId
sg-0c37f8511ff3e11f8

VPCId
vpc-065e786d3e87746c9

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Ligue para Bedrock em particular
Pontos possíveis
75
Penalidade por pista
0
Pontos disponíveis
75
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Bom trabalho! Você conseguiu colocar a função Lambda na VPC. No entanto, essa VPC não tem um gateway de Internet, portanto, a função Lambda não pode invocar o Bedrock. Na verdade, você pode tentar invocar a função Lambda. (Você deve receber um erro de tempo limite.) Você não pode conectar um gateway de Internet a essa VPC devido a requisitos rígidos de segurança. Quais etapas você precisa para invocar o bedrock executando o Lambda?

Sua tarefa
(1) Verifique JamVPCLambda.

(2) Execute a função Lambda na VPC e obtenha o resultado. A função Lambda invoca o alicerce. Devido aos requisitos de segurança, o Internet Gateway não pode ser conectado.

Inventário
Amazon VPC - JamVPC
Função AWS Lambda - JamVPCLambda
Amazon Bedrock - Which foundation model do you plan to use?
Começando
Abra o AWS Management Console e navegue até o console do Amazon VPC.
Você encontrará a VPC chamada JamVPC.
Serviços que você deve usar
Amazon VPC
AWS Lambda
Validação de tarefas
Essa tarefa será marcada automaticamente como concluída quando:

Execute a função Lambda na VPC e obtenha o resultado. (sem Internet Gateway)
Observe que, mesmo que você tenha as configurações corretas, talvez seja necessário esperar um pouco para invocar a função lambda

Além disso, você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela Detalhes do desafio.

Pistas
Alguns links úteis
7Pontos de penalidade
Desbloqueie o Clue
Soluções
9Pontos de penalidade
Desbloqueie o Clue
```

aprendi sobre por que e runtime, e nao somente o bedrock, quando e para invocar agente sera agent-runtime

aprendi a diferenca de modelo  agente, modelo seria uma ia, agente seria que faz mais tarefas

```jsx
task 3

Mentes silenciosas na nuvem: nenhuma invasão é permitida
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 3: Somente modelo específico
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Bom trabalho! Você executou com sucesso a função Lambda na VPC sem um gateway de internet. Na função Lambda, invocando o bedrock usando o modelo de fundação amazon.nova-lite-v1:0.

Se você receber um erro de tempo limite, aguarde um pouco.
No entanto, não foi o fim da história. Devido a rígidos requisitos de segurança, você foi solicitado a impossibilitar a invocação do bedrock usando qualquer outro modelo que não seja amazon.nova-lite-v1:0. Como você pode fazer isso?

Sua tarefa
Torne impossível invocar o alicerce usando qualquer outro modelo que não seja amazon.nova-lite-v1:0.

Devido aos requisitos de segurança, você não pode realizar nenhuma operação relacionada ao IAM.

Isso significa que você não pode editar ou adicionar políticas do IAM anexadas às funções do IAM e não precisa acessar um console do IAM para resolver essa tarefa.

Inventário
Amazon Bedrock - amazon.nova-lite-v1:0
Função AWS Lambda - JamVPCLambda
Começando
Abra o AWS Management Console e navegue até o console do Amazon VPC.
Você encontrará a VPC chamada JamVPC.
Serviços que você deve usar
Rocha da Amazônia
AWS Lambda
Validação de tarefas
Essa tarefa será marcada automaticamente como concluída quando:

Tornando impossível invocar o alicerce em qualquer outro modelo que não seja amazon.nova-lite-v1:0
Além disso, você sempre pode verificar seu progresso clicando no botão Verificar meu progresso na tela Detalhes do desafio.

Pistas
Alguns links úteis
4Pontos de penalidade
Desbloqueie o Clue
Soluções
5Pontos de penalidade
Desbloqueie o Clue
```

```jsx
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Principal": "*",
              "Effect": "Allow",
              "Action": "bedrock:InvokeModel",
              "Resource": "arn:aws:bedrock:REGIAO::foundation-model/MODEL-ID"
          }
      ]
  }
```

a