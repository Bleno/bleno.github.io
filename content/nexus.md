Title: Gerenciando virtualenv com pyenv-virtualenv
Date: 2015-04-15 12:00
Modified: 2015-04-15 12:00
Category: Programação
Tags: Python, pyenv, virtualenv, pyenv-virtualenv
Slug: gerenciando-virtualenv-com-pyenv-virtualenv
Authors: Bleno Silva
Summary: Gerenciando virtualenv com pyenv-virtualenv
Status: draft


# Overview

Nexus Repository Manager é uma aplicação em Java que requer o Java Runtime Environment.
O Nexus Repository Manager é uma aplicação servidor com interface web onde é possível criar e gerenciar repositórios.
Nexus Repository Manager pode oferecer repositórios para Docker NuGetnpm Bower Pypi e RubyGems.

# Requisitos

## Instalar o Java da Oracle

Infelizmente, de acordo com a documentação o Nexus não suporta o OpenJDK ou outras versões Java, então:

    sudo add-apt-repository ppa:webupd8team/java

    sudo apt-get update

    sudo apt-get install oracle-java8-installer


# Instalação

## Instalando como um plugin do virtualenv

Faça o download do pacote:

    curl -O https://sonatype-download.global.ssl.fastly.net/nexus/3/nexus-3.3.1-01-unix.tar.gz

Descompactar:

    tar -zxvf nexus-3.3.1-01-unix.tar.gz

    mv nexus-3.3.1-01 /opt/nexus

Antes de configurar o serviço, vamos criar um usuário com permissão de executar o nexus.


    sudo useradd -r nexus


## Todo

* Instalar
* Configurar serviço
* Colocar em um proxy reverso
* Criar um Repositório docker
* https://books.sonatype.com/nexus-book/reference3/install.html#configure-service