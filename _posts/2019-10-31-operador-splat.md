---
layout: post
title: PHP - O operador splat (a.k.a os três pontos...)
---

O operador splat é um operador formado por três pontos `...` utilizado para trabalhar com funções variádicas. Esse tipo de função pode receber um número ilimitado de parâmetros. A função a seguir serve para ilustrar esse recurso que está presente desde a versão 5.6 do PHP.

```php

function printMessages(...$messages){

    foreach($messages as $message){
        echo $message, PHP_EOL;
    }

}

printMessages(
    'Olá', 
    'Adeus', 
    'Como vai?', 
    'Será que algo vai melhorar?'
);

```

Como é possível perceber, a função pode receber um número infinito de parâmetros, no exemplo foram passadas três strings. O operador splat foi usado antes do nome do parâmetro da função, isso serve para indicar que ela pode receber um lista de ilimitada de argumentos.

Além da declaração dos parâmetros de uma função variádica, o operador splat também serve para converter um array em uma lista de argumentos para serem passados como parâmetros. Segue o exemplo:

```php

$messages = [
    'Olá',
    'Adeus',
    'Como vai?',
    'Será que algo vai melhorar?'
];

// Convertendo o array para argumentos
printMessages(...$messages);

```
