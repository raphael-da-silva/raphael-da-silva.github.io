---
layout: post
title: Aplicando a técnica Early return
--- 

Early return consiste numa prática onde a lógica de uma estrutura condicional é invertida retornando algum valor em vez de criar um desvio condicional (else, elseif). Utilizá-la na orientação a objetos ajuda na criação de métodos mais simples e que não possuem muitos desvios condicionais.

Essa prática promove um código mais legível e com menos complexidade nas estruturas condicionais, acabando assim com estruturas aninhadas que possuem pouca legibilidade e alta complexidade.

Sem a aplicação dessa técnica as condições possuem desvios condicionais (else) para determinarem a ação de uma tarefa. Por exemplo:

```php
<?php

/**
 *
 * Exemplo de aplicação do early return.
 * @author Raphael da Silva
 *
 */
class MensagemUsuario
{

    public function definirMensagem($nome = null): string
    {

        if(!is_null($nome)){
            $mensagem = 'Olá ' . $nome . '!';
        }else{
            $mensagem = 'Olá mundo!';
        }

        return $mensagem;

    }

}
```

Para aplicar o Early return no código, é necessário retornar antecipadamente (ou seja early), pois assim o retorno finaliza a execução. Ao aplicar o Early return a implementação ficaria da seguinte maneira:

```php
<?php

/**
 *
 * Exemplo de aplicação do early return.
 * @author Raphael da Silva
 *
 */
class MensagemUsuario
{

    public function definirMensagem($nome = null): string
    {

        if(!is_null($nome)){
            return 'Olá ' . $nome . '!';
        }

        return 'Olá mundo!';

    }

}
```

Após a aplicação do Early return não é mais necessário uma estrutura condicional de desvio (nesse caso o else) para fazer que o código seja executado em somente alguns casos, já que a parada da execução com o ```return``` já faz que o código seja executado em somente alguns casos.

A legibilidade obtida com a prática de Early return faz com que a manutenção do software seja mais fácil, já que uma estrutura condicional simples é mais fácil de entender e, consequentemente, mais fácil de manter.