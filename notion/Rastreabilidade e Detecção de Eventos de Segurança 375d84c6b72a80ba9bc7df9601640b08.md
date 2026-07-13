# Rastreabilidade e Detecção de Eventos de Segurança

```jsx
Laboratório 1
Rastreabilidade e Detecção de Eventos de Segurança
AWS Academy Cloud Architecting — Módulo: Proteção do acesso (IAM e Segurança)

Cenário
A JusePay é uma fintech fictícia que processa pagamentos para pequenos comércios. Após um incidente em que um colaborador, usando credenciais de longo prazo, encerrou instâncias EC2 de produção por engano — e ninguém soube dizer quem fez, quando ou de onde —, a liderança de segurança determinou uma nova diretriz: “nenhuma ação sensível na conta AWS pode passar despercebida”.
Você foi contratado como arquiteto de nuvem para resolver o problema. A diretoria não quer um relatório; quer uma arquitetura que garanta rastreabilidade total e que avise a equipe de segurança em tempo quase real quando algo arriscado acontecer.
Problema a resolver
Hoje a conta da JusePay não tem qualquer trilha de auditoria habilitada e não existe nenhum mecanismo de alerta. A equipe só descobre problemas quando o serviço cai. Sua missão é desenhar e implementar uma solução que responda, a qualquer momento, três perguntas: quem fez, o que fez e de onde fez — e que dispare um alerta automático diante de comportamentos de alto risco.
Objetivo de aprendizagem
Aplicar os princípios de segurança de manter a rastreabilidade e preparar-se para eventos de segurança (pilar de Segurança do Well-Architected Framework), conectando governança de identidade (IAM) a monitoramento e detecção contínuos.
Eventos de alto risco que a solução deve detectar
A solução deve monitorar e alertar sobre os dois comportamentos abaixo:
Encerramento de instâncias EC2 (TerminateInstances).
Desativação ou alteração da própria trilha de auditoria (tentativa de “apagar rastros”).
Serviços sugeridos
Você decide a arquitetura, mas considere combinar:
AWS CloudTrail — registro de todas as chamadas de API da conta.
Amazon CloudWatch (Logs, Metric Filters e Alarms) — métricas e alarmes sobre os eventos.
Amazon EventBridge — regras orientadas a evento para reação imediata.
Amazon SNS — notificação da equipe de segurança (e-mail).
Amazon S3 — armazenamento seguro e durável dos logs de auditoria.
Requisitos e parâmetros de segurança
A solução proposta deve obedecer a estes parâmetros:
Os logs de auditoria devem ser protegidos contra adulteração — quem opera no dia a dia não pode apagá-los ou editá-los (pense em menor privilégio e em separação de papéis).
Os logs em repouso devem estar criptografados.
Para fins deste laboratório, a solução pode ser configurada em uma única região. Atenção: em um ambiente real, a trilha de auditoria deve cobrir todas as regiões da conta, pois ações maliciosas ou acidentais podem ocorrer em qualquer região.
O acesso ao mecanismo de alerta e à trilha deve seguir o princípio do menor privilégio.
Entregáveis
Um diagrama de arquitetura mostrando o fluxo do evento, desde a chamada de API até o alerta na equipe de segurança.
A implementação funcional na conta (Console ou CLI), capaz de gerar um alerta real quando um dos eventos monitorados ocorrer.
Uma demonstração: provoque deliberadamente um dos eventos (ex.: encerrar uma instância EC2 de teste) e mostre a trilha no CloudTrail e o alerta recebido.
Critérios de sucesso
A solução é considerada bem-sucedida se, ao executar uma ação sensível na conta, for possível (a) localizar o evento na trilha de auditoria identificando autor, horário e origem, e (b) receber um alerta automático sem intervenção manual.

```

configurado corretamente

![image.png](image%2027.png)

```json
{
  "source": ["aws.ec2"],
  "detail-type": ["AWS API Call via CloudTrail"],
  "detail": {
    "eventName": ["TerminateInstances"]
  }
}
```

![image.png](image%2028.png)

{
"Version": "2012-10-17",
"Statement": [
{
"Sid": "AWSCloudTrailAclCheck20150319-c3571d46-4b6e-4592-958b-0d4ec45a57aa",
"Effect": "Allow",
"Principal": {
"Service": "[cloudtrail.amazonaws.com](http://cloudtrail.amazonaws.com/)"
},
"Action": "s3:GetBucketAcl",
"Resource": "arn:aws:s3:::aws-cloudtrail-logs-evit-342946498914-d95657df",
"Condition": {
"StringEquals": {
"AWS:SourceArn": "arn:aws:cloudtrail:us-east-1:342946498914:trail/JusePay-CloudTrail-EvitarAcidentes"
}
}
},
{
"Sid": "AWSCloudTrailWrite20150319-a4ba0847-8255-4d04-b12a-626f5bd72ff3",
"Effect": "Allow",
"Principal": {
"Service": "[cloudtrail.amazonaws.com](http://cloudtrail.amazonaws.com/)"
},
"Action": "s3:PutObject",
"Resource": "arn:aws:s3:::aws-cloudtrail-logs-evit-342946498914-d95657df/AWSLogs/342946498914/*",
"Condition": {
"StringEquals": {
"AWS:SourceArn": "arn:aws:cloudtrail:us-east-1:342946498914:trail/JusePay-CloudTrail-EvitarAcidentes",
"s3:x-amz-acl": "bucket-owner-full-control",
"aws:SourceArn": "arn:aws:cloudtrail:us-east-1:342946498914:trail/JusePay-CloudTrail-EvitarAcidentes"
},
"ArnNotLike": {
"aws:PrincipalArn": "arn:aws:cloudtrail:us-east-1:342946498914:trail/JusePay-CloudTrail-EvitarAcidentes"
}
}
},
{
"Sid": "Statement1",
"Effect": "Deny",
"Principal": "*",
"Action": "s3:PutObject",
"Resource": "arn:aws:s3:::aws-cloudtrail-logs-evit-342946498914-d95657df/*"
}
]
}

![image.png](image%2029.png)

```
	{
		"Sid": "Statement1",
		"Principal": "*",
		"Effect": "Deny",
		"Action": [
			"s3:DeleteObject",
			"s3:DeleteBucket",
			"s3:PutObject"
		],
		"Resource": [
			"arn:aws:s3:::aws-cloudtrail-logs-342946498914-a6af307f/*",
			"arn:aws:s3:::aws-cloudtrail-logs-342946498914-a6af307f"
		],
		"Condition": {
			"ArnNotLike": {
				"aws:SourceArn": "arn:aws:cloudtrail:us-east-1:342946498914:trail/JusePay-CloudTrail-EvitarAcidentes"
			}
		}
	}
```

deu certo essa politica de condicao

considcao se le, se nao for isso source ou arnprincipal ex3euctar a funcao tipo put deny delete e etc, bom dms

```wasm

```

![image.png](image%2030.png)

{"Quem foi?" : "$.detail.usersIdentity.userName", "o que?" : "$.detail.eventName", "de onde?" : "$.detail.sourceIPAddress" }

![image.png](image%2031.png)

deu esse erro 

- **Erro**
    
    1 validation error detected: Value '{de onde?=$.detail.sourceIPAddress, Quem foi?=$.detail.userIdentity.userName, o que?=$.detail.eventName}' at 'targets.1.member.inputTransformer.inputPathsMap' failed to satisfy constraint: Map keys must satisfy constraint: [Member must have length less than or equal to 256, Member must have length greater than or equal to 1, Member must satisfy regular expression pattern: [A-Za-z0-9\_\-]+]