---
layout: post
title: "Ensaio: programar para interface, mas para qual sentido do termo interface?"
---

Na minha cabeça eu tive uma confusão entre o termo interface sendo usado em diferentes contextos, isso me levou a ter uma obsessão em distiguir os sentidos das coisas na minha cabeça.

Em um lugar o termo se refere a API (métodos públicos), em outros lugares se refere a recursos/construções das linguagens, mas ainda parece existir um uso mais amplo do termo: que é se referir a abstrações.

## O que é uma interface?

Uma interface contém as operações que serão expostas de um objeto, essas operações são utilizadas por outros objetos fazendo a troca de mensagem entre eles e, com isso, formando o funcionamento de um software construído com Orientação a Objetos.

Resumidamente, uma interface é o que um objeto expõe para se comunicar e fazer com que objetos se relacionem.

<!-- The set of all signatures defined by an object's operation is called the interface to the object.
 -->

> O conjunto de todas as assinaturas definidas pelas operações de um objeto é chamado de interface do objeto. (GAMMA et al., 1994, p.13, tradução nossa)

A citação acima vem do livro *Design patterns: elements of reusable object oriented software* e define bem o que é uma interface, só que é uma definição bem ampla. Essa exposição de operações está nos mais recorrentes sentidos da palavra interface.

## Os sentidos do termo interface

<!--
The term API, which is short for applica-tion programming interface, is used in preference to the otherwise preferable term interface  to  avoid  confusion  with  the  language  construct  of  that  name. (BLOCH, 2018, p.4, tradução nossa)

-->

> O termo API, que é uma abreviação para Application Programming Interface, é usado em preferência ao termo interface para evitar confusão com a construção de linguagem com esse nome.

Essa citação é muito útil para evitar confusão e mostrar dois dos sentidos do termo interface, pois deixa explicíto que a palavra é usada com sentidos diferentes (API e construção de linguagem). Nos meus estudos tive contato com conteúdos usando o termo com vários sentidos. Parecem existir uns 3 usos comuns para o termo interface, eles são:

* Interface para se referir a uma API (Application Programming Interface).
* Interface para se referir a abstrações (tipos abstratos usados).
* Interface para se refetir a construção de linguagem (palavra reservada).

Sabendo disso, irei criar nomes próprios para apontar para esses sentidos e deixá-los expostos, expostos tal qual uma interface (como uma interface gráfica, que é um outro sentido dessa mesma palavra). Seguem os nomes que serão usados nesse artigo.

* Interface->API = interface como API.
* Interface->Abstração = interface como abstração
* Interface->RecursoDasLinguagens = interface como construção de linguagem.

Um dos sentidos da palavra interface está em uma das ideiais mais difundidas no paradigma: programar para interfaces.

## Programar para qual interface?

<!-- Program to an interface, not an implementation. -->

> Programe para uma interface e não para uma implementação. (GAMMA et al., 1994, p. 18, tradução nossa)

Agora vem o ponto que a confusão dessa mentalidade de programar para interface: interface parece um conceito mais amplo do que o recurso existente nas linguagens de programção, ou seja, o termo interface não é bem o que parece a primeira vista, ele parece que vai além da construção de linguagem interface.

Programar para uma interface é um dos conceitos chave em orientação a objetos, pois permite que as implementações sejam isoladas uma das outras através de uma abstração. Abstração é uma palavra-chave aqui, pois programar para interface é programar para uma abstração, é isso que a ideia de interface remete nesse contexto da citação.

Em outras palavras, a citação se refere a interface no sentido abstração (`Interface->Abstração`) e não se refere necessariamente a interface no sentido de ser uma construção de linguagem (`Interface->RecursoDasLinguagens`). O primeiro sentido de interface é mais conceitual, enquanto o segundo sentido é mais técnico e pode ser usado para aplicar o primeiro sentido na prática dentro do código-fonte.

[Programar para interface inicialmente parece simplesmente sair usando a Interface->RecursoDasLinguagens em tudo fazendo cada classe de um projeto ter uma interface implementada.](http://raphael-da-silva.github.io/exagero-interface) Só que o conceito não se restringe a construção de linguagem.

## Interfaces como construção de linguagem (`Interfaces->RecursoDasLinguagens`)

Construção de linguagem é o termo utilizado para se referir as palavras reservadas que fazem parte de uma linguagem de programação. Basicamente, uma construção de linguagem é o que compõe a sintaxe de uma linguagem.

A maioria das linguagens conhecidas possuem uma construção de linguagem para criação de interfaces, geralmente isso é feito com o uso da palavra reservada interface. No PHP, interfaces devem definir métodos com a visibilidade pública e podem conter constantes também. Segue um exemplo da construção de linguagem interface interface:

```php
<?php

/**
 *
 * Exemplo da construção de linguagem interface.
 * @author Raphael da Silva
 *
 */
interface BuscaDePosts
{

    public function buscar(): Posts;

}

```

A construção de linguagem interface quando usada para abstrair expõe métodos sem focar em implementações, essa é uma característica fundamental de uma interface (`Interface->Abstração`), pois ao não focar em implementação ela é útil para abstrair, o que resulta em baixo acoplamente e, consequentemente, mais flexibilidade ao possibilitar a troca de implementações.

A construção de linguagem interface serve como ferramenta para criar implementações completamente diferentes de um conjunto de operações. No exemplo são objetos que buscam posts de alguma fonte, onde trocar completamente de fonte dos dados é algo bem vantajoso (por exemplo, trocar a fonte de dados de um banco de dados por um arquivo). 

O que a construção de linguagem interface faz é mais uma formalização da exposição de todas as assinaturas das operações (leia-se métodos) dentro das linguagens de programação agindo como um contrato (que é uma ideia bem difundida sobre interfaces).

No caso foi utilizada a construção de linguagem interface para criar a abstração de uma busca de posts, no entanto existem outra construção de linguagem para representar uma abstração nas linguagens como as classes abstratas.

## Interface no sentido de abstração (`Interface->Abstração`)

Uma interface (no sentido de abstração) é expor uma funcionalidade sem focar e expor detalhes de implementações, fazendo com que essa característica seja fundamental, pois como não se trabalha com implementação, automaticamente não existe dependência de nenhuma implementação, o que resulta em baixo acoplamento e flexibilidade para trocar de implementações.

## Abstração vai além da construção de linguagem (e a PDO de novo...)

Programar para uma interface é programar para uma abstração, que não necessariamente é uma `Interface->RecursodasLinguagens` (ou uma classe abstrata). [A PDO é um exemplo disso, pois é uma classe concreta que force uma abstração para acessar o banco de dados.](https://raphael-da-silva.github.io/injecao-pdo)

Ou seja, ela é uma interface (`Interface->Abstração`) para acessar o banco de dados de forma abstraída, já que os detalhes são abstraídos pela interface (aqui uma abstração) que essa classe (que é concreta) fornece/expõe com seus métodos.

## Programando para `Interfaces->Abstração`

Programar para interfaces é fundamental na programação orientada a objetos, sendo uma ideia que serve como guia para obter um código flexível e que prioriza a troca de mensagem entre os objetos sem dar importância para os detalhes contidos neles.

Passar a programar com esta mentalidade faz com que um objeto cliente use apenas a interface (`Interface->Abstração`) das operações, assim ela irá funcionar com qualquer implementação da interface (`Interface->Abstração`) em questão que ela espera e depende.

Com isso, pode-se alterar as implementações e mudar o comportamento do cliente (obtendo polimorfismo), além do fato de que mudanças nas implementações não iram afetar os clientes (leia-se os objetos que consumem/requisitam as operação da interface). Dessa forma, é possível alcançar um código flexível, desacoplado e, consequentemente, mais amigável a mudanças. 

## Relação entre os todos os sentidos abordados

Uma `Interface->RecursoDasLinguagens` pode ser usada como uma ferramenta para criar uma `Interface->Abstração` e através da exposição de seus métodos públicos construir uma `Interface->API`. 

Nada disso é dado ou garantido, já que uma interface `Interface->RecursoDasLinguagens` pode não ser uma `Interface->Abstração` [se forem colocados detalhes demais nela (vazando detalhes de implementação em seus métodos).](https://raphael-da-silva.github.io/evitando-detalhes-de-implementacao-interfaces)

### Referências

* GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; Vlissides, John. Design Patterns: Elements of Reusable Object-Oriented Software.

* BLOCH, Joshua. Effective Java: Third Edition.

* A primeira vez que vi o intermo interface sendo tratado como abstração na ideia de programar para interfaces foi em um [hangout sobre refatoração onde isso foi apontado pelo programador João Batista Neto no tempo de 1 hora 7 minutos e 44 segundos](https://www.youtube.com/watch?v=lhCePvd4le4&t=4064s).

*** 

### Encerramento ninja!

Gosto muito do grupo de Rap Wu-Tang Clan, por isso vou encerrar esse artigo com o espírito ninja do grupo.

![wu cover](https://i.scdn.co/image/ab67616d0000b273340e53225fb2b3886a57ba91)
