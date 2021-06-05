---
layout: post
title: A evolução da orientação a objetos no PHP
---

Até a versão 5 o PHP não suportava a orientação a objetos de uma forma satisfatória, da quinta versão em diante novos recursos foram adicionados, além disso, a criação da ferramenta Composer trouxe para a linguagem muitas padronizações focadas no uso e na distribuição de bibliotecas como o uso de namespaces para facilitar o autoload de classes. No entanto, foi na versão 7 que a linguagem teve um ponto de virada grande na orientação a objetos.

## A orientação a objetos com a chegada do PHP7

Com a chegada do PHP7 foram adicionados recursos presentes em outras linguagens, como a adição de tipos escalares como parâmetros de funções. Além disso, também foi adicionada a possibilidade de trabalhar com uma tipagem mais forte, mas sem deixar para trás da flexibilidade da tipagem fraca que sempre existiu dentro do PHP.

Um dos destaques trazidos é o recurso de tipagem de retorno, ou seja, passou a ser possível definir o tipo que um método poderia retornar, isso é um ganho importante para a linguagem, pois com esse recurso é possível ter a garantia de que um determinado tipo vai ser retornado, o que torna a comunicação entre os objetos mais clara e garantida, já que é possível trabalhar sabendo que nenhum tipo inesperado vai ser retornado.

### Um exemplo de tipagem de retorno e tipos escalares

A classe ```MensagemDeSaudacao``` a seguir serve como exemplo para o uso da tipagem de retorno, nela será retornado um valor que é do do tipo ```string```.

```php
<?php

class MensagemDeSaudacao
{

    public function criarMensagem(string $nome): string
    {

        return sprintf('Olá %s', $nome);

    }

}
```

O exemplo também mostra a definição de tipos escalares no tipo do parâmetro e no tipo do retorno, pois o método ```criarMensagem``` espera e vai retornar uma ```string``` (que é um tipo escalar). Antes do PHP7 o mesmo código seria escrito da seguinte maneira:

```php
<?php

class MensagemDeSaudacao
{

    public function criarMensagem($nome)
    {

        return sprintf('Olá %s', $nome);

    }

}
```

Como é possível perceber, não há a garantia de que os tipos esperados serão passados, consequentemente teriam que ser feitas validações se fosse necessário garantir o recebimente de uma string no parâmetro, consequentemente isso tornaria o código mais complexo e trabalhoso.

