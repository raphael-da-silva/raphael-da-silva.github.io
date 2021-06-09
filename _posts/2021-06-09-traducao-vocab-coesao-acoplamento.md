---
layout: post
title: A tal da alta coesão e baixo acoplamento
---

Quando tive os primeiros contatos com a Orientação a Objetos, eu ouvia a frase "Alta coesão e baixo acoplamento" diversas vezes. O problema é que aquilo ficava vago, pois não era mostrado como obter essas vantagens. O foco deste livro foi o baixo acoplamento, porém antes de finalizar irei abordar a alta coesão é a contraparte dessa ideia tão difundida no paradigma. 

O conceito de coesão é utilizado para definir o quanto as operações presentes em um objeto estão relacionadas umas com as outras. Basicamente, um objeto é coeso quando faz exatamente o que se propõe, sem ir além disso. Ou seja, é quando ele que possui operações que estão focadas em compor uma determinada responsabilidade, sem misturar conceitos que não estão relacionados entre si.

Por exemplo, um objeto feito para salvar um cadastro no banco de dados e também gerar mensagens de log não é coeso, pois a responsabilidade de gerar uma mensagem de log não deveria estar nele. Para que esse objeto fosse coeso, ele deveria ter somente métodos relacionados ao cadastro no banco de dados e os detalhes necessários para realizar esse tipo de operação. Já o log deveria ter uma classe própria para ele.

Na minha visão, a frase "alta coesão e baixo acoplamento" usa palavras rebuscadas e complexas que não ajudam muito os iniciantes. Talvez se a frase "Alta coesão e baixo acoplamento" fosse traduzida por "Objetos flexíveis e com responsabilidades limitadas" as coisas seriam mais intuitivas logo de início. 

Ou melhor, se a frase fosse substituida por "use abstrações como parâmetros e mantenha só uma responsabilidade" tudo ficaria ainda mais evidente. 

### O papel da linguagem (não a de programação)

O propósito desse artigo foi fazer essa simplificação didática que evita o uso desses termos complexos e pouco intuitivos para quem inicia a aventura de entender melhor a Orientação a Objetos. 

A linguagem rebuscada e complexa dos termos do paradigma foi uma barreiraque encontrei no começo, ou seja, a barreira não foi a linguagem da programação, mas sim a linguagem usada entre programadores no seu vocabulário.

### 💀💀💀 Case closed: é isso... 💀💀💀

Gosto muito do grupo de Rap Cypress Hill (💀💀💀), existe uma música deles Chamada "Case Closed", que traduzindo significa "Caso Encerrado". Referenciei o nome dessa música para encerrar esse artigo. Caso encerrado (aka Case Closed)!!!!

![cypress cover](https://i.scdn.co/image/ab67616d0000b2734e51c518e787896bc8cdb1a5)