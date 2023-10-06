---
layout: post
title: "Interfaces + classes abstratas: recursos para criar abstrações"
---

As linguagens de programação fornecem recursos para abstrair operações no paradigma de Orientação a Objetos, esses recursos são interfaces e classes abstratas. Com elas é possível representar a ideia (ou noção básica) de uma operação sem conter nenhuma implementação (no caso das interfaces) ou somente com implementações mais genéricas somadas a métodos abstratos sem nenhuma implementação (no caso das classes abstratas).

A diferença técnica entre interfaces e classes abstratas está no fato de que uma interface não contém nenhuma implementação no corpo dos seus métodos enquanto uma classe abstrata pode conter métodos comuns (com implementação), já que apenas os seus métodos definidos abstratos não terão nenhuma implementação (sendo implementados pela classe que estender/derivar a classe abstrata em questão). 

Uma interface é um código que tem um nível mais alto de abstração, pois representa e expõe apenas as operações de uma funcionalidade sem conter nenhum tipo de implementação, o que não acontece nas classes abstratas, já que elas que podem carregar consigo algum tipo de implementação mais genérica junto com seus métodos abstratos.

Nada impede de uma classe abstrata ter só métodos abstratos, mas isso faria ela poder dar lugar a uma interface, que tem todos os métodos de uma interface são puramente abstratos (sem implementação) por padrão.

O autor Joshua Block sintetiza isso de forma muito eficiente no seu livro _Effective Java_:

<!--  The  most obvious  difference  between  the  two  mechanisms  is  that  abstract  classes  are  permitted  to  contain  implementations  for  some  methods  while  interfaces  are  not.  -->

> A diferença mais óbvia entre esses dois mecanismos é que classes abstratas permitem conter implementação para alguns métodos enquando interfaces não. (BLOCH, 2008, p.93, tradução nossa)

A ferramenta que mais gosto são as interfaces, mas é válido lembrar das classes abstratas como mais uma ferramenta disponível na criação e representação de abstrações e a construção de um código mais flexível (variando essas implementações). Quanto mais ferramentas, mais opções dá para ter na manga. Uma coisa não exclui a outra.

### Quando nem tudo precisar variar

Uma interface é útil quando é necessário criar implementações completamente diferentes. Só que também existem os casos onde apenas determinadas métodos de uma classe devem ser livre para permitir diferentes implementações, neste tipo de situação utilizar uma classe abstrata já é o suficiente, pois ela permite que apenas os métodos abstratos possam receber diferentes implementações (e não necessariamente a classe inteira).

### Código abstrato vs. Implementação: o que cada um abrange

Depender de um código mais abstrato, como é feito com o uso de interfaces ou classes abstratas, possibilita que uma implementação dessa dessa interface/classe abstrata seja trocada por outra implementação diferente, sendo essa a principal vantagem de trabalhar a relação dos objetos dependendo de abstrações.

Já depender de uma implementação é algo mais limitado conceitualmente e tecnicamente, já que a implementação se limita a algo mais específico (conceitualmente menos abrangente) que faz algo na prática mais específico (tecnicamente).

Por exemplo, uma abstração poderia definir a leitura de um arquivo de forma bem ampla, enquanto uma impleementação poderia ser uma leitura de arquivo em JSON, que é uma leitura bem mais restrita, já que está limitada a um formato de arquivo específico (no caso JSON).

Resumidamente, o código concreto (ou seja, a implementação) está restringido a trabalhar com os detalhes específicos que ele aborda, logo se torna uma opção mais limitada e, consequentemente, menos flexível. Já a abstração é o contrário, já é mais ampla, logo dá mais opções e, consequentemente, mais liberdade para operar dentro desse leque mais amplo de possibilidades.

Por fim, depender de um código abstrato é diferente de depender de uma implementação específica, e essa diferença está no que cada tipo de código aborda e os limites que cada tipo de dependência oferece na prática (onde um é mais abrangente/amplo e outro restringe mais).

### Sem focar em detalhes

Os detalhes de uma implementação não são relevantes para esses recursos (interfaces + classes abstratas), pois algo abstrato não leva detalhes específicos em consideração e sim a essência de uma operação. O motivo crucial para [não conter detalhes em abstrações](https://raphael-da-silva.github.io/evitando-detalhes-de-implementacao-interfaces/) é evitar que o código fique preso a uma determinada implementação e, consequentemente, não consiga variá-la/trocá-la depois.

### Formalidade + Exceção da regra

Apesar da existência de classes abstratas e interfaces, uma abstração é algo que está em um nível muito mais conceitual que de código, portanto a aplicação dela não depende desses recursos para ser aplicada. 

Interfaces e classes abstratas são mais uma formalidade das linguagens de programação para trabalhar com abstrações do que recursos obrigatórios para a aplicação desse conceito. Abstrair é uma tarefa mental que não obriga o uso de um recurso da linguagem de programação para ser colocada em prática.

A `PDO` é um exemplo disso, pois é uma classe que é uma abstração mesmo sendo uma classe concreta e não um desses recursos (aka construção de linguagem) para criar uma abstração (interface e classe abstrata). Com isso, ela é uma exceção curiosa, [escrevi sobre isso nesse post](https://raphael-da-silva.github.io/injecao-pdo/).

### Referências

* BLOCH, Joshua. Effective Java: Second Edition. Edição 2.