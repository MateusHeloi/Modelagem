Modelagem Dimensional no Power BI

Documentação do modelo de dados de vendas construído no Power BI. A imagem mostra uma tabela central de vendas relacionada a cinco tabelas dimensionais: calendário, canal, clientes, produtos e vendedores.


## Objetivo da modelagem

Organizar os dados para facilitar análises de vendas por período, canal, cliente, produto e vendedor. O modelo segue uma estrutura dimensional em estrela: a tabela de fatos fica no centro e as dimensões fornecem atributos para filtrar e agrupar os valores registrados nas vendas.

## Visão do modelo

![Modelo de dados no Power BI](https://private-us-east-1.manuscdn.com/sessionFile/bMOXjejioTkwIdVn2UTGM9/sandbox/Xi5Ay7b6xrZ8hOMWQhjZEE-images_1792026168025_na1fn_L2hvbWUvdWJ1bnR1L21vZGVsYWdlbS1kaW1lbnNpb25hbC1wb3dlci1iaS9pbWFnZW5zL21vZGVsby1wb3dlci1iaQ.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvYk1PWGplamlvVGt3SWRWbjJVVEdNOS9zYW5kYm94L1hpNUF5N2I2eHJaOGhPTVdRaGpaRUUtaW1hZ2VzXzE3OTIwMjYxNjgwMjVfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwyMXZaR1ZzWVdkbGJTMWthVzFsYm5OcGIyNWhiQzF3YjNkbGNpMWlhUzlwYldGblpXNXpMMjF2WkdWc2J5MXdiM2RsY2kxaWFRLnBuZyIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc5MzQ5MTIwMH19fV19&Key-Pair-Id=K2QY5QTL8JSY6C&Signature=MEUCIFsYtqJTcvUpIlceD~Jm4N1Al4PIRGH-M7j9NLbXYbisAiEAw~yb8oU37gzUQplh37EB-Cf8BM5ypghQY4~GpU-En5o_)

### Tabela fato: `fVendas`

`fVendas` concentra os registros transacionais e as medidas associadas às vendas. Na captura, aparecem campos como:

- `id_venda`: identificador da venda;
- `data_venda`: data associada à transação;
- `id_cliente`, `id_produto` e `id_vendedor`: chaves que relacionam a venda às dimensões correspondentes;
- `canal`: canal pelo qual a venda ocorreu;
- `desconto`: informação de desconto;
- `cidade_entrega` e `forma_pagamento`: atributos da transação.

Cada linha da tabela fato representa um registro de venda. Os campos numéricos, como desconto, podem ser agregados ou utilizados em medidas conforme as perguntas de análise e as regras do relatório.

### Tabelas dimensão

As dimensões guardam atributos descritivos usados para explorar as vendas:

| Dimensão | Campos visíveis na captura | Exemplos de análise |
| --- | --- | --- |
| `dCalendario` | `Date`, `Ano`, `Dia`, `Dia da semana`, `Mes Abrev` | Evolução por ano, mês, dia ou dia da semana |
| `dCanal` | `canal` | Comparação entre canais de venda |
| `dClientes` | `id_cliente`, `nome`, `segmento`, `data_cadastro` | Vendas por cliente ou segmento |
| `dProdutos` | `id_produto`, `nome_produto`, `marca`, `custo_base` | Vendas por produto ou marca |
| `dVendedor` | `id_vendedor`, `vendedor_nome`, `equipe_vendas` | Desempenho por vendedor ou equipe |

## Relacionamentos

Pelos nomes dos campos e pelas linhas visíveis no diagrama, as ligações do modelo são:

- `dCalendario[Date]` → `fVendas[data_venda]`;
- `dCanal[canal]` → `fVendas[canal]`;
- `dClientes[id_cliente]` → `fVendas[id_cliente]`;
- `dProdutos[id_produto]` → `fVendas[id_produto]`;
- `dVendedor[id_vendedor]` → `fVendas[id_vendedor]`.

A captura apresenta cardinalidade **um para muitos (1:*)**: o lado `1` está nas dimensões e o lado `*` na tabela de vendas. Assim, um cliente, produto, vendedor, canal ou data pode estar associado a vários registros de venda. As setas do diagrama representam a propagação de filtros das dimensões para a tabela fato.

> Os pares de colunas acima foram identificados pelos nomes dos campos visíveis e pelas ligações do diagrama. O arquivo do modelo não foi disponibilizado para validar configurações adicionais, como tipos de dados, chaves únicas ou direção de filtro definida em cada relacionamento.

## Como esse desenho ajuda nas análises

- As dimensões oferecem categorias consistentes para segmentar os dados de vendas.
- O calendário permite análises temporais sem depender apenas dos campos de data da tabela fato.
- Os relacionamentos 1:* evitam repetir todos os atributos descritivos em cada linha de venda.
- A organização em estrela torna mais fácil criar visuais que cruzam valores de vendas com cliente, produto, canal, vendedor ou período.
- A propagação de filtros das dimensões para `fVendas` ajuda a manter os recortes do relatório previsíveis.

## Conceitos e ferramentas

- Power BI e modelo semântico;
- Modelagem dimensional;
- Tabela fato e tabelas dimensão;
- Esquema estrela;
- Relacionamentos 1:*;
- Chaves de relacionamento;
- Filtros e análise temporal.

## Arquivos

- `README.md`: descrição da estrutura do modelo e de seus relacionamentos.
- `imagens/modelo-power-bi.png`: captura do diagrama no Power BI.

O arquivo `.pbix` poderá ser adicionado quando estiver disponível.
