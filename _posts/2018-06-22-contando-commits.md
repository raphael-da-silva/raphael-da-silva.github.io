---
layout: post
title: CLI - Contando o total de commits de um repositório git
date: 2018-06-22 19:45
---

O total de commits de um repositório git é uma informação interessante para ter uma noção do fluxo de trabalho em um projeto. Para obter o total basta encadear alguns comandos no terminal.

```shell
git log --oneline | wc -l
```

O que o comando acima faz:

* O git log com o parâmetro --oneline mostra cada mensagem do commit linha por linha.

* O output gerado pelo comando git log é encadeado com pipe para o comando wc.

* O parâmetro -l passado para o comando wc específica que é para mostrar a quantidade de linhas. Nesse caso, a quantidade de linhas do comando anterior será o resultado.
