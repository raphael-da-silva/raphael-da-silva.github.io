---
layout: post
title: "Recursos ninja: algumas classes nativas do PHP (usadas de forma estratégica)"
---

Além das [interfaces nativas](https://raphael-da-silva.github.io/advanced-php-interfaces/), o PHP também conta com algumas classes nativas. O propósito delas é fornecer algumas funcionalidades que ajudam a agilizar o desenvolvimento.

## A classe ArrayObject

A classe ```ArrayObject``` é uma das classes nativas do PHP, o seu propósito é fornecer uma implementação genérica de um objeto que pode ser manipulado como um array, já que ela implementa a interface ```ArrayAccess```. Além disso, ```ArrayObjet``` também implementa as seguintes interfaces:

* ```IteratorAgreggate```;
* ```Countable```;
* ```Serializable```;

Uma das vantagens de utilizar essa classe é reaproveitar a implementação que ela fornece, para isso basta herdar dela. Com isso, não é necessário implementar cada interface citada, já que as implementações dela são reaproveitadas através da herança.

A seguir contém um exemplo de classe que reaproveita a implementação de ArrayObject através de herança.

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class ListaDePessoas extends ArrayObject
{

}
```
A classe ```ListaDePessoas``` está herdando a implementação de ```ArrayObjet```, com isso ela pode ser manipulada da mesma forma que a classe pai.

```php
<?php

$nomes = new ListaDePessoas([
    'Raphael',
    'Bruno'
]);

// Trabalhando com o objeto como um array.
echo $nomes[0]; // Imprime Raphael.
echo $nomes[1]; // Imprime Bruno.

// O objeto pode ser contado por causa da interface Countable
echo count($nomes); // Imprime 2 (que é o total)

// Iterando o objeto
foreach($nomes as $nome){
    echo $nome, PHP_EOL;
}
```

## A classe StdClass

O php contém uma classe chamada ```StdClass```, ela é uma classe genérica que não possui métodos ou atributos, os dados passados para uma instância dessa classe são definidos no momento de sua atribuição, ou seja, são criados dinamicamente.

```php
<?php

$usuario        = new StdClass;
$usuario->nome  = 'Usuário';
$usuario->idade = 22;
```

No trecho de código acima os atributos foram adicionados de forma dinâmica, já que nenhum deles existiam na classe. O uso de ```StdClass``` pode se aplicar em casos onde é necessário agrupar alguns dados de forma rápida sem ter a necessidade de criar uma classe específica para isso.

Também é possível fazer o type casting para converter um array para uma instância de ```StdClass```, para isso basta utilizar a palavra object.

```php
<?php

$usuario = [
    'nome' => 'Usuário',
    'ano'  => 22
];

$objetoUsuario = (object) $usuario;
```

Esse tipo de conversão pode ser vantajosa em contextos onde é necessário passar um tipo que é um objeto como parâmetro reaproveitando os dados presentes em um array.

*** 

### Encerramento ninja!

Gosto muito do grupo de Rap Wu-Tang Clan, por isso vou encerrar esse artigo com o espírito ninja do grupo.

![wu cover](https://i.scdn.co/image/ab67616d0000b273340e53225fb2b3886a57ba91)