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

    sudo apt-get install apt-transport-https ca-certificates

    sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D


# Instalação via repositório

## Criar arquivo

    sudo vi /etc/apt/sources.list.d/docker.list

Dentro do arquivo
	
    deb https://apt.dockerproject.org/repo ubuntu-trusty main

## Remover repositório antigo

    sudo apt-get purge lxc-docker




# Prerequisites by Ubuntu Version
* Ubuntu Wily 15.10
* Ubuntu Trusty 14.04 (LTS)

	sudo apt-get update

	sudo apt-get install linux-image-extra-$(uname -r)


> Ubuntu Precise 12.04 (LTS)
> For Ubuntu Precise, Docker requires the 3.13 kernel version. If your kernel version is older than 3.13, you must upgrade it. Refer to this table to see which packages are required for your environment:


    $ sudo apt-get update


    $ sudo apt-get install linux-image-generic-lts-trusty

    $ sudo reboot


# Instalar
Agora que os pre requisitos estão instalados, vamos instalar os docker.

    sudo apt-get update

    sudo apt-get install docker-engine

    sudo service docker start


