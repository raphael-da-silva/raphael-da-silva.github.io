---
layout: post
title: Métodos pequenos para separar as responsabilidades
---

Separar o código de uma classe em vários métodos pequenos é algo que melhora o código, pois com essa separação a complexidade reduzida, já que cada método criado faz parte do objetivo da classe e, com isso, a compreensão da tarefa principal da classe fica mais fácil porque está divida em passos diferentes. 

Criar pequenos métodos possibilita dividir a tarefa de um objeto em partes menores (que são granulares) e de menos complexidade. É uma divisão da complexidade em estruturas menores e, portanto, mais simples de compreender.

## Separando uma classe em métodos menores na prática

No exemplo a seguir, a classe ```LeitorArquivoJson``` lê o conteúdo de um arquivo ```json```, ela contém um método que contém as seguintes tarefas: checar se o arquivo existe e depois converter/ler o seu conteúdo através das funções ```file_get_contents``` e ```json_decode```.

```php
<?php

/**
 *
 * Exemplo de aplicação de métodos pequenos na refatoração.
 * @author Raphael da Silva
 *
 */
class LeitorArquivoJson
{

    private $arquivo;

    public function __construct(string $arquivo)
    {

        $this->arquivo = $arquivo;

    }

    public function ler(): array
    {

        if(!file_exists($this->arquivo)){
            throw new RuntimeException('O arquivo não existe.');
        }

        if(pathinfo($this->arquivo, PATHINFO_EXTENSION) !== 'json'){
            throw new RuntimeException('Formato inválido.');
        }

        $conteudoJson = file_get_contents($this->arquivo);
        $conteudoJson = json_decode($conteudoJson, true);
        
        return $conteudoJson;

    }

}
```

Para aplicar a separação no exemplo em questão, é necessário extrair essas tarefas para métodos próprios, nesse caso as tarefas serão colocadas em métodos específicos para realizá-las. Segue a nova implementação:

```php
<?php

/**
 *
 * Exemplo de aplicação de métodos pequenos na refatoração.
 * @author Raphael da Silva
 *
 */
class LeitorArquivoJson
{

    private $arquivo;

    public function __construct(string $arquivo)
    {

        $this->arquivo = $arquivo;

    }

    private function checarSeArquivoExiste(): void
    {

        if(!file_exists($this->arquivo)){
            throw new RuntimeException('O arquivo não existe.');
        }

    }

    private function checarFormatoDoArquivo(): void
    {

        if(pathinfo($this->arquivo, PATHINFO_EXTENSION) !== 'json'){
            throw new Exception('Formato inválido.');
        }

    }

    private function lerConteudoJson(): array
    {

        $conteudoJson = file_get_contents($this->arquivo);
        $conteudoJson = json_decode($conteudoJson, true);
        
        return $conteudoJson;

    }

    public function ler(): array
    {

        $this->checarSeArquivoExiste();
        $this->checarFormatoDoArquivo();
        return $this->lerConteudoJson();

    }

}
```

Com a criação de novos métodos a classe fica mais separada e organizada, já que cada método tem a sua respectiva responsabilidade bem definida, consequentemente a granularidade e a coesão aumentam. Além disso, tudo passa a ser mais simples de compreender, pois foi dividido em diferentes operações.

### Mais algumas vantagens

Aplicar essa separação através de pequenos métodos também facilita a reusabilidade através dos pequenos métodos extraídos, pois o código extraído para um método pode ser reaproveitado em outros pontos da classe caso surja a necessidade.

Além do benefício da reusabilidade, a legibilidade da classe também aumenta, já que uma lógica fragmentada em partes que são mais fáceis de entender do que um grande método onde tarefas se misturam. Essa prática é chamada de **compose method** e costuma aparecer quando o assunto é refatoração.