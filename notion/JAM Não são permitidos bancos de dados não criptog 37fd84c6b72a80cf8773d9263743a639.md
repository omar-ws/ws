# JAM Não são permitidos bancos de dados não criptografa...

visao geral:

```jsx
Sua empresa está melhorando a postura de segurança em relação a dados não criptografados. Você recebeu a responsabilidade de criptografar o banco de dados MySQL do RDS primário que seu antecessor deixou sem criptografia.
```

task 1:

```jsx
Tarefa 1: Encriptar o banco de dados
Pontos possíveis
80
Penalidade por pista
0
Pontos disponíveis
0

Tarefas e pistas
Plano de fundo
Como engenheiro da AWS, seu gerente pede que você criptografe o banco de dados MySQL existente. Ele entende que a criptografia não pode ser simplesmente ativada em um banco de dados existente, então ele deixou que você decidisse isso. Você não precisa se preocupar em remover o banco de dados existente. Isso será tratado pela equipe de DevOps assim que você tiver uma cópia criptografada em seu lugar.

Começando
Acesse o serviço RDS no console da AWS para começar esse desafio. As etapas que você deve executar são:

Crie um instantâneo da instância de banco de dados de origem
Criptografar o instantâneo
Restaurar o DB snapshot criptografado
Detalhes importantes a serem considerados
**Região da AWS: ** Preste muita atenção à região da AWS onde seus recursos são implantados e certifique-se de criar snapshots na mesma região.

**Família/tamanho da instância: ** Certifique-se de que o banco de dados criptografado esteja na mesma família e tamanho de instâncias da classe Burstable do banco de dados não criptografado. O novo banco de dados deve ser db.t3.micro. Não queremos incorrer em nenhuma cobrança adicional pelo banco de dados criptografado.

Paciência: A criação e a restauração de instantâneos podem levar até 15 minutos para serem concluídas (cada). Esse desafio também testará sua paciência.

Recursos adicionais
Se precisar de assistência adicional, confira este link na documentação da AWS: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html

Inventário
Banco de dados RDS MySQL
Serviços que você deve usar
VERMELHOS
Validação de tarefas
A tarefa será concluída automaticamente quando você implantar com êxito uma instância criptografada do RDS. Além disso, você sempre pode verificar seu progresso pressionando o botão “Verificar meu progresso” na tela de detalhes do desafio.
```

documentacao

https://docs.aws.amazon.com/pt_br/AmazonRDS/latest/UserGuide/Overview.Encryption.html

esse eu demorei mais o que o normal por que nao lembrava o passo a passo eu tirei o snapshot porem eu nao lembrava que tinha que depois de criar snapshot tinha que copiar com a chave de criptografia

ordem

snapshot ⇒ copia com criptografia ⇒ restaurar