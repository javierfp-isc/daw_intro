FROM javierfpisc/lamp

MAINTAINER javierfp <javierfp@iessanclemente.net>

ENV TERM xterm
ENV PASS=abc123.
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/sbin

LABEL distribucion="Wordpress sobre LAMP en Debian 10"
LABEL descripcion="Imagen Debian con Wordpress para prácticas de DAW"
LABEL paquetes="curl"
LABEL acceso="usuario: root, password: abc123."

#Copiamos el entrypoint.sh al container
COPY entrypoint.sh /usr/bin/entrypoint.sh

#Damos permiso al entrypoint.sh
RUN set -x; \
	chmod +x /usr/bin/entrypoint.sh

#Configuración de mysql
RUN set -x; \
	service mysql start && \
	echo "CREATE DATABASE wordpress_db;" | mysql -uroot && \
	echo "GRANT ALL ON wordpress_db.* TO 'wordpress_user'@'localhost' IDENTIFIED BY '$PASS';" | mysql -uroot && \
	echo "FLUSH PRIVILEGES;" | mysql -uroot

#Instalamos paquetes necesarios
RUN set -x; \
	apt update && apt install -y curl

#Descarga de wordpress
RUN set -x; \
	cd /var/www/html && \
	curl -O https://wordpress.org/latest.tar.gz && \
	tar -xvf latest.tar.gz && \
	rm latest.tar.gz

#Configurando entorno de wordpress
RUN set -x; \
	chown -R www-data:www-data /var/www/html/wordpress && \
	find /var/www/html/wordpress/ -type d -exec chmod 750 {} \; && \
	find /var/www/html/wordpress/ -type f -exec chmod 640 {} \; && \
	cd /var/www/html/wordpress && \
	mv wp-config-sample.php wp-config.php

#Editamos el archivo wp-config.php
RUN set -x; \
	sed -i 's/database_name_here/wordpress_db/' /var/www/html/wordpress/wp-config.php && \
	sed -i 's/username_here/wordpress_user/' /var/www/html/wordpress/wp-config.php && \
	sed -i 's/password_here/abc123./' /var/www/html/wordpress/wp-config.php

#Copiamos el virtualhost
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

#Activamos mod_rewrite
RUN set -x; \
	a2enmod rewrite

#Comando para arrancar ssh y entrar en bucle de espera
ENTRYPOINT ["/usr/bin/entrypoint.sh"]
