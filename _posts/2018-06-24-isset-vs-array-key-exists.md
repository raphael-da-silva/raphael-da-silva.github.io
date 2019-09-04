---
layout: post
title: PHP - A diferença entre isset e array_key_exists
date: 2018-06-24 15:30
---

Para verificar se um índice existe em um array no PHP, existem duas opções recorrentes: elas são [isset](http://php.net/isset) e [array_key_exists](http://php.net/array_key_exists). A principal diferença está na interpretação de valores nulos nos índices verificados.

A construção de linguagem ```isset``` irá retornar falso se o índice do array existir mas tiver o valor nulo, enquanto a função ```array_key_exists``` irá retornar verdadeiro se o índice existir, mesmo que o seu valor seja nulo.

```php
$user = [
    'name' => null
];

$issetTest  = isset($user['name']); // Retorna false
$existsTest = array_key_exists('name', $user); // Retorna true
```

É importante lembrar que isset e ```array_key_exists``` não são as únicas opções disponíveis, pois é possível utilizar a função [empty](http://php.net/empty) para checar um índice de um array.