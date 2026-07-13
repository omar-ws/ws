# JAM Criptografar o Data Lake

visao geral

```jsx
Você é engenheiro de segurança trabalhando na MuMuMango em um projeto para criar um data lake para armazenar todas as frutas que sua empresa vende. Sua política corporativa determina que os dados confidenciais em seu data lake devem ser criptografados em repouso com chaves de criptografia controladas por sua organização. Você acabou de descobrir que centenas de objetos foram enviados para o S3 usando a chave de criptografia padrão do S3. Sua tarefa é remediar rapidamente essa violação da política para evitar danos à marca MuMuMango e garantir que futuros carregamentos permaneçam dentro da política.

Leia menos
```

task 1:

```jsx
Tarefa 1: Criptografe objetos do S3 não compatíveis e imponha a conformidade
Pontos possíveis
80
Penalidade por pista
30
Pontos disponíveis
0

Tarefas e pistas
Sua conta da AWS tem os seguintes recursos:

Um bucket Data Lake S3 com centenas de objetos que são criptografados com a chave de criptografia S3 padrão.
Uma chave KMS gerenciada pelo cliente que deve ser usada para criptografar em repouso todos os objetos atuais e futuros no data lake. Você pode encontrar o ID da chave na seção Propriedades de saída.
Um arquivo de inventário do S3. Para esse desafio, um único arquivo CSV de inventário é pré-criado para você.
Uma função do IAM (FixEncryptionRole) que pode e deve ser usada para corrigir o erro de criptografia. **Nota: ** você não precisa assumir essa função.
Requisitos
Seu trabalho é colocar seu data lake em conformidade com a política por meio de:

Criptografar os objetos existentes no Data Lake com a chave KMS gerenciada pelo cliente usando um método escalável.
Configurar o bucket do Data Lake S3 para que novos objetos sejam criptografados por padrão com a chave KMS gerenciada pelo cliente.
Recomendações
Certifique-se de preencher os requisitos acima, em ordem
Embora o console S3 permita que você altere a criptografia de um pequeno número de objetos, esse método não é escalável para milhões ou bilhões de objetos. A verificação do desafio não concederá pontos completos se você não usar um método escalável para criptografar objetos.
Verifique se você está usando a chave KMS gerada, não a chave KMS S3
Depois de concluir a tarefa, clicar em verificar meu progresso confirmará que você concluiu o desafio
Links úteis
Aqui estão alguns links para ajudá-lo com o desafio:

Operações em lote do S3
Criptografia padrão do Amazon S3 para buckets S3
```

documentacao

https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/batch-ops.html

https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/bucket-encryption.html

esse nao conhecia nada, ainda nao sei como cria um csv mas nao era isso que o JAM pedia, mas gostei de fazer, entendi por que nao era copiar