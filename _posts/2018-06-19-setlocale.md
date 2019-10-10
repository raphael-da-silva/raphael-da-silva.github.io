---
layout: post
title: PHP - Definindo a localização com a função setlocale
date: 2018-06-19 22:18
---

Definir a localização em PHP é bastante útil para trabalhar com funções como ```strftime```, que trabalham com o local definido.

```php

setlocale(LC_ALL, 'PT-BR', 'portuguese');

```

Quero salientar dois pontos importantes do código acima:

* A função aceita um número indefinido de valores a partir do segundo parâmetro. Ou seja, ela é uma função variádica.

* Caso algum valor não seja suportado, a função irá tentar utilizar o próximo valor e assim sucessivamente. No exemplo, caso "PT-BR" não seja suportado o  valor "portuguese" será utilizado.