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
