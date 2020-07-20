---
layout: post
title: POO - Métodos estáticos e seus problemas (em alguns casos)
---

Métodos estáticos trazem alguns problemas em certos contextos. O primeiro problema é o acoplamento, já que os objetos não estão dependendo de instâncias de outras classes de forma parametrizada (com injeção de dependência), mas sim de métodos estáticos que são declarados diretamente na classe acoplando o código.

Esse acoplamento também dificulta os testes, pois as classes que utilizam o código estático não podem ter esse código substituído por objetos de testes (mocks e etc), já que esses objetos não foram injetados, mas sim usados (de forma acoplada) através de métodos estáticos.

Além do acoplamento que pode ser gerado, criar classes com vários métodos estáticos pode acabar sendo o mesmo que definir funções procedurais, a única diferença é que as funções vão estar atreladas a uma classe, que vai acabar funcionando como uma espécie de namespace para essas funções, ou seja, o código não vai ser orientado a objetos. 

Um lugar onde é possível ver essa situação são nas famosas classes de helpers, onde o programador vai adicionando diversas funções estáticas dentro de uma classe genérica demais sem critério nenhum e que só vai crescendo de forma descontrolada.

```php
<?php

class Helpers
{

    public static function converterDataParaPtBr(array $data): string
    {

        $data = explode('-', $data);
        return $data[2] . '/' . $data[1] . '/' . $data[0];

    }

    public static function converterParaMaisculo(string $string): string
    {

        return strtoupper($string);

    }

    public static function converterParaMinusculo(string $string): string
    {

        return strtolower($string);

    }

    public static function converterJsonParaArray(string $jsonString): string
    {

        return json_decode($jsonString, true);

    }

    public static function lerArquivoEmLinhas(string $arquivo): array
    {

        return files($arquivo);

    }

    public static function lerConteudoArquivo(string $arquivo): string
    {

        return file_get_contents($arquivo);

    }

    public static function removerHttp(string $url): string
    {

        return ltrim($url, 'http://');

    }

}
```

A classe `Helpers` mostra como classes estáticas podem ser utilizadas só para agrupar funções que são procedurais e que, portanto, não são orientada a objetos. Além disso, esse tipo de classe não é coesa, já que foca em diversas tarefas sem ter um propósito bem definido. No fim, esse tipo de classe gera baixa coesão e alto acoplamento, o que é o contrário do que se busca na orientação objetos.

Nesse tipo de classe, ações como formatação de datas, leitura de arquivos e processamento de strings estão misturadas de forma bagunçada, além disso, a tendência dessa classe crescer mais ainda é grande, já que quando um novo helper ser criado ele será adicionado nessa mesma classe através de mais um método.
