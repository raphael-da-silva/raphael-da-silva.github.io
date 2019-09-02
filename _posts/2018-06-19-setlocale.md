---
layout: post
title: Definindo a localização em PHP
date: 2018-06-19 22:18
---

Definir a localização em PHP é bastante útil para trabalhar com funções como ```strftime```, que trabalham com o local definido.

```php

setlocale(LC_ALL, 'PT-BR', 'portuguese');

```

Quero salientar dois pontos importantes do código acima:

1. A função aceita um número indefinido de valores a partir do segundo parâmetro. Ou seja, ela é uma função variádica.

2. Caso algum valor não seja suportado, a função irá tentar utilizar o próximo valor e assim sucessivamente. No exemplo, caso "PT-BR" não seja suportado o  valor "portuguese" será utilizado.