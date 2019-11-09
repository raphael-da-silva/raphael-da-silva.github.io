---
layout: post
title: PHP - A ordem de execução dos middlewares no Slim framework
---

Quando um middleware é adicionado no Slim Framework a ordem seguida na execução não é a esperada a primeira vista. Isso ocorre porque o framework segue o conceito [LIFO (Last In, First Out)](https://pt.wikipedia.org/wiki/LIFO), onde o primeiro a ser adicionado é o último a ser executado. O código a seguir ilustra isso.

```php
use Slim\Http\Request;
use Slim\Http\Response;

$app->add(function(Request $request, Response $response, callable $next){

    echo 'Primeiro';
    return $next($request, $response);

});

$app->add(function(Request $request, Response $response, callable $next){

    echo 'Segundo';
    return $next($request, $response);

});

```

Quando a aplicação ser executada, será impresso ```Segundo``` e ```Primeiro``` respectivamente, isso acontece porque o primeiro middleware a ser adicionado é o último a ser executado, ou seja, os middlewares adicionados primeiro são executados por último e os adicionados por último são os primeiros a serem executados.