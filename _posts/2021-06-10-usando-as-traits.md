---
layout: post
title: Usando traits para evitar código repetido
---

Uma trait é um recurso adicionado na versão 5.4 do PHP que permite o reúso de código sem que ele esteja vinculado a nenhuma classe. Basicamente, uma trait é uma porção de código que pode ser reaproveitado em contextos diferentes. Observe o código a seguir.

```php
<?php

/**
 *
 * Usando traits para evitar repetição de código.
 * @author Raphael da Silva
 *
 */
class MensagemOlaMundo
{

    private function dizerOla($texto): string
    {

        return sprintf('Olá %s.', $texto);

    }

    public function dizerOlaMundo(): void
    {

        echo $this->dizerOla('Mundo');

    }

}

```

A próxima classe tem um método igual ao da classe anterior. 

```php
<?php

/**
 *
 * Usando traits para evitar repetição de código.
 * @author Raphael da Silva
 *
 */
class MensagemOla
{

    private function dizerOla($text): string
    {

        return sprintf('Olá %s.', $text);

    }

    public function dizerOlaParaAlguem($nome): void
    {

        echo $this->dizerOla($nome);

    }

}
```

Como é possível perceber, o método ```dizerOla``` se repete em ambas as classes, para evitar essa repetição pode ser criada uma trait que contém esse método repetido. Por exemplo:

```php
<?php

/**
 *
 * Usando traits para evitar repetição de código.
 * @author Raphael da Silva
 *
 */
trait DizerOlaTrait
{

    private function dizerOla($texto): string
    {

        return sprintf('Olá %s.', $texto);

    }

}
```

Depois de criar a trait, é necessário utilizar a palavra reservada ```use``` nas classes que antes continham o método que estava se repetindo. Com isso, o código da trait é importado para dentro da classe como se tivesse sido declarado dentro dela.

A seguir está a primeira classe de exemplo com a trait adicionada nela.

```php
<?php

/**
 *
 * Usando traits para evitar repetição de código.
 * @author Raphael da Silva
 *
 */
class MensagemOlaMundo
{

    use DizerOlaTrait;

    public function dizerOlaMundo()
    {

        echo $this->dizerOla('Mundo');

    }

}
```

Segue a trait adicionada na segunda classe:

```php
<?php

/**
 *
 * Usando traits para evitar repetição de código.
 * @author Raphael da Silva
 *
 */
class MensagemOla
{

    use DizerOlaTrait;

    public function dizerOlaParaAlguem($nome)
    {

        echo $this->dizerOla($nome);

    }

}
```

Traits são um bom recurso para evitar a repetição de código, o exemplo mostrado anteriormente serve para ilustrar isso. Com esse recurso o PHP traz muito mais possibilidades para lidar com código repetido (leia-se resolvê-lo). Ter as traits como carta na manga ajuda muito.

***

### 💀💀💀 Case Closed: é isso... 💀💀💀

Gosto muito do grupo de Rap Cypress Hill (💀💀💀), existe uma música deles chamada "Case Closed", que traduzindo significa "Caso Encerrado". Referenciei o nome dessa música para encerrar esse artigo. 

Caso encerrado (aka Case Closed)!!!!

![cypress cover](https://i.scdn.co/image/ab67616d0000b2734e51c518e787896bc8cdb1a5)