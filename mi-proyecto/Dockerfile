# Usar la imagen base de Debian
FROM debian:latest

# Establecer variables de entorno para evitar mensajes interactivos durante la instalación
ENV DEBIAN_FRONTEND=noninteractive

# Actualizar paquetes e instalar Apache, PHP, OpenSSL y utilidades necesarias
RUN apt-get update && \
    apt-get install -y apache2 php libapache2-mod-php openssl && \
    apt-get clean

# Crear directorio para el certificado
RUN mkdir /etc/apache2/ssl

# Generar un certificado autofirmado
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/apache2/ssl/apache-selfsigned.key \
    -out /etc/apache2/ssl/apache-selfsigned.crt \
    -subj "/C=US/ST=State/L=City/O=Organization/OU=Department/CN=localhost"

# Configurar Apache para HTTPS
RUN a2enmod ssl && \
    a2ensite default-ssl && \
    sed -i "s|/etc/ssl/certs/ssl-cert-snakeoil.pem|/etc/apache2/ssl/apache-selfsigned.crt|g" /etc/apache2/sites-available/default-ssl.conf && \
    sed -i "s|/etc/ssl/private/ssl-cert-snakeoil.key|/etc/apache2/ssl/apache-selfsigned.key|g" /etc/apache2/sites-available/default-ssl.conf

# Copiar un archivo de prueba en el directorio de publicación de Apache
COPY /public-html /var/www/html/index.php

# Exponer los puertos 80 y 443
EXPOSE 80 443

# Comando para iniciar Apache en modo foreground
CMD ["apachectl", "-D", "FOREGROUND"]

