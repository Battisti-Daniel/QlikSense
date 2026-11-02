## 1. Objetivo

O dashboard tem como objetivo analisar indicadores relacionados aos prazos de entrega, aos custos de frete e à qualidade dos dados de pedidos de um conjunto público de dados de e-commerce brasileiro.

## 2. Regras para cálculo do prazo de entrega

- O prazo é calculado pela diferença entre a data de entrega e a data da compra.
- O cálculo considera somente pedidos com status delivered e data de entrega preenchida.
- A diferença é calculada em dias, desconsiderando o horário.
- Pedidos cancelados ou ainda não entregues não entram no cálculo do prazo médio.

## 3. Regras para identificação de atrasos

- Um pedido é considerado atrasado quando a data real da entrega é posterior à data estimada.
- A comparação considera somente o dia, desconsiderando o horário.
- O campo Flag Atraso recebe 1 quando há atraso e 0 quando não há atraso.
- Pedidos que não atendem aos critérios de avaliação recebem valor nulo nesse campo.
- O percentual de entregas atrasadas é calculado pela média da Flag Atraso.

## 4. Regras para cálculo dos indicadores de frete

- O frete é registrado por item do pedido.
- O frete médio por pedido é calculado pela soma dos valores de frete dividida pela quantidade de pedidos distintos.
- A proporção do frete sobre o valor dos itens é calculada dividindo a soma do frete pela soma dos valores dos itens.
- A interpretação dos indicadores deve considerar que um pedido pode conter vários itens.
- Pedidos sem itens podem afetar o denominador do frete médio por pedido e devem ser investigados.

## 5. Regras de classificação geográfica

- A região brasileira é identificada a partir da UF do cliente.
- As UFs são associadas às regiões Norte, Nordeste, Centro-Oeste, Sudeste e Sul.
- Caso uma UF não seja encontrada no mapeamento, a região recebe o valor Não identificada.

## 6. Regras de qualidade dos dados

Os seguintes problemas são sinalizados:

| Problema | Critério de identificação | Tratamento inicial |
|---|---|---|
| Entregue sem data | Pedido com status delivered e data de entrega vazia | Sinalizar e investigar |
| Entrega antes da compra | Data de entrega anterior à data de compra | Sinalizar e investigar |
| Pedido sem itens | Pedido sem itens associados | Sinalizar e investigar |
| Frete zero | Item com valor de frete igual a zero | Sinalizar e investigar |
| Possíveis duplicidades | Divergência entre a contagem total e a contagem distinta de IDs de pedido | Investigar antes de corrigir |

Os registros problemáticos não devem ser excluídos automaticamente. A decisão deve considerar a causa provável, o impacto nos indicadores e a justificativa para manter, excluir ou tratar cada registro.

## 7. Período de análise

O conjunto de dados contempla registros de 2016 a 2018.

Como 2016 e o final de 2018 podem apresentar poucos pedidos, a análise pode priorizar 2017 e 2018, desde que essa decisão seja registrada.

## 8. Limitações

- Os dados representam um conjunto público de e-commerce.
- A existência de uma anomalia não comprova, por si só, a causa do problema.
- Os indicadores dependem da disponibilidade e da qualidade das datas, dos pedidos e dos itens.
- A análise de frete por pedido precisa considerar que o frete está registrado por item.