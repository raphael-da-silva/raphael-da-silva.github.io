---
layout: post
title: "Ensaio abstrato: a concepção de um processo de abstração de operações"
---

Abstração sempre foi algo que instigou muito dentro da Orientação a Objetos, sempre busquei entender bem essa prática e processar isso na minha cabeça.

A seguir estão as partes úteis para o processo mental de abstrair as operaçoes de objetos no código. São algumas etapas que podem ser englobadas nesse processo.

**Se despreender dos detalhes:** ao abstrair algo os detalhes específicos são ignorados, por isso uma abstração é algo mais genérico, no sentido de focar somente nas características principais de uma operação se despreendo dos seus detalhes.

**Focar na essência das coisas:** um código abstrato foca no conceito principal de uma operação, ou seja, foca na essência de algo que vai ser feito, ou melhor, na noção básica das operações que serão feitas.

**Trabalhar com a noção básica das operações:** ao definir as operações sem focar em detalhes (se despreendendo deles), uma abstração está trabalhando apenas com a noção básica do que vai ser feito através dessa operação.

**Distinguir o abstrato do concreto:** o código abstrato é diferente da implementação que é o código concreto. Essa diferenciação é muito importante para o entendimento do que é uma abstração e qual o seu propósito. Tendo consciência disso, é possível ter noção do que deve ser concreto e o que deve ser abstrato.

**Definir o indefinido:** como uma abstração trabalha com a noção básica de uma operação, ela é algo indefinido, pois a sua definição só feita nas implementações que vão ser a versão concreta da abstração. Uma interface não contém implementação, por isso ela é um exemplo de algo indefinido que é definido através da implementação concreta.

**Juntando cada parte descrita envolvida,** o ato mental de abstrair uma operação consiste no processo de se despreender dos detalhes focando na essência das coisas para trabalhar com a noção básica das operações (métodos) distinguindo o código abstrato (interface ou classe abstrata) do concreto (classe com a implementação concreta) e definindo (através das implementações concretas) o que está indefinido na abstração (interface ou classe abstrata).

***

### 💀💀💀 Case Closed: é isso... 💀💀💀

Gosto muito do grupo de Rap Cypress Hill (💀💀💀), existe uma música deles chamada "Case Closed", que traduzindo significa "Caso Encerrado". Referenciei o nome dessa música para encerrar esse artigo. 

Caso encerrado (aka Case Closed)!!!!

![cypress cover](https://i.scdn.co/image/ab67616d0000b2734e51c518e787896bc8cdb1a5)