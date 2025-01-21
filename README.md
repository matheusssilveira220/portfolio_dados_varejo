# :open_book: VAREJO

Projeto voltado a simular uma empresa de varejo, especificamente o setor de vendas e parcialmente o controle de estoque / fornecedores. Com ajuda do ChatGPT, criei repositorios aleatorios de dados dentro do PostgreSQL. Criado tabelas e itens dentro do BD, utilizei SQL e PowerBI para realizar a Análise + Data visualization.

### :wrench: Ferrramentas
-**ChatGPT**

-**PostgreSQL**

-**SQL**

-**PowerBI**

### :memo: Skills utilizadas

-**Criação Banco de Dados**

-**Criação Aleatória de Informações**

-**Criações de Queryes**

-**Importação de Dados ao PowerBI**

-**Data visualization**

-**Data Storytelling**

# Etapas

## Criação Banco de Dados

Optei por utilizar o BD PostgreSQL, por se tratar de um software OpenSource e de alta escalabilidade. O script para criação das tabelas, e randomização dos dados deixarei no arquivo SQL. Foram criadas 4 tabelas, sendo elas, Clientes, Fornecedores, Produtos e Vendas. Deixarei o esquema de relações entre as tabelas em um PDF.

## Conversa com stakeholder

Por se tratar de um projeto ficticio, não existe um stakeholder, para suprir essa etapa, solicitei ao ChatGPT, que simulasse essa etapa. Pedi que realizasse perguntas necessárias para entender o andamento do processo de vendas, para que eu encontrasse um norte para seguir com a análise. 

Criei o seguinte script de conversa após explicar o projeto a ele:

**Script**

Atue como o stakeholder desse projeto. Imagine que sou o analista de dados de sua empresa, e você está com algumas dúvidas quanto ao processo de vendas, me passe algumas perguntas para que eu possa analisar os dados e lhe passar as respostas.

**Reposta do ChatGPT**

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


Essas perguntas ajudam a guiar uma análise estratégica do processo de vendas, promovendo insights úteis para ações futuras. Se precisar de ajuda com queries específicas para responder a qualquer uma dessas perguntas, estou aqui para ajudar!

## Análise Exploratória

Agora com o BD montado, e as perguntas na mesa, precisava entender com oque estava trabalhando, iniciei então uma análise exploratória no banco de dados utilizando o SQL.

Separei a análise nas seguintes etapas:

1. Entender a relação entre as planilhas para poder utilizar Joins com efetividade;

2. Conhecer os tipos de dados, para não utilizar memória desencessária nas Queries;

3. Começar a responder as perguntas utilizando as Queries, de forma que a importação para o PowerBI fique mais rápida.

## Definição de como será respondido as perguntas

Como estamos simulando um stakeholder, não posso assumir a forma que ele deseja receber, dessa forma farei 2 apresentações diferentes. A primeira foi feita uma apresentação em PDF, contendo a resposta em Queries com respostas diretas. Já a segunda, em forma de dashboard contendo gráficos de evolução temporal e permitindo que o usuário visualize as áreas desejadas.
