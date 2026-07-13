# JAM Luzes, câmera, segurança!

MEDIO

VISAO GERAL

```jsx
Parabéns! Você conseguiu o emprego dos seus sonhos no BlockBuster Studios, uma das principais produtoras de filmes de Hollywood. Como arquiteto de segurança na nuvem, você é responsável por proteger seus ativos digitais mais valiosos. O estúdio armazena seus próximos roteiros de filmes e trailers exclusivos no Amazon S3, incluindo materiais para o aguardado filme de super-heróis de 300 milhões de dólares, “Quantum Knight”.

Os executivos do estúdio têm um claro requisito de segurança: todo o conteúdo do Amazon S3 só deve ser acessível a partir de um Amazon VPC, onde as equipes criativas trabalham. Você pode ajudá-los a atingir seu objetivo?
```

TASK 1 a 3

```jsx
Antecedentes
Recentemente, você ouviu falar sobre os endpoints do VPC Gateway. Isso permite que você acesse o Amazon S3 a partir da sua VPC. Além disso, o serviço S3 fornece um método para negar todo o acesso a um bucket, exceto de um endpoint VPC (ou VPC). Essa seria uma maneira promissora de garantir o acesso aos valiosos ativos cinematográficos de propriedade de sua empresa!

Sua tarefa
Nessa tarefa, você criará um endpoint do VPC Gateway para o S3. O endpoint deve ser denominado My-Vpc-Endpoint (diferencia maiúsculas de minúsculas).

Para obter mais informações sobre endpoints do VPC Gateway, consulte: https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html

Começando
Abra o console do serviço VPC e crie um endpoint de gateway chamado My-Vpc-Endpoint para o serviço S3. O nome diferencia maiúsculas de minúsculas, portanto, use o nome fornecido aqui. O endpoint deve ser criado em vpc chamado 'My-Vpc' e associado à tabela de rotas chamada 'My-Route-Table', ambas já criadas para você.

Inventário:
PVC
Tabela de rotas
Serviços que você deve usar:
Amazon VPC
Validação de tarefas
A tarefa será automaticamente marcada como concluída quando o endpoint do Gateway para Amazon S3 for criado e estiver no estado “Disponível” (o que pode levar de alguns segundos a minutos).

task 2:
Plano de fundo
Seu colega informou que as políticas do bucket do S3 podem ser usadas para conceder ou negar acesso ao bucket do S3. Essa seria uma ótima maneira de restringir o acesso. No entanto, seu colega não sabe como implementar isso. Você pode ajudá-los?

Sua tarefa
Nessa tarefa, você precisa criar e adicionar uma política de bucket ao bucket do S3. A política deve negar todas as solicitações de upload e download de arquivos, exceto aquelas originadas da VPC chamada “My-Vpc”.

Começando
Abra o console de serviço do S3 e configure a política de bucket. A política do bucket deve ser adicionada ao bucket cujo nome começa com a string 'my-s3-bucket'. Como alternativa, você pode encontrar o nome do bucket na guia “Propriedades de saída” desta página. Esse bucket já foi criado para você.

**Observação: ** É importante que a política de bucket esteja em conformidade com todos os seguintes pontos:

A política não deve negar as ações “s3: *”, “s3:ListBucket” ou “s3:getBucketPolicy”, pois elas são necessárias para concluir a tarefa e verificar seu status de conclusão.
A política deve usar o operador de condição 'stringNotEquals'
A política também deve usar a chave de condição 'aws:sourceVpc' ou 'aws:sourceVpce'
Para obter informações relacionadas a eles, você pode consultar:

Política de bucket do S3: https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html
Operadores de condição da política IAM: https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html
Chaves de condição globais da AWS: https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html
Inventário:
Balde S3
Serviços que você deve usar:
Amazon S3
Validação de tarefas
A tarefa será marcada automaticamente como concluída depois que você adicionar a política de bucket necessária.

task 3:
Antecedentes
Parabéns por ter chegado até aqui! Seus colegas ouviram que a configuração está pronta e estão entusiasmados em aproveitá-la.

Sua organização tem uma forte cultura de testar uma configuração antes de usá-la, e eles confiam em você para fazer o mesmo. Você pode ajudá-los nessa tarefa final!?

Sua tarefa
Nessa tarefa, você precisa se conectar à instância do EC2 chamada 'My-Ec2', que já foi criada para você. Você criará um arquivo na instância do EC2 e o enviará para o mesmo bucket do S3 usado na tarefa anterior, demonstrando que o bucket está acessível a partir da VPC. O arquivo que você enviará para o bucket do S3 deve ter o nome my-test-upload-file (diferencia maiúsculas de minúsculas).

Começando
Abra o console do EC2 e conecte-se à instância EC2 chamada 'My-Ec2' por meio de 'conexão de instância EC2'. Para referência, consulte: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-connect-methods.html#ec2-instance-connect-connecting-console

Depois de conectado à instância do EC2, crie um arquivo vazio chamado 'my-test-upload-file' usando o comando touch.

Faça upload desse arquivo da instância do EC2 para o mesmo bucket do S3 usado na tarefa anterior. Você pode encontrar o nome do bucket na tarefa anterior ou na guia “Propriedades de saída” desta página.

Inventário:
Instância EC2
Balde S3
Serviços que você deve usar:
Amazon EC2
Amazon S3
Validação de tarefas
A tarefa será marcada automaticamente como concluída após o upload do objeto chamado 'my-test-upload-file' para o bucket do S3.
```

a