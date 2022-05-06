---
layout: post
title: "Recursos do PHP: as interfaces nativas, parte 2"
---

Continuação do post anterior sobre interfaces nativas do PHP.

## Iterator

Definição segundo a [documentação do PHP](http://php.net/manual/pt_BR/class.iterator.php):

> Interface para iteradores externos ou objetos poderem ser iterados por eles mesmos internamente.

Com a interface ```Iterator``` é possível percorrer o objeto através de laços de repetição, ou seja, o objeto se torna iterável. Para isso, é necessário implementar os métodos que irão definir a posição durante a iteração.

```php
<?php

/**
 *
 * Exemplo de implementação da interface iterator
 * @author Raphael da Silva
 * 
 *
 */
class ColecaoDeNomes implements Iterator
{

    private $nomes   = [];
    private $posicao = 0;

    public function adicionarNome($nome): void
    {

        $this->nomes[] = $nome;

    }

    /**
     *
     * Os métodos abaixo são parte da interface Iterator.
     *
     */
    public function current()
    {

        return $this->nomes[$this->posicao];

    }

    public function key()
    {

        return $this->posicao;

    }

    public function next(): void
    {

        $this->posicao++;

    }

    public function rewind(): void
    {

        $this->posicao = 0;

    }

    public function valid(): bool
    {

        return isset($this->nomes[$this->posicao]);

    }

}
```

Com a implementação da interface concluída, é possível iterar no objeto como se o mesmo fosse um array.

```php
<?php

$nomes = new ColecaoDeNomes;
$nomes->adicionarNome('Raphael');
$nomes->adicionarNome('Bruno');

//Com a interface dá para usar o feachr direto no objeto.
foreach($nomes as $nome){
    echo $nome, PHP_EOL;
}
```

### Relembrando o que é uma iteração

Iteração é termo usado para se referir ao ato de repetir uma ação no código. Basicamente, iterar é repetir uma instrução através de um laço repetição (loop).

## IteratorAggregate

Definição segundo a [documentação do PHP](http://php.net/pt_BR/IteratorAggregate):

> Interface para criar um Iterator externo.

O objetivo da interface ```IteratorAggregate``` é definir um iterator em um objeto que não deve ser um iterator, mas por algum motivo é útil ter um interator atrelado (aka agregado) a ele. O exemplo a seguir mostra o propósito da interface, onde a única parte que é iterável é retornada através do método ```getIterator```.

```php
<?php

/**
 *
 * Exemplo de implementação de IteratorAggregate
 * @author Raphael da Silva
 *
 */
class InformacoesDeLivros implements IteratorAggregate
{

    private $nomesDeLivros;

    public function __construct(array $nomesLivros)
    {

        $this->nomesDeLivros = $nomesDeLivros;

    }

    public function getIterator(): Iterator
    {

        $nomes = new ColecaoDeNomes;

        foreach($this->nomesDeLivros as $livro){
            $nomes->adicionarNome($livro);
        }

        return $nomes;

    }

}
```

Basicamente, a ideia do ```IteratorAggregate``` é fornecer um objeto que têm um iterator e não que é um iterator, por isso o uso da palavra aggregate para dar a ideia de ter (ou **agregar**) algo. No exemplo em questão, a classe `InformacoesDeLivros` agraga o interagir `ColecaoDeNomes` que foi usado como exemplo anterior.

***

### 💀💀💀 Case Closed: é isso... 💀💀💀

Gosto muito do grupo de Rap Cypress Hill (💀💀💀), existe uma música deles chamada "Case Closed", que traduzindo significa "Caso Encerrado". Referenciei o nome dessa música para encerrar esse artigo. 

Caso encerrado (aka Case Closed)!!!!

![cypress cover](https://i.scdn.co/image/ab67616d0000b2734e51c518e787896bc8cdb1a5)
