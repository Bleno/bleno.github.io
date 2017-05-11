Title: Certificado SSL Para Website com NGINX
Date: 2016-11-09 12:00
Modified: 2016-11-09 12:00
Category: Infraestrutura
Tags: Web, Webserver, SSL, Certificado, NGINX, Ubuntu, Centos
Slug: certificado-ssl-para-website-com-nginx
Authors: Bleno Silva
Summary: Docker Container

# Introdução

[Certbot](https://certbot.eff.org/) é um automatizador para instalação de certificados SSL da [Let's Encrypt](https://letsencrypt.org/). 
Como os certificados da Let's Encrypt são válidos por apenas 3 meses a ideia do certbot é  
automatizar a renovação desse certificado além de criar o certificado.

## Instalar

Fazer o download e instalação do certbot-auto script

### Ubuntu

Download

    wget https://dl.eff.org/certbot-auto
    
Permissão de execução

    chmod a+x certbot-auto

certbot-auto instala suas próprias dependêncies inclusive atualiza seu próprio código cliente

    $ ./certbot-auto

### Centos 7

Verifique se você tem os repositório EPEL repository habilitado, caso não, habilite com o seguinte processo [enable the EPEL repository.](https://fedoraproject.org/wiki/EPEL#How_can_I_use_these_extra_packages.3F)
obs: Caso seja Centos 6 pode ser realizado o mesmo processo do ubuntu.
     
     $ sudo yum install certbot




## Gerar o certicado


No caso vou gerar o certicado para os seguintes domínios: www.exemple.com exemple.com e api.exemple.com 
usando a opção standalone do certbot-auto, no qual é aconselhável parar o serviço do webserver nginx.


### ubuntu

    $ ./path/to/certbot-auto certonly --standalone -d example.com -d www.example.com -d api.example.com
 
### centos 7

    $ certbot certonly --standalone -d example.com -d www.example.com -d api.example.com


Os certificados são gerados no caminho parecido com o seguinte

    /etc/letsencrypt/live/example.com/fullchain.pem




## Automatizando e renovando

Como disse no inicio, o certificado da Let's Encrypt é válido por 90 dias, então para que seus usuários não sejam pegos de surpresa é altamente recomendável 
que seja feita a renovação o quanto antes.

Primeiro verifique se o comando de renovação pode ser executado com sucesso, (talvez seja necessário parar o servidor web no caso Nginx)


###  Ubuntu

    ./path/to/certbot-auto renew --dry-run 


### Centos 7

    $ certbot renew --dry-run 


Para renovar o certificado poder ser executado o seguinte comando, o parâmetro --quiet não gera log 
e o parâmetro --no-self-upgrade


### Ubunutu

    ./path/to/certbot-auto renew --quiet --no-self-upgrade

### Centos 7

    $ certbot renew --quiet --no-self-upgrade

Pode ser feito um cron para executar esse processo, de renovação.


    $ sudo crontab -e
    
Adicione a seguinte tarefa

    * 2 * * * /path/to/certbot-auto renew >> /var/log/certbot-auto.log


Será executado todos os dias às 2 AM em um minuto aleatório(recomendado pelo certbot)

>Certbot recomenda também que essa tarefa seja executado duas vezes ao dia para garantir sua funcionalidade,
isso vai do seu critério.



# Referências

* [https://letsencrypt.org/](https://letsencrypt.org/)
* [https://certbot.eff.org/](https://certbot.eff.org/)
* [http://www.infowester.com/linuxcron.php](http://www.infowester.com/linuxcron.php)