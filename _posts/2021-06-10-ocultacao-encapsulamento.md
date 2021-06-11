---
layout: post
title: "Encapsulamento: detalhes de objetos ocultados/escondidos e fechados na capsula"
---

O encapsulamento é um conceito fundamental dentro da orientação a objetos, através dele objetos definem o que poderá ser acessado de dentro deles. Encapsular partes do código de um objeto é uma parte importante do paradigma, uma parte conceitual que deve ser protegida como se estivesse dentro de uma capsula...

## Encapsulando e protegendo

O encapsulamento consiste em proteger e evitar a exposição dos detalhes de implementação de um objeto dentro de um software, exemplificando com uma analogia, seria como se esses detalhes estivessem dentro de uma “capsula” sendo protegidos e não sendo expostos ao mundo exterior. 

Não sei se essa analogia é conhecida, mas a palavra encapsulamento remete a capsula, logo se acaba chegando nisso. Tanto que a palavra na língua portuguesa remete a isso, segue as definições de encapsular de acordo com o site www.dicio.com.br:

> Circundar, rodear de uma cápsula.

> Incluir ou proteger alguma coisa em uma cápsula.

> Rodear a si mesmo com uma cápsula.

O vocabulário e a linguagem (além da linguagem de programação) é algo que sempre busquei deixar bem nítido, logo remeter a palavra fora da programação é uma forma de trazer isso para a didática. Como é possível ver na definição do dicionário, encapsular remete a ideia de proteger e enconder as coisas dentro de algo. **Esconder** é uma palavra-chave aqui, pois algo escondido está **oculto**.

<!--
> Encapsulation can be defined as the hiding of internal data representation and implementation details in an object. The only way to access the data within an encapsulated object is to use defined operations. By using encapsulation, you are enforcing information hiding. (HERMES, DIAZ, 2008,  p.26)
-->

> Encapsulamento pode ser definido como esconder os dados internos e os detalhes de implementação em um objeto. O único modo de acesso aos dados de um objeto encapsulado é o uso de suas operações definidas. Usando o encapsulamento, você está forçando a ocultação de informação. (HERMES; DIAZ, 2008, p.26, tradução nossa)

Com o uso do encapsulamento os objetos clientes não podem modificar detalhes que são essenciais para o funcionamento do objeto que os objetos clientes estão requisitando, isso evita efeitos colateriais indesejados e faz com que o estado dos objetos seja mais consistente, já que os dados essenciais para o funcionamento do objeto não podem ser modificados diretamente porquem consome eles externamente. 

Um objeto encapsulado só expõe suas operações, protegendo seus dados e detalhes internos das operações. É uma forma de ter uma proteção, é uma capsula que encapsula o que é a parte interna de um objeto e, com isso, esconde/oculta esse lado interno. Isso leva até a ocultação de informação.

<!--
Ao evitar o acesso e a violação dos dados internos de um objeto, o encapsulamento também evita o acoplamento, pois a restrição de acesso aos detalhes de implementação de um objeto não permite que os clientes trabalhem desacoplados com esses detalhes de implementação, já que eles não são acessados por conta da camada externa de proteção que o encapsulamento fornece.
-->

## Ocultação de informação (aka Information Hiding)

Ocultação de informação (Information Hiding) é um dos princípios essenciais da orientação a objetos, o seu objetivo é isolar os objetos de detalhes internos e dos efeitos que mudanças internas podem gerar fora do objeto (tendo objetos mais isolados dentro de um software).

O propósito desse princípio é não revelar como um objeto faz algo, ou seja, detalhes de implementação não devem ser expostos na [comunicação entre objetos](https://raphael-da-silva.github.io/td-troca-de-mensagens/), pois **os objetos devem expor apenas o que fazem, mas não os detalhes do que fazem**. Isso é o que esse principio trata em essência.

<!--
Trabalhar ocultando os detalhes de implementação é essencial para uma boa manutenção, pois os objetos conseguem trabalhar uns com os outros evitando o acoplamento com detalhes específicos, o que evita que a mudança desses detalhes afetem outros objetos dentro do software.

-->

## Encapsulamento + Ocultação de informação

O princípio de ocultação de informação está bastante ligado ao conceito de encapsulamento, pois através do encapsulamento é possível evitar a exposição e o acesso de detalhes de um objeto e, consequentemente, fazer com esses detalhes sejam ocultados. Esse fator faz com que o encapsulamento esteja bastante ligado ao princípio de ocultação de informação.

<!--
> How is encapsulation related to information hiding? You can think of it as two ways of referring to the same idea. Information hiding is the goal, and encapsulation is the technique you use to accomplish that goal.
-->

> Como o encapsulamento é relacionado com a ocultação de informação? Você pode pensar como dois caminhos que se referem a mesma ideia. Ocultação de informação é o objetivo, e o encapsulamento é a técnica que você usa para chegar nesse objetivo. (HERMES; DIAZ, 2008, p.26, tradução nossa)

É importante salientar que conceitualmente o encapsulamento não é o mesmo que a ocultação de informação, mas o ato de encapsular faz com que as informações sejam ocultadas, dessa forma o encapsulamento pode ser visto como um caminho para a ocultação de informação.

O isolamento e a proteção que o encapsulamento promove faz com que as informações sobre os detalhes de implementação de um objeto sejam ocultadas. Ou seja, o encapsulamento é uma ferramenta para colocar em prática a ocultação de informação, assim como a citação anterior explicou.

## Vocabulário: o uso do termo encapsulamento (e seus vários aspectos)

Além do encapsulamento ser o ato de restringir o acesso aos detalhes de implementação de um objeto para evitar o acoplamento com esses detalhes, esse termo também é utilizado para designar o ato de adicionar um trecho de código dentro de um componente próprio “encapsulando” esse código em outra parte do software.

O papel do encapsulamento também pode ser explicado com algumas palavras-chave que passam a ideia dos objetivos de se encapsular um código. Entre essas palavras estão:

**Ocultação:** a aplicação do encapsulamento evita a exposição de detalhes de implementação servindo para **ocultar** partes internas e, com isso, alcançar o princípio de ocultação de informação (information hiding).

**Restrição:** um objeto encapsulado **restringe** o acesso aos seus dados e, consequentemente, evita que outros objetos trabalhem acoplados com esses dados. A restrição serve para evitar o acesso a detalhes que não devem ser expostos, essa restrição é feita através dos modificadores de acesso.

**União:** encapsular algo **une** funcionalidades e dados em lugar específico sem expor seus detalhes. De novo, é utilizada a ideia de “capsula”. Aplicar o encapsulamento possibilita a criação de uma **unidade** que representa uma parte do software. Um objeto faz a união de dados e operações dentre de sua estrutura, servindo como um pacote ou capsula para isso.

**Fechamento:** encapsular fecha o acesso aos detalhes internos do objeto, é uma forma de ninguém acessar a "capsula". É um fechamento de escopo que pode se dar através dos modificadores de acesso em linguagem com suporte a isso, ou com IIFEs no Javascript para fechar o acesso global ao código encapsulando e fechando ele dentro da IIFE.

## Os modificadores de acesso existentes

Modificadores de acesso são recursos existentes nas linguagens de programação que tem como objetivo definir a visibilidade de métodos, atributos e constantes de classes. Geralmente, as linguagens trazem os seguintes níveis de visibilidade:

* Private (Privado);
* Protected (Protegido);
* Internal (Interno);
* Public (público);

No PHP não existe (pelo menos ainda) a visibilidade internal, além disso, a possibilidade de definir a visibilidade em constantes só foi adicionada a partir da versão 7.1 da linguagem.

### Um caminho para encapsular

Muitas vezes o encapsulamento é mostrado como sinônimo de modificadores de acesso e visibilidade, mas, na verdade, os modificadores de acesso são ferramentas utilizadas para encapsular estes detalhes, mas não são a garantia de que estes detalhes serão escondidos. 

Assim como classes abstratas e interfaces são recursos usados para abstrair, os modificadores de acesso são recursos usados para encapsular, mas não significa que eles são uma garantia, para isso é preciso usá-los de forma efetiva.

Um exemplo que mostra como os modificadores de acesso não garantem o encapsulamento são o uso de setters de atributo, onde o objeto cliente está modificando e acessando detalhes do objeto que ele utiliza, nesse caso o setter viola a proteção que o atributo privado deveria prover, já que seu uso acaba dando acesso (e, consequentemente expondo) a uma propriedade que em teoria foi "encapsulada" para não ser exposta, mas que indiretamente foi exposta ao poder ser acessada via o setter (que acaba dando uma acesso indireto, mas que cria a ilusão de encapsulamento por conta por acesso não ser direto a propriedade).

Os modificadores de acesso não são obrigatórios e também não são a garantia para se alcançar o encapsulamento, pois esse conceito também pode ser aplicado em linguagens que não possuem esses recursos nativamente, como no caso do Javascript que por muito tempo emulou o controle de visibilidade e fechamento de escopo com características da linguagem como a [IIFE (Immediately Invoked Function Expression)](https://developer.mozilla.org/pt-BR/docs/Glossary/IIFE).

## Usando métodos privados para encapsular detalhes

Métodos privados são úteis para manter o encapsulamento dentro do software, pois a restrição de um método que diz respeito só ao próprio objeto ao qual ele pertence, faz com que os clientes desse objeto não utilizem o método e, consequentemente, ele fica fechado e escondido/ocultado.

Restringir o acesso aos detalhes com os métodos privados evita que os clientes conheçam partes de um objeto que não devem ser acessadas/utilizadas por eles, mantendo assim essas partes encapsuladas.

No exemplo a seguir, o método ```checarFormatoDoArquivo``` está privado para evitar a exposição de uma parte do código que não é pertinente fora da classe ```LeitorDeArquivoJSON```, ou seja, restringir o acesso desse método é uma maneira de ocultar esse tipo de detalhe específico para outros objetos externos.

```php
<?php

/**
 * 
 * Interface que auxilia no exemplo de ocultação e encapsulamento
 * @author Raphael da Silva
 *
 */
interface LeitorDeArquivo
{

    public function ler(): array;

}

/**
 *
 * Exemplo de método encapsulado e ocultado.
 * @author Raphael da Silva
 *
 */
class LeitorDeArquivoJSON implements LeitorDeArquivo
{

    private $arquivo;

    public function __construct(string $arquivo)
    {

        $this->arquivo = $arquivo;

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

        $this->checarFormatoDoArquivo();
        return $this->lerConteudoJson();

    }

}
```

Expor como público o método ```checarFormatoDoArquivo``` não faria sentido, já que ele faz algo relacionado com o tipo de arquivo específico que a classe manipula, que nesse caso é ```JSON```. Logo, essa operação faz parte do funcionamento interno da classe em questão por lidar com um formato específico de arquivo.

Já que o método foca em um detalhe interno de implementação, expor ele é expor algo que é pertinente somente a classe ```LeitorDeArquivoJSON```, logo, isso acaba quebrando o encapsulamento por conta dessa exposição indevida. 

Outra desvatagem é que expor o método `checarFormatoDoArquivo` acabaria fazendo com que os objetos de fora (fora da capsula) fossem responsáveis por requisitar a verificação do formato, o que adicionária uma responsabilidade extra nos objetos que estariam [trocando mensagem](https://raphael-da-silva.github.io/td-troca-de-mensagens/) com os objetos dessa classe `LeitorDeArquivoJSON`.

A classe em questão tem que expor como público só o método da interface que ela implementa (que é o método `ler`), já que ali nada de específico é revelado e, portanto, nenhum acesso a partes internas específicas do funcionamento da classe é dado para fora do escopo dela.

Um último adendo é que, além de respeitar o encapsulamento, o uso de métodos privados também possibilita a separação das responsabilidades de um objeto em métodos pequenos (granulares) que juntos compõem uma tarefa mais complexa. [Essa separação em partes menores foi abordada nessa postagem](https://raphael-da-silva.github.io/metodos-pequenos-granulares/).

### Referências

* HARMES, Ross; DIAZ, Dustin. Pro Javascript Design Patterns. Edição 1. USA: Apress, 2008.
* [Significado da palavra encapsulamento no site dicio.com.br](https://www.dicio.com.br/encapsulamento/)
* https://en.wikipedia.org/wiki/Information_hiding

***

### 💀💀💀 Case Closed (e escope closed...) 💀💀💀

Gosto muito do grupo de Rap Cypress Hill (💀💀💀), existe uma música deles chamada "Case Closed", que traduzindo significa "Caso Encerrado". Referenciei o nome dessa música para encerrar esse artigo. 

Caso encerrado (aka Case Closed)!!!! **No caso desse post sobre encapsulamento não é só o caso que foi fechado, mas o escopo também... Fechado dentro de uma capsula com formato de caveira.** 💀💀💀

![cypress cover](https://i.scdn.co/image/ab67616d0000b2734e51c518e787896bc8cdb1a5)
