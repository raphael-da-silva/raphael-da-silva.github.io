---
layout: post
title: PHP - Isolando valores sensíveis de configuração
---

Existem alguns valores que não devem ser colocados diretamente no código-fonte de um projeto, pois eles são sensíveis e, portanto, ficarão expostos se colocados diretamente do código. Exemplos desses valores são os tokens para consumo de API's e credenciais para o banco de dados.

No PHP existe uma biblioteca chamada DotEnv, ela lê um arquivo chamado ```.env``` e adicionar os valores definidos nesse arquivo em variáveis de ambiente do PHP. Para instalá-la via Composer basta rodar o seguinte comando:

```bash

composer require vlucas/phpdotenv

```

Após a instalação, é necessário criar e executar o objeto que irá fazer o trabalho, lembrando que é preciso passar o diretório onde o arquivo ```.env``` está armazenado. Segue o código:

```php

$dotenv = \DotEnv\DotEnv::create(__DIR__);
$dotenv->load();

```

Como é possível perceber, o uso da biblioteca é bastante simples, além disso, o isolamento do código e dos valores de configuração torna desnecessário a mudança de valores ao trocar o ambiente de desenvolvimento para o de produção. Basta que o arquivo ```.env``` esteja com os valores certos no ambiente de produção.

Para obter os valores adicionados no código PHP, é possível utilizar as variáveis superglobais ```$_ENV``` e ```$_SERVER``` ou, então, utilizar a função ```getenv``` para fazer isso.