Title: Instalando o Tornado Web Framework
Date: 2015-01-20 15:00
Modified: 2015-04-15 09:25
Category: Programação
Tags: Tornado, Web, Framework, WebSocket
Slug: instalando-o-tornado-web-framework
Authors: Bleno Silva
Summary: Tornado Web Framework



Para desenvolver a aplicação com o tornado escolhi usar a versão mais recente do python que é a 3.5.1. 
Então com a ajuda da ferramenta [pyenv]({filename}./pyenv.md) vou instalar esta versão do python.

# Verifica se a versão 3.5.1 esta disponível
    
    pyenv install --list

# Caso não esteja atualizar o pyenv

    cd /home/bleno/.pyenv/plugins/python-build/../.. && git pull && cd -


# Instalar o python 3.5.1

    pyenv install 3.5.1

A resposta esperada será aproximadamente essa
    
    Installed Python-3.5.1 to /home/bleno/.pyenv/versions/3.5.1

caso tenha problemas com a libbz2

    sudo apt-get install libbz2-dev


# Criar o virtualenv

    virtualenv -p /home/bleno/.pyenv/versions/3.5.1/bin/python project



# Instalando o Tornado

    pip install tornado