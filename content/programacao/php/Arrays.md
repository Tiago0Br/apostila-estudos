# Arrays em PHP

Array (ou vetor em português) é uma estrutura de dados que permite adicionar múltiplos elementos em uma única variável funcionando como uma espécie de lista. No PHP, os arrays podem ser associativos ou com índices numéricos. Os itens do vetor não precisam necessariamente ter o mesmo tipo de dado, podendo conter valores de tipos diferentes.


## Tipos de arrays
### Arrays com índices numéricos

São listas simples onde cada valor pode ser acessado pelo seu índice, que representa a posição que ele ocupa dentro do vetor iniciando pelo 0.

Exemplo:
```php
$fruits = ["orange", "apple", "grape", "banana"];

echo $fruits[0]; // orange
echo $fruits[2]; // grape
```

### Arrays associativos

Possuem chave e valor, são como objetos. É possível acessar seu valor por meio da chave.

Exemplo:
```php
$person = [
	'name' => 'Tiago Lopes',
	'age' => 22,
	'married' => false
];

echo $person['name']; // Tiago Lopes
echo $person['age']; // 22
```

## Adição / remoção de valores no array