---
layout: post
title: Factory estática em prol da legibilidade
---

O uso de métodos estáticos é algo controverso dentro da POO (aka Programação Orientada a Objetos), pois ele gera acoplamento quando usado nas relações de dependências, nesse caso é mais adequado substituir o código estático por injeção de dependência. No entanto, demonizar o código estático acaba sendo um tom recorrente, o que não acho algo muito bom, já que existem usos bons de código estático em algumas situações: um exemplo recorrente é para criar factorys. 

<!--
One advantage of static factory methods is that, unlike constructors, they
have names. If the parameters to a constructor do not, in and of themselves,
describe the object being returned, a static factory with a well-chosen name is easier to use and the resulting client code easier to read. -->

> Uma vantagem de factory com métodos estáticos é que, diferente de construtores, elas tem nomes. [...] uma factory estática com um nome bem escolhido é mais fácil de usar e o código resultante do cliente é mais fácil de ler. (BLOCH, 2008, p.5, tradução nossa)

Lembrando que o termo "cliente" usado pelo autor na citação se refere a quem consome o código, ou seja, é o objeto que está fazendo uso da factory estática (consumindo ela). Cliente é um termo bastante usado na orientação a objetos para tratar das relações entre dependências e é parte do vocabulário quando se lida com objetos.

A vantagem da factory estática destacada na citação é a legibilidade, pois ela podem dar nomes mais intuitivos e explicativos para criar objetos do que simplesmente ```new```. Por exemplo, um método estático ```criarNovoPostParaBlog``` é mais explicativo do que ```new Post```, pois a assinatura do método estático está dando um nome mais compreensivel/legível para o construtor que só gera um `new`.

### Os tipos de objetos criados pelas factories

Um exemplo desse tipo uso de factories é para criar objetos simples como entidades (aka entity) e value objects. Esses objetos não vão precisar ser injetados, pois não são dependências, mas sim representações das regras de negócio. Portanto, podem eles ser criados através uma factory com código estático sem que isso seja um problema de acoplamento alto que tira a flexibilidade do código (e que precisará ser trocado). 

Esse foi um valor para o código estático que só percebi depois de entender o valor desses objetos simples (entidades e value objects) quanto tentei estudar sobre o básico de DDD e separação de camadas. Foi começar a usar esses objetos para dar contexto e legibilidade para as regras de negócio que o uso desse tipo de factory deu ainda mais contexto e legibilidade para tudo.

### Referências

* BLOCH, Joshua. Effective Java: Second Edition. Edição 2.