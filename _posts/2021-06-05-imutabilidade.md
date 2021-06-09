---
layout: post
title: Criando objetos imutáveis
---  

A imutabilidade é uma abordagem na construção de objetos que evita que o estado de um objeto seja modificado após sua criação, um objeto imutável não pode ter o seu estado modificado. O foco desta prática é ter objetos que não permitem que seus dados internos sejam alterados para valores inválidos que podem trazer bugs para a aplicação ou por efeitos colaterais.

## Evitando o efeito colateral

Efeitos colaterais são as consequências inesperadas que a mudança de um estado de um objeto pode gerar em algum contexto. Esse tipo de efeito dificulta muito a manutenção, pois gera uma situação confusa e que consome tempo para entender e solucionar. Geralmente, o que cria um efeito colateral é a manutenção errada do estado, onde a chamada de um método acaba influenciando em outro de forma indevida.

A aplicação da imutabilidade serve para não deixar que o estado de um objeto seja alterado, impedindo assim os possíveis problemas de um efeito colateral. Um objeto imutável não precisa de chamadas de métodos em uma ordem específica para gerenciar o seu estado.

## As vantagens da imutabilidade

Um benefício importante alcançado com a imutabilidade é a facilidade de uso, pois para utilizar um objeto imutável não é preciso setar os valores para deixá-lo em um estado valido antes de usá-lo. A remoção das chamadas de métodos para inicialização do objeto também melhora o encapsulamento, já que nenhum método que releva dados internos do objeto é exposto.

Além de um melhor encapsulamento, a imutabilidade também torna os objetos mais simples, já que eles preservam um estado e, por isso, são mais consistentes.

<!-- Immutable objects are simple. An immutable object can be in exactly one state, the state in which it was created. -->

> Objetos imutáveis são simples. Um objeto imutável pode estar em exatamente um estado, o estado em que ele foi criado. (BLOCH, 2008, p.75, tradução nossa)

Esse trecho citado do livro Effective Java sintetiza bem a simplicidade da imutabilidade e sua relação com o estado de um objeto.

Resumidamente, a imutabilidade traz as seguintes vantagens:

* Elimina a necessidade de preparar o estado do objeto antes de usá-lo.
* O objeto não depende de uma ordem específica de inicialização.
* Elimina a necessidade de verificar se o objeto está em um estado válido.
* Ajuda a simplificar o código, já que getters e setters são desnecessários.
* Facilita o uso do objeto, pois ele já está pronto para uso desde a sua construção (sem a necessidade chamada de métodos adicionais).

## Exemplo prático

O exemplo a seguir apresenta a classe ```InfoArquivo``` que é mutável, a funcionalidade dela é obter as informações sobre um arquivo. A implementação é bem simples e servirá de base para comparar a imutabilidade com a mutabilidade.

```php
<?php

/**
 *
 * Exemplo de aplicação de imutabilidade.
 * @author Raphael da Silva
 *
 */
class InfoArquivo
{

    private $arquivo;

    public function setarArquivo(string $arquivo)
    {

        $this->arquivo = $arquivo;

    }

    public function obterInformacoes(): array
    {

        return pathinfo($this->arquivo);

    }

}
```

Como foi mencionado a classe ```InfoArquivo``` é mutável, isso torna possível que ela seja utilizada sem ter o arquivo setado pelo método ```setarArquivo```. Essa condição gera uma inconsistência, pois o método ```obterInformacoes``` pode ser chamado sem antes ter um arquivo definido para ser lido através dele. Ou seja, com o uso do setter não é garantido que o valor seja passado para o objeto.

No trecho de código a seguir, o valor do atributo ```$arquivo``` é nulo, pois ele não foi inicializado através do setter.

```php
<?php

$arquivoInfo = new InfoArquivo;
$informacoes = $arquivoInfo->obterInformacoes(); 
```

A forma como a classe está sendo utilizada não é adequada e não garante o seu funcionamento correto, pois nenhum arquivo foi passado para o objeto em questão. Para resolver esse problema pode ser adicionada uma validação no método ```obterInformacoes```, o objetivo disso é obrigar a definição de um arquivo através do método ```setarArquivo```.

```php
<?php

/**
 *
 * Exemplo de aplicação de imutabilidade.
 * @author Raphael da Silva
 *
 */
class InfoArquivo
{

    private $arquivo;

    public function setarArquivo(string $arquivo)
    {

        $this->arquivo = $arquivo;

    }

    public function obterInformacoes(): array
    {

        if(is_null($this->arquivo)){
            throw new Exception('Arquivo é necessário, use o método setter.');
        }

        return pathinfo($this->arquivo);

    }

}
```

Com a adição da validação o código se torna mais consistente e o problema é resolvido, porém foi necessária a adição de um código extra para garantir a inicialização correta da classe. Esse é o tipo de desvantagem que a mutabilidade traz em casos onde é obrigatório a inicialização de alguns atributos do objeto.

Para que não seja necessária a adição de uma validação nesse caso, é necessário tornar o objeto imutável, para isso basta utilizar o método construtor para que a sua inicialização seja forçada durante a criação da instância. Segue a implementação do objeto de forma imutável:

```php
<?php

/**
 *
 * Exemplo de aplicação de imutabilidade.
 * @author Raphael da Silva
 *
 */
class InfoArquivo
{

    private $arquivo;

    public function __construct(string $arquivo)
    {

        $this->arquivo = $arquivo;

    }

    public function obterInformacoes(): array
    {

        return pathinfo($this->arquivo);

    }

}
```

Como é possível perceber, não existe mais a necessidade de validação, além disso, para criar uma instância é necessário passar o valor no construtor, o que faz o objeto ser sempre criado com um estado válido e, portanto, pronto para uso. Esse tipo de situação mostra as vantagens da imutabilidade em relação a mutabilidade.

Para finalizar, a criação do objeto depois de torná-lo imutável ficaria da seguinte forma:

```php
<?php

$arquivoInfo = new InfoArquivo('arquivo.txt');
$informacoes = $arquivoInfo->getInfo();
```

## O suporte para a imutabilidade no PHP

Em linguagens como C# existe a palavra reservada ```readonly```, ela serve para impedir que um atributo de um objeto seja modificado depois de inicializado, esse recurso é muito útil na criação de objetos imutáveis, já que faz a própria linguagem suportar o conceito e deixa bem claro a intenção do programador.

No PHP esse tipo de recurso não existe até o momento eu escrevi esse artigo. Entretanto, não criar setters para atributos e só permitir a sua inicialização durante a construção do objeto são abordagens que ajudam a aplicar a imutabilidade dentro do PHP, mesmo que não exista um suporte completo na linguagem.

### Referências

* BLOCH, Joshua. Effective Java: Second Edition. Edição 2.