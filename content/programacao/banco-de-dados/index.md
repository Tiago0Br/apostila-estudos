# Banco de dados SQL

##  Lista de Conteúdos
**SELECT**<br />
[NORMALIZAÇÃO](./normalizacao.md)<br />
[VIEWS, TRIGGERS E PROCEDURES](./views_procedures_triggers.md)

## Lista de Comandos

<details>
<summary>
SELECT
</summary>

&emsp;&emsp;[FROM](#from)</br>
&emsp;&emsp;[WHERE](#where)</br>
&emsp;&emsp;[AND](#and)</br>
&emsp;&emsp;[AS](#as)</br>
&emsp;&emsp;[BETWEEN](#between)</br>
&emsp;&emsp;[IN](#in)</br>
&emsp;&emsp;[COUNT](#count)</br>
&emsp;&emsp;[SUM](#sum)</br>
&emsp;&emsp;[AVG](#avg)</br>
&emsp;&emsp;[SUBSTRING](#substring)</br>
&emsp;&emsp;[REPLACE](#replace)</br>
&emsp;&emsp;[CONCAT](#concat)</br>
&emsp;&emsp;[UPPER](#upper)</br>
&emsp;&emsp;[LOWER](#lower)</br>
&emsp;&emsp;[LEFT](#left)</br>
&emsp;&emsp;[RIGHT](#right)</br>
&emsp;&emsp;[LENGTH](#length)</br>
&emsp;&emsp;[LIMIT](#limit)</br>
&emsp;&emsp;[DISTINCT](#distinct)</br>
&emsp;&emsp;[GROUP BY](#group-by)</br>
&emsp;&emsp;[HAVING](#having)</br>

</details>

---

##  Comandos

##  SELECT

O comando **SELECT** permite realizar buscas em uma ou várias tabelas.

####  FROM

Tabela onde será realizada a busca</br>

**Exemplos**:

```sql
SELECT * -- * seleciona todas as colunas
FROM autores; -- "autores" é a tabela usada na consulta
```

```sql
SELECT id_autor, nome -- Especifíca as colunas buscadas
FROM autores;
```

####  WHERE

Condição da busca que será feita, serão retornados todos os registros que satisfazerem essa condição.</br>

**Exemplos**:

```sql
SELECT *
FROM autores
WHERE id_nacionalidade = 1;
```

```sql
SELECT *
FROM autores
WHERE id_autor >= 3; -- Retorna autores com ID maior ou igual a 3
```

```sql
SELECT *
FROM autores
WHERE id_autor <> 1; -- Retorna autores com ID diferente de 1
```

####  AND

Possibilita adicionar várias condições de uma vez.</br>

**Exemplo**:

```sql
SELECT *
FROM autores
WHERE id_autor > 1
AND id_nacionalidade <> 3
AND id_autor < 5;
```

####  AS

Dá um apelido a uma tabela ou a um campo da tabela.</br>

**Exemplo**:

```sql
SELECT a.nome AS autor -- Apelida a coluna "nome" de "autor"
FROM autores AS a; -- Apelida a tabela "autores" de "a"
```

O **AS** pode ser omitido, basta colocar o apelido logo depois do nome da coluna ou tabela, irá funcionar da mesma forma.

```sql
SELECT a.nome autor -- Apelida a coluna "nome" de "autor"
FROM autores a; -- Apelida a tabela "autores" de "a"
```

Caso o apelido tenha espaços ou caracteres especiais, deverá ser colocado entre aspas.

```sql
SELECT a.nome 'Autor ou autora' -- Apelida a coluna "nome" de "Autor ou autora"
FROM autores a;
```

####  BETWEEN

Possibilita fazer uma verificação se o valor de um campo está entre um intervalo de valores.</br>

**Exemplo**:

```sql
SELECT *
FROM autores
WHERE id_autor BETWEEN 2 AND 5; -- Retorna autores com IDs entre 2 e 5
```

####  IN

Possibilita fazer uma verificação se determinado campo possui um valor dentro de um intervalo de valores pré-definido.</br>

**Exemplo**:

```sql
SELECT *
FROM autores
WHERE id_autor IN(1, 3, 5); -- Retorna autores que possuem um ID com 1, 3 ou 5
```

####  COUNT

Retorna o número referente a quantidade de registros obtidos nessa pesquisa.

```sql
SELECT COUNT(*) -- Exibe a quantidade de autores da tabela
FROM autores;
```

####  SUM

Retorna a soma dos valores de determinada coluna.</br>

**Exemplo:**

```sql
SELECT SUM(a.id_autor) -- Soma os IDs de todos os autores
FROM autores a;
```

####  AVG

Retorna a média dos valores de determinada coluna.</br>

**Exemplo:**

```sql
SELECT AVG(a.id_autor) -- Tira a média dos IDs de todos os autores
FROM autores a;
```

####  SUBSTRING

"Recorta" o conteúdo de uma string com base no intervalo de valores passados</br>

**Exemplo**:

```sql
SELECT SUBSTRING(nome, 2, 8) -- Recorta o nome do autor da posição 2 até a 8
FROM autores;
```

####  REPLACE

Função para substituir um conteúdo da string por outro

```sql
SELECT CONCAT(nome, ' ', sobrenome) -- Concatena o nome e o sobrenome do autor
FROM autores;
```

####  CONCAT

Função para concatenar strings.</br>

**Exemplo**:

```sql
SELECT CONCAT(nome, ' ', sobrenome) -- Concatena o nome e o sobrenome do autor
FROM autores;
```

####  UPPER

Função para deixar as letras em caixa alta</br>

**Exemplo**:

```sql
SELECT UPPER(nome) -- Exibe o nome em caixa alta
FROM autores;
```

####  LOWER

Função para deixar as letras em caixa baixa</br>

**Exemplo**:

```sql
SELECT LOWER(nome) -- Exibe o nome em caixa baixa
FROM autores;
```

####  LEFT

Função para trazer o conteúdo à esquerda da string de uma posição informada.</br>

**Exemplo:**

```sql
SELECT LEFT(nome, 5) -- Exibe os primeiros 5 caracteres da string
FROM autores;
```

####  RIGHT

Função para trazer o conteúdo à direita da string de uma posição informada.</br>

**Exemplo:**

```sql
SELECT RIGHT(nome, 5) -- Exibe os últimos 5 caracteres da string
FROM autores;
```

####  LENGTH

Função para contar a quantidade de caracteres de uma string.</br>

**Exemplo:**

```sql
SELECT LENGTH(nome) AS 'Tamanho do nome' -- Exibe o total de caracteres do nome
FROM autores;
```

####  LIMIT

Limita a quantidade de registros retornados em uma pesquisa</br>

**Exemplo:**

```sql
SELECT *
FROM autores
LIMIT 5; -- Serão exibidos no máximo 5 autores
```

####  DISTINCT

Traz apenas resultados distintos, por exemplo: se houver 3 cadastros com o mesmo nome, irá trazer apenas 1 deles.</br>

**Exemplo:**

```sql

SELECT DISTINCT nome
FROM autores;
-- Caso tenha autores com o mesmo nome, só irá retornar um deles
```

####  GROUP BY

Agrupa elementos por determinado campo.</br>

**Exemplo:**

```sql
SELECT id_nacionalidade, COUNT(*) AS 'Quantidade de autores'
FROM autores
GROUP BY id_nacionalidade; -- Agrupa os autores pela nacionalidade
```

####  HAVING

Adiciona uma condição para o agrupamento, portando é utilizado após o GROUP BY.</br>

**Exemplo**:

```sql
SELECT id_nacionalidade, COUNT(*) AS 'Quantidade de autores'
FROM autores
GROUP BY id_nacionalidade
HAVING COUNT(*) > 1;
-- Agrupa por nacionalidade e retorna apenas se tiver mais de um autor por nacionalidade
```