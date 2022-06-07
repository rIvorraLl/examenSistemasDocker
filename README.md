# examenSistemasDocker

- 1- Introducción.

Para completar esta tarea, como prerequisitos necesitaremos tener instalado `docker-engine` y `docker-compose`. Se describe a continuación cómo hace la instalación en un sistema Ubuntu. Como prerrequisitos para la instalación, comenzamos por actualizar y añadir dependencias:

```
 sudo apt-get update

 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

A continuación añadimos la clave PGP de los repositorios oficiales de Docker:

```
 sudo mkdir -p /etc/apt/keyrings

 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Configuramos el repositorio:

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Ya con el repositorio configurado, pasamos a actualizar repositorios e instalar Docker:

```
 sudo apt-get update

 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
 ```
 
 Ya podemos comprobar que tenemos Docker instalado:
 
 ![20220607_19h46m23s_grim](https://user-images.githubusercontent.com/91564852/172448788-baeb7752-a15e-4b85-bffd-c56b12125a50.png)

Nos falta `docker-compose`, que podemos obtener con el siguiente comando:

`sudo apt install docker-compose`
 
- 2- Configuración del archivo docker-compose.yml.

Se incluye a continuación el archivo `.yml` que utilizamos en nuestra práctica y que ha resultado ser funcional.

```
version: '3.3'
services:
  db:
    image: mysql:8.0.29
    volumes:
      - /opt/test:/var/lib/mysql
      - ./back/db:/docker-entrypoint-initdb.d
    environment:
      MYSQL_ROOT_PASSWORD: **********
      MYSQL_DATABASE: alimentacion
      MYSQL_USER: sic
      MYSQL_PASSWORD: *******
    ports:
      - "3306:3306"
  backend:
    depends_on:
      - db
    image: tomcat:9.0
    ports:
      - "8080:8080"
    volumes:
      - ./back/app/target/app.war:/usr/local/tomcat/webapps/app.war
  web:
    image: nginx
    ports:
      - "80:80"
    volumes: 
      - ./front:/usr/share/nginx/html
  ```


- 3- Pasos para el despliegue de la aplicación.


- 4- Preparación y subida de la imagen a dockerhub.


- 5- Conclusiones


- 6- Annexos

Instalacihttps://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)
