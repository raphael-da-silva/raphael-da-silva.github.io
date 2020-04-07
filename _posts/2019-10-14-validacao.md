---
layout: post
title: Reflexão - Sobre a validação de dados no Back-end e Front-end
---

Confesso que validação de dados nunca foi o meu forte, pois aprendi a fazer isso errado no começo da carreira, já que eu tive os primeiros contatos no estágio com projetos que só validavam os dados no front-end, logo eu achava que aquela era a única forma de fazer. Além de aprender errado, eu nunca achei essa parte muito legal, pois sempre achei ela burocrática demais (apesar de extremamente necessária).

Depois de anos estudando programação e, principalmente, a parte de back-end com PHP, eu comecei a me conscientizar da importância de validar os dados de entrada (aka input) no back-end, também aprendi que a validação de front-end é apenas uma comodidade para o usuário não ter que recarregar a página indo e voltando em várias requisições. Aprender errado é sempre um problema (e desgaste), pois é preciso se corrigir para depois começar a aprender o jeito certo.

### Sobre a falsa dicotômicia da validação back-end vs. front-end

A validação no back-end é mais segura e garantida, pois a ela não pode ser desabilidada como acontece com a validação do front-end via Javascript, porém ela não é tão intuitiva e rápida para o usuário devido a ida e volta entre as páginas até que os dados estejam válidos.

Já na validação com Javascript no lado do front-end, a interação é melhor para o usuário, pois a página não precisa ser carregada a cada tentativa de requisição. No entanto, ela pode ser desabilitada e a aplicação pode ficar vunerável.

A validação de dados do usuário (input) pode (e deve) ser feita no back-end (com a linguagem no lado do servidor) ou no front-end (com Javascript). O ideal é que sejam feitas em ambas, pois cada uma oferece diferentes vantagems e desvantagens e, por isso, uma acaba complementando a outra.
