---
layout: post
title: Post de quarentena - Injetar é sempre uma opção mais flexível
---

Realizar a injeção de dependência com implementações específicas pode parecer uma prática sem sentido a primeira vista, já que a injeção de dependência prioriza o uso de abstrações. No entanto, ao injetar uma implementação ainda é possível variar o seu comportamento através da herança. Ou seja, a variação de comportamento ainda é possível, mesmo que de forma mais limitada do que quando é utilizada uma abstração.

### Estendendo as dependências injetadas

Ao usar herança para estender a implementação injetada, é possível  mudar seu comportamento sobrescrevendo seus métodos (públicos ou protegidos), resultando em polimorfismo para quem depende da implementaçã que foi injetada. Além disso, existem outras vantagens:

* Injetar torna as dependências utilizadas explicitas e, portanto, o código fica mais legível. Independente de ser uma implementação ou abstração que está sendo injetada, as dependências do objeto ficam explicítas.

* É possível estender a classe injetada para criar um objeto de simulação para os testes, mostrando que o código ainda pode ser testável, mesmo dependendo de uma implementação.

Basicamente, a injeção de dependência traz flexibilidade mesmo quando é algo muito específico que é injetado, pois mesmo parecendo que a limitação é a mesma de uma criação direta da instância, injetar o objeto ainda continua sendo uma opção mais flexível dp que criar uma instância diretamente de forma acoplada.

## Busque dar prioridade para abstrações

É importante lembrar que a injeção de abstrações deve ser sempre priorizada 
para que se alcance flexibilidade. O intuíto aqui é mostrar que injetar uma 
dependência é sempre mais flexível do que criar objetos diretamente uns 
dentro dos outros com o operador ```new```.