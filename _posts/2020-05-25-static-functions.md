---
layout: post
title: PHP - Funções anônimas estáticas
---

Olhando um repositório no Github (uma dia antes da criação desse post) me achamou a atenção o uso da palavra reservada `static` em uma função anônima, pois eu nunca tinha visto isso e, portanto, não sabia que existia essa possibilidade no PHP. Depois de estudar resolvi [escrever](https://raphael-da-silva.github.io/escrita-io/) sobre isso.

### A finalidade

Fui pesquisar e entendi o porquê do uso de uma função anônima assim. Basicamente, ao declarar a função estática a variável `$this` não existirá no escopo da função, ou seja, a função não irá referenciar um contexto de onde ela foi declarada. Segue o exemplo em código:

```php
<?php

class Contexto
{
    
    public function exemplo(){
        
        $funcaoSemContexto = static function(){

            // Essa variável é indefinida no escopo dessa função.
            var_dump($this);
        
        };
        
        $funcaoSemContexto();
        
    }
    
}
```

Sem usar a palavra reservada `static`, a variável `$this` iria apontar para uma instância da classe `Contexto`, já que foi nessa classe que a função anônima foi criada e, consequentemente, ela seria o contexto dessa função. Como a função foi declara estática, o seguinte erro aparece:

> Fatal error: Uncaught Error: Using $this when not in object context

### Troca de contexto

Vale lembrar que uma função anônima no PHP é uma instância da classe (interna do PHP) `Closure` e essa classe tem métodos como o método `bindTo`, que é responsável por adicionar um novo contexto (aka a variável `$this`) em uma anônima. 

Só que trocar de contexto não é possível em uma função declarada como estática, já que ela impossibilita ter contexto. Em outras palavras, não dá para usar o método `bindTo` em função anônima quando ela é estática.

Segue isso exemplificado mantendo o exemplo de código criado:

```php

<?php

class Contexto
{ 

    public function exemplo(){
        
        $funcaoSemContexto = static function(){

            // Essa variável é indefinida no escopo dessa função.
            var_dump($this);
        
        };
        
        $novoContexto = new stdClass;
        $novoContexto->texto = 'Esse objeto é o novo contexto.';

        // Isso não é possível porque a função foi criada estática
        $funcaoSemContexto->bindTo($novoContexto);
        $funcaoSemContexto();
        
    }
    
}
```
Ao executar o código acima, o erro a seguir aparece por conta da função anônima ser estática.

> Warning: Cannot bind an instance to a static closure

### Finalizando

Esse comportamento alcançado através funções anônimas estáticas é semelhante ao de classes estáticas, já que elas não tem contexto por não serem uma instância de um objeto. Declarar uma função anônima como estática dá essa mesma natureza (de não ter contexto) para a função.

Esse comportamento pode ser útil se por algum motivo é necessário evitar que o `$this` possa ser usado em uma função anônima.