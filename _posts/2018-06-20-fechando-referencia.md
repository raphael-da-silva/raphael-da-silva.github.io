---
layout: post
title: PHP - Lembrando de fechar as referências de arquivos abertos
date: 2018-06-20 13:48
---

É preciso fechar a referência a arquivos abertos para poder removê-los ou movê-los após a manipulação. Lembrar de fechar a referência do arquivo evita erros que podem ser confundidos com permissão de chmod, além de poupar um bom tempo que seria desperdiçado na tentativa de descobrir a causa do problema.

```php
$file = fopen('filename.txt', 'r');

// É necessário fechar a referência, caso contrário, não será possível apagar o arquivo.
fclose($file);

// Caso fclose não fosse chamado, a função unlink iria falhar.
unlink($file);
```

### Reforçando para não esquecer

Sei que isso pode parecer óbvio, mas para mim não foi quando aconteceu. Por isso, acho válido compartilhar essa informação para lembrar de checar se a referência do arquivo foi fechada corretamente.