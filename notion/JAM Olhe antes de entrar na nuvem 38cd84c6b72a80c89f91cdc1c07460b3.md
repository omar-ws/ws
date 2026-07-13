# JAM Olhe antes de entrar na nuvem

VISAL GERAL:

```verilog
**Descubra as armadilhas escondidas no back-end dos serviços da AWS! **

Neste evento especial de hackathon, os participantes assumirão o papel das equipes de design da AWS e explorarão minuciosamente as fraquezas no design e na implementação de serviços. Da segurança à disponibilidade e à performance, você se aprofundará em cada aspecto do design da AWS.

Junte-se a nós e prepare-se para seu projeto futuro!

Como consultor novato, você recebeu uma parte do design da infraestrutura da AWS pela primeira vez. Você já fez o exame de certificação e está tentando se familiarizar com o AWS Management Console o máximo possível, mas essa é sua primeira experiência como responsável pelo design de um projeto completo e, sinceramente, você está muito ansioso.

Nesse momento, você se deparou com o anúncio do evento de hackathon mencionado acima nas redes sociais e decidiu participar com seus colegas, na esperança de ganhar um pouco mais de experiência.
```

nao onsegui fazer a ultima task por erro do JAM

task 1

```verilog
Tarefa 1: O VPC Lambda não funciona
Pontos possíveis
20
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Você é engenheiro de aplicação e está desenvolvendo uma função do AWS Lambda.

O código do aplicativo está completo e configurado como um VPC Lambda porque você precisa acessar um recurso na Internet (http://example.com) e um servidor web hospedado em uma instância do EC2 em uma sub-rede privada.

A VPC, as sub-redes e os recursos relacionados, como tabelas de rotas, já foram criados pela equipe de infraestrutura e têm uma configuração padrão de duas sub-redes públicas e duas sub-redes privadas.

Sua tarefa
Você verificou o aplicativo e descobriu que algumas peças não estão funcionando corretamente.

Corrija esse problema sem modificar o ENI, a configuração da sub-rede na categoria VPC, a tabela de rotas, o Internet Gateway, o NAT Gateway e o código do aplicativo!

Você pode modificar a configuração do Lambda.

Começando
Abra o console do AWS Lambda e execute a função “MyFunction”.

A execução será concluída com êxito, mas você encontrará o erro no CloudWatch Logs.

Inventário: recursos que você precisa usar nesta tarefa
AWS Lambda
Registros do Amazon CloudWatch
Amazon VPC
Serviços que você deve usar
AWS Lambda
Amazon VPC
Validação de tarefas
A tarefa será automaticamente marcada como concluída em alguns minutos se você for bem-sucedido. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na seção de detalhes do desafio.

Pistas
Configuração do Lambda VPC
2Pontos de penalidade
Desbloqueie o Clue
Passo a passo completo
2Pontos de penalidade
Desbloqueie o Clue
```

task 2:

```verilog
Tarefa 2: O aplicativo não consegue acessar seu S3 Bucket
Pontos possíveis
20
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Você participou de um projeto de modernização de aplicativos.

Como arquiteto de infraestrutura, a equipe de aplicativos solicita que você forneça um bucket do S3 e uma função do IAM para a função Lambda usar com base no design CRUD. Você escreveu um modelo do CloudFormation e o implantou na conta de teste.

No entanto, algumas horas depois, você recebeu uma reclamação deles - *ei, nossa função Lambda não consegue ler/gravar nenhum objeto de/para o bucket! *

Segundo eles, a função Lambda reside na mesma conta.

Sua tarefa
Analise os recursos que você criou para descobrir o que estava errado. O que você criou foi um bucket do S3 e uma função do IAM. Parece que qualquer um deles é o culpado. Depois de encontrada, edite a parte suspeita diretamente para isolar o problema, para que você possa modificar o modelo do CloudFormation posteriormente.

**Nota: ** Consulte a seção Propriedade de saída do desafio do Jam para descobrir o nome do bucket do S3 e a função do IAM na qual você precisa trabalhar.

Começando
Abra o Management Console para dar uma olhada.

Inventário: recursos que você precisa usar nesta tarefa
Balde S3
Função do IAM e política personalizada
Serviços que você deve usar
Amazon S3
ERA O OBJETIVO
Validação de tarefas
A tarefa será automaticamente marcada como concluída em alguns minutos se você for bem-sucedido. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na seção de detalhes do desafio.

Pistas

```

task 3:

```verilog
Tarefa 3: Bloqueio do KMS! - Corrija o privilégio de administração de chaves KMS
Pontos possíveis
20
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Você é administrador de segurança da AWS e criou uma chave KMS (Key Management Service) durante a fase de desenvolvimento.
Após o término da fase de desenvolvimento, você descobriu que não conseguia mais gerenciar a chave KMS.
Sua tarefa
Investigue por que você perdeu a capacidade de gerenciar a chave KMS e resolva o problema para poder recuperar o controle administrativo sobre ela.
Você está autorizado a usar a função temporária de administrador da AWS para investigar e resolver o problema.
Observe que as permissões do KMS são gerenciadas pela política baseada em recursos do KMS, não pela política do IAM nesta empresa.
Ignore a seguinte declaração de política que você pode ver na política de chaves do KMS. Esta declaração está presente devido a restrições de plataforma no AWS Jam:
{
  "Sid": "IGNORE THE FOLLOWING POLICY",
  "Effect": "Allow",
  "Principal": {
    "AWS": "arn:aws:iam::111122223333:root"
  },
  "Action": "kms:*",
  "Resource": "*"
}
Começando
Abra o console do AWS KMS e verifique o motivo pelo qual você não consegue gerenciar a chave.
Chave KMS de destino: jam-data-encryption-key
Você pode mudar para a função IAM atribuída temporariamente para realizar a tarefa.
Função temporária de administrador do IAM: jam-aws-tmp-admin-role
Você pode encontrar seu próprio ARN de função do IAM nas “Propriedades de saída” no menu à esquerda. Verifique o valor de “JamTask3SecurityAdminRoLearn”.
Inventário: recursos que você precisa usar nesta tarefa
Serviço de gerenciamento de chaves da AWS (KMS)
ERA O OBJETIVO
Serviços que você deve usar
Serviço de gerenciamento de chaves da AWS (KMS)
https://docs.aws.amazon.com/kms/latest/developerguide/overview.html
Validação de tarefas
A tarefa será automaticamente marcada como concluída em alguns minutos se você for bem-sucedido.
Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na seção de detalhes do desafio.
Pistas
O que você deve fazer primeiro?
2Pontos de penalidade
Desbloqueie o Clue
O passo a passo completo
2Pontos de penalidade
Desbloqueie o Clue
```

task 4:

```verilog
Tarefa 4: Acesso seguro entre contas
Pontos possíveis
20
Penalidade por pista
0
Pontos disponíveis
20
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Você é engenheiro do departamento de TI e está fornecendo dados usando o Amazon S3.

Você já configurou o bucket do S3 e colocou os arquivos de dados nesse S3. Então, os usuários começaram a obter os dados no bucket S3 de outra conta da AWS. Somente usuários atribuídos a uma função específica (S3CrossAccountAccess) devem poder acessar esses dados, mas você foi informado de que todos os usuários dessa conta podem acessá-los.

Sua tarefa
Verifique as configurações e constatou que algumas peças não estão funcionando corretamente.

Observação: consulte a seção Propriedades de saída do desafio Jam para descobrir o nome do bucket do S3 e o ID da conta de acesso cruzado no qual você precisa trabalhar.

Começando
Abra o Management Console para dar uma olhada.

Inventário: recursos que você precisa usar nesta tarefa
Balde S3
Serviços que você deve usar
Amazon S3
Validação de tarefas
A tarefa será automaticamente marcada como concluída em alguns minutos se você for bem-sucedido. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na seção de detalhes do desafio.

Pistas
Uma dica
2Pontos de penalidade
Desbloqueie o Clue
O passo a passo completo
2Pontos de penalidade
Desbloqueie o Clue
```

a