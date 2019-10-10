---
layout: post
title: POO - Interfaces sem métodos. Qual a utilidade disso?
date: 2018-06-29 10:39
---

Em orientação a objetos existe uma prática que a primeira vista não faz sentido, pelo menos não fazia quando eu estava iniciando a programar. A prática a qual eu me refiro é a criação de interfaces sem métodos, também conhecidas como **marker interfaces**.

```php
interface Serializable
{

}
```

Mesmo parecendo que o código acima não tem propósito, ele tem sim. Com esse tipo de interface se define um tipo, o objetivo é utilizar esse tipo para tomar alguma decisão, ou seja, esse tipo de interface identifica um objeto para fazer algo com ele.