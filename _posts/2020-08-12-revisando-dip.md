---
layout: post
title: POO - Revisando o princípio da inversão de dependência (DIP)
---

Eu sempre entendi o princípio da inversão de dependência (DIP) como dependender de abstrações (interfaces e classes abstratas), essa visão veio do contato que tive com esse princípio no meio do aprendizado da injeção de dependência, que é incentivada com abstrações para seguir o principio DIP. Só que essa visão era limitada e focada em um só lado do conceito.

Além depender de abstrações (usando a injeção de dependência), existe um outro lado na inversão de dependência que é mais conceitual e consiste em módulos de alto nível (mais próximos no usuário) que dependem de módulos de baixo nível (mais próximos do computador/máquina). Módulos, nesse contexto, se referem ao código (classes, interfaces e etc).

O lado que eu abordava não estava errado, porém o meu foco restrito fez eu não ver o outro lado desse princípio, ou seja, a visão que eu tinha era incompleta. Antes eu não tinha me atentado e percebido essa relação entre código de alto nível e o código de baixo nível, essa é mais uma das revisões em orientação a objetos que me mostram que quando mais estudo, mais vejo que não sei nada.

Usar camadas como Domain e Infrastructure me fizeram perceber mais ainda como é a aplicação completa do princípio DIP, pois a primeira camada é alto nível e não depende da segunda, já a segunda é baixo nível e depende da primeira. Ou seja, módulos de alto nível não dependem de módulos de baixo nível, mas sim o contrário. É justamente isso que a definição clássica do princípio DIP diz.