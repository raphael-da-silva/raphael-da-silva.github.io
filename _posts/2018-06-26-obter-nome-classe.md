---
layout: post
title: PHP - Obter o nome completo de uma classe
date: 2018-06-26 18:04
---

A partir da versão 5.5.0 (segundo a [documentação](http://php.net/manual/en/language.oop5.constants.php)), o PHP traz uma constante especial para obter o nome completo de uma classe, ela se chama class e pode ser utilizada através de qualquer classe.

```php

// Imprime MeuPacote\MinhaClasse
echo \MeuPacote\MinhaClasse::class; 

```

A vantagem de utilizar esse recurso está no nome da classe já ser obtido com seu namespace completo, o que é útil em casos onde é preciso não só do nome, mas também do namespace onde a classe se encontra.
