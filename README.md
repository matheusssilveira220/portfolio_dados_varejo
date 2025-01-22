#[Ver outros projetos](https://github.com/matheusssilveira220/portfolio_dados)
---
# :open_book: VAREJO

Projeto voltado a simular uma empresa de varejo, especificamente o setor de vendas e parcialmente o controle de estoque / fornecedores. Com ajuda do DeepSeek, criei repositorios aleatorios de dados dentro do PostgreSQL. Criado tabelas e itens dentro do BD, utilizei SQL e PowerBI para realizar a Análise + Data visualization.

### :wrench: Ferrramentas
-**DeepSeek**

-**PostgreSQL**

-**SQL**

-**PowerBI**

### :memo: Skills utilizadas

-**Criação Banco de Dados**

-**Criação Aleatória de Informações**

-**Criações de Queries**

-**Importação de Dados ao PowerBI**

-**Data visualization**

-**Data Storytelling**

## Replicar projeto

Para replicar o projeto, será necessário a utilização do Banco de Dados PostgreSQL;
Criar as tabelas citadas;
Randomizar os dados;
Então executar as queries na pasta queries.

# Etapas

## Criação Banco de Dados

Optei por utilizar o BD PostgreSQL, por se tratar de um software OpenSource e de alta escalabilidade. O script para criação das tabelas, e randomização dos dados deixarei no arquivo query_criacao_bd. Foram criadas 4 tabelas, sendo elas, Clientes, Fornecedores, Produtos e Vendas. Deixarei o esquema de relações entre as tabelas em um PDF.

## Conversa com stakeholder

Por se tratar de um projeto ficticio, não existe um stakeholder, para suprir essa etapa, solicitei ao DeepSeek, que simulasse essa etapa. Pedi que realizasse perguntas necessárias para entender o andamento do processo de vendas, para que eu encontrasse um norte para seguir com a análise. 

Criei o seguinte script de conversa após explicar o projeto a ele:

**Script**

Atue como o stakeholder desse projeto. Imagine que sou o analista de dados de sua empresa, e você está com algumas dúvidas quanto ao processo de vendas, me passe algumas perguntas para que eu possa analisar os dados e lhe passar as respostas.

**Reposta do DeepSeek**

Claro! Como stakeholder do projeto, aqui estão algumas perguntas relevantes sobre o processo de vendas que podem ajudar a entender melhor o desempenho e identificar oportunidades de melhoria:

#### Perguntas sobre vendas:
1. **Quais são os produtos mais vendidos nos últimos 3 meses?**
2. **Qual é o ticket médio das vendas realizadas por cliente?**
3. **Quais cidades concentram o maior número de vendas?**
4. **Qual fornecedor possui os produtos com maior volume de vendas?**
5. **Existe alguma sazonalidade nas vendas que possamos explorar?**

#### Perguntas sobre clientes:
6. **Quais clientes têm o maior valor total de compras?**
7. **Qual é o perfil geográfico dos nossos clientes mais ativos?**
8. **Quantos clientes fizeram compras repetidas no último ano?**


## Análise Exploratória

Agora com o BD montado, e as perguntas na mesa, precisava entender com oque estava trabalhando, iniciei então uma análise exploratória no banco de dados utilizando o SQL.

Separei a análise nas seguintes etapas:

1. Entender a relação entre as planilhas para poder utilizar Joins com efetividade;
Para isso fiz o estudo do [diagrama](https://github.com/matheusssilveira220/portfolio_dados_varejo/blob/main/diagrama.png) do banco de dados.

2. Conhecer os tipos de dados, para não utilizar memória desencessária nas Queries;
Nada de anormal, por se tratar de dados criados dentro do próprio banco de dados.  

3. Começar a responder as perguntas utilizando as Queries.
Farei isso criando queries dentro do banco de dados.

4. Farei um dashboard interativo, que contenham todas as informações presentes no banco de dados, de forma que fique simples que o stakeholder ou qualquer outro consiga encontrar as informações desejadas.

## Definição de como serão respondidas as perguntas

Como estamos simulando um stakeholder, não posso assumir a forma que ele deseja receber, dessa forma farei 2 apresentações diferentes. A primeira será feita utilizando as queries, respondendo diretamente as perguntas, e buscando algum insight. Já a segunda, em forma de dashboard contendo gráficos de evolução temporal e permitindo que o usuário visualize as áreas desejadas.

## [Queries](https://github.com/matheusssilveira220/portfolio_dados_varejo/blob/main/queries.md)
As queries para resposta das dúvidas estão no arquivo queries, nele pode ver as etapas e decisões que tomei para responder cada pergunta, fiz o uso de CTES e JOINs.

## Dashboard
Ainda em construção...
