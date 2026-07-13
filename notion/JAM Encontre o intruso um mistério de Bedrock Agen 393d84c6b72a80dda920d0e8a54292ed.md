# JAM Encontre o intruso: um mistério de Bedrock Agent

```verilog
Visão geral
Você é consultor sênior de segurança da SecureXYZ Solutions, contratado para consertar um sistema de segurança residencial que usa IA para detectar intrusos. O sistema processa imagens de diferentes cômodos de uma casa armazenadas no S3. O proprietário relatou que alguém está escondido em sua casa, mas o sistema está parcialmente quebrado. Sua tarefa é consertar o sistema e encontrar a localização do intruso.
```

```verilog
Encontre o intruso: um mistério de Bedrock Agent
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
												Propriedades de saída
ApplicationCredentials
aws secretsmanager get-secret-value --secret-id arn:aws:secretsmanager:us-east-1:833437220122:secret:LabStack-prewarm-8701d96b-a02a-44e1-9af7-d256ddc2b99a-ddLR7eQ1Py5jU54LdAaEGM-2-application-credentials-f4Jhnw --region us-east-1

ApplicationCredentialsSecretArn
arn:aws:secretsmanager:us-east-1:833437220122:secret:LabStack-prewarm-8701d96b-a02a-44e1-9af7-d256ddc2b99a-ddLR7eQ1Py5jU54LdAaEGM-2-application-credentials-f4Jhnw

ApplicationURL
http://LabSta-Appli-ZoToSDHHCWIX-1372089985.us-east-1.elb.amazonaws.com

BedrockAgent
FAF9KKBGGT

BedrockAgentAlias
HFEKNI7OM4

LambdaFunction
aws-jam-challenge-lambda

Region
us-east-1

SecurityGuardrail
arn:aws:bedrock:us-east-1:833437220122:guardrail/szopy9pmf82i

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Chatty AI tem laringite: corrigindo a voz perdida do agente
Pontos possíveis
60
Penalidade por pista
13
Pontos disponíveis
47
Verifique meu progresso

Tarefas e pistas
Antecedentes:
Como consultor sênior de segurança da SecureXYZ Solutions, você foi enviado com urgência para resolver uma situação crítica na residência da família Richardson. Seu Centro de Monitoramento detectou atividades suspeitas em seu sistema de vigilância residencial, que foi configurado usando o Amazon Bedrock e o Amazon Rekognition.

Esta manhã, seus sistemas detectaram uma tentativa de acesso não autorizado em que alguém conseguiu violar as configurações de segurança. As assinaturas de intrusão sugerem um hacker sofisticado que visou especificamente a infraestrutura de vigilância alimentada por IA. Eles conseguiram corromper as configurações do sistema, potencialmente criando pontos cegos na cobertura de segurança da casa.

O que é mais alarmante é que o sistema não está mais respondendo às consultas básicas de segurança. A adulteração parece deliberada, possivelmente como precursora de uma invasão física.

Você precisa:

Execute um diagnóstico completo do sistema para identificar áreas comprometidas.
Verifique se algum acesso não autorizado já ocorreu.
Restaure as configurações originais do Amazon Bedrock e do Rekognition.
O tempo é fundamental - enquanto estamos consertando o sistema, não podemos ter certeza se alguém já se infiltrou na casa. Seu objetivo principal é restaurar a integridade do sistema e, ao mesmo tempo, garantir a segurança da família durante esse período vulnerável.

Observação: *Para este desafio JAM, simplificamos as coisas usando fotos pré-capturadas de 6 câmeras em vez de feeds de câmera ao vivo. Esses instantâneos são armazenados em um bucket do S3. Analise essas imagens para se familiarizar com o layout da casa antes de prosseguir com o desafio. *

Alimentação da câmera: Quarto 1 | Quarto 2 | Porta da frente | Jardim | Hall | Cozinha

Arquitetura de aplicativos
! agente alicerce - mistério

Começando:
Navegue até o console da AWS e verifique se você está logado na região certa Challenges -> Find the Intruder : A Bedrock Agent Mystery -> Output Properties -> Region
Navegue até a seção Bedrock Agent para verificar as configurações do Bedrock Agent.
Analise a implementação atual do esquema OpenAPI.
Navegue até o aplicativo de vigilância doméstica usando o URL do aplicativo mencionado na seção de saída do JAM. Comece seu bate-papo com o aplicativo para encontrar o intruso na casa.
Inventário:
Aplicativo de vigilância doméstica
Agente Bedrock com esquema OpenAPI
Sistema de monitoramento de salas
Capacidades de detecção de intrusos
Serviços que você deve usar:
Base da Amazônia
Agentes Amazon Bedrock
AWS Lambda (para validação)
AWS CloudWatch
Suas tarefas:
Você pode usar o modelo Amazon Nova Lite em seu JAM Challenge.

Etapa 1: atualizar a configuração do aplicativo
a. Antes de começar a usar o aplicativo, você precisa fazer login no aplicativo. O URL do aplicativo e as credenciais para login podem ser encontrados nas propriedades de saída do Jam**: Challenges -> Find the Intruder : A Bedrock Agent Mystery -> Output Properties

URL do aplicativo
Para credenciais de aplicativos, você pode usar o JAM CLI e obter o nome de usuário e a senha do AWS Secrets Manager usando o comando cli encontrado aqui: ApplicationCredentials ou usando o console da AWS, visite o console do AWS Secrets Manager e obtenha as credenciais do segredo com o ARN: ApplicationCredentialsSecretArn
b. Depois de fazer login, você precisa atualizar a seção Configuração com os valores corretos para AWS Region, Bedrock Agent, Bedrock Agent Alias ID, que podem ser encontrados em Jam Output Properties**: Challenges -> Find the Intruder : A Bedrock Agent Mystery -> Output Properties

c. (Opcionalmente), você também pode seguir as etapas abaixo para validar os valores do console do agente Bedrock:

Na seção de saída do console JAM, copie o valor deRegion e cole-o no campo AWS Region do Aplicativo de Vigilância Doméstica.
Faça login no AWS Management Console e abra o console Amazon Bedrock em https://console.aws.amazon.com/bedrock/. Selecione Agentes no painel de navegação esquerdo. Em seguida, escolha agente com o nome aws-jam-challenge-bedrock-agent na seção Agentes.
Na seçãoVisão geral do agente, copie o valor no campoID e insira-o no campoBedrock Agent ID do Aplicativo de Vigilância Doméstica.
Na seção Aliases, copie o valor no campoID do alias e cole-o no campoBedrock Agent Alias ID do Aplicativo de Vigilância Doméstica.
Etapa 2: corrigir o aplicativo
Sua tarefa é identificar o problema, corrigir o aplicativo defeituoso e garantir que você consiga obter respostas adequadas às suas dúvidas de bate-papo relacionadas à segurança doméstica.

Você pode visitar o Aplicativo de Vigilância Doméstica que interage com a base e começar a fazer perguntas.

Exemplo: “**Onde está o intruso na casa? **”

🏠🔍 Dica profissional 1: *Pense no Amazon CloudWatch como a mãe digital superprotetora de sua casa — sempre assistindo, enviando notificações constantemente e, definitivamente, sabe quando suas câmeras de segurança capturaram o gato do vizinho invadindo a casa às 3 da manhã! *.

🏠🔍 Dica profissional 2: *Sempre que você fizer algumas alterações no agente, lembre-se de prepará-lo. Quando estiver pronto para implantar seu agente, você poderá criar uma versão do seu agente, que funciona como um instantâneo do seu agente no momento em que você cria a versão. Você cria uma versão e a aponta para o alias existente. Você configura seu aplicativo para invocar seu agente consultando o alias. *

Validação de tarefas:
Sua implementação será validada com base em:

Agente passando parâmetros com sucesso para o lambda de back-end
Capacidade do agente de responder à consulta de segurança**"Onde está o intruso na casa?” **
Você deve recebê-los na resposta:

Lista de todos os quartos
Se eles estão seguros
Nível de confiança
Imagem da sala.
Verificações bem-sucedidas de validação do esquema Bedrock OpenAPI
A tarefa será concluída automaticamente assim que você encontrar a solução. Além disso, você sempre poderá verificar seu avance pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Pistas
É necessária uma revisão da configuração do esquema
6Pontos de penalidade
Ocultar pista
Nota: Caso você esteja tendo dificuldades para habilitar o Model Access, consulte: https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html

Parece que você não está recebendo respostas adequadas, pois pode haver algum problema com o esquema de API aberta.

Dê uma olhada no esquema de API aberta definido para os grupos de ação do seu agente no Amazon Bedrock.

Um grupo de ação no Amazon Bedrock deve definir os parâmetros que o agente precisa invocar do usuário. Você também pode definir operações de API que o agente pode invocar usando esses parâmetros. Para definir as operações da API, crie um esquema OpenAPI no formato JSON ou YAML. Você pode criar arquivos de esquema OpenAPI e usar o editor de texto OpenAPI no console, que validará seu esquema. Veja se os parâmetros necessários não estão comentados na seção de solicitação do esquema.

Para saber mais sobre o Open API Schema, consulte: https://docs.aws.amazon.com/bedrock/latest/userguide/agents-api-schema.html

Se você ainda não tiver certeza de como resolver essa tarefa, verifique a próxima pista para obter um passo a passo da solução.

Passo a passo completo da solução
7Pontos de penalidade
Ocultar pista
Nota: Você pode usar o modelo Amazon Nova Lite em seu JAM Challenge. O acesso a todos os modelos da Amazon Bedrock Foundation é habilitado por padrão com as permissões corretas do AWS Marketplace.

Etapa 2: corrigir o aplicativo
Faça login no AWS Management Console e abra o console do Amazon Bedrock em https://console.aws.amazon.com/bedrock/.
Selecione Agentes no painel de navegação esquerdo. Em seguida, escolha agente com o nome aws-jam-challenge-bedrock-agent na seção Agentes.
Escolha Editar no Agent builder
Na seçãoGrupos de ação, selecione o grupo de ação AwsJamChallengeBedrockAgentActiongroup para editar.
Edite o campo existenteEsquema OpenAPI em linha** em Esquema de grupo de ações
O problema pode ser identificado em requestBody do esquema OpenAPI. O parâmetro room é um dos parâmetros obrigatórios esperados pelo agente de base, que seria passado para o lambda para processamento adicional. Desde que foi comentado, suas consultas estão falhando.
Para corrigir o mesmo, descomente as linhas de código abaixo

Número da linha: 18 a 19

   #required:
   #- room
   ```
---

*Número da linha: 21 a 23*
``` yaml
   #room:
   #  type: string
   #  description: The room to analyze (kitchen, hall, garden, frontdoor, bedroom1,
   #     bedroom2)
   ```
---

<a href="https://aws-jam-challenge-resources.s3.amazonaws.com/bedrock-agent-mystery/jam_openapi_schema.yaml">NOTA: Você pode se referir a isso e copiar/colar o esquema OpenAPI corrigido</a>

Você também pode dar uma olhada nas outras seções do esquema OpenAPI, mas **NÃO** faça nenhuma outra alteração que possa interromper a solução

Lembre-se de seguir as especificações do OpenAPI 3.0 e a formatação YAML ao fazer essas alterações para garantir a compatibilidade com os Amazon Bedrock Agents.

7. Para retornar à página de detalhes do grupo de ação, escolha **Salvar e sair**.
> *Se houver problemas na validação do esquema, um banner de erro será exibido. Para ver uma lista de erros, escolha **Mostrar detalhes** no banner. *
8. Para retornar ao console do agente Bedrock, escolha **Salvar e sair**.
8. (Opcional) Para aplicar as alterações que você fez no agente antes de testá-lo, escolha **Preparar** na janela**Agente de teste** ou na parte superior da página **Rascunho de trabalho**.
9. Na seção **Aliases**, selecione o alias `prod` e selecione **Editar**.
10. Na página **Editar alias**, em **Associar uma versão**, selecione **Criar uma nova versão e associe-a a esse alias**. Mantenha todos os outros valores intactos.
11. Selecione **Salvar** para salvar suas alterações.

Agora faça login no aplicativo conforme mencionado em “Suas tarefas -> Etapa 2: Atualizar a configuração do aplicativo”
Agora você pode tentar executar exemplos de consultas para garantir que as respostas adequadas sejam recebidas e validar se o agente agora manipula as informações da sala corretamente.

Exemplo: “**Onde está o intruso na casa? **”

eu nao terminei nao sei se nao entendi por estar forcando mt aprendendo coisas novas nos outros jams mesmo que ainda consegui fazer, mas eu acho mt dificil tambem o conteudo do amazon bedrock ainda ainda nao compreendo mt bem, todas as tarefas sao desbloqueadas, entao ja vou colocar todas mas nao fiz e nao temrinei 

Tarefa 2: Ensinando seu agente de IA a permanecer na pista
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Antecedentes:
Atualmente, o agente de IA de segurança doméstica está respondendo a todos os tipos de perguntas, incluindo perguntas sobre receitas culinárias, previsões do tempo e outros assuntos fora do assunto. Esse comportamento reduz sua eficácia como ferramenta de segurança e pode potencialmente vazar informações confidenciais. Sua tarefa é implementar barreiras de proteção adequadas para garantir que o agente permaneça focado apenas nas consultas relacionadas à segurança doméstica.

Arquitetura de aplicativos
! agente alicerce - mistério

Começando:
Faça login no console de interface do usuário do aplicativo e comece a explorar as respostas do agente.

Inventário:
Aplicativo de vigilância doméstica
Capacidades de detecção de intrusos usando o Bedrock Agent
Modelo de grades de proteção predefinido
Serviços que você deve usar:
Base da Amazônia
Corrimãos Amazon Bedrock
AWS Lambda (para validação)
AWS CloudWatch
Suas tarefas:
🏠🔍 Nota: Se você encontrar erros de tempo limite ou respostas inesperadas, clique em “Nova sessão” e aguarde 60 segundos antes de iniciar uma nova interação para garantir a reinicialização adequada da sessão e a limpeza do cache.

Investigue o comportamento atual: teste o agente com as consultas abaixo para entender seus padrões de resposta.
Pergunta 1: Há algum ponto cego na casa que esteja fora da cobertura da câmera?

Pergunta 2: Como preparar o chá?

Analise os recursos disponíveis: revise a configuração do agente para quaisquer barreiras de proteção existentes

Implemente a solução: aplique os controles apropriados para restringir as respostas dos agentes aos tópicos relacionados à segurança.

🏠🔍 Dica profissional 1: explore minuciosamente a configuração do serviço Bedrock. Às vezes, as soluções já estão disponíveis em sua conta da AWS. Verifique as configurações preexistentes que possam ajudar no controle de resposta.

🏠🔍 Dica profissional 2: *Sempre que você fizer algumas alterações no agente, lembre-se de prepará-lo. Quando estiver pronto para implantar seu agente, você poderá criar uma versão do seu agente, que funciona como um instantâneo do seu agente no momento em que você cria a versão. Você cria uma versão e a aponta para o alias existente. Você configura seu aplicativo para invocar seu agente consultando o alias. *

Validação de tarefas:
Sua implementação será validada com base em:

O agente só responde a consultas relacionadas à segurança. Mensagens de erro consistentes com base em consultas fora de contexto.
Rejeição apropriada de perguntas fora do tópico, como as perguntas 1 e 2 abaixo
Pergunta 1: Há algum ponto cego na casa que esteja fora da cobertura da câmera?

Pergunta 2: Como preparar o chá?

Para qualquer uma das consultas acima,
Você deve receber uma resposta como Your request contains content that is not allowed by our security policy. Please limit your queries to home security matters.

Nota: Em certos casos, devido ao cache do navegador, você pode não obter os resultados corretos. Nesses casos, selecione o botãoNova sessão na interface de bate-papo do aplicativo.

A tarefa será concluída automaticamente quando você encontrar a solução. Além disso, você sempre poderá verificar seu avance pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Pistas
O enigma do controle de resposta
4Pontos de penalidade
Desbloqueie o Clue
O Guia Detalhado do Guardião
5Pontos de penalidade
Desbloqueie o Clue

Tarefa 3: Ajustando o olhar atento: calibrando a detecção de intrusos
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Antecedentes:
Depois de restaurar a funcionalidade do sistema, surgiu um novo problema. O aplicativo de vigilância doméstica está sendo excessivamente sensível, gerando alarmes falsos ao identificar incorretamente molduras fotográficas (Hall) e crianças (quarto 2) como possíveis intrusos. Essa hipersensibilidade pode levar à fadiga de alerta e à perda de ameaças reais. Como consultor da SecureXYZ Solutions, você precisa ajustar o sistema de detecção para distinguir com precisão entre intrusos reais e elementos domésticos inofensivos.

Arquitetura de aplicativos
! agente alicerce - mistério

Começando:
Acesse o aplicativo de vigilância doméstica usando o URL fornecido
Revise os níveis atuais de confiança de detecção no aplicativo
Teste a precisão da resposta do aplicativo consultando sobre possíveis intrusos em diferentes salas
Inventário:
Aplicativo de vigilância doméstica
Bedrock Agent e Rekognition com níveis de confiança configurados
Imagens da câmera sala por sala
Serviços que você deve usar:
Amazon Rekognition
AWS Lambda (para validação)
AWS CloudWatch
Sua tarefa:
🏠🔍 Nota: Se você encontrar erros de tempo limite ou respostas inesperadas, clique em “Nova sessão” e aguarde 60 segundos antes de iniciar uma nova interação para garantir a reinicialização adequada da sessão e a limpeza do cache.

Analise as configurações atuais do limite de confiança no back-end do aplicativo Home Sureveillance e ajuste o parâmetro do nível de confiança para reduzir os falsos positivos e, ao mesmo tempo, manter a eficácia da segurança.
Teste o sistema consultando o status de todas as salas usando a interface de bate-papo. Identifique a sala com o intruso real comparando as pontuações de confiança. Verifique se itens domésticos comuns e membros da família não estão mais sinalizados como ameaças. Você pode usar as imagens da câmera abaixo para verificar a resposta do aplicativo. Alimentação da câmera: Quarto 1 | Quarto 2 | Porta da frente | Jardim | Hall | Cozinha
Identifique a sala ou o local onde o intruso real foi detectado fazendo esta consulta
“**Onde está o intruso na casa? **”

🏠🔍 Dica profissional: *Revise a arquitetura da solução para entender onde o back-end do aplicativo de vigilância doméstica está hospedado. *

Validação de tarefas:
Sua implementação será validada com base em:

Ajuste bem-sucedido dos limites de confiança
Identificação precisa da sala com o intruso real
Redução nas detecções de falsos positivos.
A tarefa será concluída automaticamente quando você identificar a sala correta com o intruso real. Você pode verificar seu progresso usando o botão “Verificar meu progresso” na tela de detalhes do desafio.

Pistas
Confiança é fundamental
4Pontos de penalidade
Desbloqueie o Clue
Ajuste de detecção passo a passo
5Pontos de penalidade
Desbloqueie o Clue
```