---
layout: post
title: Hello World - Iniciando um blog de $programação
date: 2018-06-15 21:00
---

O intuíto desse blog é compartilhar algumas experiências sobre programação, exercitar a escrita e aprender com isso, além disso, escrever sempre me ajudou a fixar as coisas aprendidas. Vou tentar passar algumas reflexões e informações técnicas sobre desenvolvimento web aqui.

Esse é o meu primeiro passo para fixar conhecimento e buscar expressá-lo de forma simples. Espero ajudar alguém no meio do processo.

```php

$blog = new GithubPagesBlog;
$blog->setAuthor('Raphael da Silva');
$blog->setGithubUser('raphael-da-silva');
$blog->start();

```

Se você não gosta de setter e mutabilidade, não tem problema! Segue o código para você (passando o autor no construtor).

```php

$blog = new GithubPagesBlog('Raphael da Silva', 'raphael-da-silva');
$blog->start();

```

Até o próximo post!