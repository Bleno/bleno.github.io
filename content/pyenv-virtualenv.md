Title: Gerenciando virtualenv com pyenv-virtualenv
Date: 2015-04-15 12:00
Modified: 2015-04-15 12:00
Category: Programação
Tags: Python, pyenv, virtualenv, pyenv-virtualenv
Slug: gerenciando-virtualenv-com-pyenv-virtualenv
Authors: Bleno Silva
Summary: Gerenciando virtualenv com pyenv-virtualenv

# Overview

pyenv-virtualenv é um plugin do pyenv que provê alguns recursospara gerenciar virtualenvs para ambientes Python em Sistemas "Like Unix".


# Instalação

## Instalando como um plugin do virtualenv

Iremos instalar o pyenv-virtualenv como um plugin do pyenv no seguinte diretório ~/.pyenv/plugins/pyenv-virtualenv


* Clone o projeto dentro do diretório de plugin do pyenv:

    $ git clone https://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv

* Adicionar pyenv virtualenv-init para o shell  e habilitar o auto-activation dos virtualenvs. Esse recurso é opcional mas bastante útil.

    $ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile

* Reinicie o shell para habilitar pyenv-virtualenv

    $ exec "$SHELL"


# Usando pyenv virtualenv com pyenv

Para criar um virtualenv para o Python usando pyenv, execute pyenv virtualenv, especifique a versão Python que você quer e o nome do diretório do virtualenv:


    $ pyenv virtualenv 2.7.10 my-virtual-env-2.7.10

Criando um virtualenv apartir da versão atual

Verifique qual versão python você está utillizando:

    $ pyenv version
    3.4.3 (set by /home/yyuu/.pyenv/version)

Crie o virtualenv

    $ pyenv virtualenv venv34

# Fonte

https://github.com/yyuu/pyenv-virtualenv
