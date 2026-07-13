# JAM Traga-o de volta com estilo #2

CONTEXTO DO JAM:

erro 403 entender

entender cada uma desses:

![image.png](image%2034.png)

```jsx
Bloquear acesso público (configurações do bucket)
O acesso público é concedido a buckets e objetos por meio de listas de controle de acesso (ACLs), políticas de bucket, políticas de ponto de acesso ou todas elas. Para garantir o bloqueio do acesso público a todos os seus objetos e buckets do S3, ative a opção Bloquear todo o acesso público. Essas configurações se aplicam apenas a este bucket e seus respectivos pontos de acesso. A AWS recomenda ativar a opção Bloquear todo o acesso público. Porém, antes de aplicar qualquer uma dessas configurações, verifique se as aplicações funcionarão corretamente sem acesso público. Caso precise de algum nível de acesso público para os buckets ou para os objetos dentro deles, personalize as configurações abaixo de acordo com seus casos de uso de armazenamento específicos. Saiba mais 

Bloquear todo o acesso público
Ativar essa configuração é o mesmo que ativar todas as quatro configurações abaixo. Cada uma das configurações a seguir são independentes uma da outra.
Bloquear acesso público a buckets e objetos concedidos por meio de novas listas de controle de acesso (ACLs)
O S3 bloqueará as permissões de acesso público aplicadas a blocos ou objetos recém-adicionados e impedirá a criação de novas ACLs de acesso público para blocos e objetos existentes. Essa configuração não altera nenhuma permissão existente que permita o acesso público aos recursos do S3 usando ACLs.
Bloquear acesso público a buckets e objetos concedidos por meio de qualquer lista de controle de acesso (ACLs)
O S3 ignorará todas as ACLs que concedem acesso público a buckets e objetos.
Bloquear acesso público a buckets e objetos concedidos por meio de novas políticas de ponto de acesso e bucket público
O S3 bloqueará novas políticas de bucket e ponto de acesso que concedem acesso público a buckets e objetos. Essa configuração não altera nenhuma política existente que permita o acesso público aos recursos do S3.
Bloquear acesso público e entre contas a buckets e objetos por meio de qualquer política de bucket ou ponto de acesso público
O S3 ignorará o acesso público e entre contas para buckets ou pontos de acesso com políticas que concedem acesso público a buckets e objetos.
```

TASK 1: DEMOREI por falta de leitura

```jsx
Plano de fundo

Seu gerente informou você por e-mail sobre o problema atual, que está afetando diretamente os clientes e lhes custando receita. Você deve verificar o problema com o site com defeito o mais rápido possível. Identificar a seção do site que não está carregando corretamente é a primeira etapa.

Sua tarefa

Sua tarefa é identificar qual arquivo do site não está acessível e retornando um código de erro 403.

Começando

Vá para a guia Output Properties no lado esquerdo e pegue o URL para WebsiteDomain.
Abra o URL em qualquer navegador da web.
Use o console do desenvolvedor do navegador para determinar qual arquivo está sendo solicitado pelo navegador para renderizar a página da web, mas retornando o código de erro 403.
Inventário

O URL do site quebrado é fornecido na guia Output Properties.
Serviços que você deve usar

Qualquer navegador da web
Validação de tarefas

Digite o nome do arquivo que não está sendo carregado corretamente e mostra o código de erro 403 na coluna de status.
```

task 2: fui mais rapido

```jsx
Plano de fundo

Agora que você sabe qual arquivo está causando o problema, tente determinar de onde ele veio para investigar o problema mais detalhadamente. O arquivo de imagem parece vir de um bucket do S3, que se acredita ser uma fonte secundária.

Sua tarefa

Sua tarefa é identificar o bucket do S3 em que o arquivoimage.jpeg está hospedado.

Começando

Vá até a aba Output Properties no lado esquerdo e pegue a URL deWebSiteDomain.
Abra o URL em qualquer navegador da web.
Use o console do desenvolvedor do navegador para identificar o nome do bucket do S3 em que o arquivoimage.jpeg está hospedado.
Inventário

O URL do site quebrado é fornecido na guia Output Properties.
Serviços que você deve usar

Qualquer navegador da web
Amazon S3
Validação de tarefas

Digite o nome do bucket do S3 que você identificou.
```

TASK 3: 

Demorei para achar o problema pois eu achei que era pra subir um site mudar as configuracoes de metadados criacao de bucket police, ou hospedar um site

```jsx
Plano de fundo

Excelente! Você encontrou o bucket S3 de origem do arquivo inacessível. Agora você precisa identificar a causa raiz do arquivo inacessível e corrigir o mesmo.

Sua tarefa

Sua tarefa é fazer alterações nas propriedades do objeto em questão no bucket do S3 para garantir que ele fique acessível.

Começando

Navegue até o console do Amazon S3 e clique no bucket S3 identificado para acessar o arquivoimage.jpeg.

Inventário

O bucket S3 foi provisionado junto com o arquivoimage.jpeg.

Serviços que você deve usar

Amazon S3

Validação de tarefas

A tarefa será marcada automaticamente como concluída quando você atualizar corretamente a propriedade do objeto inacessível no bucket s3. Como alternativa, você pode clicar no botão “Verificar meu progresso” para verificar o status de conclusão.
```

task 4:

ESTUDAR SOBRE CORS:

(O QUE FIZ:) Liberei o site para a internet, “tornar publico por ACL”

```jsx
Plano de fundo

Parabéns por finalmente conseguir que a imagem apareça no site! Os comentários no site deixam claro que o design da página está incorreto. Veja se você consegue fazer tudo perfeito!

Sua tarefa

Agora é sua responsabilidade corrigir os problemas estilísticos na página para que cada componente apareça conforme especificado pelas anotações.

Começando

Vá até a aba Output Properties no lado esquerdo e pegue a URL deWebSiteDomain.
Abra o URL em qualquer navegador da web.
Verifique mais as ferramentas do desenvolvedor para identificar e corrigir o problema.
O site tem anotações para descrever a aparência dos componentes. Verifique as solicitações feitas pelo navegador em busca de outros erros que possam estar ocorrendo.

Inventário

Os buckets S3 foram provisionados.
O URL do site quebrado é fornecido.
Serviços que você deve usar

Amazon S3

Validação de tarefas

A tarefa será marcada automaticamente como concluída quando você corrigir o estilo na página da web. Como alternativa, você pode clicar no botão “Verificar meu progresso” para verificar o status de conclusão.
```

algumas pisatas mesmo sem eu abrir me deram dicas

```jsx
Pistas
configurar a política CORS
3Pontos de penalidade
Desbloqueie o Clue
Verifique a seção Console das ferramentas para desenvolvedores
4Pontos de penalidade
Desbloqueie o Clue
Permitir o método GET
4Pontos de penalidade

```

coisas que fiz:

codigo que usei no CORS

```jsx
  [
    {
      "AllowedHeaders": ["*"],
      "AllowedMethods": ["GET"],
      "AllowedOrigins": ["https://main-s3-bucket-775699420231.s3.ap-southeast-2.amazonaws.com/index.html"],
      "ExposeHeaders": []
    }
  ]
```

tenhoq que entender pois usei o claude

descobri sozinho que o correto e:

```jsx
  [
    {
      "AllowedHeaders": ["*"],
      "AllowedMethods": ["GET"],
      "AllowedOrigins": ["https://main-s3-bucket-775699420231.s3.ap-southeast-2.amazonaws.com"],
      "ExposeHeaders": []
    }
  ]
```

aprender sobre cada coisa desse laboratorio, CORS

usei essei esse site para ajuda sobre o S3

https://docs.aws.amazon.com/AmazonS3/latest/userguide/enabling-cors-examples.html?icmpid=docs_amazons3_console