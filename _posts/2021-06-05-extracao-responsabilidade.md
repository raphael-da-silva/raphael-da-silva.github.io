---
layout: post
title: Extraindo as responsabilidades de objetos
---

A separação das partes de um software é essencial para se obter componentes coesos, simples, de complexidade reduzida e que são mais fáceis de se reaproveitar devido a sua separação conceitual e foco específico. Essa separação é essencial em objetos, pois permite que as responsabilidades sejam separadas de forma mais coesa. Essa separação em objetos existentes pode ser feita com extração dessas responsabilidades para novos objetos.

## Extração de código para criar novos objetos

Extrair partes do código para criar novos componentes é uma prática que pode ser utilizada para separar as partes de um objeto. Caso um trecho de código de um componente precise ser reutilizado em outro ponto da aplicação, esta parte do código deve ser extraída para um novo componente e ser utilizada onde já estava sendo antes e também no novo contexto onde é preciso desta funcionalidade.

Por exemplo, caso tenha uma classe que filtre e-mails válidos e que valide um e-mail em um método e esta validação precisa ser reutilizada em outro ponto da aplicação, é possível extrair essa validação para um novo componente e utilizar este componente no novo contexto e também onde ele já estava sendo utilizado antes. Segue o exemplo antes da extração.

```php
<?php

/**
 *
 * Exemplo extração de responsabilidades
 * @author Raphael da Silva
 *
 */
class FiltroDeEmails
{

    private function validarEmail($email): bool
    {

        return (!empty($email) and filter_var($email, FILTER_VALIDATE_EMAIL));

    }

    public function extrairEmailsValidos(array $emails): array
    {

        $validos = [];

        foreach($emails as $email){

            if($this->validarEmail($email)){
                $validos[] = $email;
            }

        }

        return $validos;

    }

}
```
Ao aplicar a extração, a validação de e-mail irá ser extraída para uma classe própria, que poderá ser reaproveitada em diferentes lugares de acordo com a necessidade que surgir. Nesse caso, a classe ```ValidatorEmail``` foi criada.

```php
<?php

/**
 *
 * Exemplo extração de responsabilidades
 * @author Raphael da Silva
 *
 */
class ValidadorEmail
{

    public function validar($email): bool
    {

        return (!empty($email) and filter_var($email, FILTER_VALIDATE_EMAIL));

    }

}

```

Depois de criar a nova classe, é preciso passá-la para a classe ```FiltroDeEmails``` que antes continha a lógica que valida um e-mail.

```php
<?php

/**
 *
 * Exemplo extração de responsabilidades
 * @author Raphael da Silva
 *
 */
class FiltroDeEmails
{

    private $validatorEmail;

    public function __construct(
        ValidatorEmail $validatorEmail
    ){

        $this->validatorEmail = $validatorEmail;

    }

    public function extrairEmailsValidos(array $emails): array
    {

        $validos = [];

        foreach($emails as $email){

            if($this->validatorEmail->validar($email)){
                $validos[] = $email;
            }

        }

        return $validos;

    }

}
```

Além da extração de código possibilitar o reúso das funcionalidades separadamente devido a criação de novos componentes, ela também faz com que os componentes criados tenham uma responsabilidade única, pois eles executam apenas uma funcionalidade como no exemplo, onde o propósito é somente validar um e-mail e nada mais além disso.

A extração de partes do código (métodos, classes e etc) também é muito importante para evitar a repetição, pois um código que se repete é extraído para um novo componente e, com isso, utilizado no lugar onde estava se repetindo sem se espalhar repetidamente em diversos pontos.