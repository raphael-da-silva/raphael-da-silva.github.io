---
layout: post
title: Conceitos - Um resumo sobre o MVC
---

Neste post vou abordar o MVC de uma forma que foque no propósito de cada camada de separação, depois será feita uma reflexão sobre o uso desse modelo de separação atualmente para a web.

***

### Regras de negócio

Antes de focar propriamente no MVC e nas suas definições, é interessante explicar o que são as regras de negócio, pois esse termo é bastante utilizado para abordar a separação de camadas do MVC.

Regras de negócio, no contexto de software, são as regras de definem o funcionamento de um sistema, elas são os requisitos que definem as particularidades que compõem as funcionalidades de projeto.

### Models contém as regras de negócio

A camada de model do MVC se refere , basicamente, as regras de negócio da aplicação, em outras palavras, **ela não está limitada a banco de dados**. Apesar disso, a maioria dos exemplos encontrados na internet mostram só esse uso da camada de Model.

Todas as partes do projeto que são referentes as regras de negócio são pertencentes a camada de model. Não é necessário se limitar, pois essa camada pode conter validações, leitura de dados de arquivos e etc.

***

### Controllers não levam regras de negócio

Os controllers são parte de uma camada intermediaria. Basicamente, eles ligam o model e a view, um controller é referente uma ação de uma requisição HTTP em uma determinada rota. **Os controllers não devem conter regras de negócio**, pois isso, como já foi mencionado, é do model.

Lembre-se: mantenha seus controllers pequenos, não coloque lógicas essenciais da aplicação nele. O papel dele é utilizar os outros componentes e não conter a implementação da funcionalidade.

***

### Views mostram algo

A camada de view gera a parte que o usuário vai visualizar, o que no contexto da web vai ser HTML na maioria das vezes. Porém, é importante saber que uma view não se limita a isso, pois dependendo da aplicação a saída gerada pode ser um XML, um JSON ou qualquer outro tipo de formato.

***

### O MVC e a web atualmente

o MVC foi criado para Desktop, portanto ele não foi pensado para web, apenas foi portado para ela. Hoje existem os micro-frameworks com routers que refletem melhor o funcionamento da web e foram pensados para esse tipo de ambiente. Apesar dessa opção, o MVC ainda é usado em frameworks full-stack.