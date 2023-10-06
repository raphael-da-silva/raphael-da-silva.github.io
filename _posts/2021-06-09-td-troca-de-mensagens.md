---
layout: post
title: "Comunicação + relacionamento: a troca de mensagem entre os objetos"
---

A Orientação a Objetos é um paradigma de programação que realiza as funcionalidades de um software através de objetos que se comunicam  incentivando o fechamento de escopo e a troca de objetos de maneira flexível. O fechamento de escopo se dá pelo encapsulamento, a troca de objetos de maneira de flexível pode se dar com abstrações+injeção de dependência, já a comunicação entre os objetos se dá através do conceito de troca de mensagem.

A troca de mensagem (_message passing_) é o termo utilizado para definir a comunicação entre objetos dentro de um software. Basicamente, consiste na chamada de [métodos](https://raphael-da-silva.github.io/td-assinatura-metodo) e passagem de dados de um objeto pelo outro para formar em conjunto todo o funcionamento de um software.

No livro "Design Patterns: Elements of Reusable Object-Oriented Software" a relação com objetos é sintetizada:

<!--
> An object packages both data and the procedures that operate on that data. The procedures are typically called methods or operations. An object performs an operation when it receives a request (or message) from a client. 
-->

> Um objeto empacota dados e procecimentos que operam nesses dados. Os procedimentos são tipicamente chamados de métodos ou operações. Um objeto performa a operação quando recebe uma requisição (ou mensagem) vinda de um cliente. (GAMMA et al., 1994, p.24, tradução nossa)

Nesse fluxo de relacionamentos dos objetos a citação termina mencionando o termo "cliente", que é o objeto que chama/executa um outro objeto para realizar uma operação, por requisitar o funcionamento de um outro objeto, o termo dado para o objeto requisitor é cliente. Esse é o fluxo e as partes que geram a troca de mensagem entre objetos.

### Referências

* GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; Vlissides, John. Design Patterns: Elements of Reusable Object-Oriented Software. Edição 1.
