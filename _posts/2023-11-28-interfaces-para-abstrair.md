---
layout: post
title: Interfaces para abstrair as operações de objetos e variar/trocar as implementações
date: 2023-11-28
---

Neste artigo será mostrada a aplicação prática do uso de interfaces para abstrair operações, pois elas são uma ferramenta/instrumento útil e valioso para fazer isso quando são concebidas se despreendendo dos detalhes específicos das operações que carregam. E se despreender dos detalhes é abstrair os detalhes e trabalhar só com as noções das operações.

## Noção indefinida da operação

Quando uma pessoa vai jogar videogame para ter um passatempo é necessário ligar o aparelho para começar a jogar. A forma como cada aparelho de videogame é ligado é um detalhe específico de cada modelo e esse tipo de detalhe não importa para quem liga o videogame, pois quem vai ligá-lo só precisa ter uma noção básica (e abstrata) do que essa ação/operação (ligar) faz para usar ela, é só disso que se precisa **depender** (e essa noção é o que aparece quando se trabalha com **injeção de dependência**).

A seguir está uma inferface criada para abstrair a operação em questão. Ela será a ferramenta usada para trabalhar com a abstração da operação de ligar um videogame.

```php
<?php

interface Videogame
{

    public function ligar(): void;

}
```

A interface `Videogame` não leva em consideração os detalhes de como um videogame é ligado, por isso ela define apenas o método referente a essa operação de ligar o videogame, pois o que importa é definir essa operação na sua essência (sem detalhes) e não como ela vai ser feita (implementada) na prática com detalhes específicos.

## Definindo as implementações da interface criada

Uma implementação desta interface é onde estariam os detalhes específicos, mas quem for utilizar/depender da interface não vai lidar com esses detalhes, pois a interface irá estar entre a implementação e quem for utilizar/depender da implementação. A seguir está o exemplo de uma implementação para a interface em questão.

```php
<?php

class MeuVideoGameObsoleto implements Videogame
{

    private $ligaSeTiverSorte;

    private const AZAR  = 0;
    private const SORTE = 1;

    public function __construct()
    {

        $this->ligaSeTiverSorte = rand(self::AZAR, self::SORTE);

    }

    public function ligar(): void
    {

        if(!$this->ligaSeTiverSorte){
            throw new RuntimeException('Dessa vez não ligou.');
        }

        echo 'Dessa vez o videogame ligou, que sorte!!!';

    }

}
```

Como é possível perceber, essa classe trata de um tipo de videogame específico que contém a operação `ligar`, ou seja, essa classe é uma implementação que contém os detalhes de como a operação é feita de forma concreta na prática (definindo o que estava indefinido na interface). 

Além dessa implementação, poderiam ser criadas várias outras classes diferentes que implementam essa mesma interface `Videogame` representando videogames específicos com o mesmo método `ligar`, cada implementação tendo seus detalhes específicos.

Por exemplo, imagine um videogame novo que funciona sem dar problema nenhum, mas que implementa a mesma interface `Videogame`. Segue uma implementação da interface para representar esse cenário.

```php
<?php

class VideoGameNovo implements Videogame
{

    private $voltagem;

    private const VOLTAGEM_MINIMA = 127;
    private const VOLTAGEM_MAXIMA = 220;

    public function __construct(
        int $voltagem
    ){

        $this->voltagem = $voltagem;

    }

    private function estaDentroDaVoltagemEsperada(): bool
    {

        return (
            $this->voltagem >= self::VOLTAGEM_MINIMA and 
            $this->voltagem <= self::VOLTAGEM_MAXIMA
        );

    }

    public function ligar(): void
    {

        if(!$this->estaDentroDaVoltagemEsperada()){
            throw new Exception('Voltagem errada, não ligou.');
        }

        echo 'Ligou e está funcionando bem demais!';

    }

}
```

## Infinitas implementações da mesma interface

Uma interface trabalha em cima da noção básica de uma operação, com isso ela fornece a possibilidade para criar qualquer implementação a partir dessa noção básica mais abstrata.

Basicamente, ao usar a interface `Videogame` no exemplo aprensentado **a possibilidade de criar novas implementações é infinita**. Esse é o tipo de flexibilidade que é obtida ao usar uma interface para abstrair os detalhes de uma operação. **Usar uma interface é abrir o caminho para usar qualquer implementação, por isso ela é uma ferramenta/instrumento valioso.**

A fórmula a seguir é uma maneira de decompor a vantagem obtida com o uso de uma interface.

**Interfaces + abstração de operações = várias formas de fazer a mesma coisa**

Outro aspecto vantajoso de usar interfaces pode ser representado com essa outra fórmula:

**Várias implementações = várias possibilidades = liberdade de troca**

A criação de novas implementações de uma mesma interface permite a troca delas para mudar o comportamento dos objetos. A vantagem aqui se traduz através de uma palavra-chave: **flexibilidade**. Ao utilizar abstrações a mudança/troca de implementações é facilitada, consequentemente isso deixa o código mais flexível/maleável. 

Esse tipo de vantagem é crucial para deixar o código com a manutenção mais fácil, pois ele se torna mais adaptável a mudanças (tendo um nível baixo de acoplamento). Com isso, a flexibilidade um ponto-chave: **liberdade de troca**.

Os conceitos de interface e abstração são muito vantajosos quando usados como os tipos definidos e esperados em parâmetros dos métodos dos objetos, pois ao definir uma interface que abstraí operações como parâmetro os detalhes de uma implementação estão sendo abstraídos.

### Referências

[Hangout sobre OOD - Princípio da inversão de dependências](https://www.youtube.com/watch?v=RCbJxgAkehY)