# JAM Dados com as estrelas! #8

conexto:

> 
> 
> 
> Um problema comum no gerenciamento de dados da área de saúde são os usuários internos que, de outra forma, deveriam ter acesso às PHI, deixarem sua curiosidade se apoderar deles. Eles ouvem que uma pessoa famosa está ou esteve em suas instalações e vasculham seus registros de saúde. Dê uma olhada neste [artigo - Violações internas identificadas por três profissionais de saúde](https://www.hipaajournal.com/insider-breaches-healthcare-providers-fl-ma-in/) para ler sobre um exemplo da vida real. Em parte, é por isso que a HIPAA 45 C.F.R. § 164.312 (b) exige que todo acesso ao ePHI seja registrado. No entanto, isso pode ser difícil de implementar.
> 
> Você faz parte da equipe de conformidade da área de saúde e deseja garantir que sua equipe esteja seguindo os processos em conformidade com a HIPAA. Você tem seus dados de pacientes armazenados em buckets S3 na conta da AWS e quer ter certeza de que tem o registro correto habilitado para descobrir quem está acessando quais dados.
> 
> Serviços da AWS usados:
> 
> 1. IAM
> 2. S3
> 3. Registros de acesso do S3
> 4. KMS

o que e PHI?

task 1:

```jsx
O Código 164.308 (a) (4) (4)) dos Estados Unidos especifica que todo o acesso a informações eletrônicas de saúde protegidas (ePHI) deve ser restrito apenas a partes com funções aprovadas para acessar tais dados. Nesta tarefa, você é um membro da equipe de segurança da AWS que tem a tarefa de proteger buckets do AWS S3 que contêm dados ePHI (esse bucket já está configurado para você).

Sua tarefa:

Existem 2 usuários com contas do IAM, USER-A e USER-B. Seu trabalho é:

Restrinja completamente o USER-B de ver ou interagir com quaisquer dados no intervalo com o nome que contém patientdata
Conceda ao USUÁRIO-A acesso total a todos os dados nesse intervalo.
Validação de tarefas:

Para marcar como concluída, termine sua tarefa e clique em verificar meu progresso no console Jam.

Aprendizados adicionais:

Consulte a documentação da AWS para saber quais outros controles você pode aplicar usando as políticas de bucket do S3.

https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html
```

o que indica que aqui eu deveria mexer no s3 bucket do que no IAM?

tenho que aprender a resovler direto o problemae

fiz esse bucket

```jsx
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Principal": {
			    "AWS":"arn:aws:iam::078995151897:user/USER-B"
			} ,
			"Effect": "Deny",
			"Action": [
				"s3:*"
			],
			"Resource": [
				"arn:aws:s3:::jam-challenge-patientdata-us-east-1-078995151897"
				"arn:aws:s3:::jam-challenge-patientdata-us-east-1-078995151897/*"
			]
		}
	]
}
```

se aprofundar mais nisso

EU TENHO QUE ENTENDER A DIFERENCA DE QUANDO E UM BUCKET POLICE PARA SUBIR UM SITE E QUANDO E UM BUCKET POLICE PARA PARA BLOQUEAR UM USUARIO POR EXEMPLO, QUANDO USAR O O ARN NORMAL E O /*

quando tem mais de uma opcao no json tipo um principal 

maneira ERRADA:

```jsx
}
“AWS”:”ARNSHFNS”,
”AWS”:”ARNSEDFSE” 
}
```

maneira CORRETA

```jsx
}
  [
“AWS”:”ARNSHFNS”,
”AWS”:”ARNSEDFSE” 
   ]
}
```

dessa forma:

```jsx
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Allow",
			"Principal": {
			    "AWS": [
			        "arn:aws:iam::078995151897:user/USER-B",
			        "arn:aws:iam::078995151897:user/USER-A"
			        ]
			},
			"Action": "s3:*",
			"Resource": [
				"arn:aws:s3:::jam-challenge-accesslogs-us-east-1-078995151897",
				"arn:aws:s3:::jam-challenge-accesslogs-us-east-1-078995151897/*"
			]
		}
	]
}
```

conseguiiiiii, compreendi

task 2: 

```wasm
Antecedentes:

Conforme mencionado na descrição resumida desse desafio, 45 CFR 164.312 (b)) afirma que uma entidade coberta ou um associado comercial deve implementar hardware, software e/ou mecanismos processuais que registrem e examinem a atividade em sistemas de informação que contêm ou usam informações eletrônicas de saúde protegidas.

O bucket de dados do paciente já está configurado para você e que você usou nas Tarefas 1 e 2. Além disso, o bucket de destino para armazenar registros de acesso já foi criado para você.

Sua tarefa:

Essa tarefa tem dois componentes:

Você deve fazer o upload do arquivo PHI de amostra fornecido para ser baixado aqui. para o bucket de dados do paciente criado para você.
Em seguida, como membro da equipe de segurança da AWS, deve habilitar o registro de acesso ao S3 Server no bucket que contém o ePHI.
Os registros de acesso devem ser armazenados em um bucket separado que já foi criado para você com o nome contendo accesslogs.
Validação da tarefa:

Para marcar como concluída, conclua sua tarefa e clique em verificar meu progresso no console Jam.

Exercício opcional:

Quando você configura os registros de acesso do S3 pela primeira vez, leva de 30 a 45 minutos para obter o conjunto inicial de registros. Depois disso, ele carrega os registros para que você acesse o bucket e o objeto com frequência.

Se você quiser ver a aparência dos registros de acesso do S3, terá que esperar aproximadamente 45 minutos e depois disso, poderá ver alguns registros preenchidos. Essa etapa é totalmente opcional e não será considerada para avaliação de tarefas.

Pistas
Você fez upload do arquivo de amostra e habilitou os logs de acesso do S3?
4Pontos de penalidade
Desbloqueie o Clue
Como encontrar o bucket de destino para o registro de acesso
5Pontos de penalidade
Desbloqueie o Clue
Instruções passo a passo
6Pontos de penalidade

```

o que e um acess server?

conseguiiii, compreendi

server s3, sao logs

servidor e acesso geram logs

bora pra outro JAM