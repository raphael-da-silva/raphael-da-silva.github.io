---
layout: post
title: Codificação - Condição invertida (a.k.a Yoda Condition)
date: 2018-06-16 00:00
---

Em alguns projetos open-source eu sempre via as condições nos ```ifs``` serem declaradas de forma invertida. Isso era algo que me gerava dúvida e curiosidade. Basicamente, em vez do valor comparado estar depois da variável, em vários projetos grandes ele vinha antes dela, ou seja, a posição era invertida. 

```php
if($name === "User"){
    // ...
}
```
Ao contrário do exemplo acima eu encontrava o seguinte:

```php
if("User" === $name){
    // ...
}
```

Pesquisando descobri que essa prática tem um nome, esse nome é Yoda Condition. Aparentemente, seguir essa prática é uma questão de estilo e não impacta na performance ou na interpretação do código. **Como quase tudo que envolve estilo, uns são a favor e outros nem tanto e, portanto, dificilmente existe um consenso.**

Eu não imaginava que existia um termo próprio para isso, mas ter um nome me ajuda a fazer uma associação e passar a lembrar disso, além disso, o nome é bastante intuitívo para quem conhece Star Wars, pois o mestre Yoda fala de forma invertida, então o código que segua essa condição "fala" para o programador de forma intertida também. Agora sempre que vejo uma condição invertida eu consigo reconhecer e saber o motivo dela estar ali.
