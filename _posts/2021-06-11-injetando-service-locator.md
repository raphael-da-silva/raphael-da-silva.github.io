---
layout: post
title: A injeção de containers como dependência (a.k.a Service Locator)
---

Existe uma prática que é injetar um container (de injeção de dependência) inteiro em um objeto e obter suas dependências através dele, isso é considerado um anti-pattern chamado Service Locator. 

O uso do Service Locator não é muito considerado uma boa prática, pois tira a transparência da injeção de dependência direta que mostra nitidamente de quais objetos um objeto depende (adicionando um nível de complexidade extra entre a relação dos objetos, tornando elas indiretas). 

### O uso de Service Locator

Service Locator é um padrão que utiliza um container para obter as dependências necessárias para um objeto, com isso se evita a criação direta dessas dependências. Apesar do acoplamento da criação direta de um objeto ser evitado, o Service Locator não oferece tantas vantagens assim e, por isso, é considerado um anti-pattern.

O primeiro problema é que Service Locator faz com que as classes fiquem forçadas a usar esse padrão, ou seja, para reaproveitar as classes será necessário usar um Service Locator e isso pode dificultar o reúso de classes em contextos diferentes (e até projetos em diferentes). 

No exemplo a seguir, a classe `ImpressaoProdutos` precisaria de um container para ser portada para outro projeto, o que dificulta o seu reaproveitamento, já que ela depende de um container completo que tem que ser levado junto com ela (adicionando uma complexidade que se transforma em um "peso" que tem que ser carregado junto).

```php
<?php

use Pimple\Container;

/**
 *
 * Exemplo para ilustrar os problemas do padrão Service Locator.
 * @author Raphael da Silva
 *
 */
class ImpressaoProdutos
{

    private $container;

    public function __construct(
        Container $container
    ){

        $this->container = $container

    }

    public function imprimir(): void
    {

        $busca = $this->container['BuscaDeProdutos'];

        foreach($busca->buscar() as $produto){
            echo $produto['nome'], PHP_EOL;
            echo $produto['descricao'], PHP_EOL;
        }

    }

}
```

Outro problema de injetar o container completo, é que os objetos não declaram as suas dependências explicitamente, isso reduz a legibilidade devido ao fato de as dependências ficarem implícitas. Além disso, também não existe a garantia de que o objeto obtido através do container seja do tipo esperado (perdendo o benefício do type hinting). 

Isso poderia ser resolvido com um container menos genérico que retorne o tipo abstrato `BuscaDeProdutos` usando a tipagem de retorno do PHP 7, só que a ainda existiria uma dependência do container e a forma de obter os objetos ainda seria indireta e pouco transparente.

Para evitar essas desvantagens do uso do Service Locator na classe `ImpressaoProdutos`, usar a injeção de dependência passando o objeto que ela precisa diretamente é uma alternativa muito mais transparente e, portanto, melhor. 

Segue a classe com aplicação da injeção de dependência direta (via construtor) eliminando a necessidade de um container inteiro ser passado para ela e, com isso, deixando a sua dependência nítida no seu construtor.

```php
<?php

/**
 *
 * Exemplo para ilustrar a injeçaõ de dependência 
 * substituindo o Service Locator.
 * @author Raphael da Silva
 *
 */
class ImpressaoProdutos
{

    private $buscaProdutos;

    public function __construct(
        BuscaDeProdutos $buscaProdutos
    ){

        $this->buscaProdutos = $buscaProdutos;

    }

    public function imprimir(): void
    {

        foreach($this->buscaProdutos->buscar() as $produto){
            echo $produto['nome'], PHP_EOL;
            echo $produto['descricao'], PHP_EOL;
        }

    }

}
```

Injetar as dependências diretamente tira a necessidade de usar o container inteiro no objeto e, com isso, oferece muito mais flexibilidade, além de deixar a dependência necessária para o objeto explícita/transparente no seu código-fonte, por isso injetar os objetos necessários diretamente é melhor do que injetar o container inteiro criando um Service Locator.

### Para tudo existe uma exceção

O único uso válido que consegui enxergar de Service Locator é quando por algum motivo é preciso obter os objetos dinâmicamente, para isso o container injetado pode ser usado para resolver a criação desses objetos com toda sua complexidade e necessidade dinâmica. 

Um dispatcher que instância controllers dinâmicamente (de acordo com a rota informada) dentro de uma arquitetura MVC é um exemplo desse uso para um Service Locator, pois ele precisa criar controllers dinâmicamente e o Service Locator pode ser usado para obter dinâmicamente os objetos dos controllers que foram registrados no container para executá-los de acordo com a rota vinda da URL. 

Esse foi um uso que acabei enxergando enquanto fazia um Dispatcher de uma arquitetura MVC para entender o funcionamento dos frameworks. Fora esses casos específicos, injetar as dependências de forma simples, direta e transparente é uma opção melhor do que injetar o container inteiro, essa injeção simples traz muito mais efeitos saudáveis para o código e não tem esses efeitos limitantes que dificutam as coisas.

### Conclusão

Enfim, existem casos válidos para usar esse conceito ao mesmo tempo que seu uso pode ser bem problemático, portanto chamar eles de antipattern é muito mais um reflexo de um mal uso de um padrão do que o padrão ser um problema por si só. Existem discussões na internet com blogs chamando de anti-patter e outros dizendo que não é, acho mais válido ponderar as características do que afirmar o que é certo ou errado.

### Referências 

* https://www.lambda3.com.br/2009/04/injecao-de-dependencia-ou-service-locator/