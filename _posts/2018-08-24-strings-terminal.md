---
layout: post
title: CLI - Passando strings complexas como argumentos
date: 2018-08-24 18:48
---

Por padrão, no terminal tudo entre espaços vai ser interpretado como coisas separadas. Por exemplo, no script a seguir o argumento vai se transformar em "mais", "de", "uma" e "palavra". Ou seja, eles serão reconhecidos como argumentos separados e não como uma string única.

```bash
myscript mais de uma palavra
```

Para passar uma string com mais de uma palavra sem que ela seja interpretada como argumentos separados, é preciso colocá-las entre aspas. Basicamente, é como se o argumento fosse escapado para ser reconhecido como único no terminal.

```bash
# Exemplo da declaração correta dos argumentos da string.
myscript "mais de uma palavra"
```