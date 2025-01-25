# [Ver outros projetos](https://github.com/matheusssilveira220/portfolio_dados)
---
# :open_book: VAREJO

Projeto voltado a simular uma empresa de varejo, especificamente o setor de vendas. Com ajuda do DeepSeek, criei repositorios aleatorios de dados dentro do PostgreSQL. Criado tabelas e itens dentro do BD, utilizei SQL para realizar as queries e encontrar os insights dentro do Banco de Dados

---

### :wrench: Ferrramentas
-**DeepSeek**

-**PostgreSQL**

-**SQL**

### :memo: Skills utilizadas

-**Criação Banco de Dados**

-**Criação Aleatória de Informações**

-**Criações de Queries**

-**Data Storytelling**

---

## Replicar projeto

Para replicar o projeto, será necessário a utilização do Banco de Dados PostgreSQL;

Criar as tabelas citadas;

Randomizar os dados;

Então executar as queries na pasta queries.

---

# Etapas

## Criação Banco de Dados

Optei por utilizar o BD PostgreSQL, por se tratar de um software OpenSource e de alta escalabilidade. O script para criação das tabelas, e randomização dos dados deixarei no arquivo query_criacao_bd. Foram criadas 4 tabelas, sendo elas, Clientes, Fornecedores, Produtos e Vendas. Deixarei o esquema de relações entre as tabelas em um PDF.

---

## Análise Exploratória

Agora com o BD montado, e as perguntas na mesa, precisava entender com oque estava trabalhando, iniciei então uma análise exploratória no banco de dados utilizando o SQL.

Separei a análise nas seguintes etapas:

1. Entender a relação entre as planilhas para poder utilizar Joins com efetividade;
Para isso fiz o estudo do [diagrama](https://github.com/matheusssilveira220/portfolio_dados_varejo/blob/main/diagrama.png) do banco de dados.

2. Conhecer os tipos de dados, para não utilizar memória desencessária nas Queries;
Nada de anormal, por se tratar de dados criados dentro do próprio banco de dados.  

3. Começar a responder as perguntas utilizando as Queries.
   
---

## Definição de como serão respondidas as perguntas

Farei a resposta crua no arquivos queries, e montarei um storytelling no arquivo storytelling.

### [Queries](https://github.com/matheusssilveira220/portfolio_dados_varejo/blob/main/queries.md)
As queries para resposta das dúvidas estão no arquivo queries, nele pode ver as etapas e decisões que tomei para responder cada pergunta, fiz o uso de CTES e JOINs.

### [Stotytelling](https://github.com/matheusssilveira220/portfolio_dados_varejo/blob/main/storytelling.md)
No arquivo Storytelling, podera conferir os insights que obtive realizando a análise nesse banco de dados.
