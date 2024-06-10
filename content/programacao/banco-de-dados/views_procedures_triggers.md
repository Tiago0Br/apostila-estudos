Lista de comandos SQL aprendidos na disciplina de Banco de dados.

##  Lista de Conteúdos
[SELECT](index.md)
[NORMALIZAÇÃO](./normalizacao.md)
**VIEWS, TRIGGERS E PROCEDURES**

## Lista de Comandos

## FUNCTIONS

É possível criar funções que retornam valores

#### CREATE FUNCTION

Comando para criação de funções, estas podem ou não receber parâmetros e retornam algum conteúdo.

**Exemplos:**
```sql
CREATE FUNCTION hello_world() -- Criação de função sem parâmetros
RETURNS VARCHAR(20)
	RETURN "HELLO WORLD!";
```

```sql
CREATE FUNCTION FUNC_SOMA(PI_NRO1 INT, PI_NRO2 INT) -- Nome da funções e parâmetros que ela recebe
RETURNS INT -- Tipo de dados que ela retorna
	RETURN PI_NRO1 + PI_NRO2; -- Valor que ela retorna
    
SELECT FUNC_SOMA(20, 5) AS "Resultado"; -- Execução da função
```

Quando a função possui variáveis, é necessário utilizar delimitadores antes do início e após o fim da função
```sql
DELIMITER //
CREATE OR REPLACE FUNCTION FNC_SOMA_ID_AUTOR() RETURNS INT
BEGIN
	DECLARE soma INT;
	SELECT SUM(a.id_autor) INTO soma FROM autores a;
    RETURN soma;
END //
DELIMITER ;
```

## Views

Uma View funciona como uma tabela, é possível criar Views que trazem dados de colunas específicas, são bem úteis para consultas que são executadas repetidas vezes, dessa forma, criando uma view para uma consulta complexa, basta executar a view para obter o retorno esperado.<br/>
**Exemplo:**

```sql
CREATE OR REPLACE VIEW vw_livros AS -- Cria a view se ela não existir, caso contrário substitui
SELECT l.id_livro, l.titulo, l.isbn, l.ano, c.descricao AS 'categoria', e.nome AS 'editora'
FROM livros l
JOIN categorias c
USING(id_categoria)
JOIN editoras e
USING(id_editora)
ORDER BY l.titulo;
```

Para se executar essa view, basta chamar ela utilizando um SELECT, como numa tabela comum

```sql
SELECT * FROM vw_livros; -- Executa a view, retornando todos os seus dados
```

## Triggers

São funções que são acionadas quando determinados eventos ocorrem.<br/>
**Exemplos:**

```sql
DELIMITER $$
	CREATE OR REPLACE TRIGGER trg_ins_autor
    BEFORE INSERT -- Essa trigger é executada antes de qualquer inseração na tabela "autores"
    ON autores
    FOR EACH ROW -- Itera sobre cada registro da tabela
    BEGIN
        IF NEW.nome IS NULL THEN -- "NEW" faz referência ao novo registro que será inserido
        	SIGNAL SQLSTATE '45000'
            SET MESSAGE_TEXT = 'Digite um nome para o autor!'; -- Exibe um erro caso não seja inserido o nome do autor
        END IF;
   END$$
DELIMITER ;
```

## Procedures

São funções que realizam ações dentro do banco de dados, como inserção de dados, alteração de dados, consultas, entre outras ações. Pode ou não receber parâmetros.<br/>
**Exemplos:**

```sql
DELIMITER $$
CREATE PROCEDURE PRC_INCLUIR_CATEGORIA(
	IN pi_descricao_categoria VARCHAR(100) -- o "IN" indica que é um parâmetro de "entrada"
)
BEGIN
	INSERT INTO categorias(descricao)
    VALUES (pi_descricao_categoria); -- Utiliza o parâmetro recebido na chamada da função
END $$
DELIMITER ;
```

Para executar a procedure basta utilizar o comando "CALL" passando o nome da procedure e os parâmetros dentro de parênteses.

```sql
CALL PRC_INCLUIR_CATEGORIA("Suspense"); -- Chama a função passando o parâmetro entre parênteses
```

```sql
DELIMITER $$
CREATE PROCEDURE IF NOT EXISTS PRC_INCLUIR_AUTOR(IN pi_nome VARCHAR(100), IN pi_nacionalidade INT)
BEGIN
	INSERT INTO autores(nome, id_nacionalidade)
    VALUES (pi_nome, pi_nacionalidade);
END $$
DELIMITER ;

CALL PRC_INCLUIR_AUTOR("James Dashner", 3);
```

Para parâmetros de saída utiliza-se "OUT" antes do nome do parâmetro

```sql
DELIMITER $$
CREATE PROCEDURE PCR_LISTAR_QTDE_CATEGORIA(
	OUT pi_qtde_categoria INT -- Recebe um parâmetro de saída
)
BEGIN
	SELECT COUNT(*)
    INTO pi_qtde_categoria
    FROM categorias;
END $$
DELIMITER ;
```

Um parâmetro de saída pode ser armazenado numa variável e utilizado fora da procedure, em um "SELECT" ou até em uma outra procedure por exemplo.

```sql
CALL PCR_LISTAR_QTDE_CATEGORIA(@total); -- O parâmetro de saída foi armazenado nessa variável "@local"
SELECT @total; -- A variável está sendo exibida em um SELECT
```

```sql
DELIMITER $$
CREATE OR REPLACE PROCEDURE PRC_QTDE_AUTOR_POR_NACIONALIDADE(IN pi_nacionalidade INT, OUT pi_qtde INT)
BEGIN
	SELECT COUNT(*)
    INTO pi_qtde
    FROM autores a
    WHERE a.id_nacionalidade = pi_nacionalidade;
END $$
DELIMITER ;

CALL PRC_QTDE_AUTOR_POR_NACIONALIDADE(5, @qtde);
SELECT @qtde;
```

Para parâmetros que são usados na entrada e também na saída usa-se "INOUT" antes do parâmetro

```sql
DELIMITER $$
CREATE PROCEDURE PCR_QUADRADO (
	INOUT pi_valor INT -- Recebe um parâmetro de entrada e saída
)
BEGIN
	SET pi_valor = POW(pi_valor, 2); -- Altera o valor desse parâmetro e retorna o valor novo
END $$
DELIMITER ;
```

Para parâmetros do tipo "INOUT", deve ser declarada uma variável com um valor inicial antes de executar a procedure
```sql
SET @valor = 10; -- Cria uma variável "@valor" que recebe o valor inicial 10
CALL PCR_QUADRADO(@valor); -- Ao executar a procedure, o valor da variável é alterado
SELECT @valor; -- Exibe o novo valor dessa variável
```