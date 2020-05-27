---
layout: post
title: CLI - O uso do pipe
---

O pipe é um recurso que serve para mandar o output de um comando para outro, e com isso possibilitar que o resultado de um comando seja passado como parâmetro para o outro, fazendo com que os comandos sejam encadeados.

O nome pipe significa tubo, e isso pode ser utilizado como analogia para compreender melhor o recurso, pois assim como um tubo o pipe passa uma coisa para outra ligando elas.

Abaixo contém um exemplo de dois comandos combinados com o pipe para [contar o total de commits de um repositório no Github](https://raphael-da-silva.github.io/contando-commits/):

```bash
git status -s | wc -l
```

A instrução acima passa o retorno do comando `git status` para o comando `wc` (word count) do Linux , que nesse caso está contando o total de linhas da saída do comando anterior que foi passada com pipe. O uso desse recurso é muito útil, pois faz com que vários programas possam ser utilizados em conjunto para compor tarefas mais complexas (seguindo a filosofia UNIX).
