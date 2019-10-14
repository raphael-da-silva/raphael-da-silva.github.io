---
layout: post
title: Ferramentas - Ambiente no Windows com Laragon
---

Confesso que nunca gostei muito de configurar ambientes para desenvolvimento, sempre preferi dedicar tempo para o código-fonte do projeto. Por isso, sempre utilizei programas que empacotam as principais ferramentas para desenvolvimento, comecei como todo mundo utilizando Xampp. Depois utilizei Linux por alguns anos e continuei com o Xampp, só que configurando Virtual Hosts manualmente.

Quando voltei para o Windows passei a usar o Wammp, pois ele parecia uma ferramenta mais moderna e prática do que do Xampp, além disso, ele permitia a criação de Virtual Hosts no Windows de forma prática e rápída. No entanto, ele deu alguns problemas e isso me frustrou, consequentemente fui buscar alternativas.

### A solução encontrada

Pesquisando eu encontrei o [Laragon](https://laragon.org/download/), logo de cara ele parecia uma proposta mais interessante, já que ele parece uma evolução das ferramentas citadas anteriormente. Baixei a versão portátil que vem só com o PHP, um servidor Nginx e o MySQL. Logo de cara, existem as seguintes vantagens:

* Os Virtual Hosts são criados automaticamente seguindo o nome do diretório do projeto. Por exemplo, a pasta ```meu-projeto``` é acessada pelo endereço ```meu-projeto.dev```. Além disso, é possível trocar a extensão ```.dev``` para outra de acordo com a preferência do programador.

* A interface gráfica dele oferece um menu que acessa configurações do PHP rapidamente, outra vantagem é a possibilidade de adicionar versões diferentes do PHP e trocá-las rapidamente através desse menu. Com isso, é possível alternar da versão 5 para a 7 da linguagem para utilizá-las em diferentes projetos.

* Ele sobe os serviços rapidamente. Na sua versão portátil tudo é muito rápida, até porque essa é a versão mais simples.

* E-mails enviados com a função ```mail``` do PHP são convertidos para arquivos que podem ser acessados através da interface do Laragon para serem abertos com programas de cliente de e-mail como o Outlook.

Enfim, essa ferramenta está sendo uma opção boa, pois oferece uma praticidade que agiliza muito as coisas na hora de rodar um projeto.