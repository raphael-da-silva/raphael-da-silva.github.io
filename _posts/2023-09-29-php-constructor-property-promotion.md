---
layout: post
title: PHP 8.0 - Constructor Property Promotion para simplificar o código
date: 2023-09-29
---

Constructor Property Promotion é um recurso que está disponivel a partir da versão 8.0 do PHP. Com esse recurso o código fica mais simples na definição das propriedades de uma classe, pois dá para definir tudo no construtor, o que vira uma mão na roda quando se trabalha com injeção de dependência, por exemplo.

Segue um exemplo de classe usando Constructor Property Promotion:

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
 
É uma classe simples com os dados de uma entidade, os parâmetros definidos no contrutor são também as propriedades definidas para essa classe, tendo o mesmo nome. Isso elima muito código de inicialização de propriedades no construtor, antes ficaria da seguinte forma:

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

Ou seja, teria muito mais código e teria que escrever mais linhas, o que mostra como esse novo recurso do PHP é algo simplificador. E mostra uma evolução constante da linguagem para trabalhar com Orientação a Objetos. É isso, nesse post eu queria trazer de forma simples e direta o uso de Constructor Property Promotion.