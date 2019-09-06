---
layout: post
title: PHP - Uso básico do Doctrine DBAL
---

A biblioteca Doctrine DBAL oferece uma camada adicional por cima da PDO, com isso ela disponibiliza uma API de alto nível que simplifica operações que são mais verbosas e repetitivas com o PDO. Essa API conta com alguns métodos bastante úteis para fazer operações básicas de [CRUD](https://pt.wikipedia.org/wiki/CRUD).

## Criação da conexão

Antes de começar, é preciso instalar a biblioteca com o Composer, para isso é preciso rodar o seguinte comando no terminal:

```bash

composer require "doctrine/dbal"

```
Para criar o objeto referente a conexão, a biblioteca disponibiliza o método estático ```getConnection``` da classe ```DriverManager```. Esse método espera um array com as credenciais as informações para fazer a conexão com o banco de dados.

```php

$dbal = \Doctrine\DBAL\DriverManager::getConnection([
    'dbname'   => 'nomedobanco',
    'user'     => 'usuario',
    'password' => 'senha',
    'host'     => 'localhost',
    'driver'   => 'pdo_mysql',
    'driverOptions' => []
]);

```

## Operações de CRUD

### Método ```insert```

**Parâmetros:**
* Primeiro: nome da tabela do banco de dados.
* Segundo: array associativo com o nome das colunas e seus valores

```php

$dbal->insert('noticias', [
    'Titulo' => 'Notícia nova!',
    'Texto'  => 'Texto da notícia nova.'
]);

```

### Método ```update```

**Parâmetros:**
* Primeiro: nome da tabela do banco de dados.
* Segundo: array associativo com o nome das colunas e seus valores.
* Terceiro: array associativo equivalente a clausula ```WHERE``` do SQL.

```php

$dbal->insert('noticias', [
    'Titulo' => 'Notícia nova (atualizada)!',
    'Texto'  => 'Texto da notícia nova (atualizada).'
], ['Id' => 1]);

```

### Método ```delete```

**Parâmetros:**
* Primeiro: nome da tabela do banco de dados.
* Segundo: array associativo com a coluna e o valor que será utilizado como critério para a exclusão.

```php

$dbal->delete('noticiss', [
    'Id' => 1
]);

```

## Busca de dados

Buscar vários registros:

```php

$rows = $dbal->fetchAll('SELECT * FROM noticias');

```

Buscar um registro:

```php

$rows = $dbal->fetchAssoc('SELECT Titulo FROM noticias WHERE Id = :id', [
    'Id' => 1
]);

```

Buscar uma coluna de um registro:

```php

$title = $dbal->fetchColumn('SELECT Titulo FROM noticias WHERE Id = :id', [
'Id' => 1] 'Titulo');

```

## Conclusão

A biblioteca Doctrine DBAL é uma ótima opção para acesso ao banco de dados com PHP. Através dela as operações básicas são simplicadas, o que é de grande ajuda para agilizar as coisas.