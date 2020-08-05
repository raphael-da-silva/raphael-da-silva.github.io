---
layout: post
title: POO - Explicando acoplamento com sofrimento mental
---

Flexibilidade mental é essencial para não ficar preso a pensamentos e comportamentos que levam ao sofrimento. Eu sofri muito mentalmente por ficar preso por uma inflexibilidade mental que me prejudicou ao lidar com a realidade e me adaptar a vida.

No contexto da orientação a objeto, a inflexibilidade mental pode ser comparada com o acaplamento no código. Essa é uma analogia que pode explicar a "dor de cabeça" que um código acoplado pode gerar. A classe `Pessoa` representa uma pessoa, o problema surge quando ela está acoplada. Segue a classe em questão:

```php

// Author: Raphael da Silva
class Pessoa
{

    public function viver()
    {

        $inconformacao = new Inconformacao;
        $inconformacao->ativar();

    }

}
```

No método `viver` existe um acoplamento com a classe `Inconformacao`, essa classe representa um sentimento. Uma pessoa inconformada vai sofrer muito, pois nunca via deixar para trás o que aconteceu de ruim com ela. Ficar preso a esse sofrimento é algo massacrante.

Para resolver isso, é precisa se desapegar da informação, trazudindo isso para o código signigica que a classe `Pessoa` não pode ficar presa (acoplada) a classe `Inconformacao`. Para fazer isso na prática, é precivo passá-la como parâmetro (com injeção de dependência) através de uma abstração para possibilitar a troca de implementações.

A abstração será feita através de uma interface, ela vai representar um sentimento, não importando qual sentimento seja. Segue a interface e a classe `Inconformacao` implementamdo essa nova interface criada.

```php

// Author: Raphael da Silva
interface Sentimento
{

    public function ativar();

}

class Inconformacao implements Sentimento
{

    public function ativar()
    {

        echo 'A inconformação será levada para todo lugar e vair atrapalhar.';

    }

}
```

Agora que a interface foi criada (junto com uma implementação dela), a classe `Pessoa` ela precisa receber como parâmetro a outra classe que vai usar, ou seja, é preciso remover a criação direta (e acoplada) da instância da classe `Inconformacao`.

```php

// Author: Raphael da Silva
class Pessoa
{

    private $sentimento;

    public function __construct(
        Sentimento $sentimento
    ){

        $this->sentimento = $sentimento;

    }

    public function viver()
    {

        $this->sentimento->ativar();

    }

}
```

Agora a pessoa pode ter qualquer sentimento, inclusive os bons. Isso elimina a sua dependência com sentimentos específicos, inclusive os ruins. Sem flexibilidade uma pessoa sofre, pois ficar preso a sentimentos pode ser muito destrutivo. 

Essa analogia entre acoplamento e flexibilidade mental foi uma forma que encontrei de explicar sobre acoplamento e flexiblidade no código através de experiências que tive. Para acabar com a inconformação de vez, será criada uma nova classe, agora representando um sentimento positivo. 

```php

// Author: Raphael da Silva
class BemEstar implements Sentimento
{

    public function ativar()
    {

        echo 'Com bem-estar as coisas ficam melhores :)';

    }

}

// Agora a pessoa pode viver com bem-estar como sentimento
$pessoaMentalmenteSaudavel = new Pessoa(
    new BemEstar
);

$pessoaMentalmenteSaudavel->viver();
```

É importante não ficar preso (leia-se acoplado) a algo, isso vale para o código-fonte e, principalmente, para a vida.