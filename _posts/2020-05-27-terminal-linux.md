---
layout: post
title: CLI - Comandos básicos do terminal
---

Este post tem o objetivo de mostrar os comandos básicos para o terminal do Linux. Esse conteúdo foi fruto da época em que eu usei Linux (com Ubuntu), comecei a usar esse sistema operacional em 2014 para ganhar afinidade com o terminal e poder usar isso na programação. Usei o ubunto até o começo de 2017 quando o computador quebrou (de vez).

***

# Terminal Linux

Seguem os comandos separados por tópicos.

#### Diretórios especiais

```bash

# Diretório atual
./

# Diretório pai do diretório atual
../

# Diretório inicial do usuário/home nos sistemas Linux
~

```

#### Comandos para manipulação de arquivos

```bash

# Mudar de diretório (cd significa change directory)
cd nome-do-diretorio

# Remover um arquivo
rm nome-do-arquivo

# Remover um arquivo recursivamente
# O parâmetro -rf faz com que os arquivos executem a remoção recursivamente.
# Esse comando é útil para remover diretórios (que são arquivos dentro de arquivos, por isso a recursão).
rm -rf nome-do-arquivo

# Mostrar conteúdo de arquivo: 
cat nome-do-arquivo

# Pesquisar por um padrão em um arquivo: 
grep 'string com o padrão' nome-do-arquivo

# Mostra os arquivos ocultos de um diretório
ctrol + H

# Comando para deixar um arquivo executável
# Este comando é extremamento útil para tornar scripts em shell executáveis.
chmod +x nome-do-arquivo

# Copiando um arquivo/diretório (pois um diretório é um arquivo)
cp nome-arquivo nome-destino

# Mover arquivo/diretório
mv nome-do-arquivo caminho/para/destino

# Mudando o chmod em todos os arquivos de um diretório (e não no diretório somente)
# Lembrando que o 777 foi apenas para exemplo e qualquer número referente ao chmod pode ser inserido
chmod 777 diretorio/*

```

#### Comandos para controle do output

```bash
# Avançar uma página em uma listagem
ctrl + v

# Limitar os resultados de um listagem no terminal (passando a saída de um comando para o more com o pipe)
output-do-comando | more

# Salvando a sáida do comando do terminal em um arquivo (redirecionamento de output)
comando > nome-arquivo

# Apagar o conteúdo de um arquivo
echo "" > nome-do-arquivo

```

#### Comandos para usuário root

```bash

# Comando para executar tarefas como administrator
# Sudo significa "super user do" (fazer como super usuário)
sudo nome-do-comando

# Navegação em interface gráfica (arquivos, pastas) como root
sudo nautilus

```

Essa foi uma visão geral dos comandos para fazer o básico. Até o próximo post!
