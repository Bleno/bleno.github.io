Title: Instalando Node JS Ubuntu 14.04
Date: 2015-07-11 16:24
Modified: 2015-07-11 16:24
Category: Programação
Tags: nodejs, node, js, instalar, javascript, npm, package manager
Slug: instalando-nodejs
Authors: Bleno Silva
Summary: Node JS npm


# Instalando via script

Esse script automatiza o processo de adicionar repositório.

    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -

# Executando a instalação

    sudo apt-get install -y nodejs

# Atualizando npm

    sudo npm install npm -g

## Para compilar algumas ferramentas nativas é necessário instalar o build tools

    sudo apt-get install -y build-essential


# Referências:

* [https://docs.npmjs.com/getting-started/installing-node#updating-npm](https://docs.npmjs.com/getting-started/installing-node#updating-npm)
* [https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions)