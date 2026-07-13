# JAM Otimizando o EBS para o aumento do comércio eletrônico

```bash
Visão geral
Na AnyCompany, líder em comércio eletrônico, a próxima promoção da época festiva promete ser o maior aumento de tráfego do ano. Os riscos são altos e a equipe está se esforçando para garantir que sua infraestrutura possa lidar com a enxurrada de clientes. Um dos componentes mais críticos é uma instância**Amazon Elastic Compute Cloud (Amazon EC2) ** que hospeda a lógica principal do aplicativo. O desempenho do servidor é fundamental para garantir que a venda ocorra sem problemas, mas benchmarks recentes mostram que a configuração atual do disco pode não ser suficiente para lidar com os picos de tráfego esperados.

O líder de sua equipe, John, forneceu a configuração de disco necessária para melhorar o IOPS, a taxa de transferência e o tamanho dos volumes do EBS anexados. Faltando apenas algumas horas para o lançamento da venda, você foi encarregado de analisar esses requisitos e fazer os ajustes necessários nos volumes do EBS da instância crítica do EC2. O sucesso da venda e a reputação da empresa dependem da sua capacidade de otimizar o sistema para obter o máximo desempenho. Deixar de agir com rapidez e precisão pode levar a um período de inatividade desastroso durante a época mais lucrativa do ano.

Leia menos

Propriedades de saída
EC2InstanceID
i-0ed80176b697a9448

RDPCredentials
Username: Administrator | Password: p@SSword@123

SecurityGroupID
sg-0aabb4968d5064af4

Seu desafio está pronto!
Tudo de bom, e lembre-se de se divertir!

Tarefa 1: Modificar a configuração do volume raiz do EBS
Pontos possíveis
45
Penalidade por pista
0
Pontos disponíveis
45
Verifique meu progresso

Tarefas e pistas
Antecedentes
Benchmarks recentes de uma instância**Amazon Elastic Compute Cloud (Amazon EC2) ** mostram que a configuração atual do disco pode não ser suficiente para lidar com os picos de tráfego esperados para a próxima promoção da temporada festiva.

A instância EC2 em questão precisa de configuração de disco para melhorar IOPS, throughput e size para o volume EBS anexado. Após uma análise minuciosa e a realização de vários testes de benchmarking, concluiu-se que o volume do EBS deve ter a seguinte configuração:

Tipo de volume | SSD de uso geral (** gp3 **)
Tamanho do volume (GiB) | ** 100 **
Volume IOPS | ** 5000 **
Taxa de transferência (MiB/s) | ** 150 *
Modifique o volume do EBS em questão anexado à determinada instância do EC2 com base nas configurações acima.

** NOTE: ** Qualquer modificação subsequente do volume do EBS é permitida após ** 6 hours **, portanto, você deve modificar cuidadosamente os atributos na primeira tentativa, caso contrário encontrará o seguinte erro:

Modify Volume Request Failed for volume vol-xxxxxxxxxxxxxxx.
You've reached the maximum modification rate per volume limit. 
Wait at least 6 hours between modifications per EBS volume.
Além disso, antes de modificar o volume raiz do EBS, você deve marcá-lo com os dois pares de valores-chave a seguir:

Chave: ** Name ** | Valor: ** Production-Volume **
Chave: ** challenge ** | Valor: ** extend-windows-disk **
Sua tarefa
Sua tarefa é:

Marque o volume raiz do EBS anexado à determinada instância do EC2, conforme explicado acima.
Modifique o volume do EBS para aplicar as configurações mencionadas acima.
Começando
Vá para o console Amazon EC2 e selecione a instância EC2 chamada Production-Server e, na guia Storage, escolha o volume raiz com o nome do dispositivo como ** \dev\sda1 **.
Marque esse volume raiz do EBS com os seguintes dois pares de valores-chave:
Chave: ** Name ** | Valor: ** Production-Volume **
Chave: ** challenge ** | Valor: ** extend-windows-disk **
Em seguida, modifique o volume do EBS com base nas configurações explicadas acima.
Inventário
Instância do Amazon EC2 chamada Production-Server.
Para IDs de recursos, consulte a seção Propriedades de saída deste desafio.
Serviços que você deve usar
Nuvem de computação elástica da Amazon (Amazon EC2)
Amazon Elastic Block Store (Amazon EBS)
Validação de tarefas
Depois de modificar com êxito a configuração do volume do EBS conforme mencionado acima, essa tarefa será automaticamente marcada como concluída. Além disso, você sempre pode verificar seu progresso pressionando o botãoVerificar meu progresso na tela de detalhes do desafio.

Pistas
Ajude-me a começar!
4Pontos de penalidade
Desbloqueie o Clue
Mais algumas dicas seriam ótimas!
5Pontos de penalidade
Desbloqueie o Clue

```

nao terminei nem a primeira tinha 3 que porcaria