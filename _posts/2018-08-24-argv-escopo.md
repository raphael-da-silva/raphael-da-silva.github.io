---
layout: post
title: PHP - O escopo da variável pré-definida argv
date: 2018-08-24 18:48
---

A variável pré-definida `argv` é utilizada para armazenar os argumentos de um script php executado no terminal. A documentação da linguagem traz a seguinte definição sobre esta variável:

> $argv — Array de argumentos passados para o script

Ela está disponível apenas no escopo global de um script php, ou seja, dentro de métodos ela não fica disponível, sendo necessário acessá-la de outra maneira nesse caso. Uma das formas de acessar `argv` em qualquer lugar é através da variável global `$GLOBALS`.

```php
class Arg
{

    public function getArg($index)
    {

        $argv = $GLOBALS['argv'];
        
        if(isset($argv[$index])){
            return $argv[$index];
        }

    }

}
```

### Alternativa sem variáveis globais

Para quem se incomoda com o uso de variáveis globais e sabe dos seus efeitos colaterais, é possível fazer o mesmo de uma maneira mais legível e com menos dependências de contextos externos, para isso basta passar a variável como parâmetro, assim como qualquer outra dependência que é injetada.

```php
class Arg
{

    private $argv;

    public function __construct(
        $argv
    ){

        $this->argv = $argv;

    }

    public function getArg($index)
    {
        
        if(isset($this->argv[$index])){
            return $this->argv[$index];
        }

    }

}
```

### Escrevendo para fixar

Esse post surgiu depois que eu acabei vendo como funciona o escopo de essa variável pré-definida. Esse foi mais um post onde escrevi algo para fixar na minha mente um detalhe observado enquanto eu estava lidando com código.