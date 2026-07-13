# JAM Acesso negado: o AWS IAM Access Analyzer afasta aqueles incômodos Gremlins de permissão!

task 1

eu consegui mas nao entendi o que era aqueles numeros

```wasm
Acesso negado: o AWS IAM Access Analyzer afasta aqueles incômodos Gremlins de permissão!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
JamAccessAnalyzer
arn:aws:access-analyzer:ap-southeast-2:375373117421:analyzer/JamChallengeAnalyzer

JamRegion
ap-southeast-2

JamS3Bucket
challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569

JamS3BucketArn
arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Identifique o ID de descoberta do acesso excessivamente permissivo
Pontos possíveis
24
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Você deve começar a procurar qualquer acesso excessivamente permissivo ou políticas configuradas incorretamente que possam permitir acesso não autorizado ao bucket de desafios do JAM. O IAM Access Analyzer é uma ferramenta poderosa para identificar e abordar vulnerabilidades de segurança em seu ambiente da AWS. Ao analisar políticas de recursos, listas de controle de acesso (ACLs) e outras configurações de permissões, o IAM Access Analyzer pode ajudar você a identificar possíveis riscos de segurança e garantir que seus recursos estejam devidamente protegidos. Especificamente para o bucket JAM Challenge, o IAM Access Analyzer pode ajudar a detectar e solucionar quaisquer configurações incorretas ou políticas de acesso excessivamente permissivas que possam estar deixando o bucket aberto ao acesso não autorizado.

Sua tarefa
Sua tarefa é examinar as descobertas ativas no IAM Access Analyzer, que lista os buckets do JAM challenge S3 como o recurso e identificar o Finding ID.

Começando
Aguarde até que o processo de criação do Analyzer seja concluído e, em seguida, inspecione as descobertas ativas do bucket de desafio JAM. Veja as descobertas ativas que listam o bucket S3 do desafio JAM como o recurso.

Observação: Certifique-se de ter feito login na região correta da AWS na qual esse desafio foi implantado. Você pode encontrar a região do desafio em Output Properties -> JamRegion

Inventário
O AWS IAM Access Analyzer já foi criado para você. Você pode encontrar o bucket JAM challenge S3 na seção Output Properties.

Serviços que você deve usar
AWS IAM, analisador de acesso IAM, Amazon S3

Validação de tarefas
A tarefa será concluída quando você inserir o Finding ID correto (listado no bucket de desafios do JAM) no campo de resposta. por exemplo: Uma amostra de Finding ID seria semelhante a: 9d1bbab7-cfbe-41fe-8fb3-1a4818b2f273

Observação: Você não precisa corrigir nenhuma descoberta nesta tarefa. Você consertaria a descoberta como parte da próxima tarefa.

Pistas
Como usar o IAM Access Analyzer
2Pontos de penalidade
Desbloqueie o Clue
Precisa de ajuda para identificar o acesso não intencional ao bucket de desafios
3Pontos de penalidade
Desbloqueie o Clue
```

task 2: 

```wasm
Acesso negado: o AWS IAM Access Analyzer afasta aqueles incômodos Gremlins de permissão!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Propriedades de saída
JamAccessAnalyzer
arn:aws:access-analyzer:ap-southeast-2:375373117421:analyzer/JamChallengeAnalyzer

JamRegion
ap-southeast-2

JamS3Bucket
challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569

JamS3BucketArn
arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 2: Resolva o acesso excessivamente permissivo
Pontos possíveis
56
Penalidade por pista
5
Pontos disponíveis
51
Verifique meu progresso

Tarefas e pistas
Plano de fundo
Agora que você encontrou um acesso excessivamente permissivo que poderia potencialmente permitir acesso não autorizado ao bucket do Jam Challenge, você precisa resolver essas políticas de acesso excessivamente permissivas que podem estar deixando o bucket aberto ao acesso não autorizado.

Sua tarefa
Sua tarefa é garantir que não haja descobertas ativas no IAM Access Analyzer, que lista os buckets JAM challenge S3 como o recurso.

Começando
Visite o bucket de desafios do Jam no console S3 e tente resolver o acesso excessivamente permissivo, conforme mencionado nas descobertas do IAM Access Analyzer.

Inventário
O AWS IAM Access Analyzer já foi criado para você. Você pode encontrar o bucket do Jam challenge S3 na seção Output Properties.

Serviços que você deve usar
AWS IAM, analisador de acesso IAM, Amazon S3

Validação de tarefas
Para confirmar uma alteração que você fez para resolver a descoberta, talvez seja necessário examinar novamente o recurso relatado na descoberta usando o link Examinar na página de detalhes das Conclusões do IAM Access Analyzer.

A tarefa será concluída automaticamente quando você corrigir o acesso excessivamente permissivo no bucket do Challenge e o Rescan mostrar um status de sucesso. Você também pode validar seu progresso selecionando o botão Check my progress.

Pistas
Conheça as descobertas do Access Analyzer
5Pontos de penalidade
Mostrar pista
Como resolver as descobertas do Access Analyzer
7Pontos de penalidade
Desbloqueie o Clue
Tudo o que você precisa saber para resolver as descobertas do Access Analyzer
8Pontos de penalidade
Desbloqueie o Clue
```

nao consegui fazer, nao entndi, tentei corrigir assim o bucket era esse:

```wasm
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::173358130759:root"
			},
			"Action": "s3:ListBucket",
			"Resource": "arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569"
		}
```

adicionei isso pra ninguem acessar:

```wasm
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::173358130759:root"
			},
			"Action": "s3:ListBucket",
			"Resource": "arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569"
		},
		{
			"Sid": "Statement1",
			"Effect": "Deny",
			"Principal": "*",
			"Action": [
				"s3:ListBucket",
				"s3:GetObject"
			],
			"Resource": [
				"arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569",
				"arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569/*"
			],
			"Condition": {
				"ArnNotLike": {
					"aws:PrincipalArn": "arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569"
				}
			}
		}
	]
}
```

bloqueie todos contra ele mas nao deu

vou pegar as dicas quero entender sobre esse servico

documentacao que a aws recomendou: (eu pesquisei mas nao apareceu tenho que aprender a pesquisar)

[https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/access-analyzer-findings-remediate.html](https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/access-analyzer-findings-remediate.html)

tentei isso aqui mas tamebm nao deu

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::173358130759:root"
			},
			"Action": "s3:ListBucket",
			"Resource": "arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569"
		},
		{
			"Sid": "Statement1",
			"Effect": "Deny",
			"Principal": "*",
			"Action": [
				"s3:GetObject",
				"s3:ListBucket"
			],
			"Resource": [
				"arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569",
				"arn:aws:s3:::challenge1bucket-12b8f020-61de-11f1-87ab-0ac462171569/*"
			],
			"Condition": {
				"StringNotLike": {
					"aws:PrincipalAccount": "3753-7311-7421"
				}
			}
		}
	]
}
```

consegui sim, CARACAAAA EU CONSEGUI

vou enviar a task dois ate onde peguei dica, eu amei esse jam insisti ate o final ate entender, ainda pedi um pouco sua ajuda

```json
Acesso negado: o AWS IAM Access Analyzer afasta aqueles incômodos Gremlins de permissão!
Selecione um desafio abaixo para começar.

Resolva usando:

Abra o console da AWS
>_AWS_CLI
Reiniciar o desafio
Tarefa 2: Resolva o acesso excessivamente permissivo
Pontos possíveis
56
Penalidade por pista
12
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Agora que você encontrou um acesso excessivamente permissivo que poderia potencialmente permitir acesso não autorizado ao bucket do Jam Challenge, você precisa resolver essas políticas de acesso excessivamente permissivas que podem estar deixando o bucket aberto ao acesso não autorizado.

Sua tarefa
Sua tarefa é garantir que não haja descobertas ativas no IAM Access Analyzer, que lista os buckets JAM challenge S3 como o recurso.

Começando
Visite o bucket de desafios do Jam no console S3 e tente resolver o acesso excessivamente permissivo, conforme mencionado nas descobertas do IAM Access Analyzer.

Inventário
O AWS IAM Access Analyzer já foi criado para você. Você pode encontrar o bucket do Jam challenge S3 na seção Output Properties.

Serviços que você deve usar
AWS IAM, analisador de acesso IAM, Amazon S3

Validação de tarefas
Para confirmar uma alteração que você fez para resolver a descoberta, talvez seja necessário examinar novamente o recurso relatado na descoberta usando o link Examinar na página de detalhes das Conclusões do IAM Access Analyzer.

A tarefa será concluída automaticamente quando você corrigir o acesso excessivamente permissivo no bucket do Challenge e o Rescan mostrar um status de sucesso. Você também pode validar seu progresso selecionando o botão Check my progress.

Pistas
Conheça as descobertas do Access Analyzer
5Pontos de penalidade
Ocultar pista
Você pode usar essa documentação para resolver as descobertas geradas pelo Access Analyzer: https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-findings-remediate.html

Como resolver as descobertas do Access Analyzer
7Pontos de penalidade
Ocultar pista
A descoberta do IAM Access Analyzer mostra que o bucket do S3 tem uma política de bucket excessivamente permissiva que precisa ser abordada.

Resolva essa política excessivamente permissiva e, para confirmar a alteração que você fez para resolver a descoberta, talvez seja necessário examinar novamente o recurso relatado na descoberta usando o link Redigitalizar na página de detalhes Descobrimentos.

AccessAnalyzerFindingsFixing
```

dcumantacao que usei 

[https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/access-analyzer-resources.html#access-analyzer-s3-directory](https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/access-analyzer-resources.html#access-analyzer-s3-directory)

[https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/access-analyzer-findings-remediate.html](https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/access-analyzer-findings-remediate.html)