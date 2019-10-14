---
layout: post
title: Validação - Back-end vs. Front-end
---

A validação de dados do usuário (input) pode ser feita no back-end (com a linguagem no lado do servidor) e no front-end (com Javascript). O ideal é que sejam feitas em ambas, pois cada uma oferece diferentes vantagems e desvantagens e, por isso, uma acaba complementando a outra.

A validação no back-end é mais segura e garantida, pois a ela não pode ser desabilidada como acontece com a validação do front-end via Javascript, porém ela não é tão intuitiva e rápida para o usuário devido a ida e volta entre as páginas até que os dados estejam válidos.

Já na validação com Javascript no lado do front-end, a interação é melhor para o usuário, pois a página não precisa ser carregada a cada tentativa de requisição. No entanto, ela pode ser desabilitada e a aplicação pode ficar vunerável.
