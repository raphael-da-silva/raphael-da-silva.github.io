# Buscando definir a responsabilidade de um objeto

Os objetos de uma aplicação são melhores quando têm uma responsabilidade bem definida, pois isso facilita o entendimento do código e a sua manutenção. Objetos menores e coesos também são mais fáceis de combinar com outros para realizar novas funcionalidades, além de serem mais fáceis de utilizar em contextos diferentes, pois focam em uma funcionalidade só (sendo mais granulares).

## O problema de misturar várias responsabilidades

Se um objeto ter mais de uma responsabilidade a chance de reaproveitamento é reduzida, já que um contexto onde seja necessário essas duas (ou mais) responsabilidades será mais difícil de acontecer. Para que um objeto tenha uma responsabilidade bem definida e seja coeso a separação é algo essencial, pois ela permite que componentes menores com um foco bem definido sejam criados.

Basicamente, quando um objeto possui mais de uma responsabilidade ele se torna mais difícil encontrar cenários onde ele possa ser reutilizado, pois as responsabilidades extras que o objeto carrega prejudicam o seu reúso, já que quanto mais responsabilidades, menores são as chances de surgir um contexto que precise dessas responsabilidades que estão misturadas.

## Decomposição: um caminho para definir as responsabilidades

A decomposição consiste no processo de extrair partes de um componente de um software para criar componentes menores, mais simples e coesos. Ou seja, é a ação de "quebrar" as coisas em partes menores. Os objetos criados com a prática de decomposição podem ser utilizados para compor novos objetos facilmente, já que possuem uma responsabilidade mais bem definida.

A prática de decomposição também facilita a manutenção e o reaproveitamento destes componentes, além de diminuir a complexidade, já que o funcionamento do software como um todo é fragmentado em componentes menores e de mais fácil entendimento que juntos formam algo mais complexo.

### Decompondo para ter uma responsabilidade bem definida

Um envio de e-mail com log é uma tarefa que pode acontecer em um projeto, portanto essas operações serão utilizadas para mostrar um exemplo prático de como decompor para separar as responsabilidades que o código deve ter.

No cenário onde um objeto envia um e-mail e registra um log dessa operação, pode ser necessário reutilizar apenas uma dessas duas operações em outro ponto. Caso seja necessário apenas o envio de e-mail ou o registro de log não será possível utilizar essas funcionalidades separadamente se elas estiverem misturadas, pois o objeto possui mais de uma responsabilidade. A classe ```RegistroDeUsuario``` a seguir exemplifica esse tipo de mistura responsabilidades.

```php
<?php

class RegistroDeUsuario
{

    private $pdo;
    private $arquivo;

    public function __construct(
        PDO $pdo,
        $arquivo = 'arquivo-log.txt'
    ){

        $this->pdo     = $pdo;
        $this->arquivo = $arquivo;

    }

    private function salvarDadosUsuario(array $dados)
    {

        $sql  = 'INSERT INTO usuarios (nome, ano) 
                VALUES (:nome, :ano)';
                
        $stmt = $this->pdo->prepare($sql);
        $stmt->execute([
            ':nome' => $dados['nome'],
            ':ano'  => $dados['ano']
        ]);

    }

    private function log($mensagem)
    {

        file_put_contents($this->arquivo, $mensagem, FILE_APPEND);

    }

    public function registrarUsuario(array $dados)
    {

        $this->salvarDadosUsuario($dados);
        $this->log('O usuário foi registrado.');

    }

}
```

O ideal nesse caso é decompor o objeto em dois outros objetos, cada um com uma única responsabilidade. Quando esses novos objetos precisarem funcionar em conjunto basta passá-los para o outro objeto que necessita deles.

Decompondo o código da classe mostrada, as responsabilidades extras seriam separadas em duas novas classes. A primeira seria responsável apenas por salvar os dados do usuário.

```php
<?php

class DadosUsuario
{

    private $pdo;

    public function __construct(
        PDO $pdo
    ){

        $this->pdo = $pdo;

    }

    public function salvarDadosUsuario(array $dados)
    {

        $sql  = 'INSERT INTO usuarios (nome, ano) 
                VALUES (:nome, :ano)';
                
        $stmt = $this->pdo->prepare($sql);
        $stmt->execute([
            ':nome' => $dados['nome'],
            ':ano'  => $dados['ano']
        ]);

    }

}
```

A segunda é responsável por fazer o log de uma mensagem em um arquivo.

```php
<?php

class GeradorDeLog
{

    private $arquivo;

    public function __construct(
        $arquivo = 'arquivo-log.txt'
    ){

        $this->arquivo = $arquivo;

    }

    public function log($mensagem)
    {

        file_put_contents($this->arquivo, $mensagem, FILE_APPEND);

    }

}

```

Após a criação das novas classes, a classe```RegistroDeUsuario``` que antes continha todas as responsabilidades misturadas seria refatorada para uma nova versão. Segue o código dessa nova versão da classe:

```php
<?php

class RegistroDeUsuario
{

    private $dadosUsuario;
    private $geradorDeLog;

    public function __construct(
        DadosUsuario $dadosUsuario,
        GeradorDeLog $geradorDeLog
    ){

        $this->dadosUsuario = $dadosUsuario;
        $this->geradorDeLog = $geradorDeLog;

    }

    public function registrarUsuario(array $dados)
    {

        $this->dadosUsuario->salvarDadosUsuario($dados);
        $this->geradorDeLog->log('O usuário foi registrado.');

    }

}
```

Ao separar as funcionalidades em objetos diferentes elas podem ser utilizadas em contextos variados livremente. No exemplo, o log e a lógica para salvar os dados do usuário foram separadas para serem representadas pelas classes ```GeradorDeLog``` e ```DadosUsuario```, respectivamente. A partir dessa separação, essas classes criadas podem ser reaproveitadas em outras partes de um projeto.