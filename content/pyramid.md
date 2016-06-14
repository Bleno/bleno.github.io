Title: Pyramid the web framework
Date: 2015-04-15 12:00
Modified: 2015-04-15 12:00
Category: Programação
Tags: Python, deploy, pyramid, web, framework, develop
Slug: pyramid-the-web-framework
Authors: Bleno Silva
Summary: Pyramid the web framework
Status: draft

Instalação do LBGenerator com Nginx, pserve e supervisor

==========================================

# Criando usuário (Opcional)


## Adicione o usuário
    adduser neolight


## Altere a senha do usuário
    passwd neolight


# Dê privilégios de root para o usuário

Encontre o código:

 root ALL=(ALL) ALL
 
Adicione logo abaixo do código
neolight ALL=(ALL) ALL



###########################################

Iniciando o processo de preparação para instalação

 sudo yum -y update
 sudo yum -y install gcc-c++
 sudo yum -y install zlib-devel
 sudo yum -y install openssl-devel
 sudo yum -y install postgresql-devel
 sudo yum -y install git

##########################################

Baixando e instalando o Python3.2.2

curl -O https://www.python.org/ftp/python/3.2.2/Python-3.2.2.tar.xz

sudo mkdir /usr/local/lbneo

sudo ./configure --prefix=/usr/local/lbneo/ --with-threads --enable-shared LDFLAGS=-Wl,-rpath=/usr/local/lbneo/lib/

sudo make && sudo make install

curl -O https://pypi.python.org/packages/source/v/virtualenv/virtualenv-1.11.6.tar.gz

==============================================

Virtualenv

curl -O https://pypi.python.org/packages/source/v/virtualenv/virtualenv-1.11.6.tar.gz

tar -xvf virtualenv-1.11.6.tar.gz

cd virtualenv-1.11.6


sudo /usr/local/lbneo/bin/python3.2 setup.py install


================================================

Criar virtualenv

cd /usr/local/lbneo

sudo bin/virtualenv-3.2 -p bin/python3.2 virtenvlb3.2


==================================================
Criar virtualenv2.6 para o supervisor


cd /usr/local/lbneo

sudo bin/virtualenv -p python2.6 virtenvlb2.6


==================================================

Instalando o NGINX

cd ~

# Dependências
    sudo yum -y install gcc gcc-c++ make zlib-devel pcre-devel openssl-devel.


mkdir -p src && cd src

curl -O http://nginx.org/download/nginx-1.8.1.tar.gz

tar -xzf nginx-1.8.1.tar.gz

ln -sf nginx-1.8.1 nginx


# Configurar

Essas configurações a baixo são similar as instaladas via RPM

cd nginx

	./configure \
	--user=nginx                          \
	--group=nginx                         \
	--prefix=/etc/nginx                   \
	--sbin-path=/usr/sbin/nginx           \
	--conf-path=/etc/nginx/nginx.conf     \
	--pid-path=/var/run/nginx.pid         \
	--lock-path=/var/run/nginx.lock       \
	--error-log-path=/var/log/nginx/error.log \
	--http-log-path=/var/log/nginx/access.log \
	--with-http_gzip_static_module        \
	--with-http_stub_status_module        \
	--with-http_ssl_module                \
	--with-pcre                           \
	--with-file-aio                       \
	--with-http_realip_module             \
	--without-http_scgi_module            \
	--without-http_uwsgi_module           \
	--without-http_fastcgi_module


# Compilar e instalar

	make
 	sudo make install

# Adicionar usuário

    sudo useradd -r nginx


# Configurando /etc/init.d/nginx para iniciar com o sistema

 	sudo vi /etc/init.d/nginx

"""
	#!/bin/sh
	#
	# nginx - this script starts and stops the nginx daemin
	#
	# chkconfig:   - 85 15
	# description:  Nginx is an HTTP(S) server, HTTP(S) reverse \
	#               proxy and IMAP/POP3 proxy server
	# processname: nginx
	# config:      /etc/nginx/nginx.conf
	# pidfile:     /var/run/nginx.pid
	# user:        nginx

	# Source function library.
	. /etc/rc.d/init.d/functions

	# Source networking configuration.
	. /etc/sysconfig/network

	# Check that networking is up.
	[ "$NETWORKING" = "no" ] && exit 0

	nginx="/usr/sbin/nginx"
	prog=$(basename $nginx)

	NGINX_CONF_FILE="/etc/nginx/nginx.conf"

	lockfile=/var/run/nginx.lock

	start() {
	    [ -x $nginx ] || exit 5
	    [ -f $NGINX_CONF_FILE ] || exit 6
	    echo -n $"Starting $prog: "
	    daemon $nginx -c $NGINX_CONF_FILE
	    retval=$?
	    echo
	    [ $retval -eq 0 ] && touch $lockfile
	    return $retval
	}

	stop() {
	    echo -n $"Stopping $prog: "
	    killproc $prog -QUIT
	    retval=$?
	    echo
	    [ $retval -eq 0 ] && rm -f $lockfile
	    return $retval
	}

	restart() {
	    configtest || return $?
	    stop
	    start
	}

	reload() {
	    configtest || return $?
	    echo -n $"Reloading $prog: "
	    killproc $nginx -HUP
	    RETVAL=$?
	    echo
	}

	force_reload() {
	    restart
	}

	configtest() {
	  $nginx -t -c $NGINX_CONF_FILE
	}

	rh_status() {
	    status $prog
	}

	rh_status_q() {
	    rh_status >/dev/null 2>&1
	}

	case "$1" in
	    start)
	        rh_status_q && exit 0
	        $1
	        ;;
	    stop)
	        rh_status_q || exit 0
	        $1
	        ;;
	    restart|configtest)
	        $1
	        ;;
	    reload)
	        rh_status_q || exit 7
	        $1
	        ;;
	    force-reload)
	        force_reload
	        ;;
	    status)
	        rh_status
	        ;;
	    condrestart|try-restart)
	        rh_status_q || exit 0
	            ;;
	    *)
	        echo $"Usage: $0 {start|stop|status|restart|condrestart|try-restart|reload|force-reload|configtest}"
	        exit 2
	esac
"""


# Alterando a permissão do script

    sudo chmod +x /etc/init.d/nginx

# Iniciar no boot

    sudo chkconfig --add nginx
    sudo chkconfig --level 345 nginx on


# Configure o arquivo /etc/nginx/nginx.conf types_hash_bucket_size and server_names_hash_bucket_size altere de acordo com a sua necessidade:


	http {
	    include       mime.types;
	    default_type  application/octet-stream;
	    # add the below 2 lines under http around line 20
	    types_hash_bucket_size 64;
	    server_names_hash_bucket_size 128;


# Inicie o serviço e teste na porta 80

	service nginx start




===============================================
Instalando a liblightbase

    sudo mkdir -p /usr/local/lbneo/virtenvlb3.2/src

    cd /usr/local/lbneo/virtenvlb3.2/src

    sudo git clone http://<user>:<password>@git.lightbase.cc/liblightbase.git

    cd /usr/local/lbneo/virtenvlb3.2/src/liblightbase

    /usr/local/lbneo/virtenvlb3.2/bin/python3.2 setup.py install


===============================================
Instalando o LBGenerator

   cd /usr/local/lbneo/virtenvlb3.2/src

   sudo git clone -b master http://<user>:<password>@git.lightbase.cc/LBGenerator.git

   cd /usr/local/lbneo/virtenvlb3.2/src/LBGenerator

   sudo /usr/local/lbneo/virtenvlb3.2/bin/python3.2 setup.py install

Caso ocorre em algum pacote instale via pip cada pacote com sua devida versão.

===============================================


Configurando o LBGenerator

	cd /usr/local/lbneo/virtenvlb3.2/src/LBGenerator

	sudo vi /usr/local/lbneo/virtenvlb3.2/src/LBGenerator/production.ini

	Na seção app:main alterar sqlalchemy.url

	sqlalchemy.url = postgresql://user:password@127.0.0.1/database

	Na seção alembic alterar sqlalchemy.url 

	sqlalchemy.url = postgresql://user:password@127.0.0.1/database

	Antes da seção loggers adicionar as seguintes configurações:


	#---------- Pipeline Configuration ----------
	[filter:paste_prefix]
	use = egg:PasteDeploy#prefix

	#[pipeline:main]
	#pipeline =
	#    paste_prefix
	#    # a good spot for some logging middleware!
	#    myapp

	#---------- Server Configuration ----------
	[server:main]
	use = egg:waitress#main
	host = 127.0.0.1
	port = %(http_port)s

	#---------- Logging Configuration ----------
	# ...


Teste o pserve daemon

	sudo /usr/local/lbneo/virtenvlb3.2/bin/pserve --daemon --pid-file=pserve_5000.pid production.ini http_port=5000
	sudo /usr/local/lbneo/virtenvlb3.2/bin/pserve --daemon --pid-file=pserve_5001.pid production.ini http_port=5001

	curl 127.0.0.1:5000

Parar o teste

	sudo /usr/local/lbneo/virtenvlb3.2/bin/pserve --stop-daemon --pid-file=pserve_5000.pid
	sudo /usr/local/lbneo/virtenvlb3.2/bin/pserve --stop-daemon --pid-file=pserve_5001.pid


No teste foi executado 2 processos em portas diferentes.


====================================================

Configurando o NGINX como proxy para o LBGenerator

	cd /etc/nginx

	sudo mkdir conf.d

    sudo vi /etc/nginx/nginx.conf

    # nginx.conf

	user nginx;
	worker_processes 4;
	pid /var/run/nginx.pid;

	events {
	    worker_connections 1024;
	    # multi_accept on;
	}

	http {

	    ##
	    # Basic Settings
	    ##

	    sendfile on;
	    tcp_nopush on;
	    tcp_nodelay on;
	    keepalive_timeout 65;
	    types_hash_max_size 2048;
	    # server_tokens off;

	    # server_names_hash_bucket_size 64;
	    # server_name_in_redirect off;

	    include /etc/nginx/mime.types;
	    default_type application/octet-stream;

	    ##
	    # Logging Settings
	    ##

	    access_log /var/log/nginx/access.log;
	    error_log /var/log/nginx/error.log;

	    ##
	    # Gzip Settings
	    ##
	    gzip on;
	    gzip_disable "msie6";

	    ##
	    # Virtual Host Configs
	    ##

	    include /etc/nginx/conf.d/*.conf;
	    #include /etc/nginx/sites-enabled/*;
	}



   sudo vi /etc/nginx/conf.d/lbgenerator.conf


   # lbgenerator.conf

	upstream lbgenerator {
	    server 127.0.0.1:5000;
	    server 127.0.0.1:5001;
	}

	server {
	    listen 80;

	    # optional ssl configuration

	    #listen 443 ssl;
	    #ssl_certificate /path/to/ssl/pem_file;
	    #ssl_certificate_key /path/to/ssl/certificate_key;

	    # end of optional ssl configuration

	    server_name  127.0.0.1;

	    access_log  /var/log/nginx/lbgenerator-access.log;

	    location /api/ {
	        proxy_set_header        Host $http_host;
	        proxy_set_header        X-Real-IP $remote_addr;
	        proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
	        proxy_set_header        X-Forwarded-Proto $scheme;

	        client_max_body_size    10m;
	        client_body_buffer_size 128k;
	        proxy_connect_timeout   60s;
	        proxy_send_timeout      90s;
	        proxy_read_timeout      90s;
	        proxy_buffering         off;
	        proxy_temp_file_write_size 64k;
	        proxy_pass http://lbgenerator/;
	        proxy_redirect          off;
	    }
	}



	sudo service nginx restart

	cd /usr/local/lbneo/virtenvlb3.2/src/LBGenerator/
	
	sudo /usr/local/lbneo/virtenvlb3.2/bin/pserve --daemon --pid-file=pserve_5000.pid production.ini http_port=5000
	sudo /usr/local/lbneo/virtenvlb3.2/bin/pserve --daemon --pid-file=pserve_5001.pid production.ini http_port=5001

	curl -L localhost/api



============================================================
Instalando o supervisor para python3

Supervisor é um gerenciador de processos unix que vai ajudar a automatizar a tarefa de iniciar 
os processos do pserve e monitorar cada processo, caso algum desses processos tenha problema ele automaticamente é reiniciado.

A versão que recomendada a instalar para Python3 é a 4.0.0.dev0 que só é encontrada direto no github

O ideal seria criar um virtualenv com Python2.x só pra usar o supervisor,então lembrando, o supervisor monitora qualquer processo unix.



/usr/local/lbneo/virtenvlb3.2/bin/pip3.2 install -e git+https://github.com/Supervisor/supervisor.git@master#egg=supervisor

=== Instalando o supervisor para python3 ===

    cd /usr/local/lbneo/virtenvlb3.2

    sudo /usr/local/lbneo/virtenvlb3.2/bin/pip3.2 install -e git+https://github.com/Supervisor/supervisor.git@master#egg=supervisor

Dessa forma ele será instalado em modo develop e os fontes ficarão em /usr/local/lbneo/virtenvlb3.2/src automaticamente!

============================================================
Instalando o supervisor para python2



cd /usr/local/lbneo

sudo virtenvlb2.6/bin/pip2.6 install supervisor


============================================================
Criar o arquivo de configuração do supervisor supervisord.conf

	vi /usr/local/lbneo/virtenvlb3.2/src/LBGenerator/supervisord.conf

[unix_http_server]
file=%(here)s/supervisor.sock

[supervisord]
pidfile=%(here)s/supervisord.pid
logfile=%(here)s/supervisord.log
logfile_maxbytes=50MB
logfile_backups=10
loglevel=info
nodaemon=false
minfds=1024
minprocs=200

[rpcinterface:supervisor]
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

[supervisorctl]
serverurl=unix://%(here)s/supervisor.sock

[program:lbgenerator]
autorestart=true
command= /usr/local/lbneo/virtenvlb3.2/bin/pserve %(here)s/production.ini http_port=50%(process_num)02d
process_name=%(program_name)s-%(process_num)01d
numprocs=4
numprocs_start=0
redirect_stderr=true
stdout_logfile=%(here)s/%(program_name)s-%(process_num)01d.log

[inet_http_server]
port=127.0.0.1:9001
#username = user # Basic auth username
#password = pass # Basic auth password



Supervisor client web (Opcional)

Adicione ao final do arquivo supervisord.conf as seguintes configurações.
Os paramêtros username e password descomente e preencha como queira.

	[inet_http_server]
	port=127.0.0.1:9001
	#username = user # Basic auth username
	#password = pass # Basic auth password



Teste as configurações

Execute o supervisord

	sudo /usr/local/lbneo/virtenvlb3.2/bin/supervisord -c supervisord.conf
ou para python2
	/usr/local/lbneo/virtenvlb2.6/bin/supervisord -c supervisord.conf

Verifique se os processos estão rodando

	curl 127.0.0.1:5000


Parar processos:

	sudo /usr/local/lbneo/virtenvlb3.2/bin/supervisorctl stop all
ou para python2
	sudo /usr/local/lbneo/virtenvlb2.6/bin/supervisorctl stop all
	



===============================================================
Configurando o supervisord para iniciar no boot

Crie um arquivo  /etc/init.d/supervisord

    sudo vi supervisord

    #!/bin/bash
	#
	# supervisord   This scripts turns supervisord on
	#
	# Author:       Mike McGrath <mmcgrath@redhat.com> (based off yumupdatesd)
	#               Jason Koppe <jkoppe@indeed.com> adjusted to read sysconfig,
	#                   use supervisord tools to start/stop, conditionally wait
	#                   for child processes to shutdown, and startup later
	#               Mikhail Mingalev <mingalevme@gmail.com> Merged
	#                   redhat-init-jkoppe and redhat-sysconfig-jkoppe, and
	#                   made the script "simple customizable".
	#               Brendan Maguire <maguire.brendan@gmail.com> Added OPTIONS to
	#                   SUPERVISORCTL status call
	#
	# chkconfig:    345 83 04
	#
	# description:  supervisor is a process control utility.  It has a web based
	#               xmlrpc interface as well as a few other nifty features.
	#               Script was originally written by Jason Koppe <jkoppe@indeed.com>.
	#

	# source function library
	. /etc/rc.d/init.d/functions

	set -a

	PREFIX=/usr/local/lbneo/virtenvlb3.2

	SUPERVISORD=$PREFIX/bin/supervisord
	SUPERVISORCTL=$PREFIX/bin/supervisorctl

	PIDFILE=$PREFIX/src/LBGenerator/supervisord.pid
	LOCKFILE=/var/lock/subsys/supervisord

	OPTIONS="-c $PREFIX/src/LBGenerator/supervisord.conf"

	# unset this variable if you don't care to wait for child processes to shutdown before removing the $LOCKFILE-lock
	WAIT_FOR_SUBPROCESSES=yes

	# remove this if you manage number of open files in some other fashion
	ulimit -n 96000

	RETVAL=0


	running_pid()
	{
	    # Check if a given process pid's cmdline matches a given name
	    pid=$1
	    name=$2
	    [ -z "$pid" ] && return 1
	    [ ! -d /proc/$pid ] && return 1
	    (cat /proc/$pid/cmdline | tr "\000" "\n"|grep -q $name) || return 1
	    return 0
	}

	running()
	{
	# Check if the process is running looking at /proc
	# (works for all users)

	    # No pidfile, probably no daemon present
	    [ ! -f "$PIDFILE" ] && return 1
	    # Obtain the pid and check it against the binary name
	    pid=`cat $PIDFILE`
	    running_pid $pid $SUPERVISORD || return 1
	    return 0
	}

	start() {
        echo "Starting supervisord: "

        if [ -e $PIDFILE ]; then
                echo "ALREADY STARTED"
                return 1
        fi

        # start supervisord with options from sysconfig (stuff like -c)
        $SUPERVISORD $OPTIONS

        # show initial startup status
        $SUPERVISORCTL $OPTIONS status

        # only create the subsyslock if we created the PIDFILE
        [ -e $PIDFILE ] && touch $LOCKFILE
	}

	stop() {
        echo -n "Stopping supervisord: "
        $SUPERVISORCTL $OPTIONS shutdown
        if [ -n "$WAIT_FOR_SUBPROCESSES" ]; then
            echo "Waiting roughly 60 seconds for $PIDFILE to be removed after child processes exit"
            for sleep in  2 2 2 2 4 4 4 4 8 8 8 8 last; do
                if [ ! -e $PIDFILE ] ; then
                    echo "Supervisord exited as expected in under $total_sleep seconds"
                    break
                else
                    if [[ $sleep -eq "last" ]] ; then
                        echo "Supervisord still working on shutting down. We've waited roughly 60 seconds, we'll let it do its thing from here"
                        return 1
                    else
                        sleep $sleep
                        total_sleep=$(( $total_sleep + $sleep ))
                    fi

                fi
            done
        fi

        # always remove the subsys. We might have waited a while, but just remove it at this point.
        rm -f $LOCKFILE
	}

	restart() {
        stop
        start
	}

	case "$1" in
    start)
        start
        RETVAL=$?
        ;;
    stop)
        stop
        RETVAL=$?
        ;;
    restart|force-reload)
        restart
        RETVAL=$?
        ;;
    reload)
        $SUPERVISORCTL $OPTIONS reload
        RETVAL=$?
        ;;
    condrestart)
        [ -f $LOCKFILE ] && restart
        RETVAL=$?
        ;;
    status)
        $SUPERVISORCTL $OPTIONS status
        if running ; then
            RETVAL=0
        else
            RETVAL=1
        fi
        ;;
    *)
        echo $"Usage: $0 {start|stop|status|restart|reload|force-reload|condrestart}"
        exit 1
	esac

	exit $RETVAL

OBS: Se estiver usando o supervisor com python2.6 altere e crie as seguintes variáveis:
	
	PREFIX=/usr/local/lbneo/virtenvlb2.6
	PREFIX2=/usr/local/lbneo/virtenvlb3.2
	PIDFILE=$PREFIX2/src/LBGenerator/supervisord.pid
	OPTIONS="-c $PREFIX2/src/LBGenerator/supervisord.conf"


Salve e feche o arquivo


Altere a permissão

	sudo chmod +x /etc/rc.d/init.d/supervisord

	sudo chkconfig --add supervisord

	sudo chkconfig supervisord on

	sudo service supervisord start


Teste o acesso

	curl -L 127.0.0.1/api


Liberando porta http para acesso externo

	sudo iptables -I INPUT 5 -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
	sudo service iptables save
	sudo service iptables restart

=========================================================
Configurando o NGINX como proxy para o supervidor web interface Opcional


reinicie o NGINX

	sudo service nginx restart