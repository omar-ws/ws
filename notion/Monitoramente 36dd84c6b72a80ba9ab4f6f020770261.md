# Monitoramente

Use flowlogs quando voce nao tem opcao, nao sabe sobre o SG, ACL, ROTA quando voce nao consegue achar o erro do problema

Com o flowlogs sao 3 rotas, uma rota para o flowlog, e uma rota pra subrede publica e uma pra privada, ou seja

rota privada ⇒ 0.0.0.0/0 ⇒ NAT

rota publica ⇒ 0.0.0.0/0 ⇒ firewall

rota firewall ⇒ 0.0.0.0/0 ⇒ IGW

Flow Logs IAMrole (quem vai administrar) (nao para colocar em uma EC2, mas sim em um usuario o Flow Logs escreve automaticamente):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:CreateFlowLogs",
        "ec2:DescribeFlowLogs",
        "ec2:DeleteFlowLogs"
      ],
      "Resource": "*"
    }
  ]
}
```

a parte :

```jsx
"Resource": "*"
```

poderia ser apenas em uma ARN especifica porem nesse sentido pode ser esse flow em VPC, Subnetes ou Network, nesses servico a aws obriga

## Criar Log permitindo ler escrever no CloudWatch

```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": [
          "logs:CreateLogGroup",
          "logs:CreateLogStream",
          "logs:PutLogEvents",
          "logs:DescribeLogGroups",
          "logs:DescribeLogStreams"
        ],
        "Resource": "*"
      }
    ]
  }
```

“monitores logs da vpc”: flow logs

- Flow Logs → S3 = Bucket Policy com principal [delivery.logs.amazonaws.com](http://delivery.logs.amazonaws.com/)

- Flow Logs → CloudWatch = IAM Role

## Bucket Policy para receber Flow Logs:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "delivery.logs.amazonaws.com"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::SEU-BUCKET/AWSLogs/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "bucket-owner-full-control"
        }
      }
    }
  ]
}
```

Os pontos importantes:

- Principal → [delivery.logs.amazonaws.com](http://delivery.logs.amazonaws.com/) — quem vai entregar
- Action → só PutObject — só escrever, nada mais
- Resource → o caminho específico onde os logs vão cair
- Condition → garante que sua conta é dona dos objetos gravados