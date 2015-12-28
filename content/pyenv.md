Title: Instalando diferentes versões de Python com pyenv
Date: 2015-12-25 21:08
Modified: 2015-12-25 21:08
Category: Programação
Tags: Python, pyenv
Slug: instalando-diferentes-versões-de-python-com-pyenv
Authors: Bleno Silva
Summary: Instalar pyenv

>Hoje resolvi falar do __pyenv__, que é nada mais nada menos que um gerenciador para instalações de interpretador Python.
>
>__Pyenv__ é um simples e magnifico gerenciador de versões Python, essa ferramenta permite instalar várias versões do interpretador Python e alternar entre elas. O que pode facilitar muito para testar aplicações em diversas versões.

>##O que o pyenv faz?
>
* Permite que você altere a versão global do Python
* Alternar entre versões por projeto Python
* Permitem substituir a versão Python com uma variável de ambiente.
* Pesquisa comandos a partir de múltiplas versões do Python em um momento. Isto pode ser útil para testar em todas as versões do Python com [tox](https://pypi.python.org/pypi/tox "Clique e conheça")


>##Como funciona? 
>
>
>Então, por alto, o __pyenv__ intercepta comandos Python usando o executável shim que foi colocado na variável de ambiente PATH, no qual determina a versão do Python foi solicitada pela sua aplicação, e passa seus comando junto com a correta instalação Python.
>

>##Instalação
>
>####Existe a instalação automática 
[pyenv-installer](https://github.com/yyuu/pyenv-installer)
>
>
>e a instalação manual que é muito fácil também =).

>####Instalação manual:
>
>É basicamente um clone do projeto, um ótimo local para instalação é [$HOME/.pyenv] , mas você pode instalar em qualquer lugar que desejar =).
>
>
    $ git clone https://github.com/yyuu/pyenv.git ~/.pyenv
>
>
>Definir a variável de ambiente PYENV_ROOT:
>
    $ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
    $ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
>
>Adicionar pyenv init ao seu shel:

    $ echo 'eval "$(pyenv init -)"' >> ~/.bashrc
>
>
>Reiniciar o shel para que as alterações façam efeito:
>
    exec $SHELL
>
>Instalar Python. As versões do Python são instaladas em $PYENV_ROOT/versions. Por exemplo vou instalar o Python 3.5.1
>
    $ pyenv install 3.5.1
>
>
>
>##Atualizando
>
>Se você já tem o __pyenv__ instalado, você pode atualizar usando o comando git pull:
>
    $ cd ~/.pyenv
    $ git pull
>
>
>
>##Comando básicos do __pyenv__:
>
    pyenv install x.x.x #instala uma versão específica do Python
    pyenv uninstall x.x.x #desinstala uma versão específica do Python
    pyenv versions # lista todas versões de Python instalada
    pyenv global # Mostra a versão do Python global ou configura passando o número da versão como parâmetro
>    
>####Para mais informações e ajuda:
>    
    pyenv help <comando> # Para informações específicas sobre um comando.
>
>
>##Desinstalando __pyenv__
>
>Remova a linha pyenv init do seu shel (.bashrc)
>Remova  o diretório pyenv shims da várial PATH
>
>Então, remova todas as versões de Python instaladas
>
    rm -rf `pyenv root`


##Local do projeto:
> Para mais informações do projeto
> 
>[https://github.com/yyuu/pyenv](https://github.com/yyuu/pyenv)
