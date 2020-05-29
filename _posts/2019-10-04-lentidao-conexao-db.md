---
layout: post
title: Banco de dados - Resolvendo a lentidão na conexão
---

Programando no Windows 10 tive um problema de performance utilizando MySQL, achei que poderia ser algum problema com o ambiente novo, porém depois de tentar encontrar o problema, encontrei uma resposta do Stackoverflow que dizia para trocar o host. Basicamente, é necessário trocar localhost para o número de ip do ambiente local.

A seguir está a conexão feita com Doctrine adaptada para utilizar o ip e resolver os problemas de performance. Lembrando que o endereço de ip do [localhost](https://pt.wikipedia.org/wiki/Localhost) é ```127.0.0.1```.

```php
$dbal = \Doctrine\DBAL\DriverManager::getConnection([
    'dbname'   => 'nomedobanco',
    'user'     => 'usuario',
    'password' => 'senha',
    'host'     => '127.0.0.1',
    'driver'   => 'pdo_mysql',
    'driverOptions' => []
]);
```

**Isso pode ser óbvio, mas para mim não era, então acho válido registrar isso para lembrar e não deixar essas pequenas coisas atrapalharem de novo.**