# JAM Backups resilientes: proteção contra o inesperado

```bash
Após uma interrupção global provocada por uma atualização defeituosa de um software antivírus amplamente usado, organizações em todo o mundo foram forçadas a reavaliar suas estratégias de backup. O incidente destacou a vulnerabilidade até mesmo dos sistemas mais robustos e enfatizou a necessidade crítica de soluções de backup confiáveis e automatizadas.

Na InnovateCorp, uma empresa de tecnologia com visão de futuro, a equipe de infraestrutura em nuvem foi encarregada de criar um processo de backup resiliente para suas instâncias do Amazon EC2. O objetivo é garantir que, no caso de falhas ou interrupções futuras causadas por fatores externos, a empresa possa restaurar rapidamente seus servidores de produção a partir dos backups mais recentes.

A equipe iniciou o processo de implementação dessa solução de backup usando recursos do AWS Systems Manager, como janelas de manutenção e runbooks de automação. No entanto, quando o projeto estava ganhando força, o arquiteto principal da iniciativa deixou a empresa inesperadamente, deixando o projeto incompleto. A responsabilidade de concluir essa tarefa crítica agora recai sobre você.
```

```bash
Tarefa 1: Prepare a instância!
Pontos possíveis
75
Penalidade por pista
0
Pontos disponíveis
75
Verifique meu progresso

Tarefas e pistas
Antecedentes
Você acabou de ser informado sobre o estado atual do projeto. A equipe havia estabelecido a base inicial, mas não tinha a arquitetura e a automação necessárias para realizar totalmente a estratégia de backup. Com o tempo passando e a ameaça de outra possível interrupção iminente, você tem a tarefa de concluir a solução de automação de backup.

Sua primeira tarefa é avaliar a configuração existente e identificar quaisquer lacunas na arquitetura. A partir daí, você precisará projetar e implementar uma solução abrangente que automatize o backup de instâncias críticas do EC2 e programe backups periódicos para garantir uma recuperação rápida em caso de falha do sistema.

Sua equipe começou a trabalhar em uma prova de conceito (POC), na qual criou uma Janela de manutenção do AWS Systems Manager para ser executada periodicamente a fim de capturar o backup da instância do EC2, mas sem nenhuma tarefa adicionada no momento. Além disso, para esse POC, uma instância de teste do Amazon EC2 foi provisionada. No entanto, para criar um backup consistente, você foi informado de que a instância deve ser interrompida primeiro. Então, como primeira etapa, você planejou encontrar uma maneira de automatizar a interrupção de uma instância do EC2 antes de criar o backup final.

Sua tarefa
Você é obrigado a realizar as seguintes ações:

Registre uma tarefa de automação com a janela de manutenção fornecida, que deve interromper a instância fornecida do Amazon EC2.
Após adicionar a tarefa, edite a programação da Janela de Manutenção para ser executada nos próximos 2 minutos para que a tarefa recém-registrada possa ser acionada.
Essa tarefa será concluída quando a determinada instância do EC2 entrar no estado stopped por meio da execução da tarefa de automação da janela de manutenção em questão.
Começando
Abra o AWS Console na página do desafio JAM e, em seguida, acesse o console AWS Systems Manager.
No painel de navegação, escolha Janelas de manutenção em Gerenciamento de alterações e, em seguida, escolha a Janela de manutenção chamada Backup-MaintenanceWindow.
Vá para a guia Tarefas e registre a nova tarefa Automação com o documento AWS-StopEC2Instance.
** NOTE: ** Para a opçãofunção de serviço do IAM, pesquise no menu suspenso fornecido e selecione Production-MaintenanceWindowsExecutionRole nome da função.

Finalmente, vá para a guia Descrição e edite a Janela de manutenção para modificar a expressãocron a fim de agendar a execução após os próximos 2 minutos (o timestamp deve ser especificado no fuso horário UTC).
Em caso de execução bem-sucedida, a instância EC2 em questão Production-Server deve entrar no estado stopped.

Inventário
Instância do Amazon EC2 chamada Servidor de produção.
Janela de manutenção denominada Janela de manutenção de backup.
Verifique a seçãoPropriedades de saída para obter mais detalhes.
Serviços que você deve usar
Instância de nuvem Amazon Elastic Compute (EC2)
AWS Systems Manager (janela de manutenção e automação)
Validação de tarefas
A tarefa será concluída automaticamente quando a janela de manutenção em questão, chamada Backup-MaintenanceWindow, executar e interromper com êxito o servidor de produção especificado. Além disso, você sempre pode verificar seu progresso pressionando o botãoVerificar meu progresso na tela de detalhes do desafio.

** NOTE: ** *Se essa tarefa for concluída com êxito, a instância será reiniciada automaticamente para as próximas ações da tarefa. *

Pistas
Preso! Posso obter ajuda, por favor?
7Pontos de penalidade
Desbloqueie o Clue
Ok! Preciso de mais algumas dicas para seguir em frente.
9Pontos de penalidade
Desbloqueie o Clue

```

```bash

```

a