Title: Instalando e usando docker compose
Date: 2016-12-26 11:53
Modified: 2017-05-11 09:34
Category: Infraestrutura
Tags: Docker, Container, Compose, Ferramentas
Slug: instalando-e-usando-docker-compose
Authors: Bleno Silva
Summary: Docker Container



Compose é a ferramenta que permite definir e executar multiplos containers. É uma ótima forma
para criar ambientes através de seu arquivo de configuração no formato <code>.yml</code>.
 Usando um único comando é possível iniciar todos os serviços a partir do seu arquivo de configuração.


# Verifique se já possui o docker instalado

Caso não tenha do docker instalado veja [instalando o docker]({filename}/docker.md) para mais informações


# Instalado o docker compose

Com o docker instalado instale o python-pip

    $ sudo apt-get install -y python-pip

Então, você pode instalar o Docker Compose:

    $ sudo pip install docker-compose


# Executando um container com Docker Compose

## Exemplo wordpress

No exemplo a seguir, será criado um arquivod docker-compose.yml no qual vai subir
dois serviços: Banco de dados e Wordpress.


	:::yaml
	version: '2'

	services:
	   db:
	     image: mysql:5.7
	     volumes:
	       - db_data:/var/lib/mysql
	     restart: always
	     environment:
	       MYSQL_ROOT_PASSWORD: somewordpress
	       MYSQL_DATABASE: wordpress
	       MYSQL_USER: wordpress
	       MYSQL_PASSWORD: wordpress

	   wordpress:
	     depends_on:
	       - db
	     image: wordpress:latest
	     ports:
	       - "8000:80"
	     restart: always
	     environment:
	       WORDPRESS_DB_HOST: db:3306
	       WORDPRESS_DB_USER: wordpress
	       WORDPRESS_DB_PASSWORD: wordpress
	volumes:
	    db_data:



Então temos dois serviços configurados _db_ e _wordpress_, o serviço db utiliza a imagem mysql:5.7
 onde utiliza o volume db_data e restart always.
  Já o serviço wordpress tem um _depends\_on_ no qual segnifica que esse serviço depende do serviço db.
  Para mais informações ssbre o [Compose file](https://docs.docker.com/compose/compose-file/)


Nesse exemplo a cima foi criado uma pasta chamada my_wordpress e o arquivo docker-compose.yml foi salvo dentro dela.

Agora pra executar basta entrar na poasta my_wordpress fazer o seguinte comando:

    $ docker-compose up -d


## Parar / apagar

__docker-compose down__ irá remover os containers e a rede padrão, mas vai preservar o banco de dados do wordpress.
 __docker-composer down --volumes__ irá remover os containers, rede padrão e o banco de dados wordpress.