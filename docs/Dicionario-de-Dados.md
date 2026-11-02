## 1. Tabela Pedidos

| Campo | Tabela | Descrição | Regra de cálculo |
|---|---|---|---|
| ID Pedido | Pedidos | Identificador do pedido | Valor original do arquivo |
| ID Cliente | Pedidos | Identificador do cliente associado ao pedido | Valor original do arquivo |
| Status Pedido | Pedidos | Situação do pedido | Valor original do arquivo |
| Data Compra | Pedidos | Data e hora da compra | Convertida para formato de data e hora |
| Data Entrega | Pedidos | Data e hora da entrega ao cliente | Convertida para formato de data e hora |
| Data Estimada | Pedidos | Data estimada de entrega | Convertida para formato de data e hora |
| Ano | Pedidos | Ano da compra | Extraído da Data Compra |
| Ano-Mês | Pedidos | Ano e mês da compra | Obtido a partir da Data Compra |
| Dias Entrega | Pedidos | Quantidade de dias entre compra e entrega | Data da entrega menos data da compra, somente para pedidos entregues com data preenchida |
| Flag Atraso | Pedidos | Indica se o pedido foi entregue depois da data estimada | 1 se a data da entrega for posterior à data estimada; 0 caso contrário |
| Flag Entregue Sem Data | Pedidos | Identifica pedidos entregues sem data de entrega | 1 se o status for delivered e a data estiver vazia; 0 caso contrário |
| Flag Entrega Antes da Compra | Pedidos | Identifica datas de entrega anteriores à compra | 1 se a data da entrega for anterior à compra; 0 caso contrário |
| Flag Sem Itens | Pedidos | Identifica pedidos sem itens associados | 1 se não houver itens associados; 0 caso contrário |

## 2. Tabela Clientes

| Campo | Tabela | Descrição | Regra de cálculo |
|---|---|---|---|
| ID Cliente | Clientes | Identificador do cliente associado ao pedido | Valor original do arquivo |
| ID Cliente Único | Clientes | Identificador que representa o cliente entre pedidos | Valor original do arquivo |
| Cidade | Clientes | Cidade do cliente | Valor original do arquivo |
| UF | Clientes | Estado do cliente | Valor original do arquivo |
| Região | Clientes | Região brasileira do cliente | Mapeada a partir da UF |

## 3. Tabela Produtos

| Campo | Tabela | Descrição | Regra de cálculo |
|---|---|---|---|
| ID Produto | Produtos | Identificador do produto | Valor original do arquivo |
| Categoria | Produtos | Categoria do produto | Categoria original; valores vazios são classificados como Sem categoria |
| Categoria EN | Produtos | Categoria em inglês | Obtida pelo mapeamento das categorias; valores sem correspondência recebem Sem categoria |

## 4. Tabela Itens

| Campo | Tabela | Descrição | Regra de cálculo |
|---|---|---|---|
| ID Pedido | Itens | Identificador do pedido ao qual o item pertence | Valor original do arquivo |
| Nº Item | Itens | Identificador do item dentro do pedido | Valor original do arquivo |
| ID Produto | Itens | Identificador do produto associado ao item | Valor original do arquivo |
| ID Vendedor | Itens | Identificador do vendedor | Valor original do arquivo |
| Valor Item | Itens | Valor do item do pedido | Valor original do arquivo |
| Valor Frete | Itens | Valor do frete associado ao item | Valor original do arquivo |
| Flag Frete Zero | Itens | Identifica itens com frete zerado | 1 se o frete for zero; 0 caso contrário |

## 5. Indicadores do Dashboard

| Indicador | Fórmula | Interpretação |
|---|---|---|
| Pedidos | Count(DISTINCT [ID Pedido]) | Quantidade de pedidos distintos |
| Prazo médio (dias) | Avg([Dias Entrega]) | Média de dias entre compra e entrega |
| % entregas atrasadas | Avg([Flag Atraso]) | Proporção de pedidos entregues após a data estimada |
| Frete médio por pedido | Sum([Valor Frete]) / Count(DISTINCT [ID Pedido]) | Valor total do frete dividido pela quantidade de pedidos distintos |
| Frete sobre valor dos itens | Sum([Valor Frete]) / Sum([Valor Item]) | Proporção entre o frete total e o valor total dos itens |