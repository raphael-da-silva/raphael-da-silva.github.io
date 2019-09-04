---
layout: post
title: PHP - O escopo da variável argv
date: 2018-08-24 18:48
---

A variável pré-definida argv é utilizada para armazenar os argumentos de um script php executado no terminal. Ela está disponível apenas no escopo global de um script php, ou seja, dentro de métodos ela não fica disponível, sendo necessário acessá-la de outra maneira nesse caso. Uma das formas de acessar argv em qualquer lugar é através da variável global ```$GLOBALS```.

```php
public function getArg($index)
{

    $argv = $GLOBALS['argv'];
    
    if(isset($argv[$index])){
        return $argv[$index];
    }

}
```