---
layout: post
title: Parâmetros e seus tipos podem ser as dependências injetadas em um objeto
date: 2023-12-02
---

Nesto artigo será mostrada como a parametrização é parte essencial para injetar as depêndencias, essa é a continuação do artigo anterior sobre interfaces com o exemplo da interface `Videogame`.

## A parametrização de objetos e os tipos definidos como parâmetro

Ao parametrizar objetos, o conceito de Type Hinting é essencial, já que definir os tipos como parâmetros nos métodos dos objetos é fundamental na prática que norteia a injeção de depência.

Parametrizar objetos usando tipos também é algo que envolve uma parte mais conceitual, pois geralmente envolve interfaces (ou classes abstratas), que são defininidas como tipos esperados para serem passados como parâmetro, que na prática vão ser as implementações dessas mesmas interfaces (ou classes abstratas).

## Voltando ao exemplo do vídeogame

Se voltarmos para o exemplo prático do artigo anterior videogame, uma pessoa iria jogar o videogame e utilizar a operação de ligar um videogame.  Segue uma classe para representar essa pessoa que vai utilizar a interface `Videogame` que continha o método `ligar`.

```php
<?php

class PessoaQueJogaVideogame
{

    private $videogame;

    public function __construct(
        Videogame $videogame
    ){

        $this->videogame = $videogame

    }

    public function jogar(): void
    {

       try {
            $this->videogame->ligar();
       } catch (Exception $e) {
           echo 'Parece que o videogame não ligou.';
       }

    }

}
```

Como a classe `PessoaQueJogaVideogame` define a interface `Videogame` como parâmetro esperado no seu construtor, o type hinting é feito com essa interface como tipo definido. Com isso, é possível trocar de implementação a qualquer momento livremente, pois esperar uma interface como parâmetro permite que qualquer implementação dessa interface seja passada via esse parãmetro e usada. Por exemplo:

```php
<?php

/**
 *
 * Passando a implementação MeuVideoGameObsoleto
 * da interface para a classe PessoaQueJogaVideogame
 *
 */
$pessoaQueJoga = new PessoaQueJogaVideogame(
    new MeuVideoGameObsoleto
);

// Jogando com videogame velho.
$pessoaQueJoga->jogar();

/**
 *
 * Passando a implementação VideoGameNovo
 * da interface para a classe PessoaQueJogaVideogame
 *
 */
$pessoaQueJoga = new PessoaQueJogaVideogame(
    new VideoGameNovo
);

// Jogando com videogame novo.
$pessoaQueJoga->jogar();
```

Devido a essa flexibilidade de trabalhar com a interface, a classe `PessoaQueJogaVideogame` pode receber tanto uma instância da classe `MeuVideoGameObsoleto` quanto uma instância da classe `VideoGameNovo` ou qualquer outra nova implementação criada que implemente a interface `Videogame`, pois a possibilidade de criar implementações é infinita.

## Juntando as práticas mostradas (e chegando na injeção de dependência)

O que aconteceu no exemplo mostrado foi que a classe `PessoaQueJogaVideogame` está trabalhando através de um parâmetro que define uma interface como tipo esperado. Essa parametrização com uma interface como tipo está abstraindo os detalhes através do uso dessa interface, com isso diferentes implementações dessa interface poderão ser passadas via esse parâmetro definido (o que gerada a liberdade para trocar de implementação).

Basicamente, é juntar os conceitos de abstração e interface com a parâmetrização de objetos. Definir interfaces como os tipos esperados dos parâmetros é uma das práticas essenciais para ter baixo acoplamento no código, além disso, toda a parametrização de objetos feita nesse artigo é um exemplo prático do conceito de injeção de dependência.