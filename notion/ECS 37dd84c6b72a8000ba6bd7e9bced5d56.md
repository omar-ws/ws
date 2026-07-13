# ECS

## Rolling:

muda de um em um, se for atualizacao de banco de dados por dar conflito ex:

r2 atualizado

r1 ainda

r1 ainda

## Blue/Green:

muda de uma vez, e da quantos minutos porem necessario para terminar

Target group 1                               |                                 Target group 2      (da 15 minutos para os  ECS do

r1 ainda                                            |                                 r2 atualizao            target 1  terminar o que estava 

r1 ainda                                            |                                r2 atualizao             fazendo)

r1 ainda                                            |                               r2 atualizao

![image.png](image%2045.png)

quando usar cada um:

![image.png](image%2046.png)