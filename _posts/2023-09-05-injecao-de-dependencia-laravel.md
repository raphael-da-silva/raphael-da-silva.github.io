---
layout: post
title: Injeção de dependência, interfaces e Laravel
date: 2023-09-05
---

Em 2020 eu fiz um repositorio com o Laravel, o objetivo era testar o framework, busquei usar inferfaces para desacoplar o código. Nisso injetei nos controllers a dependencia para uma interface, que é programar voltado para abstrações, pois isso desacopla o código, o que significa poder trocar de implementações.

```php
<?php

namespace App;

use \stdClass as User;

/**
 *
 * @author Raphael da Silva
 *
 */
interface UserFinder
{
   	public function getById(int $id): User;
}
``

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Contracts\Support\Renderable;
use App\UserFinder;

/**
 *
 * @author Raphael da Silva
 *
 */
class UserDetailsController extends Controller
{
	private $userFinder;

	public function __construct(
		UserFinder $userFinder
	){
		$this->userFinder = $userFinder;
	}
    
	public function index(int $id): Renderable
	{
		return view('user-details', [
			'user' => $this->userFinder->getById($id)
		]);
	}

}
```

Ou seja, a interface ```UserFinder``` permite criar qualquer classe para buscar um usuario. A implementacao padrao foi usando os componentes (as classes) de acesso a banco de dados o Laravel, pois essa implementacao em questão busca usuarios no banco de dados. Mas poderia ser em qualquer outra fonte de dados (um arquivo XML, um arquivo JSON).

E o acesso ao banco de dados do Laravel é um monte de método estático (agrupado num namespace chamado DB, que significa DataBase) do qual nao gosto muito, mas a beleza da coisa é que isso nao importa pq todo esse código esta abstraido com a interface, apenas a implentacao (```LaravelDBUserFinder```) usa esses métodos estáticos que sao pertinentes a como o Laravel faz as coisas no seu ecossistema.

```php
<?php

namespace App;

use App\UserFinder;
use Illuminate\Support\Facades\DB;
use \stdClass as User;
use Illuminate\Database\Eloquent\ModelNotFoundException;

/**
 *
 * @author Raphael da Silva
 *
 */
class LaravelDBUserFinder implements UserFinder 
{
   	public function getById(int $id): User
   	{
   		$user = DB::table('users')->find($id);

   		if(is_null($user)){
   			throw new ModelNotFoundException('User not found.');
   		}

   		return $user;
   	}
}
```

Eu nao sou fluente em Laravel, nem domino esse framework, o máximo que fiz com ele foi testes para vagas de emprego (porque ele é muito usado pelo mercado, virou uma espécie de convencao), mas tento observar a arquitetura das coisas e busoc desacoplar o código no paradigma da orientacao a objetos. Entao gosto de ver as interfaces aplicadas e como isso traz legibilidade e desacoplamento para o código.

Link para o repositório: https://github.com/raphael-da-silva/testando-o-laravel

