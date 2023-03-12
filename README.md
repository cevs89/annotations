# annotations

# Actualizar repos
sudo apt-get install software-properties-common

sudo add-apt-repository ppa:deadsnakes/ppa

sudo apt update

# instalar python 3.6
sudo apt install python3.6


# instalar versión 2.7 de python
sudo apt install python


# Saber todas las versiones de python instaladas.
ls -lh /usr/bin/python*


# Agregar las versiones en prioridad
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 0

sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1

sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 2


# A la palabra python se le agregan 3 tipos de versiones distintas de python, cuando queramos decidir cual usar corremos los siguiente:


# seleccionar la versión a utilizar
sudo update-alternatives --config python

para usar los entornos segun un version de python.

Instalamos virtualenv.


# Iniciar entorno virtual con una version de python especifica.

virtualenv path_env --python=python3.8








# Install PIP
sudo apt install python3-pip


# Intall Virtualenv
sudo apt-get install python3-pip

sudo pip3 install virtualenv 



# Install Shutter

sudo add-apt-repository -y ppa:linuxuprising/shutter

sudo apt install shutter


# Install Curl
sudo apt install curl


# Install POstgres

-Install the public key for the repository (if not done previously):

sudo curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add


-Create the repository configuration file:

sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'


-Install pgAdmin

sudo apt install pgadmin4


# Install Postgres

sudo apt update

sudo apt install postgresql postgresql-contrib

- Cambio de ROl:

sudo -i -u postgres

- Postgres
psql

- Nuevo usuarios:


createuser --interactive

- Alter Password:

psql

ALTER USER crehana PASSWORD '947620';

ALTER USER postgres PASSWORD 'postgres';


- Nueva DB:

psql

createdb name_db

______



Configurar flower.

Referencia de la configuración en Saturno, se debe cambiar los datos de configuración para cada server que se necesite.

La URL se solicita a Nelson y se indica que se apunte al balanceador de carga de las instancias requeridas ya que la IP de los balanceadores no cambia y lo que se hace en el nginx es un proxy al puerto donde correo flower.


Supervisor:

Raíz: /etc/supervisor/conf.d/flower.conf

habilite el puerto: 9165 para flower.

[program:flower-celery-saturno]
command=/home/jenkins_reco_ab/workspace/myenv/bin/flower -A ebisuu.celery -l info --port=9165 --basic_auth=aituring2021:AB2021$$
directory=/home/jenkins_reco_ab/workspace/ebisuu3/ebisuu3
user=root
numprocs=1
stdout_logfile=/home/ubuntu/logs/flower_celery.log
stderr_logfile=/home/ubuntu/logs/flower_celery_err.log
autostart=true
autorestart=true
startsecs=10

; Need to wait for currently executing tasks to finish at shutdown.
; Increase this if you have very long running tasks.
stopwaitsecs = 600

stopasgroup=true

; Set Celery priority higher than default (999)
; so, if rabbitmq is supervised, it will start first.
priority=1000

Supervisor tome los cambios:

supervisorctl reread
supervisorctl update





Nginx.

/etc/nginx/sites-available/flower
server {
	listen 80;
	server_name flower.aituring.co;
	charset utf-8;

	location / {
    	proxy_pass http://localhost:9165;
    	proxy_set_header Host $host;
    	proxy_redirect off;
    	proxy_http_version 1.1;
    	proxy_set_header Upgrade $http_upgrade;
    	proxy_set_header Connection "upgrade";
	}
}

Adicionales Importantes:

sudo ln -s /etc/nginx/sites-available/flower /etc/nginx/sites-enabled/flower

sudo service nginx restart
