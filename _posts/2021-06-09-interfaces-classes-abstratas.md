---
layout: post
title: Interfaces e classes abstratas
---

As linguagens de programação fornecem recursos para abstrair operações no paradigma de Orientação a Objetos, esses recursos são interfaces e classes abstratas. Com elas é possível representar a ideia (ou noção básica) de uma operação sem conter nenhuma implementação (no caso das interfaces) ou somente com implementações mais genéricas somadas a métodos abstratos sem nenhuma implementação (no caso das classes abstratas).

A diferença técnica entre interfaces e classes abstratas está no fato de que uma interface não contém nenhuma implementação no corpo dos seus métodos enquanto uma classe abstrata pode conter métodos comuns (com implementação), já que apenas os seus métodos definidos abstratos não terão nenhuma implementação (sendo implementados pela classe que estender/derivar a classe abstrata em questão). 

Nada impede de uma classe abstrata ter só métodos abstratos, mas isso faria ela poder dar lugar a uma interface, que tem todos os métodos de uma interface são puramente abstratos (sem implementação) por padrão.

O autor Joshua Block sintetiza isso de forma muito eficiente no seu livro _Effective Java_:

<!--  The  most obvious  difference  between  the  two  mechanisms  is  that  abstract  classes  are  permitted  to  contain  implementations  for  some  methods  while  interfaces  are  not.  -->

> A diferença mais óbvia entre esses dois mecanismos é que classes abstratas permitem conter implementação para alguns métodos enquando interfaces não. (BLOCH, 2008, p.93, tradução nossa)

A ferramenta que mais gosto são as interfaces, mas é válido lembrar das classes abstratas como mais uma ferramenta disponível na criação e representação de abstrações e a construção de um código mais flexível (variando essas implementações). Quanto mais ferramentas, mais opções dá para ter na manga. Uma coisa não exclui a outra.

### Referências

* BLOCH, Joshua. Effective Java: Second Edition. Edição 2.

***

### 💀💀💀 Case Closed: é isso... 💀💀💀

Gosto muito do grupo de Rap Cypress Hill (💀💀💀), existe uma música deles chamada "Case Closed", que traduzindo significa "Caso Encerrado". Referenciei o nome dessa música para encerrar esse artigo. 

Caso encerrado (aka Case Closed)!!!!

![cypress cover](https://i.scdn.co/image/ab67616d0000b2734e51c518e787896bc8cdb1a5)