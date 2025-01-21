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
	vendas_total DESC;
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
---

## 8. Quantos clientes fizeram compras repetidas no último ano?
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
	COUNT(*) > 5
;
```
---
