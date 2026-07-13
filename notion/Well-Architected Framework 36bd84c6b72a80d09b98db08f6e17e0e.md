# Well-Architected Framework

![image.png](image%2043.png)

Pilares:

Confiabilidade: Garante que a alocacao de sub-rede IP leve em conta a expansao e a disponibilidade

Seguranca: Criar camada de redes (sub) Implementar inspecao e protecao, controla trafego em todas as camadas

Eficiencia e Desempenho: Entender como as redes afetam o desempenho, avalaiar recursos de rede dsponivel, escolha protocolos de rede para melhor desempenho

Otimizacao de custo: Implementar regioes com base em custo

R.Pratico:

- Confiabilidade → planeje subnets com espaço pra crescer e em múltiplas AZs
- Segurança → use subnets como camadas (pública, privada, banco), SG, NACL
- Desempenho → recursos que se comunicam muito = mesma região/AZ
- Custo → evita transferência de dados entre regiões desnecessária