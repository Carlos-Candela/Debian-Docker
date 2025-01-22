# Proyecto Docker: Debian + Apache + PHP

Este proyecto crea un contenedor Docker que ejecuta una imagen base de Debian, instala Apache y PHP, y publica una pequeña página web. Además, configura Apache para soportar conexiones HTTP y HTTPS (usando un certificado autofirmado).

## Requisitos

Antes de comenzar, asegúrate de tener instalados los siguientes programas:

- Docker (https://www.docker.com/get-started)
- Un editor de texto o IDE para editar archivos (opcional)

## Estructura del Proyecto

/mi-proyecto ├── Dockerfile ├── public-html/ └── index.php


## Pasos para usar el contenedor

### 1. Clonar o descargar el proyecto

Si aún no tienes el proyecto, clónalo o descárgalo en tu máquina local.

### 2. Construir la imagen Docker

Desde el directorio donde tienes el archivo `Dockerfile`, abre una terminal y ejecuta el siguiente comando para construir la imagen Docker:

```bash
docker build -t debian-apache-php .

Este comando construye la imagen con el nombre debian-apache-php.
3. Ejecutar el contenedor

Una vez construida la imagen, ejecuta el contenedor mapeando los puertos 80 (HTTP) y 443 (HTTPS) a tu máquina local:

docker run -d -p 80:80 -p 443:443 --name debian-apache-container debian-apache-php

Esto arrancará el contenedor en segundo plano y podrás acceder a tu web.
4. Acceder a la web

Abre tu navegador web y accede a las siguientes URLs:

    HTTP: http://localhost
    HTTPS: https://localhost

Es posible que veas una advertencia sobre el certificado SSL ya que es autofirmado. Acepta la advertencia para continuar.

En ambos casos, deberías ver la página web con el mensaje:

¡Hola, mundo desde Debian + Apache + PHP!

5. Detener y eliminar el contenedor

Cuando termines de usar el contenedor, puedes detenerlo y eliminarlo con los siguientes comandos:

    Detener el contenedor:

docker stop debian-apache-container

    Eliminar el contenedor:

docker rm debian-apache-container

6. Verificar los logs de Apache

Si necesitas revisar los logs del contenedor (por ejemplo, si hay algún error), puedes usar:

docker logs debian-apache-container

Descripción del Dockerfile

El archivo Dockerfile está configurado para realizar los siguientes pasos:

    Usar una imagen base de Debian.
    Instalar Apache, PHP y módulos necesarios.
    Configurar un certificado SSL autofirmado para habilitar HTTPS.
    Copiar el archivo index.php al directorio adecuado de Apache para que sea servido como una pequeña página web.
    Exponer los puertos 80 y 443.
    Ejecutar Apache en primer plano para mantener el contenedor activo.

Personalización

Si deseas personalizar la página web publicada o agregar más configuraciones, puedes modificar el archivo public-html/index.php o agregar más archivos a la carpeta public-html/.
