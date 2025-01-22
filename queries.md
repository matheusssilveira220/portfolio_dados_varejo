# Perguntas sobre vendas:

## 1.	Quais são os produtos mais vendidos nos últimos 3 meses?
Com essa query é possível localizar os top3 produtos nos últimos 3 meses:

```sql
SELECT 
	v.id_produto, 
	COUNT (*) AS vendas_total, 
	p.nome
FROM 
	vendas AS v
LEFT JOIN 
	produtos AS p
ON v.id_produto = p.id_produto
WHERE 
	v.data_venda >= CURRENT_DATE - INTERVAL '3 MONTHS' 
GROUP BY 
	v.id_produto, p.nome
ORDER BY 
	vendas_total DESC
LIMIT 3;
```
O resultado da Query está representado abaixo:

```markdown
|id_produto  |vendas_total  |nome        |
|------------|--------------|------------|
|38          |10            |Produto 38  |
|12          |9		    |Produto 12  |
|26          |8             |Produto 26  |
```
---

## 2.	Qual é o ticket médio das vendas realizadas por cliente?
Com essa query, encontramos o ticket médio:

```sql
SELECT 
	ROUND(SUM (valor) / COUNT (*),2) AS ticket_medio
FROM
	vendas;
```

```markdown
|ticket_medio |
|-------------|
|112.17       |
```
---

## 3.	Quais cidades concentram o maior número de vendas?
Essa query demostra as cidades onde se concentram o maior número de vendas:

```sql
SELECT  
COUNT (*) AS vendas_total,
	c.cidade
FROM
	vendas AS v
LEFT JOIN 
	clientes AS c
ON v.id_cliente = c.id_cliente
GROUP BY
	c.cidade
ORDER BY
	vendas_total DESC;
```

```markdown
|vendas_total   |cidade		 |
|---------------|----------------|
|210		|Rio de Janeiro	 |
|178		|Porto Alegre	 |
|171		|Curitiba	 |
|153		|São Paulo	 |
|145		|Belo Horizonte  |
|143		|Salvador	 |
```
---

## 4.	Qual fornecedor possui os produtos com maior volume de vendas?
Essa query já é algo mais avançado, fiz o uso de CTE e de JOINs para poder encontrar quais fornecedores possuem maior participação nas vendas:

```sql
WITH top_produtos AS (
    SELECT
        COUNT(*) AS contagem_geral,
        p.nome AS produto,
        p.id_fornecedor
    FROM 
        vendas AS v
    LEFT JOIN
        produtos AS p
    ON v.id_produto = p.id_produto
    GROUP BY 
        p.id_produto, p.nome
    ORDER BY
        contagem_geral DESC
)

SELECT 
    SUM(tp.contagem_geral) AS contagem_total,
    f.nome AS fornecedor
FROM 
    top_produtos AS tp
LEFT JOIN
    fornecedores AS f
ON tp.id_fornecedor = f.id_fornecedor
GROUP BY 
	fornecedor
ORDER BY 
	contagem_total DESC;
```

```markdown
|contagem_total	|fornecedor   |
|---------------|-------------|
|187		|Fornecedor 10|
|142		|Fornecedor 5 |
|130		|Fornecedor 2 |
|126		|Fornecedor 7 |
|93		|Fornecedor 9 |
```
---

## 5.	Existe alguma sazonalidade nas vendas que possamos explorar?
Nessa query encontramos os meses com maior venda, por se tratar de dados aleatórios, não encontrei nenhuma sazonalidade efetivamente dito:

```sql
SELECT 
	EXTRACT (MONTH FROM data_venda) AS mes,
	COUNT (*) AS contagem_venda
FROM 
	vendas
GROUP BY
	mes
ORDER BY
	contagem_venda DESC;
```

```markdown
| mes | contagem_venda |
|-----|----------------|
| 7   | 98             |
| 11  | 89             |
| 10  | 88             |
| 2   | 88             |
| 5   | 86             |
| 3   | 85             |
| 12  | 84             |
| 1   | 79             |
| 4   | 78             |
| 6   | 76             |
| 9   | 75             |
| 8   | 74             |
```
---

# Perguntas sobre clientes:

## 6. Quais clientes têm o maior valor total de compras?
Nessa query decidir ir um pouco mais longe, e encontrar também o ticket médio de cada cliente:
```sql
SELECT
	id_cliente,
	SUM (valor) AS valor_total,
	COUNT (*) AS qtde_compras,
	ROUND(SUM (valor) / COUNT (*),2) AS ticket_medio
FROM
	vendas
GROUP BY 
	id_cliente
ORDER BY
	valor_total DESC
LIMIT 5;
```

```markdown
| id_cliente | valor_total | qtde_compras | ticket_medio |
|------------|-------------|--------------|--------------|
| 232        | 1271.94     | 8            | 158.99       |
| 161        | 1236.48     | 8            | 154.56       |
| 111        | 1151.11     | 9            | 127.90       |
| 34         | 1143.14     | 9            | 127.02       |
| 182        | 1120.31     | 8            | 140.04       |
```

Notemos que o ticket medio dos melhores consumidores ficam bem proximos do ticket medio geral, isso indica que não possuimos algum cliente fora da curva, fazendo diversas compras, por um lado isso é bom, pois não dependemos de um cliente apenas.
---

## 7. Qual é o perfil geográfico dos nossos clientes mais ativos?
Nessa decidi seguir duas respostas, separando primeiramente por estado, e então por cidade.
Essa primeira query representa os estados:
```sql
SELECT
    c.estado,
    COUNT(*) AS qtde_compras
FROM
    vendas AS v
LEFT JOIN
    clientes AS c
ON 
    v.id_cliente = c.id_cliente
GROUP BY 
    c.estado
ORDER BY
    qtde_compras DESC;
```

```markdown
| estado | qtde_compras |
|--------|--------------|
| SP     | 196          |
| RJ     | 183          |
| MG     | 178          |
| BA     | 164          |
| PR     | 143          |
| RS     | 136          |
```
Nessa outra representa as cidades:
```sql
SELECT
    c.cidade,
    COUNT(*) AS qtde_compras
FROM
    vendas AS v
LEFT JOIN
    clientes AS c
ON 
    v.id_cliente = c.id_cliente
GROUP BY 
    c.cidade
ORDER BY
    qtde_compras DESC;
```

```markdown
| cidade           | qtde_compras |
|------------------|--------------|
| Rio de Janeiro   | 210          |
| Porto Alegre     | 178          |
| Curitiba         | 171          |
| São Paulo        | 153          |
| Belo Horizonte   | 145          |
| Salvador         | 143          |
```

Nos dois resultados notamos valores próximos, também nos levando a entender que não dependemos de apenas um estado ou cidade para a empresa seguir em frente.
---

## 8. Quantos clientes fizeram compras repetidas no último ano?
Nessa query encontramos diversos clientes que fizeram mais de 8 compras no último ano:
```sql
SELECT
	v.id_cliente,
	c.nome,
	COUNT(*) AS compras
FROM
	vendas AS v
LEFT JOIN
	clientes AS c
ON
	v.id_cliente = c.id_cliente
WHERE
	EXTRACT(YEAR FROM data_venda) = 2024
GROUP BY 
	v.id_cliente, c.nome
HAVING
	COUNT(*) > 8
;
```

```markdown
| id_cliente | nome         | compras |
|------------|--------------|---------|
| 14         | Cliente 14   | 9       |
| 34         | Cliente 34   | 9       |
| 54         | Cliente 54   | 9       |
| 55         | Cliente 55   | 9       |
| 61         | Cliente 61   | 9       |
| 102        | Cliente 102  | 9       |
| 111        | Cliente 111  | 9       |
| 139        | Cliente 139  | 9       |
| 195        | Cliente 195  | 9       |
| 223        | Cliente 223  | 9       |
```

Aqui encontramos uma frequencia alta de compra entre diversos consumidor, reduzi o valor de corte para 8, visto que até 7 compras recentes traria boa parte da tabela.
---
