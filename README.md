# Lanzamiento escenarios

## Servidor apache

Tras clonar el repositorio, desde el directorio daw_intro/apache ejecutamos:

`docker-compose up -d`

Esto creará el container para el servicio apache en docker-compose

Este servicio:

* Mapea el puerto 8080 del anfitrión al 80 del container
* Asocia el directorio de datos de apache del container /var/www/html al volumen de datos docker apache_data

## Servidor LAMP

Tras clonar el repositorio, desde el directorio daw_intro/lamp ejecutamos:

`docker-compose up -d`

Esto creará el container para el servicio lamp en docker-compose

Este servicio:

* Mapea el puerto 8081 del anfitrión al 80 del container
* Asocia el directorio de datos de apache del container /var/www/html al volumen de datos docker apache_data
* Asocia el directorio de datos de mysql del container /var/lib/mysql al volumen de datos docker mariadb_data

## Servidor Wordpress sobre LAMP

Tras clonar el repositorio, desde el directorio daw_intro/wordpress ejecutamos:

`docker-compose up -d`

Esto creará el container para el servicio wordpress en docker-compose

Este servicio:

* Mapea el puerto 8082 del anfitrión al 80 del container
* Asocia el directorio de datos de apache del container /var/www/html al volumen de datos docker apache_data
* Asocia el directorio de datos de mysql del container /var/lib/mysql al volumen de datos docker mariadb_data

# Acceso a containers

## Acceso a container apache

Desde el directorio daw_intro/apache:

`docker-compose exec apache bash`

o bien directamente accediendo al container

`docker exec -it apache_apache_1 bash`

## Acceso a container lamp

Desde el directorio daw_intro/lamp:

`docker-compose exec lamp bash`

o bien directamente accediendo al container

`docker exec -it lamp_lamp_1 bash`

## Acceso a container wordpress

Desde el directorio daw_intro/wordpress:

`docker-compose exec wordpress bash`

o bien directamente accediendo al container

`docker exec -it wordpress_wordpress_1 bash`
