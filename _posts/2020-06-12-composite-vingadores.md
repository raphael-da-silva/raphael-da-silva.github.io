---
layout: post
title: POO - Compondo os vingadores (da marvel) com objetos
---

Criar objetos do mesmo tipo e usá-los para compor outros objetos é algo que permite juntar todos os objetos em uma composição única que faz algo que reune todos eles. Para ilustrar essa união eu irei usar os hérois da Marvel que formam os vingadores.

Primeiramente, será criada uma interface para representar esses heróis e seus atos:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
interface Vingador
{

    public function avante();

}
```

Depois disso serão criados os heróis que são implementações diferentes dessa mesma interface que representa cada um dos heróis. Segue o código:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */

class CapitaoAmerica implements Vingador
{

    public function avante()
    {

        return 'Jogar o escudo';

    }

}

class PanteraNegra implements Vingador
{

    public function avante()
    {

        return 'Atacar com o equilíbrio perfeito entre mente e corpo.';

    }

}

class HomemFormiga implements Vingador
{

    public function avante()
    {

        return 'Encolher e atacar.';

    }

}

class DoutorEstranho implements Vingador
{

    public function avante()
    {

        return 'Projetar magia.';

    }

}

```

Depois de ter vários objetos do mesma da mesma interface (ou seja, do mesmo tipo), será criada uma classe que é composta por todos esses objetos juntos e representa a junção de todos eles, no exemplo desse artigo essa classe junta todos os heróis e, com isso, forma os Vingadores, já que ela é composta por todos os heróis juntos (composta é a palavra-chave aqui).

Segue a classe que representa os Vingarores:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class Vingadores
{

    private $vingadores;

    public function __construct(
        Vingador ...$vingadores
    ){

        $this->vingadores = $vingadores;

    }

    public function avanteVingadores()
    {

        foreach($this->vingadores as $vingador){
            echo $this->vingador->avancar(), PHP_EOL;
        }

    }

}

```

Para usar as classes o código e juntar tudo na prática ficaria da seguinte forma:

```php
<?php

$vingadores = new Vingadores(
    new CapitaoAmerica,
    new PanteraNegra,
    new HomemFormiga,
    new DoutorEstranho
);

$vingadores->avanteVingadores();
```

Agora todos os hérois em formação podem ir avante!