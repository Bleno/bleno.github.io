Title: Instalando Elastic com Kibana no Ubuntu 14.04
Date: 2015-01-20 15:00
Modified: 2015-04-15 08:49
Category: Programação
Tags: Elastic, Kibana
Slug: instalando-elastic-kibana-no-ubuntu-14-04
Authors: Bleno Silva
Summary: Elastic Kibana


=== Instalando Elastic com Kibana no Ubuntu 14.04 ===




# Dependências ====
## instalação do Java 7
    
    sudo add-apt-repository ppa:webupd8team/java && sudo apt-get update
    
    sudo apt-get install oracle-jdk7-installer



# Baixando e instalando o Elastic ====

    wget https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.1.1/elasticsearch-2.1.1.tar.gz

    tar -zxvf elasticsearch-2.1.1.tar.gz

    cd elasticsearch-2.1.1/

# Instalação via pacote .deb

    wget https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/deb/elasticsearch/2.1.1/elasticsearch-2.1.1.deb

    chmod +x elasticsearch-2.1.1.deb

    sudo dpkg -i elasticsearch-2.1.1.deb

# Alterar configurações de acesso (Optional)

> Muitas dessas configurações podem ser vistas em [Configurações Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-configuration.html), essas configurações vão de acordo com o seu uso e personalização, tal como reservar memória desabilitar o uso de swap entre outras.

    vi /etc/elasticsearch/elasticsearch.yml 


# Liberar porta para acesso externo

    sudo iptables -A INPUT -p tcp --dport 9200 -j ACCEPT


# Iniciar com sistema



    sudo update-rc.d elasticsearch defaults 95 10

    sudo /etc/init.d/elasticsearch start

    curl 'http://localhost:9200/?pretty'



#  Kibana


## Fazer o download:
    
    wget https://download.elastic.co/kibana/kibana/kibana-4.1.4-linux-x64.tar.gz

## Descompactar:

    tar -zxvf kibana-4.1.4-linux-x64.tar.gz


## Abrir o arquivo config/kibana.yml 

    cd kibana-4.1.4-linux-x64
    vi config/kibana.yml


Alterar o elasticsearch.url para o endereço do Elastic


Executar o kibana

    ./bin/kibana

















=======================================================================



=======================================================================
