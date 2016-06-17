Title: Instalando Docker Ubuntu 14.04
Date: 2015-04-11 10:00
Modified: 2015-04-15 09:23
Category: Programação
Tags: Docker, Container
Slug: instalando-docker-ubuntu-14-04
Authors: Bleno Silva
Summary: Docker Container

# Dependências

    sudo apt-get update

    sudo apt-get upgrade

    sudo apt-get install apt-transport-https ca-certificates

    sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D


# Instalação rápida

Baixar e executar o script bash de instalação. O script já adiciona o repositório e faz a instalação necessária.

    curl -sSL https://get.docker.com/ | sh

Adicionar o seu usuário ao grupo docker para executar os comandos docker sem precisar de sudo.

    sudo usermod -aG docker neolight

Apartir daqui já é possível usar e fazer o hello word docker =)

    docker run hello-world

Deve apresentar a seguinte saída:

<pre>
Unable to find image 'hello-world:latest' locally
    latest: Pulling from hello-world
    a8219747be10: Pull complete
    91c95931e552: Already exists
    hello-world:latest: The image you are pulling has been verified. Important: image verification is a tech preview feature and should not be relied on to provide security.
    Digest: sha256:aa03e5d0d5553b4c3473e89c8619cf79df368babd1.7.1cf5daeb82aab55838d
    Status: Downloaded newer image for hello-world:latest
    Hello from Docker.
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
     1. The Docker client contacted the Docker daemon.
     2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
            (Assuming it was not already locally available.)
     3. The Docker daemon created a new container from that image which runs the
            executable that produces the output you are currently reading.
     4. The Docker daemon streamed that output to the Docker client, which sent it
            to your terminal.

    To try something more ambitious, you can run an Ubuntu container with:
     $ docker run -it ubuntu bash

    For more examples and ideas, visit:
     http://docs.docker.com/userguide/
</pre>
Caso ocorra o seguinte erro docker: <pre>Cannot connect to the Docker daemon. Is the docker daemon running on this host?.</pre> saia e conecte novamente no servidor ou recarregue o bash.

    source ~/.bashrc
ou
    bash

# Instalação via repositório

## Criar arquivo

    sudo vi /etc/apt/sources.list.d/docker.list

Dentro do arquivo
	
    deb https://apt.dockerproject.org/repo ubuntu-trusty main

## Remover repositório antigo

    sudo apt-get purge lxc-docker




## Prerequisites by Ubuntu Version
* Ubuntu Wily 15.10
* Ubuntu Trusty 14.04 (LTS)

	sudo apt-get update

	sudo apt-get install linux-image-extra-$(uname -r)


> Ubuntu Precise 12.04 (LTS)
> For Ubuntu Precise, Docker requires the 3.13 kernel version. If your kernel version is older than 3.13, you must upgrade it. Refer to this table to see which packages are required for your environment:


    $ sudo apt-get update


    $ sudo apt-get install linux-image-generic-lts-trusty

    $ sudo reboot


## Instalar
Agora que os pre requisitos estão instalados, vamos instalar os docker.

    sudo apt-get update

    sudo apt-get install docker-engine

    sudo service docker start


