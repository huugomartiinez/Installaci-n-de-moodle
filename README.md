# Installaci-n-de-moodle

## Instalación del moodle
Creamos la carpeta donde instalaremos el Moodle
```
mkdir ejemplo
```
Nos metemos en la carpeta
```
cd ejemplo
```
Hacemos la vagrant
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
