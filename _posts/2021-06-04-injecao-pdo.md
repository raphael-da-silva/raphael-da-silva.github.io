---
layout: post
title: POO - Injetar classes concretas é sempre um problema? E a PDO?
---

Nem sempre é preciso de construções de linguagem para criar abstrações, em outras palavras, nem sempre é necessário de uma inferface ou uma classe abstrata. Quando a classe concreta faz uma abstração, injetá-la é ainda é estar trabalhando de forma flexível. Ou seja, nesse tipo de situação uma classe concreta já é uma abstração suficiente.

Por exemplo, injetar a ```PDO``` em uma outra classe não é um problema, pois ela abstrai detalhes mesmo sendo uma classe concreta. Ao usá-la a troca de drivers de banco de dados é abstraída da classe que usa ela, portanto está sendo injetada uma abstração, pois a essência do conceito está ali.

No exemplo a seguir, a classe ```ProdutosDoBancoDeDados``` depende da PDO, ou seja, ela trabalha como uma abstração de banco de dados, mesmo que essa abstração seja feita através de uma classe concreta.

```php
<?php

class ProdutosDoBancoDeDados
{

    private $pdo;

    public function __construct(
        PDO $pdo
    ){

        $this->pdo = $pdo;

    }

    public function buscar($id): array
    {

        $sql  = 'SELECT * FROM produtos WHERE id = :id';
        $stmt = $this->pdo->prepare($sql);
        $stmt->execute([':id' => $id]);

        return $stmt->fetch(PDO::FETCH_ASSOC);

    }

}
```

Quando uma classe concreta é abstrata o suficiente como no caso da ```PDO```, ela serve como uma amostra que programar para abstrações é programar para um código que expõe funcionalidades sem revelar detalhes em seus métodos expostos, independente se esse código é uma interface, classe abstrata ou até mesmo uma classe concreta (como nesses casos específicos onde a `PDO` serve de exemplo).

## Classes concretas, interfaces e classes abstratas

A `PDO`, apesar de ser uma classe concreta, faz com quem dependa dela trabalhe com uma abstração, já que ela oculta detalhes sobre o driver de conexão com o banco de dados que é utilizado. Isso ilustra bem um caso onde se trabalha de forma abstraída, mesmo sem utilizar uma construção de linguagem para isso ([interface ou classe abstrata](https://raphael-da-silva.github.io/interfaces-classes-abstratas/)), mostrando que é possível trabalhar com uma abstração até mesmo com uma classe concreta.

Esse tipo de situação da `PDO` mostra que em alguns casos injetar uma classe concreta ainda possibilita que se programe para uma abstração. Isso deixa evidente que trabalhar abstrações não depende de uma construção de linguagem fornecida por uma linguagem de programação, pois a abstração é algo conceitual.

Interface e classes abstratas são mais uma formalidade para trabalhar com 
abstrações do que recursos obrigatórios para a aplicação desse conceito. O
exemplo da PDO mostra que eles não são obrigatórios para se ter abstração no 
código.

## Referências

Este post surgiu de uma observação feita pelo desenvolver João Batista Neto em um hangout sobre Orientação a Objetos no Youtube onde era discutido sobre dependender de abstrações. Ele chamar a atenção para o caso (fora da curva) da PDO e a natureza do seu código me instigou a refletir e escrever detalhadamente sobre o tema.

<!-- ADD link do youtube -->
