---
layout: post
title: A função array_filter sem nenhum parâmetro
date: 2018-06-29 19:28
---

A função ```array_filter``` serve para filtrar um array com base em um filtro espeficado, esse filtro é um callback que vai definir a regra para filtrar os elementos do array. Porém, a função tem um comportamento padrão quando nenhum callback é passado para ela.

```php
$values = [
    'Some string',
    '',
    null,
    false,
    10,
    '0',
    0
];

// Apenas os valores 'Some string' e 10 serão preservados.
$values = array_filter($values);
```

Por padrão, a função irá descartar todos os valores que são [interpretados como false](http://php.net/manual/pt_BR/types.comparisons.php) pelo PHP. A função ```array_filter``` sem callbacks é útil em alguns contextos, pois poupa o trabalho de filtrar valores vazios.