---
layout: post
title: Distinguindo diferentes conceitos (organizando mentalmente as coisas)
---

Como a injeção de dependência anda de mãos dadas com outros conceitos, ela acaba gerando uma confusão grande (pelo menos, para mim gerou no início dos meus estudos). Além disso, existem ferramentas como containers que, a primeira vista, parecem sinônimos da injeção de dependência, mas que são só ferramentas auxiliares para ajudar na aplicação de um conceito (e não garatem por si só a aplicação desses conceitos).

### Injeção de dependência vs. Inversão de dependência

O conceito de injeção de dependência pode se confundir com o princípio da inversão de dependência por causa da sua nomenclatura semelhante e por esses conceitos serem bastante ligados. No entanto, são conceitos diferentes e é importante separá-los para utilizá-los de forma correta.

De maneira simplificada, injetar as dependências é passar objetos como parâmetro, isso vale fazendo uso de abstrações ou não. Já inverter a dependência envolve depender necessariamente de abstrações através da aplicação um princípio que é muito conceitual.

Sabendo disso, a injeção de dependência pode ser usada para aplicar o princípio da inversão de dependência, mas ela não garante que o princípio seja seguido, pois para segui-lo é necessário depender de abstrações. Ou seja, a injeção de dependência deve ser utilizada com abstrações, pois uma das ideias básicas desse princípio é fazer que os objetos dependam de abstrações. Injeção de dependência não garante a aplicação do princípio, assim como usar interfaces por si só não garatem uma abstração correta.

## Containers de injeção de dependência

Os containers de injeção de dependência instanciam os objetos de uma aplicação injetando as dependências necessárias para a criação do objeto, sabendo disso **é preciso deixar nítida uma coisa: o container não é a mesma coisa que a injeção de dependência.**

Apesar de serem assuntos que andam juntos, eles tem conceitos e propósitos diferentes, pois injeção de dependência é a técnica utilizada para ter flexibilidade na relação entre os objetos, já o container é a ferramenta utilizada para facilitar a criação de objetos que tem as suas dependências injetadas através dessa técnica. Em outras palavras, a injeção de dependência são os fins enquanto o container são uns dos meios disponíveis para faciliar a chegada nesses fins.

No PHP existe uma biblioteca chamada Pimple, essa biblioteca fornece uma classe que serve como container para registrar os objetos e suas dependências. No exemplo a seguir o container está sendo utilizado para definir a criação de objetos com suas respectivas dependências.

```php
<?php

$container = new \Pimple\Container;

/**
 *
 * Sobre a sintaxe do container:
 * O container pode ser acessado como um array porque ele implementa a interface ArrayAccess que é nativa do PHP e permite fazer isso.
 *
 */

$container['BuscaDeProdutos'] = function($container){

    return new BuscaDeProdutosDeJSON('produtos.json');

};

$container['ImpressaoDeProdutos'] ($container){

    return new ImpressaoDeProdutos(
        $container['BuscaDeProdutos']
    );

};
```

Quando uma instância da classe `ImpressaoDeProdutos` ser obtida através do container, ela já virá com uma instância da classe `BuscaDeProdutosDeJSON` injetada como sua dependência. Isso é possível porque o container executa as funções anônimas registradas nele recursivamente, ou seja, a primeira função anônima executada chama a segunda (através do container) e assim sucessivamente.

Basicamente, o container é uma ferramenta que realiza a construção de objetos já configurados para serem utilizados, pois ele instância todas as dependências de um objeto e as dependências dessas dependências para formar toda a árvore de dependêcia dos objetos.

## A confusão entre diferentes conceitos que estão relacionados

Além da confusão entre injeção de dependência e inversão de dependência, também existe uma confusão relacionada aos containers. Durante meu aprendizado desses conceitos, eu tive uma necessidade de separá-los bem na minha cabeça para saber usá-los sem confundir achando que tudo é a mesma coisa.

Por isso, acho importante importante distinguir todos esses conceitos de forma nítida e objetiva. De forma resumida, a relação entre os conceitos na prática acontence através dos seguintes passos:

* Uma classe inverte a dependência ao depender de uma abstração.
* Uma implementação concreta da abstração é injetada através da injeção de dependência.
* O container é usado para criar os objetos já com as suas dependências injetadas.

Nos passos mostrados o uso de um container é opcional, já que ele é apenas uma ferramenta para instânciar objetos que seguem a injeção de dependência, não sendo obrigatórios para injetar os objetos.

### A nomenclatura dos containers ajudando a confundir

Geralmente, os containers disponíveis no mercado recebem os nomes desses conceitos e, por isso, podem gerar uma confusão no uso e separação conceitual da coisas. Meu objetivo com esse artigo é descomplicar e seperar essas coisas que eram confusas para mim no início, é uma tentativa de expor os conceitos através de uma linguagem mais nítida e transparente.