
# Comandos básicos

### echo

O comando **echo** exibe um texto no console ou em tela (dependendo de onde o código está sendo executado). Exemplo:

```php
<?php

function hello(string $name, int $age): void  
{  
    echo "Olá, meu nome é $name, eu tenho $age anos." . PHP_EOL;  
}
```

### var_dump

O comando **var_dump** exibe o conteúdo de variáveis de forma bem detalhada especificando o tipo da variável. Se for um array associativo exibe o tipo de cada chave do array. Exemplo:
```php
<?php

$people = [  
    ["nome" => "Tiago Lopes",  
        "idade" => 21,  
        "trabalha" => true  
    ],   
    [  
        "nome" => "Gisele Lopes",  
        "idade" => 25,  
        "trabalha" => true  
    ],  
];

var_dump($people);
```

Saída:
```
array(2) {
  [0]=>
  array(3) {
    ["nome"]=>
    string(11) "Tiago Lopes"
    ["idade"]=>
    int(21)
    ["trabalha"]=>
    bool(true)
  }
  [1]=>
  array(3) {
    ["nome"]=>
    string(12) "Gisele Lopes"
    ["idade"]=>
    int(25)
    ["trabalha"]=>
    bool(true)
  }
}
```

# Tipos de variáveis

### Tipos primitivos

O PHP é uma linguagem com tipagem dinâmica e forte. Possui os seguintes tipos primitivos:

- **int**: Números inteiros;
- **float**: Números com vírgula;
- **string**: Texto;
- **bool**: true (verdadeiro) ou false (falso);
- **mixed**: É quanto o tipo de uma variável não foi inferido, então pode ser qualquer tipo (funciona como o "any" do Typescript).

Exemplo:
```php
<?php  
  
$age = 22; // int  
$name = 'Tiago'; // string  
$weight = 75.20; // float  
$married = false; // bool  
  
function hello(string $name, int $age, float $weight, bool $married): void  
{  
    $isMarried = $married ? 'sou casado.' : 'não sou casado.';  
    echo "Olá, meu nome é $name, eu tenho $age anos, peso $weight KG e $isMarried" . PHP_EOL;  
}  
  
hello($name, $age, $weight, $married);
```

Saída:
```
Olá, meu nome é Tiago, eu tenho 22 anos, peso 75.2 KG e não sou casado.
```

### Variáveis e constantes

No PHP podemos ter variáveis cujo o valor pode variar e aquelas cujo o valor não muda (constante). Na declaração de uma variável, é necessário utilizar o caractere $ antes do nome da variável. No caso da constante, é utilizada a palavra reservada "const" e o caractere $ não precisa ser utilizado no nome da constante.

Exemplo:
```php
<?php

const name = 'Tiago Lopes';  
$age = 22;

echo 'Name: ' . name . PHP_EOL;
echo "Age: $age" . PHP_EOL;
```

Também é possível declarar constantes utilizando o comando "define".

Exemplo:
```php
<?php

define('name', 'Tiago Lopes');
echo "Name: " . name;
```
### Arrays

No PHP temos 2 tipos de arrays: com **índices numéricos** (como listas simples) e **associativos** (com chave e valor, conhecidos como "objetos" em outras linguagens, como o Javascript, por exemplo).

Exemplo:
```php
<?php

$names = ["Tiago", "Gisele", "Jéssica", "Pedro"]; // Array com índices numéricos 
  
$person = [  // Array associativo
    "nome" => "Gisele Lopes",  
    "idade" => 25,  
    "trabalha" => false  
];
```


# Condicionais

### if

O **if** verifica se uma determinada condição retorna verdadeiro, se sim, o código dentro do bloco é executado. Exemplo:

```php
<?php  
  
$number = rand(1, 10);  
  
if ($number > 5) {  
    echo "$number é maior que 5";  
}
```
### else

O **else** permite executar um bloco de código caso a condição do **if** não seja atendida. Exemplo:
```php
<?php  
  
$number = rand(1, 10);  
  
if ($number > 5) {  
    echo "$number é maior que 5";  
} else {  
    echo "$number é menor ou igual a 5";  
}
```

### elseif

O **elseif** permite adicionar outras condições após um **if**. Exemplo:
```php
<?php  
  
$number = rand(1, 30);  
  
if ($number > 20) {  
    echo "$number é maior que 20";  
} elseif ($number > 10) {  
    echo "$number é maior que 10 e menor que 20";  
} else {  
    echo "$number é menor que 10";  
}
```

### Operador ternário

O operador ternário permite verificar se uma condição for verdadeira e realizar uma ação, caso seja verdadeira, e uma outra ação, se for falsa. Exemplo:
```php
<?php  
  
$number = rand(1, 10);  
  
echo $number > 5 ? "$number é maior que 5" : "$number é menor ou igual a 5"
```


### Coalesce

É semelhante ao operador ternário. Verifica se o primeiro valor passado é um valor que é considerado falso (false, 0, null), se não for, retorna o primeiro valor, caso contrário, retorna o segundo valor. Exemplo:
```php
<?php  

$number = rand(1, 10);  
$valor = null;  
  
if ($number > 5) $valor = $number;  
  
echo $valor ?? 'O valor é nulo';
```

### switch

Compara o valor de uma variável com uma série de casos definidos, caso o valor seja correspondente em algum dos casos, o código desse bloco é executado, caso contrário é executado o caso do bloco 'default', caso este seja definido. Exemplo:
```php
<?php

$number = rand(1, 4);  
$options = ['A', 'B', 'C', 'D'];  
$option = $options[$number-1];  
  
switch ($option) {  
    case 'A':  
        echo 'A opção sorteada foi A';  
        break;  
    case 'B':  
        echo 'A opção sorteada foi B';  
        break;  
    case 'C':  
        echo 'A opção sorteada foi C';  
        break;  
    case 'D':  
        echo 'A opção sorteada foi D';  
        break;  
    default:  
        echo 'Ocorreu um erro!';  
}
```
O comando **break** faz com que o programa saia do bloco **switch** assim que um dos casos for atendido.

### match

Semelhante ao switch temos o comando match, que verifica se o valor de uma variável bate com uma série de valores definidos dentro do bloco, possuindo uma sintaxe mais enxuta que o switch. Exemplo:
```php
<?php

$number = rand(1, 4);  
$options = ['A', 'B', 'C', 'D'];  
$option = $options[$number-1];  
  
echo match ($option) {  
    'A' => 'A opção sorteada foi A',  
    'B' => 'A opção sorteada foi B',  
    'C' => 'A opção sorteada foi C',  
    'D' => 'A opção sorteada foi D',  
    default => 'Ocorreu um erro!',  
};
```
### while

Executa um bloco de código repetidamente enquanto uma condição for verdadeira, saindo do bloco somente quando a condição passa a ser falsa. Exemplo:
```php
<?php

int $number = 0;  
  
while ($number < 8) {  
    echo "O número $number é menor que 8" . PHP_EOL;  
  
    $number = rand(1, 10);  
}
```

### do while

Executa o bloco pelo menos uma vez, após a primeira execução só continuará no bloco caso a condição definida no final do bloco seja verdadeira, saindo quando a condição passar a ser falsa.
```php
<?php

$number;  
  
do {  
    echo "Passou pelo bloco" . PHP_EOL;  
  
    $number = rand(1, 10);  
} while ($number < 8);
```


### For

Executa um bloco de código uma quantidade pré-determinada de vezes. Exemplo:
```php
<?php

$number = rand(1, 30);
  
for ($i = 1; $i <= $number; $i++) {  
    echo $i . PHP_EOL;  
}
```
# Operadores

O PHP possui operadores aritméticos, para realização de cálculos, relacionais para comparações e lógicos para operações lógicas.

### Operadores aritméticos

Os principais operadores aritméticos são:
- + (Soma)
- - (Subtração)
- / (Divisão)
- * (Multiplicação)
- % (Resto da divisão)
- ** (Potenciação)
- . (Concatenação)

Exemplo:
```php
<?php  
  
$firstNumber = 5;  
$secondNumber = 3;  
  
echo $secondNumber + $firstNumber . PHP_EOL;  
echo $firstNumber - $secondNumber . PHP_EOL;  
echo $firstNumber * $secondNumber . PHP_EOL;  
echo $firstNumber / $secondNumber . PHP_EOL;  
echo $firstNumber % $secondNumber . PHP_EOL;  
echo $firstNumber ** $secondNumber . PHP_EOL;  
echo $firstNumber . $secondNumber . PHP_EOL;

/* Resultado:

8
2
15
1.6666666666667
2
125
53
*/
```

### Operadores relacionais

Os operadores relacionais do PHP são:
* \> (Maior)
* \>= (Maior ou igual)
* < (Menor)
* <= (Menor ou igual)
* == (Igual a)
* === (Estritamente igual. Verifica se o tipo de ambos os valores também é o mesmo)
* <=> (Maior, igual ou menor. Retorna 1 se o primeiro valor for maior, -1 se o segundo valor for maior e 0 caso ambos sejam iguais)

Exemplo:
```php
<?php  
  
$firstNumber = 5;  
$secondNumber = 3;  
$thirdNumber = '5';  
  
echo ($firstNumber > $secondNumber ? 'Verdadeiro' : 'Falso') . PHP_EOL;  
echo ($firstNumber >= $secondNumber ? 'Verdadeiro' : 'Falso') . PHP_EOL;  
echo ($firstNumber < $secondNumber ? 'Verdadeiro' : 'Falso') . PHP_EOL;  
echo ($firstNumber <= $secondNumber ? 'Verdadeiro' : 'Falso') . PHP_EOL;  
echo ($firstNumber == $thirdNumber ? 'Verdadeiro' : 'Falso') . PHP_EOL;  
echo ($firstNumber === $thirdNumber ? 'Verdadeiro' : 'Falso') . PHP_EOL;  
echo ($secondNumber <=> $firstNumber) . PHP_EOL;

/*
Resultado:

Verdadeiro
Verdadeiro
Falso
Falso
Verdadeiro
Falso
-1
*/
```

### Operadores lógicos

Os operadores lógicos do PHP são:
* && (E): Todas as asserções devem ser verdadeiras para que o resultado final seja verdadeiro;
* || (Ou): Basta uma das asserções ser verdadeira para que o resultado final seja verdadeiro;
* ! (Não): Nega o resultado, ou seja: se o resultado for verdeiro, será invertido para falso e o inverso também;
* ^ (Ou exclusivo): Apenas uma das asserções deve ser verdadeira para que o resultado final seja verdadeiro, caso mais de uma seja verdadeira ou nenhuma seja, o resultado será falso.

Exemplo:
```php
<?php  
  
$firstNumber = 5;  
$secondNumber = 10;  
$thirdNumber = 3;  
  
if ($firstNumber < $secondNumber && $firstNumber > $thirdNumber) {  
    echo "$firstNumber é menor que $secondNumber E maior que $thirdNumber." . PHP_EOL;  
}  
  
if ($firstNumber < $secondNumber || $firstNumber < $thirdNumber) {  
    echo "$firstNumber é menor que $secondNumber OU que $thirdNumber." . PHP_EOL;  
}  
  
if (!($firstNumber > $secondNumber)) {  
    echo "$firstNumber NÃO é maior que $secondNumber." . PHP_EOL;  
}  
  
if ($firstNumber < $secondNumber ^ $firstNumber > $thirdNumber) {  
    echo "$firstNumber é SOMENTE menor que $secondNumber OU SOMENTE maior que $thirdNumber." . PHP_EOL;  
}

/*
Resultado:

5 é menor que 10 E maior que 3.
5 é menor que 10 OU que 3.
5 NÃO é maior que 10.
*/
```

# Funções

Funções são blocos de código que podem ou não retornar um valor e podem receber parâmetros, realizando diferentes comportamentos de acordo com os parâmetros recebidos e são uma ótima forma de eliminar repetições de códigos.

No PHP, existem duas formas de se declarar funções, da maneira **convencional** ou por meio de **Arrow functions**.

* **Funções convencionais**: São declaradas com a palavra chave **function** seguido pelo nome da função, abertura de parênteses, onde podem ser recebidos parâmetros de diferentes tipos. Em versões do PHP superiores a 7.4 deve ser especificado o tipo de cada parâmetro e o tipo do retorno da função. Exemplo:

```php
<?php

function sum(int $firstNumber, int $secondNumber): int  
{  
    return $firstNumber + $secondNumber;
}

echo sum(10, 5); // Resultado 15
```

* **Arrow function**: São declaradas como variáveis, portanto precisam do caractere **$** antes do nome da função,  possuem uma sintaxe mais simples e objetiva e possuem um retorno implícito através do operador **=>**. Exemplo:

```php
<?php

$sum = fn(int $firstNumber, int $secondNumber): int => 
	$firstNumber + $secondNumber;

echo $sum(10, 5); // Resultado 15
```

# Importação de arquivos

Arquivos PHP podem ser importados em outros arquivos através dos comandos **require** e **require_once**.

* **require**: Faz a importação de um arquivo PHP, deve ser passado o caminho relativo desse arquivo partindo da pasta do arquivo que está fazendo essa importação.
* **require_once**: Também realiza importação assim como o **require**, a única diferença entre eles é que o **require_once** verifica se o arquivo já está sendo importado, para não correr o risco de ele ser importado mais de uma vez, já o **require** não faz essa verificação.

Exemplo:
```php
<?php  
  
require 'strings.php';  
require_once 'funcoes.php';
  
$person = [  
    "nome" => "Matheus Cunha",  
    "idade" => 32,  
    "trabalha" => false  
];  
  
echo hello($person); // Método que vem de um arquivo importado
```

Quando é feita a importação de uma classe e esta possui um **namespace**, a importação pode ser feita utilizando o comando **use**. Nesse caso, o **autoload** deve estar corretamente configurado para a importação funcionar corretamente.

Exemplo:
```php
<?php  
  
require_once 'autoload.php';  
  
use model\{Endereco};  
use model\funcionario\{Gerente, Diretor, Desenvolvedor};  
use service\ControleDeBonificacoes;
```