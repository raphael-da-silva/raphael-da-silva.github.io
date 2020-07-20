---
layout: post
title: PHP - Converter array para objeto rapidamente
date: 2018-06-16 13:36
---

No PHP é possível fazer o uso de [typecast](http://php.net/manual/pt_BR/language.types.type-juggling.php#language.types.typecasting) para criar um objeto através de um array. Em alguns casos é interessante converter um array para ter um objeto rapidamente. Lembrando que o objeto criado é da classe [`stdClass`](http://php.net/manual/pt_BR/language.types.object.php#language.types.object.casting) do PHP.

```php
$console = (object) [
  'name'  => 'PS3',
  'price' => 1000.00
];

echo $console->name; // Imprime PS3
echo $console->price; // Imprime 1000.00
```
