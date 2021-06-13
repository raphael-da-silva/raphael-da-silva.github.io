---
layout: post
title: Evitando colocar detalhes específicos em interfaces
---

Uma interface tem como objetivo expor operações (métodos) que farão parte de um objeto, além disso, ela possibilita a troca de funcionalidades de forma flexível no código através da criação de novas implementações.

No entanto, para que a troca entre diferentes implementações seja feita sem problemas (leia-se limitações), é preciso expor os métodos da interface sem conter informações na sua assinatura que revelam detalhes sobre a sua implementação. Ou seja, é preciso expor os métodos de forma abstraída.

## Uma interface não garante uma abstração

Uma interface pode ser vista como uma ferramenta para criar uma abstração, mas uma ferramenta só traz benefícios na mão de quem sabe tirar proveito dela e por si só não garante nada.

Ou seja, uma interface não garante que os seus métodos sejam abstratos o suficiente para possibilitar a troca fácil entre diferentes implementações. Quem garante que os detalhes de uma operação sejam abstraídos é o programador (que faz a tarefa mental de abstrair). 

A essencia de uma interface é expor operações para objetos interagirem, isso é sintetizado na seguinte citação conhecida do Gang of Four:

<!-- The set of all signatures defined by an object's operation is called the interface to the object.
 -->

> O conjunto de todas as assinaturas definidas pelas operações de um objeto é chamado de interface do objeto. (GAMMA et al., 1994, p.13, tradução nossa)

Com isso, uma interface não garante uma abstração, pois se detalhes de implementação forem colocados na assinatura dos métodos (nos seus nomes e parâmetros) definidos na interface ela não vai ser uma ferramenta útil para gerar operações abstraídas. 

Por isso é importente evitar detalhes de implementação nas assinaturas dos métodos de uma interface. Lembrando que a assinatura de um método é composta pelo nome do método e seus respectivos parâmetros e retornos (basicamente são todas as informações que um método expõe na sua declaração).

## Evitando detalhes nos parâmetros dos métodos

Uma interface pode conter detalhes através de parâmetros e isso traz limitações, pois os detalhes podem ser um empecilho gerador de dificuldades na hora de criar uma nova implementação. Um exemplo desse tipo de problema seria uma interface criada para verificar um usuário e nela contém um método que recebe como parâmetro o e-mail e o nome da tabela de um banco de dados onde usuário está armazenado.

```php
<?php

/**
 *
 * Exemplo de como evitar detalhes em interfaces
 * @author Raphael da Silva
 *
 */
interface VerificadorDeUsuario
{

    public function verificarSeExiste(
        string $email, 
        string $tabelaBancoDados
    ): bool;

}
```

O segundo parâmetro `$tabelaBancoDados` expõe detalhes nesse contexto, pois ele faz a verificação se limitar ao uso de um banco de dados. O erro na abstração fica evidante neste exemplo, pois essa interface está presa a detalhes de implementação ao fazer com que validação seja realizada através de um banco de dados, o que irá impossibilitar que uma nova classe implemente esta interface com uma verificação diferente que não use um banco de dados para fazer essa operação.

Para melhorar o exemplo da interface em questão o segundo parâmetro deveria ser removido.

```php
<?php

/**
 *
 * Exemplo de como evitar detalhes em interfaces
 * @author Raphael da Silva
 *
 */
interface VerificadorDeUsuario
{

    public function verificarSeExiste(string $email): bool;

}
```

Informações como o nome da tabela poderiam ser passadas no construtor e, com isso, retiradas da interface e ocultadas ao serem colocadas construção de um objeto específico que é uma implementação da interface. Assim esse detalhe que tem a ver com banco de dados não ficaria expostosna interface. Por exemplo:

```php
<?php

/**
 *
 * Exemplo de como evitar detalhes em interfaces
 * @author Raphael da Silva
 *
 */
class VerificadorComBancoDeDados implements VerificadorDeUsuario
{

    private $conexaoComPDO;
    private $tabelaBancoDados;

    public function __construct(
        PDO $conexaoComPDO,
        string $tabelaBancoDados
    ){
        
        $this->conexaoComPDO    = $conexaoComPDO;
        $this->tabelaBancoDados = $tabelaBancoDados;

    }

    private function verificarNoBanco(string $email): PDOStatement
    {

        $stmt = $this->conexaoComPDO->prepare(
            'SELECT * FROM ' . $this->tabelaBancoDados . ' WHERE Email = :email'
        );

        $stmt->execute([
            'email' => $email
        ]);

        return $stmt;

    }

    public function verificarSeExiste(string $email): bool
    {

        $query  = $this->verificarNoBanco($email);
        $existe = ($query->rowCount() !== 0); 

        return $existe;

    }

}
```

Basicamente, o nome da tabela do banco de dados é um detalhe de implementação e, portanto, não faz parte da interface nesse contexto, pois somente o parâmetro referente ao e-mail é parte essencial do que operação se propõe a fazer.

Já o parâmetro `$tabelaBancoDados` que foi retirado da interface revelava como essa operação seria feita, ou seja, ele revelava detalhes de como a implementação seria na realidazada prática, portanto não faz parte da operação que está sendo abstraída com a interface. Retirar o o parâmetro `$tabelaBancoDados` é exemplo de se despreender dos detalhes no processo de abstrair como foi mencionado no começo do livro.

Evitar esses detalhes de implementação em interfaces também simplifica a interação (aka [troca de mensagens](https://raphael-da-silva.github.io/td-troca-de-mensagens/)) entre os objetos, já que os objetos que vão trabalhar com uma implementação da interface não terão que passar valores para parâmetros que são referentes aos detalhes de implementação, mantendo assim os detalhes ocultados e simplificando as coisas ao fazer a interação entre objetos se a ter a abstração.

**Um lembrete sobre o contexto:** é importante lembrar que as informações referentes a banco de dados são detalhes de implementação no contexto apresentado, mas se o contexto fosse referente a operações de banco de dados, informações como nome de tabelas poderiam fazer parte de uma interface focada nesse tipo de operação. Esse lembrete serve para mostrar a importância de se analisar do contexto do que está sendo trabalhado.

## Evitando detalhes nos nomes dos métodos

Além evitar detalhes nos parâmetros, também é importante não expor detalhes nos nomes de métodos de uma interface, caso contrário, o nome vai acabar revelando detalhes sobre o seu funcionamento, por isso é importante que o método mostre o que faz, mas não mostre detalhes de como faz determinada ação. 

Caso o nome do método revele detalhes de implementação ela estará prejudicando a abstração e, consequentemente, prendendo os objetos a esses detalhes (limitando eles). Um exemplo é a definição de um método chamado `lerJSON` em uma interface para leitura de um documento, esse método revela detalhes de implementação, pois informa um tipo de documento (que no caso é JSON) em seu próprio nome, limitando a criação de implementações a esse tipo específico de documento. 

Segue a interface que ilustra a situação em questão:

```php
<?php

/**
 *
 * Exemplo de como evitar detalhes em interfaces
 * @author Raphael da Silva
 *
 */
interface LeitorDeArquivoDeConfiguracao
{

    public function lerJSON(string $arquivo): array;

}
```

O nome `lerJSON` dado para o método é ruim, pois revela detalhes que limitam a tudo a um formato de arquivo JSON. Obviamente, a limitação é conceitual e não técnica, portanto nada impede que na prática seja feito o seguinte:

```php
<?php

/**
 *
 * Exemplo de como evitar detalhes em interfaces
 * @author Raphael da Silva
 *
 */
class LeitorDeArquivoDeConfiguracaoIni implements LeitorDeArquivoDeConfiguracao
{

    public function lerJSON(string $arquivo): array
    {

        return parse_ini_file($arquivo);

    }

}
```

Como é possível perceber, o código não faz sentido conceitualmente por causa dos nomes de classe e método, pois o método contém JSON no nome e na prática está sendo lido um arquivo INI. Esse seria o tipo de erro que a interface geraria por conter um método que é específico demais e que, portanto, não abstraí a operação.

O foco da interface em questão deveria ser na ideia de ler um documento de forma abstrata, ou seja, sem focar em nenhum detalhe como o formato específico do documento que vai ser lido, o que volta para um exemplo que eu descrevi lá no capítulo sobre abstração. 

Para melhorar a interface um nome que não revela detalhes deveria ser adotado, como no exemplo a seguir:

```php
<?php

/**
 *
 * Exemplo de como evitar detalhes em interfaces
 * @author Raphael da Silva
 *
 */
interface LeitorDeArquivoDeConfiguracao
{

    public function lerArquivo(string $arquivo): array;

}
```

Com o novo nome (que é mais abstrato) qualquer tipo de arquivo pode ser lido, pois o detalhe foi ocultado da assinatura do método presente na interface, consequentemente qualquer implementação pode ser livre para implementar qualquer tipo de leitura de arquivo sem ficar preso a arquivos JSON como o nome anterior deixava.

O exemplo que antes estava conceitualmente confuso, agora ficaria correto. Segue o código:

```php
<?php

/**
 *
 * Exemplo de como evitar detalhes em interfaces
 * @author Raphael da Silva
 *
 */
class LeitorDeArquivoDeConfiguracaoIni implements LeitorDeArquivoDeConfiguracao
{

    public function lerArquivo(string $arquivo): array
    {

        return parse_ini_file($arquivo);

    }

}
```

## A importância de evitar detalhes nas assinaturas dos métodos

Os métodos presentes em uma interface não devem revelar detalhes de implementação, pois como os exemplos mostrados neste capítulo ilustraram, o problema de revelar detalhes específicos é que as implementações da interface serão limitadas por esses detalhes e, consequentemente, isso acaba tirando um dos principais benefícios do uso de interfaces, que é liberdade para criar implementações totalmente diferentes de uma mesma interface.

Nos exemplos foram mostradas formas de se desprender dos detalhes tanto nos parâmetros informados quanto nos próprios nomes escolhidos para os métodos da interface. Tudo foi uma forma de mostrar como tirar os detalhes das assinaturas dos métodos.

### Referências

* GAMMA, Erich; HELM, Richard; JOHNSON, Ralph; Vlissides, John. Design Patterns: Elements of Reusable Object-Oriented Software. Edição 1.

***

### 💀💀💀 Case Closed: é isso... 💀💀💀

Gosto muito do grupo de Rap Cypress Hill (💀💀💀), existe uma música deles chamada "Case Closed", que traduzindo significa "Caso Encerrado". Referenciei o nome dessa música para encerrar esse artigo. 

Caso encerrado (aka Case Closed)!!!!

![cypress cover](https://i.scdn.co/image/ab67616d0000b2734e51c518e787896bc8cdb1a5)
