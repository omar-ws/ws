# Armazenamento (S3)

Quando uma conexão de peering de VPC é criada, a VPC de destino precisa aceitar a solicitação de conexão porque ela pode pertencer a uma conta diferente. Entretanto, o usuário que cria a conexão de peering pode não ter permissão para aceitar a solicitação de conexão da VPC de destino. No entanto, neste laboratório, você mesmo aceitará a conexão.

![image.png](image%208.png)

exemplo de CORS:

```jsx
● [
    {
      "AllowedHeaders": ["*"],
      "AllowedMethods": ["GET"],
      "AllowedOrigins": ["https://meu-site.com"],
      "ExposeHeaders": [],
      "MaxAgeSeconds": 3000
    }
  ]
```

permissao da caferole:

para fazer um cross origin:

![image.png](image%209.png)

S3 server logging (acesso de servidor):

quem acessou o que no bucket, IP, objeto, hora de operacao

CloudTrail data events:

quase a mesma coisa mas armazena getobject putobject deleteobject com a identidade IAM que fez

S

tipos de uso:

site estatico: S3 + CloudFront

midia & streaming: netflix por exemplo

data lake / analytics: junto com ferramentas tipo readshift

backup e arquivamento: rds usa o S3 por baixo backup, S3 e subir o glacier

upload por:

Console

CLI

SDK

API REST

Transfer Family para FTP FTPS E SFTP (acima do S3)

S3 Standard Acesso frequente, baixa latencia

S3 inteligent tireting ele tira automaticamente

S3 Standard IA:

S3 One zone IA:

saida para o cloudfront nao tem cobranca

com vpc endpoint nao tem cobranca

transferencia de entrada (upload) nao tem cobranca

seguranca: criptografia repouso controle, controle de acesso restrito

confiabilidade: zonas, locais

eficiencia de desempenho: ao inves de deletar arquvos em massa, usar o lifecicle

otimizacao de custo: life cicle e classes