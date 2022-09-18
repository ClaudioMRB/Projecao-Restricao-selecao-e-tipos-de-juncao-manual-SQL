## --------------------------Restrições de SQL-----------------------------------

[SQL restrições (w3bai.com)](https://www.w3bai.com/pt/sql/sql_constraints.html#gsc.tab=0)



restrições de SQL são usadas para especificar as regras para os dados em uma tabela.

Se houver qualquer violação entre a restrição e a ação de dados, a ação é abortada pela restrição.

As restrições podem ser especificado quando a tabela é criada (dentro da instrução CREATE TABLE) ou após a tabela é criada (dentro da instrução ALTER TABLE).

### SQL CREATE TABLE + CONSTRAINT Sintaxe

CREATE TABLE *table_name*
(
*column_name1 data_type* ( *size* ) *constraint_name* ,
*column_name2 data_type* ( *size* ) *constraint_name* ,
*column_name3 data_type* ( *size* ) *constraint_name* ,
....
);

Em SQL, temos as seguintes restrições:

- **NOT NULL** - Indica que a coluna não pode armazenar o valor NULL

- **UNIQUE** - Garante que cada linha para uma coluna deve ter um valor único

- **PRIMARY KEY** - Uma combinação de um NOT NULL e único. Garante que uma coluna (ou a combinação de duas ou mais colunas) tem uma identidade única, que ajuda a localizar um registo em particular, uma tabela com mais facilidade e rapidamente

- **FOREIGN KEY** - Assegurar a integridade referencial dos dados em uma tabela para coincidir com os valores em outra tabela

- **CHECK** - Garante que o valor em uma coluna corresponde a uma condição específica

- **PADRÃO** - especifica um valor padrão para uma coluna

  

## -------------------------SQL NOT NULL Constraint------------------------

A restrição NOT NULL impõe uma coluna de não aceitar valores nulos.

A restrição NOT NULL impõe um campo para conter sempre um valor. Isso significa que você não pode inserir um novo registro, ou atualizar um registro sem adicionar um valor para este campo.

O seguinte SQL impõe a "P_Id" coluna e "LastName" coluna para não aceitar valores nulos:

### Exemplo

CREATE TABLE PersonsNotNull
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)



## -----------------------SQL restrição exclusiva------------------------------

A restrição UNIQUE identifica exclusivamente cada registro em uma tabela de banco de dados.

As UNIQUE e PRIMARY KEY restrições tanto fornecer uma garantia de exclusividade para uma coluna ou conjunto de colunas.

Uma restrição de chave primária tem automaticamente uma restrição UNIQUE definida nele.

Note que você pode ter muitas restrições UNIQUE por mesa, mas apenas uma restrição PRIMARY KEY por tabela.

------

## SQL restrição exclusiva em CREATE TABLE

O seguinte SQL cria uma restrição UNIQUE na "P_Id" coluna quando a "Persons" tabela é criada:

**SQL Server / Oracle / MS Access:**

CREATE TABLE Persons
(
P_Id int NOT NULL UNIQUE,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)

**MySQL:**

CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
UNIQUE (P_Id)
)

Para permitir a nomeação de uma restrição UNIQUE, e para a definição de uma restrição exclusiva em várias colunas, use a seguinte sintaxe SQL:

**MySQL / SQL Server / Oracle / MS Access:**

CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName)
)

## SQL restrição exclusiva em ALTER TABLE

Para criar uma restrição UNIQUE na "P_Id" coluna quando a tabela já é criado, use o seguinte SQL:

**MySQL / SQL Server / Oracle / MS Access:**

ALTER TABLE Persons
ADD UNIQUE (P_Id)

Para permitir a nomeação de uma restrição UNIQUE, e para a definição de uma restrição exclusiva em várias colunas, use a seguinte sintaxe SQL:

**MySQL / SQL Server / Oracle / MS Access:**

ALTER TABLE Persons
ADD CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName)

------

## Para excluir uma restrição exclusiva

Para eliminar uma restrição UNIQUE, use o seguinte SQL:

**MySQL:**

ALTER TABLE Persons
DROP INDEX uc_PersonID

**SQL Server / Oracle / MS Access:**

ALTER TABLE Persons
DROP CONSTRAINT uc_PersonID



## -------------------------SQL restrição CHECK--------------------------------

A verificação de restrição é usada para limitar a gama de valores que pode ser colocada em uma coluna.

Se você definir uma restrição CHECK em uma única coluna que permite que apenas determinados valores para esta coluna.

Se você definir uma restrição CHECK em uma tabela que pode limitar os valores em determinadas colunas com base nos valores em outras colunas na linha.

------

## Restrição CHECK SQL em CREATE TABLE

O seguinte SQL cria uma restrição CHECK no "P_Id" coluna quando a "Persons" tabela é criada. A restrição CHECK especifica que a coluna "P_Id" deve incluir apenas números inteiros maiores do que 0.

**MySQL:**

CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CHECK (P_Id>0)
)

**SQL Server / Oracle / MS Access:**

CREATE TABLE Persons
(
P_Id int NOT NULL CHECK (P_Id>0),
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)

Para permitir a nomeação de uma restrição CHECK, e para a definição de uma restrição CHECK em várias colunas, use a seguinte sintaxe SQL:

**MySQL / SQL Server / Oracle / MS Access:**

CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes')
)

------

## SQL restrição CHECK em ALTER TABLE

Para criar uma restrição CHECK no "P_Id" coluna quando a tabela já é criado, use o seguinte SQL:

**MySQL / SQL Server / Oracle / MS Access:**

ALTER TABLE Persons
ADD CHECK (P_Id>0)

Para permitir a nomeação de uma restrição CHECK, e para a definição de uma restrição CHECK em várias colunas, use a seguinte sintaxe SQL:

**MySQL / SQL Server / Oracle / MS Access:**

ALTER TABLE Persons
ADD CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes')

------

## Para excluir uma restrição CHECK

Para eliminar uma restrição CHECK, use o seguinte SQL:

**SQL Server / Oracle / MS Access:**

ALTER TABLE Persons
DROP CONSTRAINT chk_Person

**MySQL:**

ALTER TABLE Persons
DROP CHECK chk_Person



## ------------------------------Restrição padrão SQL-------------------------

A restrição padrão é utilizado para inserir um valor predefinido para uma coluna.

O valor padrão será adicionado a todos os novos registros, se nenhum outro valor for especificado.

------

## Restrição padrão SQL em CREATE TABLE

O seguinte SQL cria uma restrição DEFAULT na "City" coluna quando a "Persons" tabela é criada:

**My SQL / SQL Server / Oracle / MS Access:**

CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255) DEFAULT 'Sandnes'
)

A restrição padrão também podem ser usadas para inserir os valores do sistema, usando funções como GETDATE ():

CREATE TABLE Orders
(
O_Id int NOT NULL,
OrderNo int NOT NULL,
P_Id int,
OrderDate date DEFAULT GETDATE()
)

------

## Restrição padrão SQL em ALTER TABLE

Para criar uma restrição padrão no "City" coluna quando a tabela já é criado, use o seguinte SQL:

**MySQL:**

ALTER TABLE Persons
ALTER City SET DEFAULT 'SANDNES'

**SQL Server / MS Access:**

ALTER TABLE Persons
ALTER COLUMN City SET DEFAULT 'SANDNES'

**Oracle:**

ALTER TABLE Persons
MODIFY City DEFAULT 'SANDNES'

------

## Para excluir uma restrição padrão

Para eliminar uma restrição padrão, use o seguinte SQL:

**MySQL:**

ALTER TABLE Persons
ALTER City DROP DEFAULT

**SQL Server / Oracle / MS Access:**

ALTER TABLE Persons
ALTER COLUMN City DROP DEFAULT



**-------------------------------------------------------SELECT (SELEÇÃO)------------------------------------------------------------------------------------**

[Select (SQL) – Wikipédia, a enciclopédia livre (wikipedia.org)](https://pt.wikipedia.org/wiki/Select_(SQL)#:~:text=SELECT é uma declaração SQL que retorna um,Linguagem de Manipulação de Dados (DML) mais utilizado.)



**SELECT** é uma declaração SQL que retorna um [conjunto de resultados](https://pt.wikipedia.org/wiki/Conjunto_de_resultados) de registros de uma ou mais tabelas. Ela recupera zero ou mais linhas de uma ou mais tabelas-base, tabelas temporárias ou visões em um banco de dados. Na maioria das aplicações, `SELECT` é o comando de [Linguagem de Manipulação de Dados](https://pt.wikipedia.org/wiki/Linguagem_de_Manipulação_de_Dados) (DML) mais utilizado. Como SQL é uma linguagem não [procedural](https://pt.wikipedia.org/wiki/Linguagem_procedural), consultas `SELECT` especificam um conjunto de resultados, mas não especificam como calculá-los, ou seja, a consulta em um "[plano de consulta](https://pt.wikipedia.org/w/index.php?title=Plano_de_consulta&action=edit&redlink=1)" é deixada para o sistema de banco de dados, mais especificamente para o [otimizador de consulta](https://pt.wikipedia.org/w/index.php?title=Otimizador_de_consulta&action=edit&redlink=1).





## Visão Geral

**SELECT** é a operação mais comum em SQL, chamada de "consulta". SELECT recupera dados de uma ou mais tabelas ou expressões. As instruções SELECT padrão não têm efeitos persistentes no banco de dados. Algumas implementações não padrão de SELECT podem ter efeitos persistentes, como a sintaxe SELECT INTO fornecida em alguns bancos de dados. As consultas permitem que o usuário descreva os dados desejados, cabendo ao sistema de gerenciamento de banco de dados (DBMS) realizar o planejamento, a otimização e a execução das operações físicas necessárias para produzir aquele resultado conforme sua escolha.

Uma consulta inclui uma lista de colunas a serem incluídas no resultado final, normalmente imediatamente após a palavra-chave SELECT. Um asterisco ("*") pode ser usado para especificar que a consulta deve retornar todas as colunas das tabelas consultadas. SELECT é a instrução mais complexa em SQL, com palavras-chave e cláusulas opcionais que incluem:

- A cláusula **FROM**, que indica a (s) tabela (s) das quais recuperar dados. A cláusula **FROM** pode incluir subcláusulas **JOIN** opcionais para especificar as regras de junção de tabelas.
- A cláusula **WHERE** inclui um predicado de comparação, que restringe as linhas retornadas pela consulta. A cláusula **WHERE** elimina todas as linhas do conjunto de resultados onde o predicado de comparação não é avaliado como True.
- A cláusula **GROUP BY** projeta linhas com valores comuns em um conjunto menor de linhas. **GROUP** **BY** é freqüentemente usado em conjunto com funções de agregação SQL ou para eliminar linhas duplicadas de um conjunto de resultados. A cláusula **WHERE** é aplicada antes da cláusula **GROUP BY**.
- A cláusula **HAVING** inclui um predicado usado para filtrar linhas resultantes da cláusula **GROUP** **BY**. Como ela atua sobre os resultados da cláusula **GROUP** **BY**, as funções de agregação podem ser usadas no predicado da cláusula **HAVING**.
- A cláusula **ORDER** **BY** identifica quais colunas usar para classificar os dados resultantes e em que direção classificá-los (crescente ou decrescente). Sem uma cláusula **ORDER** **BY**, a ordem das linhas retornadas por uma consulta SQL é indefinida.
- A palavra-chave **DISTINCT** elimina dados duplicados.

O exemplo a seguir de uma consulta SELECT retorna uma lista de livros caros. A consulta recupera todas as linhas da tabela Livro na qual a coluna de preço contém um valor maior que 100,00. O resultado é classificado em ordem crescente por título. O asterisco (*) na lista de seleção indica que todas as colunas da tabela Book devem ser incluídas no conjunto de resultados.

```
SELECT *
 FROM  Book
 WHERE price > 100.00
 ORDER BY title;
```

O exemplo a seguir demonstra uma consulta de várias tabelas, agrupamento e agregação, retornando uma lista de livros e o número de autores associados a cada livro.

```
SELECT Book.title AS Title,
       count(*) AS Authors
 FROM  Book
 JOIN  Book_author
   ON  Book.isbn = Book_author.isbn
 GROUP BY Book.title;
```

O resultado de exemplo pode ser semelhante ao seguinte:

```
Title                  Authors
---------------------- -------
SQL Examples and Guide 4
The Joy of SQL         1
An Introduction to SQL 2
Pitfalls of SQL        1
```

Sob a pré-condição de que isbn é o único nome de coluna comum das duas tabelas e que uma coluna chamada title só existe na tabela Book, pode-se reescrever a consulta acima da seguinte forma:

```
SELECT title,
       count(*) AS Authors
 FROM  Book
 NATURAL JOIN Book_author
 GROUP BY title;
```

No entanto, muitos fornecedores de não oferecem suporte a essa abordagem ou exigem certas convenções de nomenclatura de coluna para que as junções naturais funcionem de maneira eficaz. SQL inclui operadores e funções para calcular valores em valores armazenados. O SQL permite o uso de expressões na lista de seleção para projetar dados, como no exemplo a seguir, que retorna uma lista de livros que custam mais de 100,00 com uma coluna sales_tax adicional contendo um valor de imposto sobre vendas calculado a 6% do preço.

```
SELECT isbn,
       title,
       price,
       price * 0.06 AS sales_tax
 FROM  Book
 WHERE price > 100.00
 ORDER BY title;
```

### Subqueries

As consultas podem ser aninhadas para que os resultados de uma consulta possam ser usados em outra consulta por meio de um operador relacional ou função de agregação. Uma consulta aninhada também é conhecida como subconsulta. Embora junções e outras operações de tabela forneçam alternativas computacionalmente superiores (ou seja, mais rápidas) em muitos casos, o uso de subconsultas introduz uma hierarquia na execução que pode ser útil ou necessária. No exemplo a seguir, a função de agregação AVG recebe como entrada o resultado de uma subconsulta:

```
SELECT isbn,
       title,
       price
 FROM  Book
 WHERE price < (SELECT AVG(price) FROM Book)
 ORDER BY title;
```

Uma subconsulta pode usar valores da consulta externa e, nesse caso, é conhecida como subconsulta correlacionada

Desde 1999, o padrão SQL permite subconsultas nomeadas chamadas expressões de tabela comuns (nomeadas e projetadas após a implementação do IBM DB2 versão 2; o Oracle chama essas subconsultas de fatoração). CTEs também podem ser recursivos referindo-se a si próprios; o mecanismo resultante permite percursos de árvore ou gráfico (quando representados como relações) e, de forma mais geral, cálculos de pontos fixos.

### Inline view

Uma visualização embutida é o uso de referência a uma subconsulta SQL em uma cláusula FROM. Essencialmente, a visualização embutida é uma subconsulta que pode ser selecionada ou associada. A funcionalidade de visualização embutida permite que o usuário faça referência à subconsulta como uma tabela. A visualização embutida também é conhecida como tabela derivada ou subseleção. A funcionalidade de visualização embutida foi introduzida no Oracle 9i.

No exemplo a seguir, a instrução SQL envolve uma junção da tabela Books inicial para a visualização Inline "Vendas". Esta visualização em linha captura informações de vendas de livros associadas usando o ISBN para unir à tabela Livros. Como resultado, a visualização em linha fornece o conjunto de resultados com colunas adicionais (o número de itens vendidos e a empresa que vendeu os livros):

```
SELECT b.isbn, b.title, b.price, sales.items_sold, sales.company_nm
FROM Book b
  JOIN (SELECT SUM(Items_Sold) Items_Sold, Company_Nm, ISBN
        FROM Book_Sales
        GROUP BY Company_Nm, ISBN) sales
  ON sales.isbn = b.isbn
```

## Exemplo

Selecionando campos específicos, está é a melhor opção para se trabalhar, pois quando utilizamos esse jeito de retornar os campos especificamos somente os que precisamos e a consulta ao banco de dados fica mais rápida, e o outro ponto forte de fazer a consulta deste modo é que você sabe quais são os campos que terá retorno.

```
SELECT campo1,campo2 
FROM table1
WHERE campo1 = "Laisa"
```

Selecionando todos os campos, somente aconselhavel utilizar se você for usar todas as colunas de uma tabela.

```
SELECT * FROM table1
```

Para fazer testes se uma clausula SQL está funcionando.

```
SELECT 1 FROM table1
```







# --A que se refere o termo "projeção" em uma consulta SQL (ou definição de exibição)--------

[A que se refere o termo "projeção" em uma consulta SQL (ou definição de exibição) (qastack.com.br)](https://qastack.com.br/dba/12619/what-does-the-term-projection-refer-to-in-an-sql-query-or-view-definition)



No documento da Oracle, *o Query Optimizer* , em [Exibir mesclagem](http://docs.oracle.com/cd/E11882_01/server.112/e16638/optimops.htm#i55044) , encontrei as seguintes informações

> A otimização de mesclagem de vistas se aplica a vistas que contêm apenas seleções, **projeções** e junções. Ou seja, as exibições mescláveis não contêm operadores de conjunto, funções agregadas, DISTINCT, GROUP BY, CONNECT BY e assim por diante. *(ênfase minha)*

No entanto, só posso adivinhar como o que essa projeção realmente se refere.



Na álgebra relacional, projeção significa coletar um subconjunto de colunas para uso em operações, ou seja, uma projeção é a lista de colunas selecionadas.

Em uma etapa do otimizador de consulta, a projeção se manifestará como uma área de buffer ou spool de alguma descrição que contém um subconjunto das colunas da tabela ou do operador subjacente, ou uma visualização lógica com base nas colunas usadas pelas operações subseqüentes.

Em uma exibição, uma projeção equivale à lista de colunas selecionadas na consulta subjacente à exibição.



***Projeção\*** refere-se ao subconjunto do conjunto de todas as colunas encontradas em uma tabela que você deseja retornar. Pode variar de 0 ** até o conjunto completo.

Existem dois "conjuntos" em uma tabela que correspondem às duas dimensões de uma tabela. Cada tabela possui um conjunto de ***colunas\*** e um conjunto de ***linhas\*** . Cada valor individual em uma tabela pode ser encontrado em uma *interseção* específica desses dois * conjuntos **. No entanto, seu valor não é encontrado "indo para" um endereço, como **T60** , da mesma maneira que você faria com o Excel.

**Não há ordem inerente às tabelas relacionais** . É importante lembrar. Em vez disso, para recuperar seu valor único, você selecionaria um subconjunto das colunas (uma neste caso) e um subconjunto das linhas (uma neste caso). Para selecionar um subconjunto de uma coluna dentre todas as disponíveis, você só precisa saber o nome e o nome da tabela. O nome da coluna será exclusivo em sua tabela.

Depois de escolher a coluna em que seu valor está, você precisará escolher a linha específica em que está. No entanto, as linhas não têm nomes como as colunas. A maneira como especificamos uma linha é. . . bem, nós não fazemos exatamente. . . Especificamos algo que sabemos sobre o valor que estamos procurando. Você precisa saber algo relacionado (literalmente) ao valor que está procurando. Se você puder especificar informações relacionadas suficientes, poderá reduzir o conjunto de linhas retornadas para o que você está procurando.

Pense nisso como se um estudante universitário tivesse perdido sua mochila. Digamos que um cara tenha perdido. Ele liga para achados e perdidos, e a mulher que atende diz: "Sim, temos algumas dúzias de mochilas. Você pode descrever?" Você diz "Bem, é azul?". Ao que ela responde: "Você está me perguntando ou me dizendo", e depois diz: "Eu tenho oito azuis, vou ter que fazer melhor que isso, e você não parecia muito certo disso". Você diz "Vamos ver, umm, sim! Tinha o meu livro de matemática 1010 nele". "Bom, agora você está com quatro anos." Então você se lembra de que deveria conhecer sua namorada, Lucy, em 15 minutos, e isso provocou outra lembrança - da época em que você estava entediado no Math 1010 e escreveu - em letras minúsculas reais na parte inferior da mochila: "Eu amo Lucy ".*Ricky* ".

**A projeção** pode ser comparada a dizer o *que* você perdeu - uma mochila. **A seleção** pode ser comparada à descrição de *seus atributos* : é azul, possui um livro de matemática 1010 e tem "I love Lucy" escrito na parte inferior.

Você faz a mesma coisa com o SQL. Primeiro, que tipo de informação você deseja ver. Segundo, critérios que descrevem qual deles você deseja ver. Estes são chamados de *predicados* ou *declarações de verdade* . Eles são verdadeiros para um ou mais membros do conjunto. Caso contrário, eles não retornam nenhum valor.

\* As implementações SQL de alguns fornecedores fornecem meios para quebrar essas regras, como Tabelas Aninhadas no Oracle. No entanto, as tabelas bidimensionais padrão ainda são a forma predominante.

** CJ Date escreveu um artigo muito interessante chamado "Uma Tabela Sem Colunas". Achei que valeu a pena ler, como faço com a maioria dos seus muitos artigos "Escritos". Eu recomendo!



[A que se refere o termo "projeção" em uma consulta SQL (ou definição de exibição) (qastack.com.br)](https://qastack.com.br/dba/12619/what-does-the-term-projection-refer-to-in-an-sql-query-or-view-definition)



# -------------------Joins (Junções SQL Server)---------

[Joins (SQL Server) - SQL Server | Microsoft Learn](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/joins?view=sql-server-ver16)



- Artigo
- 18/08/2022
- 21 minutos para o fim da leitura
- 8 colaboradores

**Aplica-se a:**![img](https://learn.microsoft.com/pt-br/sql/includes/media/yes-icon.svg?view=sql-server-ver16) SQL Server (todas as versões com suporte) ![img](https://learn.microsoft.com/pt-br/sql/includes/media/yes-icon.svg?view=sql-server-ver16) SQL do Azure Banco ![img](https://learn.microsoft.com/pt-br/sql/includes/media/yes-icon.svg?view=sql-server-ver16) de Dados Instância Gerenciada de SQL do Azure ![img](https://learn.microsoft.com/pt-br/sql/includes/media/yes-icon.svg?view=sql-server-ver16) Azure Synapse PDW (Analytics ![img](https://learn.microsoft.com/pt-br/sql/includes/media/yes-icon.svg?view=sql-server-ver16) Analytics Platform System)

SQL Server executa operações de classificação, interseção, união e diferença usando classificação de memória e a tecnologia de junção de hash. Usando esse tipo de plano de consulta, o SQL Server dá suporte ao particionamento de tabela vertical.

SQL Server implementa operações de junção lógica, conforme determinado pela sintaxe Transact-SQL:

- Junção interna
- Junção externa esquerda
- Junção externa direita
- Junção externa completa
- União cruzada

 Observação

Para obter mais informações sobre a sintaxe de junção, confira a [Cláusula FROM mais JOIN, APPLY, PIVOT (Transact-SQL)](https://learn.microsoft.com/pt-br/sql/t-sql/queries/from-transact-sql?view=sql-server-ver16).

SQL Server emprega quatro tipos de operações de junção física para realizar as operações de junção lógica:

- Junções de Loops Aninhados
- Junções de mesclagem
- Junções de hash
- Junções adaptáveis (a partir do SQL Server 2017 (14.x))

## Conceitos básicos de junção

Usando junções, é possível recuperar dados de duas ou mais tabelas com base em relações lógicas entre as tabelas. Junções indicam como SQL Server deveria usar dados de uma tabela para selecionar as linhas em outra tabela.

Uma condição de junção define o modo como duas tabelas são relacionadas em uma consulta por:

- Especificando a coluna de cada tabela a ser usada para a junção. Uma condição de junção típica especifica uma chave estrangeira de uma tabela e sua chave associada na outra tabela.
- Especificação de um operador lógico (por exemplo, = ou <>,) a ser usado na comparação de valores das colunas.

As junções são expressas logicamente usando a seguinte sintaxe Transact-SQL:

- INNER JOIN
- LEFT [ OUTER ] JOIN
- RIGHT [ OUTER ] JOIN
- FULL [ OUTER ] JOIN
- CROSS JOIN

As **junções internas** podem ser especificadas nas cláusulas `FROM` ou `WHERE`. As **junções externas** e as **uniões cruzadas** podem ser especificadas apenas na cláusula `FROM`. As condições de junção combinam-se com as condições de pesquisa `WHERE` e `HAVING` para controlar as linhas selecionadas das tabelas base referenciadas na cláusula `FROM`.

Especificar as condições de junção na cláusula `FROM` ajuda a separá-las de qualquer outro critério de pesquisa que possa ser especificado em uma cláusula `WHERE` e é o método recomendado para a especificação de junções. Uma sintaxe de junção de cláusula ISO `FROM` simplificada é:

SQLCopiar

```sql
FROM first_table < join_type > second_table [ ON ( join_condition ) ]
```

*join_type* especifica que tipo de junção é executado: uma junção interna, externa ou cruzada. *join_condition* define o predicado a ser avaliado para cada par de linhas unidas. O seguinte exemplo refere-se a uma especificação de junção da cláusula `FROM`:

SQLCopiar

```sql
FROM Purchasing.ProductVendor INNER JOIN Purchasing.Vendor
     ON ( ProductVendor.BusinessEntityID = Vendor.BusinessEntityID )
```

O seguinte exemplo refere-se a uma instrução `SELECT` simples que usa esta junção:

SQLCopiar

```sql
SELECT ProductID, Purchasing.Vendor.BusinessEntityID, Name
FROM Purchasing.ProductVendor INNER JOIN Purchasing.Vendor
    ON (Purchasing.ProductVendor.BusinessEntityID = Purchasing.Vendor.BusinessEntityID)
WHERE StandardPrice > $10
  AND Name LIKE N'F%'
GO
```

A instrução `SELECT` retorna as informações de produto e de fornecedor para qualquer combinação de partes fornecidas por uma empresa cujo nome começa com a letra F e o preço do produto é maior que US$ 10.

Quando várias tabelas são referenciadas em uma única consulta, todas as referências de coluna devem ser inequívocas. No exemplo anterior, as tabelas `ProductVendor` e `Vendor` têm uma coluna chamada `BusinessEntityID`. Qualquer nome de coluna que seja duplicado entre duas ou mais tabelas referenciadas na consulta deve ser qualificado com o nome da tabela. Todas as referências às colunas `Vendor` no exemplo estão qualificadas.

Quando um nome de coluna não está duplicado em duas ou mais tabelas usadas na consulta, a referências a ele não precisam ser qualificadas com o nome da tabela. Isso é mostrado no exemplo anterior. Às vezes, uma cláusula `SELECT` é difícil de ser compreendida, pois não há nada que indique a tabela que forneceu cada coluna. A legibilidade da consulta será aprimorada se todas as colunas estiverem qualificadas com seus nomes de tabela. A legibilidade é aperfeiçoada se aliases de tabela são usados, principalmente quando os nomes de tabelas precisam ser qualificados com nomes de proprietários e de banco de dados. O exemplo seguinte é o mesmo, exceto que aliases de tabela foram atribuídos e as colunas foram qualificadas com aliases de tabela para aperfeiçoar a legibilidade:

SQLCopiar

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv 
INNER JOIN Purchasing.Vendor AS v
    ON (pv.BusinessEntityID = v.BusinessEntityID)
WHERE StandardPrice > $10
    AND Name LIKE N'F%';
```

Os exemplos anteriores especificaram as condições de junção na cláusula `FROM`, que é o método preferencial. A seguinte consulta contém a mesma condição de junção especificada na cláusula `WHERE`:

SQLCopiar

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv, Purchasing.Vendor AS v
WHERE pv.BusinessEntityID=v.BusinessEntityID
    AND StandardPrice > $10
    AND Name LIKE N'F%';
```

A lista `SELECT` para uma junção pode referenciar todas as colunas nas tabelas unidas ou qualquer subconjunto das colunas. A lista `SELECT` não precisa conter colunas de todas as tabelas na junção. Por exemplo, em uma junção de três tabelas, somente uma tabela pode ser usada para ligar uma das tabelas à terceira e, nenhuma das colunas da tabela do meio, precisa ser referenciada na lista de seleção. Isso também é chamado de **antisemijunção**.

Embora as condições de junção tenham comparações de igualdade (=), outros operadores relacionais ou de comparação podem ser especificados, como também outros predicados. Para obter mais informações, consulte [Operadores de Comparação (Transact-SQL)](https://learn.microsoft.com/pt-br/sql/t-sql/language-elements/comparison-operators-transact-sql?view=sql-server-ver16) e [WHERE (Transact-SQL).](https://learn.microsoft.com/pt-br/sql/t-sql/queries/where-transact-sql?view=sql-server-ver16)

Quando o SQL Server processa as junções, o otimizador de consulta escolhe o método mais eficaz (entre várias possibilidades) de processamento da junção. Isso inclui escolher o tipo mais eficiente de junção física, a ordem na qual as tabelas serão unidas e até mesmo usar tipos de operações de junção lógica que não podem ser expressas diretamente com sintaxe Transact-SQL, como **junções semi** e **anti-junções**. A execução física de várias junções pode usar muitas otimizações diferentes e portanto não pode ser prevista de maneira confiável. Para obter mais informações sobre as semijunções e as antisemijunções, confira [Referência de operadores lógicos e físicos do plano de execução](https://learn.microsoft.com/pt-br/sql/relational-databases/showplan-logical-and-physical-operators-reference?view=sql-server-ver16).

Colunas usadas em uma condição de junção não precisam ter o mesmo nome ou ter o mesmo tipo de dados. Entretanto, se os tipos de dados não forem idênticos, eles precisarão ser compatíveis ou ser tipos que o SQL Server possa converter implicitamente. Se o tipo de dados não puder ser convertido implicitamente, a condição de junção deverá converter explicitamente o tipo de dados usando a função `CAST`. Para obter mais informações sobre conversões implícitas e explícitas, consulte [a Conversão de Tipo de Dados (Mecanismo de Banco de Dados).](https://learn.microsoft.com/pt-br/sql/t-sql/data-types/data-type-conversion-database-engine?view=sql-server-ver16)

A maioria das consultas que usam uma junção pode ser regravada usando uma subconsulta (uma consulta aninhada dentro de outra consulta) e a maioria das subconsultas pode ser regravada como junções. Para obter mais informações sobre subconsultas, veja [Subconsultas](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/subqueries?view=sql-server-ver16).

 Observação

Tabelas não podem ser unidas diretamente em colunas ntext, text ou image. No entanto, as tabelas podem ser unidas indiretamente em colunas ntext, text ou image usando `SUBSTRING`.
Por exemplo, `SELECT * FROM t1 JOIN t2 ON SUBSTRING(t1.textcolumn, 1, 20) = SUBSTRING(t2.textcolumn, 1, 20)` executa uma junção interna de duas tabelas nos primeiros 20 caracteres de cada coluna de texto em tabelas t1 e t2.
Além disso, outra possibilidade de comparação das colunas ntext ou text de duas tabelas é comparar o comprimento das colunas com a cláusula `WHERE`, por exemplo: `WHERE DATALENGTH(p1.pr_info) = DATALENGTH(p2.pr_info)`

## Compreendendo junções de Loops Aninhados

Se uma entrada de junção for pequena (menos que 10 linhas) e a outra entrada de junção for bastante grande e indexada a suas colunas de junção, uma junção de loops aninhados de índice será a operação de junção mais rápida porque eles requerem o mínimo de E/S e comparações.

A junção de loops aninhados, também denominada *iteração aninhada*, usa uma entrada de junção como a tabela de entrada externa (mostrada como a entrada superior no plano de execução) e outra como a tabela de entrada interna (na parte inferior). O loop externo consome a tabela de entrada externa linha por linha. O loop interno, executado para cada linha externa, pesquisa linhas correspondentes na tabela de entrada interna.

No caso mais simples, a pesquisa examina toda uma tabela ou índice; isto é chamado de *junção de loops aninhados naive*. Se a pesquisa explorar um índice, será chamado de *junção de loops aninhados de índice*. Se o índice for criado como parte do plano de consulta (e destruído na conclusão da consulta), será chamado de *junção de loops aninhados de índice temporário*. Todas essas variantes são consideradas pelo Otimizador de Consulta.

Uma junção de loops aninhados será particularmente eficaz se a entrada externa for pequena e a entrada interna for pré-indexada e grande. Em muitas transações pequenas, como as que afetam apenas um pequeno conjunto de linhas, as junções de loops aninhados de índice são superiores às junções mescladas e junções de hash. Em consultas grandes, contudo, as junções de loops aninhados não são frequentemente a melhor escolha.

Quando o atributo OPTIMIZED de um Operador de junção de loops aninhados é definido como **True**, isso significa que um Loop aninhado otimizado (ou Classificação em lote) é usado para minimizar a E/S quando a tabela de lado interno é grande, independentemente de ser paralelizada ou não. A presença dessa otimização em um determinado plano pode não ser muito óbvia durante a análise de um plano de execução, uma vez que a própria classificação é uma operação oculta. Mas ao examinar o XML do plano para o atributo OPTIMIZED, isso indica que a Junção de loops aninhados pode tentar reordenar as linhas de entrada para melhorar o desempenho de E/S.

## Junções de mesclagem

Se as duas entradas de junção não são pequenas, mas são classificadas na coluna de junção (por exemplo, se foram obtidas de exames em índices classificados), uma junção de mesclagem será a operação de junção mais rápida. Se ambas as entradas de junção forem grandes e as duas entradas forem de tamanhos semelhantes, uma junção de mesclagem com classificação prévia e uma junção de hash oferecerão desempenho semelhante. Porém, operações de junção de hash são muitas vezes mais rápidas quando os dois tamanhos da entrada diferem significativamente um do outro.

A junção de mescla exige que as duas entradas sejam classificadas nas colunas de mesclagem, que são definidas pelas cláusulas de igualdade (ON) do predicado de junção. O otimizador de consulta geralmente examina um índice, caso exista um no conjunto de colunas, ou coloca um operador de classificação abaixo da junção de mescla. Em casos raros, podem existir diversas cláusulas de igualdade, mas as colunas de mesclagem são tiradas somente de algumas das cláusulas de igualdade disponíveis.

Uma vez que cada entrada é classificada, o operador **Junção de Mesclagem** adquire uma linha de cada entrada e as compara. Por exemplo, em operações de junção internas, serão retornadas as linhas que forem iguais. Se elas não forem iguais, será descartada a linha com o menor valor e será obtida outra linha daquela entrada. Esse processo repete-se até que todas as linhas tenham sido processadas.

A operação mesclar junção pode ser uma operação habitual ou uma operação muitos para muitos. Uma junção de mescla muitos para muitos usa uma tabela temporária para armazenar linhas. Se houver valores duplicados de cada entrada, uma das entradas terá que retroceder ao início das linhas duplicadas à medida que cada linha duplicada da outra entrada for processada.

Se houver um predicado residual presente, todas as linhas que satisfaçam ao predicado de mesclagem avaliarão o predicado residual e serão retornadas somente as linhas que o satisfaçam.

A junção de mescla é muito rápida, mas pode ser uma escolha cara se forem necessárias operações de classificação. Porém, se o volume de dados for grande e os dados desejados puderem ser obtidos pré-classificados de índices da árvore B existentes, frequentemente a junção de mescla será o algoritmo de junção mais rápido disponível.

## Junções de hash

Junções de hash podem processar com eficácia grande volume de entradas não classificadas e não indexadas. Elas são úteis para resultados intermediários em consultas complexas por que:

- Os resultados intermediários não são indexados (a menos que salvos explicitamente no disco e depois indexados) e muitas vezes não são classificados adequadamente para a próxima operação no plano de consulta.
- Otimizadores de consulta só calculam tamanhos de resultado intermediário. Como as estimativas podem ser muito imprecisas para consultas complexas, os algoritmos para processar resultados intermediários não só devem ser eficientes, mas também devem ser degradados de forma suave se um resultado intermediário for muito maior do que o previsto.

A junção de hash permite reduções no uso da desnormalização. A desnormalização é usada geralmente para obter melhor desempenho e reduzir as operações de junção, apesar dos perigos de redundância, como atualizações inconsistentes. As junções de hash reduzem a necessidade a desnormalização. As junções de hash permitem particionamento vertical (representando grupos de colunas de uma única tabela em arquivos separados ou índices) para se tornar uma opção viável no design do banco de dados físico.

A junção hash tem duas entradas: a entrada **build** e entrada **probe**. O otimizador de consulta nomeia estes papéis de forma que a menor das duas entradas é a entrada de construção.

Junções de hash são usadas para muitos tipos de operações para definir correspondente: junção interna; esquerda, direita e junção externa completa; semijunção esquerda e direita ; interseção; união; e diferença. Além disso, uma variante da junção de hash pode fazer remoção e agrupamento duplicados, como `SUM(salary) GROUP BY department`. Essas modificações usam só uma entrada para os papéis de construção e investigação.

As seções seguintes descrevem tipos diferentes de junções de hash: junção de hash em-memória, junção de hash de cortesia e junção de hash recursiva.

### Junção Hash em-Memória

A junção de hash primeiro verifica ou calcula a entrada de construção inteira e então constrói uma tabela de hash em memória. Cada linha é inserida em um compartimento de memória hash que depende do valor de hash computado para a chave hash. Se a entrada de construção inteira for menor que a memória disponível, todas as linhas poderão ser inseridas na tabela de hash. Essa fase de construção é seguida pela fase de investigação. A entrada de investigação inteira é verificada ou calculada uma linha de cada vez e o valor da chave de hash é calculado para cada linha de investigação, o compartimento de hash correspondente é verificado e as correspondências são produzidas.

### Junção hash de cortesia

Se a entrada de construção não couber na memória, uma junção de hash continua em vários passos. Isso é conhecido como uma junção hash de cortesia. Cada passo tem uma fase de construção e fase de investigação. Inicialmente, a construção inteira e entradas de investigação são consumidas e particionadas (usando uma função de hash na chave hash) em arquivos múltiplos. Usando a função de hash nas chaves de hash garante que quaisquer dois registros de junção devem estar no mesmo par de arquivos. Portanto, a tarefa de unir duas entradas grandes foi reduzida a instâncias múltiplas, mas menores, das mesmas tarefas. A junção de hash é se aplicada então a cada par de arquivos particionados.

### Junção hash recursiva

Se a entrada de construção for tão grande que entradas para uma fusão externa padrão requereriam níveis de fusão múltiplos, serão requeridos passos de particionamentos múltiplos e níveis de particionamentos múltiplos. Se somente algumas das partições forem grandes, passos de particionamentos adicionais serão usados apenas para essas partições específicas. Para fazer todos os passos de particionamento tão rápido quanto possível, operações grandes, assíncronas de I/O são usadas de forma que um único thread pode manter unidades de disco múltiplas ocupadas.

 Observação

Se a entrada de construção só for ligeiramente maior que a memória disponível, elementos de junção de hash em-memória e junção de hash de cortesia serão combinados em um único passo, produzindo uma junção de hash híbrida.

Nem sempre é possível durante otimização determinar qual junção de hash é usada. Portanto, o SQL Server começa usando uma junção hash em memória e gradualmente passa para a junção hash de cortesia e para a junção hash recursiva, dependendo do tamanho da entrada de compilação.

Se o Otimizador de Consulta prever incorretamente qual das duas entradas será menor e, portanto, deveria ter sido a entrada de compilação, os papéis de compilação e investigação serão invertidos dinamicamente. A junção de hash garante que usa o menor arquivo com excedente como entrada de construção. Essa técnica é chamada de reversão de papel. A reversão de papel acontece dentro da junção de hash depois de pelo menos um derramamento para o disco.

 Observação

A reversão de papel acontece independente de qualquer dica de consulta ou estrutura. A reversão de papel não aparecerá em seu plano de consulta; quando acontecer, é transparente ao usuário.

### Abandono de hash

O termo de esgotamento de hash às vezes é usado para descrever junções hash de cortesia ou junções hash recursivas.

 Observação

Junções de hash recursivas ou abandonos de hash causam desempenho reduzido em seu servidor. Se você vir muitos eventos de Aviso de Hash em um rastreamento, atualize as estatísticas nas colunas que estão sendo unidas.

Para obter mais informações sobre esgotamento de hash, veja [Classe de evento de aviso de Hash](https://learn.microsoft.com/pt-br/sql/relational-databases/event-classes/hash-warning-event-class?view=sql-server-ver16).

## Junções adaptáveis

As Junções adaptáveis de [Modo de lote](https://learn.microsoft.com/pt-br/sql/relational-databases/query-processing-architecture-guide?view=sql-server-ver16#batch-mode-execution) permitem a escolha de um método de [Junção Hash](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/joins?view=sql-server-ver16#hash) ou de [Junção de loops aninhados](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/joins?view=sql-server-ver16#nested_loops) a ser adiado até **depois** que a primeira entrada for verificada. O operador de Junção Adaptável define um limite que é usado para decidir quando mudar para um plano de Loops aninhados. Portanto, um plano de consulta pode alternar dinamicamente para uma estratégia de junção melhor durante a execução sem precisar ser recompilado.

 Dica

As cargas de trabalho com oscilações frequentes entre verificações de entradas de junção pequenas e grandes terão mais benefícios com esse recurso.

A decisão de runtime se baseia nas seguintes etapas:

- Se a contagem de linhas da entrada de junção de build for pequena o suficiente para que uma Junção de loops aninhados seja mais ideal do que uma Junção Hash, o plano será alternado para um algoritmo de Loops Aninhados.
- Se a entrada de junção de build exceder um limite de contagem de linhas específico, o plano não mudará e continuará com uma Junção hash.

A consulta a seguir é usada para ilustrar um exemplo de Junção Adaptável:

SQLCopiar

```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

A consulta retorna 336 linhas. Habilitar as [Estatísticas de consultas dinâmicas](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/live-query-statistics?view=sql-server-ver16) exibe o plano a seguir:

![Resultados da consulta: 336 linhas](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/media/4_aqpstats336rows.png?view=sql-server-ver16)

No plano, observe o seguinte:

1. Uma verificação de índice columnstore usada para fornecer linhas para a fase de build da Junção hash.
2. O novo operador de Junção Adaptável. Este operador define um limite que é usado para decidir quando mudar para um plano de Loops Aninhados. Para esse exemplo, o limite é de 78 linhas. Tudo que for >= 78 linhas usará uma Junção hash. Quando estiver abaixo do limite, uma junção de Loops aninhados será usada.
3. Como a consulta retorna 336 linhas, excede o limite. Portanto, a segunda branch representa a fase de investigação de uma operação de Junção de hash padrão. Observe que as Estatísticas de consultas dinâmicas mostram as linhas que passam pelos operadores – nesse caso, "672 de 672".
4. E a última branch é uma Busca de índice clusterizado a ser usada pela junção de Loops aninhados que não teve o limite excedido. Observe que podemos ver "0 de 336" linhas exibidas (o branch não é usado).

Agora compare o plano com a mesma consulta, mas quando o valor de *Quantidade* só tem uma linha na tabela:

SQLCopiar

```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```

A consulta retorna uma linha. Habilitar as Estatísticas de consultas dinâmicas exibe o plano a seguir:

![Resultado da consulta: uma linha](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/media/5_aqpstatsonerow.png?view=sql-server-ver16)

No plano, observe o seguinte:

- Com uma linha retornada, a Busca de índice clusterizado agora tem linhas que passam por ela.
- E, como a fase de build da Junção Hash não continuou, não há linhas passando pela segunda branch.

### Comentários de junção adaptável

As junções adaptáveis apresentam um requisito de memória maior do que um plano equivalente de Junção de Loops Aninhados indexados. A memória adicional é solicitada como se os Loops Aninhados fossem uma Junção hash. Também há sobrecarga para a fase de build como uma operação de “parar e ir” em vez de uma junção equivalente de fluxo de Loops Aninhados. Com esse custo adicional vem a flexibilidade para cenários em que as contagens de linhas podem flutuar na entrada de build.

As Junções adaptáveis de modo de lote funcionam para a execução inicial de uma instrução. Depois que são compiladas, as próximas execuções permanecem adaptáveis com base no limite de Junção Adaptável compilada e nas linhas de runtime que passam pela fase de build da entrada externa.

Se uma Junção Adaptável alterna para uma operação de Loops Aninhados, ela usa as linhas já lidas pelo build de Junção Hash. O operador **não** lê novamente as linhas de referência externa novamente.

### Controlando a atividade da Junção adaptável

O operador de Junção Adaptável tem os seguintes atributos de operador de plano:

| Atributo de plano     | Descrição                                                    |
| :-------------------- | :----------------------------------------------------------- |
| AdaptiveThresholdRows | Mostra o uso de limite para alternar de uma junção hash para uma junção de loops aninhados. |
| EstimatedJoinType     | Qual é o provável tipo de junção.                            |
| ActualJoinType        | Em um plano real, mostra qual algoritmo de junção foi finalmente escolhido com base no limite. |

O plano estimado mostra a forma do plano de Junção Adaptável, juntamente com um limite de Junção Adaptável definido e o tipo de junção estimado.

 Dica

O Repositório de Consultas captura e é capaz de forçar um plano de Junção Adaptável de modo de lote.

### Instruções qualificadas para junção adaptável

Algumas condições tornam uma junção lógica qualificada para uma Junção Adaptável de modo de lote:

- O nível de compatibilidade do banco de dados é 140 ou superior.
- A consulta é uma instrução `SELECT` (as instruções de modificação de dados não são qualificadas no momento).
- A junção é qualificada para ser executada por uma Junção de loops aninhados indexada ou um algoritmo físico de Junção hash.
- A Junção hash usa o modo de Lote, habilitado pela presença de um Índice columnstore na consulta geral, uma tabela indexada por Columnstore referenciada diretamente pela junção ou pelo uso do [Modo de lote em rowstore](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/intelligent-query-processing-details?view=sql-server-ver16#batch-mode-on-rowstore).
- As soluções alternativas geradas da Junção de loops aninhados e da Junção hash devem ter o mesmo primeiro filho (referência externa).

### Linhas de limite adaptável

O gráfico a seguir mostra uma interseção de exemplo entre o custo de uma Junção hash e o custo de uma alternativa de Junção de loops aninhados. Neste ponto de interseção, o limite é determinado e, por sua vez, ele determina o algoritmo real usado para a operação de junção.

![Limite de junção](https://learn.microsoft.com/pt-br/sql/relational-databases/performance/media/6_aqpjointhreshold.png?view=sql-server-ver16)

### Desabilitar Junções adaptáveis sem alterar o nível de compatibilidade

Junções adaptáveis podem ser desabilitadas no escopo do banco de dados ou da instrução, mantendo o nível de compatibilidade do banco de dados como 140 e superior.
Para desabilitar as Junções adaptáveis para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

SQLCopiar

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

Quando habilitada, essa configuração aparecerá como habilitada em [sys.database_scoped_configurations](https://learn.microsoft.com/pt-br/sql/relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql?view=sql-server-ver16). Para reabilitar as junções adaptáveis para todas as execuções de consulta originadas do banco de dados, execute o seguinte dentro do contexto do banco de dados aplicável:

SQLCopiar

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ADAPTIVE_JOINS = ON;
```

As Junções adaptáveis também podem ser desabilitadas para uma consulta específica designando `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` como uma [dica de consulta USE HINT](https://learn.microsoft.com/pt-br/sql/t-sql/queries/hints-transact-sql-query?view=sql-server-ver16#use_hint). Por exemplo:

SQLCopiar

```sql
SELECT s.CustomerID,
       s.CustomerName,
       sc.CustomerCategoryName
FROM Sales.Customers AS s
LEFT OUTER JOIN Sales.CustomerCategories AS sc
       ON s.CustomerCategoryID = sc.CustomerCategoryID
OPTION (USE HINT('DISABLE_BATCH_MODE_ADAPTIVE_JOINS')); 
```

 Observação

Uma dica de consulta USE HINT tem precedência sobre uma configuração de escopo do banco de dados ou uma configuração de sinalizador de rastreamento.

## Valores nulos e junções

Quando há valores nulos nas colunas de tabelas sendo associadas, eles não correspondem uns aos outros. A presença de valores nulos em uma coluna de uma das tabelas que estão sendo associadas pode ser retornada apenas usando uma junção externa (a menos que a cláusula `WHERE` exclua valores nulos).

Veja duas tabelas que contêm NULL na coluna que participará da junção:

Copiar

```
table1                          table2
a           b                   c            d
-------     ------              -------      ------
      1        one                 NULL         two
   NULL      three                    4        four
      4      join4
```

Uma junção que compara os valores na coluna a com os valores da coluna c não obtém uma correspondência nas colunas que têm valores de NULL:

SQLCopiar

```sql
SELECT *
FROM table1 t1 JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```

Somente uma linha com 4 na coluna a e c é retornada:

Copiar

```
a           b      c           d      
----------- ------ ----------- ------ 
4           join4  4           four   

(1 row(s) affected)
```

Os valores nulos retornados de uma tabela base também são difíceis de distinguir dos valores nulos retornados de uma junção externa. Por exemplo, a seguinte instrução `SELECT` faz uma junção externa esquerda nestas duas tabelas:

SQLCopiar

```sql
SELECT *
FROM table1 t1 LEFT OUTER JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```

Este é o conjunto de resultados.

Copiar

```
a           b      c           d      
----------- ------ ----------- ------ 
NULL        three  NULL        NULL 
1           one    NULL        NULL 
4           join4  4           four   

(3 row(s) affected)
```

Os resultados não facilitam a distinção de um NULL nos dados de um NULL que representa uma falha na junção. Quando os valores nulos estão presentes nos dados que estão sendo associados, geralmente é preferível omiti-los nos resultados usando uma junção comum.

## 
