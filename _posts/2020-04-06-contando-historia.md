---
layout: post
title: Post de quarentena - Contando histórias com uma inferface
---

Criei um repositório no Github com o intuíto utilizar interfaces para mostrar que existem várias formas de contar uma história. Cada tipo de mídia é uma implementação diferente da interface `MidiaParaContarHistoria` criada para contar uma história independente da mídia escolhida. Segue a interface:

```php
<?php

namespace ContarHistoria;

/**
 *
 * @author Raphael da Silva
 *
 */
interface MidiaParaContarHistoria
{

    public function contarHistoria();

}
```

Como a história é contada não é importante, pois o que importa é a história ser contada e não qual tipo de mídia que será utilizada para fazer isso. O tipo de mídia é um detalhe de implementação e, portanto, não é o mais importante. O que é mais importante é o que deve ser feito: contar uma história.

### Implementações

Segue a implementação da interface para contar a história com um filme:

```php
<?php

namespace ContarHistoria\Midias;

use ContarHistoria\MidiaParaContarHistoria;

/**
 *
 * @author Raphael da Silva
 *
 */
class HistoriaEmFilme implements MidiaParaContarHistoria
{

    public function contarHistoria()
    {

        echo 'Usar um filme para contar uma história.';

    }

}
```

Segue a implementação da interface para contar a história com um quadrinho:

```php
<?php

namespace ContarHistoria\Midias;

use ContarHistoria\MidiaParaContarHistoria;

/**
 *
 * @author Raphael da Silva
 *
 */
class HistoriaEmQuadrinhos implements MidiaParaContarHistoria
{

    public function contarHistoria()
    {

        echo 'Usar um quadrinho (aka comicbook) para contar história.';

    }

}
```

Segue a implementação da interface para contar a história com um livro:

```php
<?php

namespace ContarHistoria\Midias;

use ContarHistoria\MidiaParaContarHistoria;

/**
 *
 * @author Raphael da Silva
 *
 */
class HistoriaEmLivro implements MidiaParaContarHistoria
{

    public function contarHistoria()
    {

        echo 'Usando um livro para contar uma história.';

    }

}

```

### Links

[Ver o código no repositório](https://github.com/raphael-da-silva/contando-historia-com-interface)