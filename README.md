# Lanzamiento del escenario

Tras clonar el repositorio, desde el directorio daw_intro/apache ejecutamos:

`docker-compose up -d`

Esto creará el container para el servicio apache en docker-compose

Este servicio:
* Mapea el puerto 8080 del anfitrión al 80 del container
* Asocia el directorio de datos de apache del container /var/www/html al volumen de datos docker apache_data

# Acceso al container

Desde el directorio en el que se encuentra el daw_intro/apache

`docker-compose exec apache bash`

o bien directamente accediendo al container

`docker exec -it apache_apache_1 bash`
