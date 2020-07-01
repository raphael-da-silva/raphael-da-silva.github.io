---
layout: post
title: Javascript - Função construtura e prototype
---

Na época em que eu estava estudando javascript e modularização acabei entrando em contato com o conceito de função construtura e prototype. O uso desses recursos do javascript permitem instânciar as funções como objetos com o operador `new` e usar os métodos adicionados no seu prototype como métodos de instância, assim como classes de outras linguagens de programação.

O código a seguir [que está disponível neste repositório](https://github.com/raphael-da-silva/jquery-menu-prototype) é um exemplo desse uso de funções construtura e prototype. 

```js

/**
 *
 * @author Raphael da Silva
 *
 */
var JqueryResponsiveMenuToggle = (function(){

    // Função construtura
	function ResponsiveMenuToggle(icon, wrapper, toggleClass){

		this.icon    = icon;
		this.wrapper = wrapper;
		this.class   = toggleClass;

	}

    // Armazenando a função no prototype
	ResponsiveMenuToggle.prototype.toggleMenuClass = function(){

		this.wrapper.toggleClass(this.class);

	};

	ResponsiveMenuToggle.prototype.toggleMenu = function(){

		if(this.wrapper.length === 0){
			throw new Error('Menu wrapper not exists in DOM.');
		}

		this.icon.on('click', this.toggleMenuClass.bind(this));

	};

	// A IIFE retorna a função construtora ResponsiveMenuToggle
	return ResponsiveMenuToggle;

})();

```

A função `ResponsiveMenuToggle` que recebeu funções em seu prototype é instanciada com `new` funcionando como uma função construtora que age como o construtor de uma classe. Por isso, é possível usar `this` dentro das funções armazenadas no protype, esse comportamento faz com que essas funções tenham o comportamento de métodos da instância de um objeto.

Outro ponto foi que essa função construtura foi encapsulada em uma IIFE (que foi armazenada na variável `JqueryResponsiveMenuToggle`), ou seja, o uso de prototype/função construtura foi combinado com uma IIFE que retorna a prototype/função construtura.

### Syntax sugar com wrappers

No [repositório original](https://github.com/raphael-da-silva/jquery-menu-prototype) existe um arquivo com o seguinte código-fonte:

```js

/**
 *
 * @author Raphael da Silva
 *
 */
var $menuToggleInit = (function($, menuToggle){

	return function(selectors){

		var menuToggle = new menuToggle(
			$(selectors.icon),
			$(selectors.wrapper),
			selectors.toggleClass
		);

		menuToggle.toggleMenu();

	};

})($, JqueryResponsiveMenuToggle);

```

Basicamente, a função armazenada na variável `$menuToggleInit` funciona como um syntax sugar para instanciar e usar a função construtora `ResponsiveMenuToggle` criada anteriormente. Esse código é um wrapper para facilitar o uso de tudo, seria algo analogo a um método estático que usa uma classe de forma prodecural em linguagens com suporte a orientação a objetos.

Para usar essa função de wrapper é só passar os parâmetro que correspondem aos elementos HTML obtidos via Jquery, segue o código:

```js

$menuToggleInit({
    icon: '.menu-icon',
    wrapper: '.menu-wrapper',
    toggleClass: 'toggle-menu'
});

```