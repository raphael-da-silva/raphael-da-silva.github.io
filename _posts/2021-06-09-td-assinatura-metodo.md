---
layout: post
title: As assinaturas de métodos de objetos (e seus elementos)
---

Na troca de mensagem entre objetos tudo se dá através dos métodos, por isso acho válido decompor do que um método é feito para entender os elementos da troca de mensagem.

Os métodos são definidos através da sua assinatura, que é constituída pelo nome que o método recebe e os seus parâmetros definidos e o tipo do retorno do método. 

O conteúdo do método não faz parte da sua assinatura. Um exemplo onde a composição da assinatura de um método é bem explícita é no caso das interfaces, pois nelas apenas as assinaturas dos métodos são declaradas (sem nenhum conteúdo no corpo do método). Por exemplo:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
interface LeitorDeArquivoDeConfiguracao
{

    public function ler(string $arquivo): array;

}
```

A interface em questão traz o método `ler`, decompondo os elementos que fazem a assinatura desse método fica o seguinte:

* Nome do método que é `ler`.
* Parâmetro de entrada que é um arquivo representado pela variável `$arquivo`.
* Tipo esperado como retorno da leitura que é um `array`.

Este post é mais a anatomia de objetos e sua comunicação.