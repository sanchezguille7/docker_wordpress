# docker_wordpress

## docker-compose.yml:

Este archivo describe los servicios para el entorno Docker utilizando Docker Compose. Configura cuatro servicios: https-portal, wordpress, mysql y phpMyAdmin. También define volúmenes y redes para los contenedores.

 **Instrucciones de Uso:**
Clona este repositorio en tu máquina local.
Asegúrate de tener Docker y Docker Compose instalados en tu sistema.

En el directorio del proyecto clonado, crea un archivo .env y define las variables de entorno necesarias, como `WORDPRESS_DOMAIN`, `WORDPRESS_DATABASE_NAME`, `WORDPRESS_DATABASE_USER`, `WORDPRESS_DATABASE_PASSWORD`, `WORDPRESS_BLOG_NAME`, `WORDPRESS_USERNAME`, `WORDPRESS_PASSWORD`, `WORDPRESS_EMAIL` y `MYSQL_ROOT_PASSWORD`.

  

Ejecuta el siguiente comando para construir y ejecutar los contenedores:

    docker-compose up -d

  

Una vez que los contenedores estén en ejecución, visita http://localhost para acceder a tu sitio de WordPress y https://localhost para acceder a la versión segura utilizando HTTPS.

Para acceder a phpMyAdmin, visita http://localhost:8080 en tu navegador y utiliza las credenciales de MySQL definidas en el archivo *.env*.

**servicios:**
-   **https-portal**: Este servicio utiliza la imagen `steveltn/https-portal:1` para proporcionar soporte **HTTPS** a través de un proxy inverso. Expone los puertos **80** y **443** y se encarga de manejar el tráfico **HTTPS** para el dominio definido en la variable de entorno `DOMAINS`. Dependiendo del valor de esta variable, redirige el tráfico **HTTP** a un servicio específico, en este caso, redirige el tráfico **HTTP** al servicio de WordPress en el puerto **8080**.
    
-   **wordpress**: Este servicio utiliza la imagen `bitnami/wordpress:6.4.3` para ejecutar una instancia de **WordPress**. Configura todas las variables de entorno necesarias para la instalación y funcionamiento de **WordPress**, como la conexión a la base de datos **MySQL**, las credenciales de administrador, etc. También mapea un volumen para persistir los datos de **WordPress**.
    
-   **mysql**: Este servicio utiliza la imagen `mysql:8.0` para ejecutar un servidor **MySQL**. Configura las variables de entorno necesarias para la inicialización del servidor **MySQL**, como la contraseña de *root* y el nombre de la base de datos. Mapea un volumen para persistir los datos de **MySQL**.
    
-   **phpmyadmin**: Este servicio utiliza la imagen `phpmyadmin:5.2.1` para ejecutar una interfaz web de administración de **MySQL**. Expone el puerto **8080** y se conecta al servicio de **MySQL**. No es necesario configurar variables de entorno adicionales.
    
-   **Volumenes**: Se definen tres volúmenes para persistir los datos de **MySQL**, **WordPress** y los certificados **SSL** utilizados por **https-portal**.
    
-   **Redes**: Se definen dos redes, `frontend-network` y `backend-network`, para facilitar la comunicación entre los servicios.