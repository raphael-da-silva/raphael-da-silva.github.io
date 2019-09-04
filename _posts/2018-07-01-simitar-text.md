---
layout: post
title: PHP - Verificando a similaridade entre duas strings
date: 2018-07-01 11:32
---

O PHP possuí uma função chamada [simitar_text](http://php.net/similar_text), o seu propósito é calcular a similaridade entre duas strings.

```php
$string = 'Hello World';
similar_text($string, $string, $percentage);

// Imprime 100, que é a porcentagem de similaridade
echo $percentage; 
```

É importante salientar alguns pontos sobre o código acima:

* A função retorna o número de caracteres iguais entre as strings. Nesse caso, o número retornado vai ser 11, já que é o tamanho da string, ou seja, aqui elas são completamente iguais.

* Para obter a porcentagem é necessário definir o terceiro parâmetro, pois ele passa o número para uma variável por referência.
