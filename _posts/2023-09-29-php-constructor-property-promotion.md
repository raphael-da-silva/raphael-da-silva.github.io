---
layout: post
title: PHP 8.0 - Constructor property promotion - PHP
date: 2023-09-29
---

Constructor property promotion é um recurso que está disponivel a partir da versão 8.0 do PHP. Com esse recurso o código fica mais simples na definição das propriedades de uma classe, pois dá para definir tudo no construtor, o que vira uma mão na roda quando se trabalha com injeção de dependência.

Segue um exemplo de classe usando Constructor property promotion.

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class Quote
{
	public function __construct(
		private string $text,
		private string $movie
	){}

	public function getText(): string
	{
		return $this->text;
	}

	public function getMovie(): string
	{
		return $this->movie;
	}
}

```
 
É uma classe simples com os dados de uma entidade, os parâmetros definidos no contrutor são também as propriedades definidas para essa classe, tendo o mesmo nome. Isso elima muito código de inicialização de propriedades no contrustor, antes ficaria da seguinte forma:

```php
<?php

/**
 *
 * @author Raphael da Silva
 *
 */
class Quote
{
	private $text;
	private $movie;

	public function __construct(
		string $text,
		string $movie
	){
		$this->text = $text;
		$this->movie = $movie;
	}

	public function getText(): string
	{
		return $this->text;
	}

	public function getMovie(): string
	{
		return $this->movie;
	}
}
```

Ou seja, teria muito mais código e teria que escrever mais linhas, o que mostra como esse novo recurso do PHP é algo simplificador. E mostra uma evolução constante da linguagem para trabalhar com orientação a objetos. É isso, nesse post eu queria trazer de forma simples e direta o uso de Constructor property promotion.