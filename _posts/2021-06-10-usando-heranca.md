---
layout: post
title: Usando herança de forma coerente (com relação entre tipos)
---

A herança é um recurso disponível na orientação a objetos e bastante utilizado, ela serve para permitir uma especialização de um código mais genérico. Ela também permite que o código de uma classe seja reaproveitado através da criação de uma classe derivada dela, essa possibilidade de reaproveitamento faz com que este recurso seja bastante utilizado de forma confusa.

## A relação entre as classes na herança

Apesar da herança oferecer a vantagem do reaproveitamento de código, ela deve ser utilizada com cuidado e em situações onde a classe derivada seja a mesma coisa que a classe pai, dessa forma, a classe derivada tem que ser um subtipo da sua classe pai, ou seja, ela tem que ser realmente uma extensão. Esse é o tipo de relação que deve ser priorizada em uma hierarquia entre classes.

<!-- Inheritance is appropriate only in circumstances where the subclass really is a subtype of the superclass. In other words, a class B should extend a class A only if an “is-a” relationship exists between the two classes. -->

> A herança é apropriada apenas em circunstâncias onde a subclasse realmente é um subtipo da superclasse. Em outras palavras, uma classe B deve estender a classe A só se um relaciamento "é um" existe entre essas duas classes. (BLOCH, 2008, p.85, tradução nossa)

A herança deve ser utilizada com a ideia **“é um”** e não com classes herdadas que não fazem sentido e são criadas apenas para reaproveitar código fora de contexto. Por isso, não se deve herdar só para reaproveitar parte de um código, para herdar é preciso estar de acordo com o conceito da classe pai, caso contrário, será apenas uma extensão sem sentido.

## A regra para usar herança

Como foi mencionado no início deste capítulo, a herança deve ser utilizada com a ideia de **“é um”** em mente, ou seja, a classe filha tem que ser a mesma coisa, conceitualmente falando, que a sua classe pai. Sabendo disso, fica mais evidente perceber quando a herança é utilizada de uma forma errada.

Por exemplo, uma classe que serve para dar acesso a um banco de dados ser herdada por uma classe que faz cadastro é um erro, pois o cadastro não é o mesmo que um banco de dados. 

```php
<?php

/**
 *
 * Exemplo de uso sem sentido de herança.
 * @author Raphael da Silva
 *
 */
class RegistroDeUsuario extends PDO
{

    public function registrar(string $nome, string $email): void
    {

        $sql = 'INSERT INTO usuarios (nome, email) 
                VALUES (:nome, :email)';

        $stmt = parent::prepare($sql);
        $stmt->execute([
            ':nome' => $nome,
            ':email'=> $email
        ]);

    }

}
```

A herança utilizada na classe ```RegistroDeUsuario``` não faz sentido, pois o cadastro de um usuário não é um banco de dados. A herança só faria sentido se o cadastro herdasse de algum cadastro mais genérico e não uma classe referente a banco de dados como a ```PDO```.

Muitas vezes o uso errado da herança surge da ideia de reaproveitamento, já que geralmente o programador deseja utilizar o código da classe pai em outras classes de acordo com suas necessidades. Voltando para o exemplo em questão, o cadastro necessitar de acesso ao banco de dados é o que acaba levando a seguir por esse caminho de estender coisas nem nexo nenhum.

## Antes da correção: o conceito de composição

Composição, como o próprio nome remete, é o termo utilizado para definir a criação de objetos através de outros. Quando a funcionalidade de um objeto é feita sendo “composta” por outros objetos, significa que ele utiliza composição.

O uso da composição é amplamente visto como uma alternativa para a herança, pois através dela os objetos são reaproveitados sem serem ligados por um tipo ou presos a uma hierarquia como acontece na herança, além disso, a composição é uma forma bem mais flexível de lidar com as dependências de um objeto (dependências essas que são injetadas para compor os objetos).

### Corrigindo o exemplo da herança com composição (e injeção)

Para que ```RegistroDeUsuario``` utilizar ```PDO``` sem usar herança, ela poderia ser passada como parâmetro (sendo injetada como dependência) em vez de herdar dela. Segue a classe depois dessa modificação:

```php
<?php

/**
 *
 * Exemplo de correção do uso de herança.
 * @author Raphael da Silva
 *
 */
class RegistroDeUsuario
{

    private $pdo;

    public function __construct(
        PDO $pdo
    ){

        $this->pdo = $pdo;

    }

    public function registrar(string $nome, string $email): void
    {

        $sql = 'INSERT INTO usuarios (nome, email) 
                VALUES (:nome, :email)';

        $stmt = $this->pdo->prepare($sql);
        $stmt->execute([
            ':nome' => $nome,
            ':email'=> $email
        ]);

    }

}
```

Com o uso de composição a relação entre as duas classes faz mais sentido, pois agora ```RegistroDeUsuario``` **tem** uma instância de ```PDO``` e **não é** uma instância de ```PDO```. Além disso, a classe que antes nem tinha um construtor, agora tem um com um papel bem definido, sendo um objeto mais completo e transparente.

## Reaproveitando código sem herança através de traits

Nos casos onde é preciso apenas utilizar o código sem necessariamente ser um subtipo é mais adequado utilizar [traits](https://raphael-da-silva.github.io/usando-as-traits), pois elas servem apenas o reaproveitamento de um pedaço de código sem ser preciso ter uma relação de tipo. Como uma das alternativas para herança estão as traits.

Uma situação onde existe uma classe ```Aviao``` e é preciso do mesmo método para voar de uma classe ```Passaro```, não é correto fazer com que o avião herde do pássaro, pois isso não faz sentido, já que um avião **não é** um pássaro. Como alternativa é possível criar uma trait com o código que será utilizado por classes de diferentes tipos.

```php
<?php

/**
 *
 * Exemplo de uso de trait entre tipos não relacionados.
 * @author Raphael da Silva
 *
 */
trait TraitVoar
{

    public function voar(): void
    {

        echo 'Voando';

    }

}
```

Ao ter uma trait, o código contido nela pode ser reaproveitado por qualquer classe. Basicamente, a trait é uma porção de código que pode ser reutilizada em qualquer lugar, ela não tem a mesma relação que a herança, portanto serve para reaproveitar código de implementações que não fazem sentido ser herdadas, como no caso do avião e do pássaro.

```php
<?php

/**
 *
 * Exemplo de uso de trait entre tipos não relacionados.
 * @author Raphael da Silva
 *
 */
class Passaro
{

    use TraitVoar;

    // O método voar pode ser usado por essa classe por causa da trait.

}
```

```php
<?php

/**
 *
 * Exemplo de uso de trait entre tipos não relacionados.
 * @author Raphael da Silva
 *
 */
class Aviao
{

    use TraitVoar;

    // O método voar pode ser usado por essa classe por causa da trait.

}
```

Como é possível perceber, ambas as classes utilizaram a trait para reaproveitar a mesma implementação. Esse reaproveitamento foi feito sem nenhum vínculo de tipo, diferente do que aconteceria se a herança tivesse sido usada (e estaria errado por forçar uma relação entre classes que não tem relação de tipo).

### Referências

* BLOCH, Joshua. Effective Java: Second Edition. Edição 2.

***

### 💀💀💀 Case Closed: é isso... 💀💀💀

Gosto muito do grupo de Rap Cypress Hill (💀💀💀), existe uma música deles chamada "Case Closed", que traduzindo significa "Caso Encerrado". Referenciei o nome dessa música para encerrar esse artigo. 

Caso encerrado (aka Case Closed)!!!!

![cypress cover](https://i.scdn.co/image/ab67616d0000b2734e51c518e787896bc8cdb1a5)