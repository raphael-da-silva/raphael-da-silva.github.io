---
layout: post
title: Post de Quarentena - Namorando com interfaces
---

Imagine que alguém quer namorar e deseja que seu namorado seja carinhoso. Para isso, o namorado deve se comportar de certa maneira, pois para ser carinhoso ele deve fazer o seguinte:

* Beijar
* Abraçar
* Entrelaçar os dedos

Ou seja, para ser o namorado esperado, o namorado deve implementar a seguinte interface e fazer as seguintes operações:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
interface NamoradoCarinhoso
{

    public function beijar();

    public function abracar();

    public function entrelacarOsDedos();

}
```

Agora um cara carinhoso mais introvertido pode implementar essa interface fazendo as ações (operações) do seu jeito (de acordo com a sua implementação):

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class CaraIntrovertido implements NamoradoCarinhoso
{

    public function beijar()
    {   

        echo 'Beijo delicado';

    }

    public function abracar()
    {

        echo 'Abraço delicado';

    }

    public function entrelacarOsDedos()
    {

        echo 'Dedos entrelaçados de forma calma';

    }

}
```

Além do cara mais introvertido, um cara mais extrovertido também pode implementar a interface e, com isso, ser um namorado carinhoso:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class CaraExtrovertido implements NamoradoCarinhoso
{

    public function beijar()
    {

        echo 'Beijo intenso';

    }

    public function abracar()
    {

        echo 'Beijo intenso';

    }

    public function entrelacarOsDedos()
    {

        echo 'Entrelaçar de dedos intenso';
        
    }

}
```

Para a namorada um cara que atenda a interface ```NamoradoCarinhoso``` poderá ser um namorado para ela, pois ela procura alguém que seja carinhoso e se comporte dessa forma como a interface representa. Segue a classe que representa a namorada:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class Namorada
{

    private $namorado;

    public function __construct(
        NamoradoCarinhoso $namorado
    ){

        $this->namorado = $namorado;

    }

    public function namorar()
    {

        $this->namorado->abracar();
        $this->namorado->beijar();
        $this->namorado->entrelacarOsDedos();

    }

}
```

Como é possível perceber, a namorada espera alguém que atenda o comportamento esperado, logo **ela confia na interface que atenda isso e todo mundo sabe que confiança é a base para um relacionamento (tando em objetos quanto em namoros).**