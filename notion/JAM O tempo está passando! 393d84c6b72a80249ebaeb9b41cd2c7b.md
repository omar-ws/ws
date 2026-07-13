# JAM O tempo está passando!

```verilog
Visão geral
Esta é a história da Ticking Clock Media Company e de você, seu novo engenheiro de segurança.

! Logotipo da Ticking Clock Media Company

Como engenheiro de segurança trabalhando para Ticking Clock Media, você recebeu a tarefa de garantir que um aplicativo web estático esteja on-line e disponível ao público. O aplicativo foi criado por um arquiteto de soluções contratado, que usou o S3 e o Cloudfront para hospedar o site.

Depois de analisar o aplicativo, você descobriu que o contratante havia adicionado vários arquivos a um bucket do S3 para testar as permissões e ver se o site carregaria esses arquivos corretamente. No entanto, após a implantação, o site de produção ainda não estava acessível.

Você imediatamente começou a investigar o problema, começando por verificar o bucket do S3 e a distribuição do Cloudfront. Você descobriu rapidamente que as permissões do bucket estavam definidas como privadas, o que significava que somente usuários autenticados com as permissões corretas podiam acessar os arquivos no bucket.

Em seguida, você verificou a distribuição do Cloudfront e descobriu que ela estava configurada para usar uma identidade de acesso de origem (OAI) para acessar os arquivos no bucket do S3. No entanto, o OAI não recebeu as permissões corretas para acessar os arquivos no bucket.

Você percebeu que essa era a causa raiz do problema e rapidamente trabalhou para corrigi-lo. Você adicionou o OAI à política de bucket, concedendo a ela as permissões necessárias para acessar os arquivos. Em seguida, você limpou o cache do Cloudfront e o site ficou acessível ao público.

Você ficou aliviado por eu ter conseguido identificar e resolver o problema rapidamente e por o site estar online e disponível ao público.

Leia menos
```

```verilog
Tarefa 1: Alterar o protocolo de política
Pontos possíveis
60
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Ao usar o CloudFront com um bucket do Amazon S3 como origem, você pode configurar o CloudFront e o Amazon S3 de uma forma que ofereça os seguintes benefícios:

Restringe o acesso ao bucket do Amazon S3 para que ele não seja acessível ao público
Garante que os clientes possam acessar o conteúdo no bucket somente por meio da distribuição especificada do CloudFront. Os clientes são impedidos de acessar o conteúdo diretamente do bucket ou por meio de uma distribuição não autorizada do CloudFront.
Como engenheiro de segurança, seu trabalho é garantir que o conteúdo fornecido pelo CloudFront siga as melhores práticas de segurança para o aplicativo de produção.

Inventário:
Distribuição CloudFront
Bucket S3 que serve o conteúdo
Tarefa
Você tem a tarefa de corrigir o protocolo de política de visualização da distribuição de produção do CloudFront para que somente solicitações HTTPS sejam aceitas. Modifique o comportamento da distribuição associada ao bucket de produção do S3.

Serviços que você deve usar
CloudFront
Começando
Verifique as configurações de comportamento da distribuição do CloudFront.
Validação de tarefas
A tarefa será validada automaticamente quando a Política do CloudFront Viewer for definida como somente HTTPS.

Tarefa 2: O site não está ativo
Pontos possíveis
90
Penalidade por pista
20
Pontos disponíveis
0

Tarefas e pistas
Antecedentes
Você tentou acessar o site de produção depois de alterar a política de protocolo da distribuição do CloudFront. No entanto, você não consegue acessá-lo. O aplicativo deve estar ativo até o final do dia.

Inventário:
Distribuição CloudFront
Balde S3
Tarefa
Você tem a tarefa de descobrir o problema com a aplicação do produto e corrigi-lo. Você pode validar testando o URL do aplicativo no navegador.

Serviços que você deve usar
CloudFront
S3
Começando
No CloudFront, verifique as permissões concedidas para o usuário OAI.
Validação de tarefas
A tarefa será validada automaticamente quando a URL do site https://{cloudfront_domainname}/production-application/index.html for retornada com sucesso.
```

a