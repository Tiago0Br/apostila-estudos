
# Tamanho de strings

### strlen

O comando **strlen** retorna o tamanho de uma string, considerando acentuação como caracteres. Exemplo:
```php
<?php  
  
$name = 'Tiagão';  

echo strlen($name) . PHP_EOL; // Resultado: 7
```

### mb_strlen

O comando **mb_strlen** faz parte do módulo **mbstring** e também retorna o tamanho de uma string, porém desconsiderando as acentuações e outros caracteres especiais. Exemplo:
```php
<?php  
  
$name = 'Tiagão';  

echo mb_strlen($name) . PHP_EOL; // Resultado: 6
```

# Verificar se a string contém um certo conteúdo

### str_contains

Verifica se contém um certo conteúdo dentro de uma string retornando verdadeiro, caso contenha e falso, caso não contenha, exemplo:
```php
<?php  
  
$name = 'Tiago Tavares Lopes';  
  
if (str_contains($name, 'Lopes')) {
    echo "$name contém 'Lopes'" . PHP_EOL;  
}

// Resultado:
// Tiago Tavares Lopes contém 'Lopes'
```

### str_starts_with

Verifica se uma string se inicia com um determinado conteúdo, retornando verdadeiro ou falso, por exemplo:
```php
<?php  
  
$name = 'Tiago Tavares Lopes';  
  
  
if (str_starts_with($name, 'Tiago')) {
    echo "$name começa com 'Tiago'" . PHP_EOL;  
}

// Resultado:
// Tiago Tavares Lopes começa com 'Tiago'
```

### str_ends_with

Verifica se uma string termina com um determinado conteúdo, retornando verdadeiro ou falso, por exemplo:
```php
<?php  
  
$name = 'Tiago Tavares Lopes';
  
if (str_ends_with($name, 'Lopes')) {
    echo "$name termina com 'Lopes'" . PHP_EOL;  
}

// Resultado:
// Tiago Tavares Lopes termina com 'Lopes'
```

# Manipulação de Strings

### strtoupper

Transforma a string deixando todos os caracteres em caixa alta (com exceção de caracteres acentuados). Exemplo:
```php
<?php  
  
$name = 'Tiagão Lopes';  
  
echo strtoupper($name) . PHP_EOL;

// Resultado: TIAGãO LOPES
```

### mb_strtoupper

Realiza a mesma função da **strtoupper**, porém também deixa em caixa alta os caracteres acentuados. Faz parte da extensão [mbstring](https://www.php.net/manual/pt_BR/book.mbstring.php). Exemplo:
```php
<?php  
  
$name = 'Tiagão Lopes';  
  
echo mb_strtoupper($name) . PHP_EOL;

// Resultado: TIAGÃO LOPES
```

### strtolower

Transforma a string deixando todos os caracteres em caixa baixa (com exceção de caracteres acentuados). Exemplo:
```php
<?php  
  
$name = 'TIAGÃO LOPES';  
  
echo strtolower($name) . PHP_EOL;

// Resultado: tiagÃo lopes
```

### mb_strtolower

Realiza a mesma função da **strtolower**, porém também deixa em caixa baixa os caracteres acentuados. Faz parte da extensão [mbstring](https://www.php.net/manual/pt_BR/book.mbstring.php). Exemplo:
```php
<?php  
  
$name = 'TIAGÃO LOPES';  
  
echo mb_strtolower($name) . PHP_EOL;

// Resultado: tiagão lopes
```

### explode

Transforma a string em um array de strings com base em um separador. Exemplo:
```php
<?php  
  
$name = 'Tiago Lopes';  
  
[$firstName, $lastName] = explode(' ', $name);
echo "Meu nome é $firstName e meu sobrenome é $lastName" . PHP_EOL;

// Saída: Meu nome é Tiago e meu sobrenome é Lopes
```

### implode

Faz o inverso do comando **explode**, transforma um array em uma string, cada item separado por um separador definido na chamada da função. Exemplo:
```php
<?php
  
$students = ['Tiago', 'Gisele', 'Jéssica'];  
$strStudents = implode(', ', $students);
echo "Os alunos são: $strStudents." . PHP_EOL;

// Saída: Os alunos são: Tiago, Gisele, Jéssica.
```

### trim

Remove espaços em branco do início e fim de uma string e também pode remover outros caracteres definidos na chamada da função. Exemplo:
```php
<?php

$email = '  ,  teste@gmail.com  ,./  ';  
echo trim($email) . PHP_EOL; // Remove somente espaços em brancos
echo trim($email, ' ,./') . PHP_EOL; // Remove outros caracteres
```