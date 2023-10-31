# Installaci-n-de-moodle

## Instalación del moodle
Creamos la **carpeta** donde instalaremos el Moodle
```
mkdir ejemplo
```
Nos metemos en la carpeta
```
cd ejemplo
```
Hacemos la **vagrant**
```
vagrant init ubuntu/jammy64
vagrant up --provider=virtualbox
```
Hacemos ssh a la vagrant 
```
vagrant ssh
```
Nos convertimos en root para poder ejecutar todos los comandos
```
sudo -s
```
Actualizamos paquetes
```
apt update
apt upgrade
```
Instalamos **apache2**
```
apt install -y apache2
```
Y también instalamos **mysql**
```
apt install -y mysql-server
```
Instalamos las **librerias** 
```
apt install -y php libapache2-mod-php
apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```
Reiniciamos el servidor 
```
systemctl restart apache2
```
Entramos a **MYSQL**
```
mysql
```
Creamos la base de datos
```
CREATE DATABASE bbdd;
```
Creamos el usuario
```
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
Asignamos permisos
```
GRANT ALL ON bbdd.* to 'usuario'@'localhost';
```
Salimos
```
exit
```
Nos descargamos el **zip** del moodle para poderlo descarlar y lo copiamos a la carpeta que hemos creado anteriormente.

Ahora moveremos el archivo a */var/www/html/*
```
mv /vagrant/moodle.zip /var/www/html/
```
Entramos a la carpeta
```
cd /var/www/html/
```
Installamos el zip y unzipeamos el archivo 
```
apt install unzip
unzip moodle.zip
```
Eliminamos el *index.html*
```
rm -rf index.html
```
Damos **permisos** a nuestras aplicaciones web
```
cd /var/www/
chmod -R 775 .
chown -R root:www-data .
```
Y tambien en el */var/www/html/*
```
cd /var/www/html
chmod -R 775 .
chown -R root:www-data .
```
Salimos de el root y de la vagrant
```
exit
exit
```
Editamos el **Vagrant file** para hacer publica nuestra web
```
vi Vagrantfile
```
Y desmarcamos las siguientes lineas:
```
# Create a forwarded port mapping which allows access to a specific port
# within the machine from a port on the host machine. In the example below,
# accessing "localhost:8080" will access port 80 on the guest machine.
# NOTE: This will enable public access to the opened port
config.vm.network "forwarded_port", guest: 80, host: 8080
```
```
# Create a public network, which generally matched to bridged network.
# Bridged networks make the machine appear as another physical device on
# your network.
config.vm.network "public_network"
```
Entramos de nueva a la vagrant y nos hacemos root
```
vagrant ssh
sudo -s
```
Editamos el **php**
```
vi /etc/php/8.1/apache2/php.ini
```
Y añadimos al archivo la siguiente linea
```
max_input_vars = 5000
```
Salimos y reiniciamos la vagrant
```
exit
exit
vagrant reload
```