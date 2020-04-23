---
layout: post
title: Post de quarentena - Nullable types vs. Parâmetros opcionais
---

[Nullable Types](https://wiki.php.net/rfc/nullable_types) é um recurso adicionado a partir da versão 7.1 do PHP, ele serve para permitir que um parâmetro possa receber nulo além do tipo definido como type hinting. A função ```printName``` a seguir espera um parâmetro do tipo ```StdClass```, só que o ponto de interrogação (?) antes da declaração do tipo define esse parâmetro como nullable type.

```php
<?php

function printName(?StdClass $user)
{

    if(!is_null($user)){
        echo sprinf('Meu nome é %s', $user->name), PHP_EOL;
        return;
    }
    
    echo 'Nenhum nome!', PHP_EOL;

}

```

Como o parâmetro é nullable type, ele pode ser executado de duas formas: passando o tipo esperado ou passando um valor nulo.

```php
<?php

$user = new \StdClass;
$user->name = 'Usuário da Silva';

printName($user); // Imprime 'Meu nome é Usuário da Silva'
printName(null); // Imprime 'Nenhum nome!'

```

Isso difere o recurso de nullable types dos parâmetros opcionais, pois quando um parâmetro opcional é definido, significa que a função pode ser chamada sem nenhum parâmetro. Segue o código:

```php
<?php

// Agora o parâmetro é opcional
function printName(StdClass $user = null)
{

    if(!is_null($user)){
        echo sprinf('Meu nome é %s', $user->name), PHP_EOL;
        return;
    }
    
    echo 'Nenhum nome!', PHP_EOL;

}

$user = new \StdClass;
$user->name = 'Usuário da Silva';

printName($user); // Imprime 'Meu nome é Usuário da Silva'
printName(null); // Imprime 'Nenhum nome!'

// É possível executar a função sem parâmetro.
printName(); // Imprime 'Nenhum nome!'

```
Como é possível perceber na terceira execução da função, nenhum parâmetro está sendo passado, isso é possível porque o parâmetro foi declarado como opcional. Essa é a diferença principal, já que no nullable type não dá para omitir um parâmetro, pois é necessário que ele receba um valor nulo explicitamente (além do tipo esperado, é claro).