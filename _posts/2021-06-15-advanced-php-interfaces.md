---
layout: post
title: "Recursos ninja: as interfaces nativas do PHP"
---

O PHP conta com algumas interfaces padrões para serem utilizadas. Esse tipo de código está presente por padrão no PHP, ou seja, eles já vem como um recurso nativo da linguagem. Elas são bastante úteis para dar comportamentos diferentes para objetos, um exemplo é a interface ```ArrayAccess``` que tem como objetivo fazer um objeto poder ser manipulado como um array.

## A nomenclatura das interfaces

Existe uma prática muito comum que é dar nomes de interfaces que expressam um adjetivo, por exemplo, para definir se um objeto é serializável existem linguagens, como o próprio PHP, que contam com uma interface chamada ```Serializable```.

Basicamente, o adjetivo usado no nome expressa o comportamento que a interface vai implementar. Essa lógica de nomenclatura com adjetivos é bastante utilizada dentro do PHP, sendo aplicada nas interfaces que serão apresentadas a seguir.

## Countable

Definição segundo a [documentação do PHP](http://php.net/pt_BR/countable):

> Classes que implementam Countable podem ser usadas com a função count().

Esta interface torna possível que objetos sejam contados pela função ```count```. Isso é útil em casos onde determinados dados precisam ser contados para fazer alguma verificação. Um exemplo seria um objeto que contém uma lista de nomes, nesse contexto a interface ```Countable``` pode ser implementada para possibilitar a contagem desses nomes.

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class ColecaoNomes implements Countable
{

    private $nomes = [];

    public function adicionarNome($nome)
    {

        $this->nomes[] = $nome;

    }

    /**
     *
     * Método da interface Countable.
     *
     */
    public function count()
    {

        return count($this->nomes);

    }

}
```

O método ```count``` é o que faz parte da interface, portanto ele é o que deve ser implementado. Lembrando que ele deve retornar um valor do tipo inteiro.

## JsonSerializable

Definição da interface segundo a [documentação do PHP](http://php.net/pt_BR/JsonSerializable):

> Os objetos que implementam o JsonSerializable podem customizar sua representação JSON quando codificados com json_encode().

Esta interface tem como objetivo possibilitar que um objeto seja passado como parâmetro para a função ```json_encode```, isso pode ser útil para converter determinados dados de um objeto em ```json``` com suporte da linguagem.

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class InformacoesLocalizacao implements JsonSerializable
{

    private $cidades;
    private $estados;

    public function __construct(
        array $cidades,
        array $estados
    ){

        $this->cidades = $cidades;
        $this->estados = $estados;

    }

    public function jsonSerialize()
    {

        return [
            'cidades' => $this->cidades,
            'estados' => $this->estados
        ];

    }

}
```

No exemplo em questão, o método ```jsonSerialize``` faz parte da interface, sendo utilizado para gerar um ```json``` com a junção dos estados e cidades, o array retornado será utilizado pela função ```json_encode```.

```php
<?php

$cidades = [
    'Brasilia',
    'Rio de Janeiro',
    'Nova York'
];

$estados = [
    'SP',
    'SC',
    'RJ'
];

$dadosLocalizacao = new InformacoesLocalizacao($cidades, $estados);
$jsonLocalizacao  = json_encode($dadosLocalizacao);

echo $jsonLocalizacao;
```

O ```json``` que será gerado através do objeto terá a seguinte estrutura:

```json
{
   "city":[
      "Brasilia",
      "Rio de Janeiro",
      "Nova York"
   ],
   "states":[
      "SP",
      "SC",
      "RJ"
   ]
}
```

## ArrayAccess

Definição da interface segundo a [documentação do PHP](http://php.net/pt_BR/ArrayAccess):

> Interface que provê o acesso a objetos como se fossem arrays.

O objetivo desta interface é fazer com que um objeto possa ser manipulado como um array, o que pode ser bastante benéfico quando um objeto possuir dados que representam uma coleção de algo, como cidades e estados, por exemplo.

A interface é composta pelos seguintes métodos:

* ```offsetSet```: é responsável por atribuir um valor que será adicionado.
* ```offsetGet```: é responsável por obter um valor.
* ```offsetExists```: é responsável por verificar se o índice existe.
* ```offsetUnset```: é responsável por remover um valor com base no índice.

Segue um exemplo da implementação da interface ```ArrayAccess```, onde os dados do objeto poderão ser manipulados como se fossem um array:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class ColecaoNomes implements ArrayAccess
{

    private $nomes = [];

    public function adicionarNome($nome)
    {

        $this->nomes[] = $nome;

    }

    /**
     *
     * Os métodos abaixo são parte da interface Iterator.
     *
     */
    public function offsetSet($indice, $valor)
    {

        $this->nomes[$indice] = $valor;

    }

    public function offsetGet($indice)
    {

        return $this->nomes[$indice];

    }

    public function offsetExists($indice)
    {

        return isset($this->nomes[$indice]);

    }

    public function offsetUnset($indice)
    {

        unset($this->nomes[$indice]);

    }

}
```

Os métodos implementados são executados quando o objeto ser manipulado como um array, basicamente eles definem o comportamento do objeto quando ele for manipulado nesse tipo de situação. Por exemplo:

```php
$nomes    = new ColecaoNomes;
$nomes[0] = 'Fulano'; // Executa o método offsetSet.

echo $nomes[0]; // Executa o método offsetGet.

if(isset($nomes[0])){ // Executa o método offsetExists.
    unset($nomes[0]); // Executa o método offsetUnset.
}
```

*** 

### Encerramento ninja!

Gosto muito do grupo de Rap Wu-Tang Clan, por isso vou encerrar esse artigo com o espírito ninja do grupo.

![wu cover](https://i.scdn.co/image/ab67616d0000b273340e53225fb2b3886a57ba91)