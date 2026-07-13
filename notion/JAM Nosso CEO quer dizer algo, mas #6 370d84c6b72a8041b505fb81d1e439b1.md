# JAM Nosso CEO quer dizer algo, mas... #6

contexto: (voce nao consegue ver fotos imagino porem tem um diagrama mais ou menos assim)

      ⇒ team console (role tbm) ⇒ negado (X)

pc swithc role                                                                            S3

     ⇒ JAMCEOMESSAGE (role tbm) ⇒ PERMITIDO (O) 

> 
> 
> 
> A Example Corp é uma empresa líder global em tecnologia. Todos os anos, muitos engenheiros ingressam na organização como recém-formados.
> 
> Hoje, esses recém-formados estão participando da cerimônia de boas-vindas da empresa. Durante o evento, o CEO entusiasta da tecnologia anunciou: “Salvei uma mensagem especial para você em um bucket do S3. Por favor, encontre e leia.”
> 
> Neste Jam Challenge, você aprenderá como configurar políticas de acesso e recursos e, ao mesmo tempo, obter uma compreensão mais profunda da lógica de avaliação de políticas do IAM.
> 
> ![overview](https://aws-jam-challenge-resources.s3.amazonaws.com/s-3-policy-game/1.0.0/overview.png)
> 

task 1:

```jsx

Por favor, insira a resposta
Enviar resposta
Antecedentes
A Example Corp é uma empresa líder global em tecnologia. Todos os anos, muitos engenheiros ingressam na organização como recém-formados.

Hoje, esses recém-formados estão participando da cerimônia de boas-vindas da empresa. Durante o evento, o CEO entusiasta da tecnologia anunciou: “Salvei uma mensagem especial para você em um bucket do S3. Por favor, encontre e leia.”

Sua tarefa
Você precisa ver quais buckets do S3 estão disponíveis em sua conta da AWS. Para fazer isso, você deve saber qual ação do IAM permite listar todos os buckets do S3.

**Insira o nome específico da ação do IAM que permite listar todos os buckets do S3 em sua conta. **

Validação de tarefas
Depois de identificar a ação correta do IAM, insira o nome da ação no campo de validação.
```

eu percebi que nao sei a diferenca de s3 get object, eu tentei e nao foi, nao sei a diferenca de criar la de listar e de dar get, achei que get listava

tive que pesquisar to desapontado comigo, eu achei que getobject era listar objetos e get e mas a resposta correta (pesquisei é:)

```jsx
s3:ListAllMyBuckets
ou
s3:ListBucket
```

tenho que entender a diferenca

entendi a diferenca de getobject para listbucket

ListBucket sao em casos que voce quer listar um bucket especifico no IAM

ListAllMyBuckets voce lista todos os buckets no IAM, ou seja listar e ver no S3

Get (pegar) e voce ter prmissao apra instalar os arquivos do bucket, nao adianta ter um list mas sem um get se sua ideia e isntalar os arquivos do bucket S3, sao um conjunto tipo:

```jsx
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": "s3:ListBucket",
        "Resource": "arn:aws:s3:::meu-bucket"
      },
      {
        "Effect": "Allow",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::meu-bucket/*"
      }
    ]
  }
```

task 2:

```jsx
Tarefa 2: Qual é a mensagem do nosso CEO?
Pontos possíveis
72
Penalidade por pista
0
Pontos disponíveis
72
Verifique meu progresso

Tarefas e pistas
Enviar resposta
Antecedentes
Excelente trabalho! Seus colegas concederam permissão ao s3:ListAllBuckets para JamCEOMessageIAMRole. Use essa função do IAM para essa tarefa.

Agora, vamos recuperar a mensagem do CEO sobre o balde!

Sua tarefa
Open AWS Console e mude para a função JamCEOMessageIAMRole.
***Observação: você deve usar a função IAM (JamCEOMessageIamRole) a partir desse ponto. ***

Agora você pode ver a lista de desejos do S3. Você vê algum balde que possa conter a mensagem do CEO?

Dica: procure um bucket relacionado à mensagem do CEO

Ah, não! Você não pode ver o conteúdo do bucket. Por quê?

Encontre a causa raiz desse problema de acesso.
Recupere a mensagem do CEO.
***Dica: você pode remover a política do IAM da função do IAM, mas não remova o DoNotDeletePolicy. ***

***Observação: você deve usar a função IAM (JamCEOMessageIamRole) a partir desse ponto. ***

Inventário
Função do IAM chamada JamCEOMessageIAMRole
Bucket S3 com um nome como labStack-prewarm-Number-JamCEOMessageS3Bucket-
Serviços que você deve usar
Amazon S3
ERA O OBJETIVO
Validação de tarefas
Depois de recuperar a mensagem do CEO, insira a mensagem exata na caixa de entrada no console do JAM.
```

nao entendi como vou colocar uma role que nao e minha

tive que pesquisar

o que e swicth role

entender mais a fundo sobre switch role, como funciona qualquer umn cosnegue acessar o IAM dessa forma?

sqith role me possibilita me vestir com uma IAM, me vesti com a IAM do boss, por que serve a cor

switch role e genial

```jsx
  Usuário IAM (você)
      └── faz Switch Role
           └── assume um Role
                └── age com as permissões daquele Role
```

eu nao consegui fazer desisti, deu mt problema,

resolucao pois pedir todas as dicas: eu estava correto mas apguei primeiro o getdeny antes de arrumar o bucket police e nao dava para reiniar o laboratorio

```jsx
Clues
S3 Bucket Policy
Penalty 7 points
Hide Clue
Please refer to the S3 Bucket Policy documentation.

Policy evaluation logic
Penalty 9 points
Hide Clue
Are you familiar with AWS policy evaluation logic? What happens when there is an explicit "Deny" statement in a policy?

Understanding how AWS determines if a request is allowed or denied within an account

Solutions
Penalty 10 points
Hide Clue
Solution using the AWS Management Console

Switch role

Go to the IAM console, then to the IAM Role page.
Select the IAM Role named JamCEOMessageIAMRole.
From the Summary section, copy the "Link to switch roles in console".
Paste this link into your browser.
Select "Switch Role".
You are now using this IAM Role to solve this task.
Edit S3 Bucket Policy

Go to the S3 console.
Select the S3 bucket with a name like labStack-prewarm-Number-JamCEOMessageS3Bucket-.
From the Permissions tab, go to "Bucket Policy" and select "Edit".
Allow the actions (S3:ListBucket, S3:GetObject) for the IAM role.
The bucket policy should look like this:
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
            "Principal": { 
                "AWS": "arn:aws:iam::YOUR-AWS-ACCOUNT-ID:role/YOUR-ROLE-NAME"
            },
			"Effect": "Allow",
			"Action": [
				"s3:GetObject",
				"s3:ListBucket"
			],
			"Resource": [
				"arn:aws:s3:::YOUR-S3-BUCKET/*",
				"arn:aws:s3:::YOUR-S3-BUCKET"
			]
		}
	]
}
YOUR-ROLE-NAME is JamCEOMessageIAMRole
YOUR-S3-BUCKET is the bucket name like LabStack-prewarm-Number-JamCEOMessageS3Bucket-
Select "Save Changes".
Edit IAM policy

Go to the IAM console.
Navigate to the IAM Role section.
Select the IAM Role named JamCEOMessageIAMRole.
From the Permissions tab, locate a policy named DenyS3GetObject and select "Remove".
You should now be able to view the CEO's message in the S3 bucket.

Answer
Penalty 10 points
Hide Clue
Enter Every Day is Still Day One! in the validation box.
```

vou pro proximo jam