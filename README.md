# Examen Sistemas Informáticos



- **1.- Introducción.**

Para completar esta tarea, como prerrequisito necesitaremos tener instalado `docker-engine` y `docker-compose`. Se describe a continuación cómo hace la instalación en un sistema Ubuntu. Comenzamos por actualizar y añadir dependencias:

```
 sudo apt-get update

 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

A continuación añadimos la clave GPG de los repositorios oficiales de Docker:

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

Ya con el repositorio configurado, pasamos a actualizar repositorios e instalar toda la base para utilizar Docker:

```
 sudo apt-get update

 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
 ```
 
 Ya podemos comprobar que tenemos Docker instalado, corriendo un simple "Hello world".
 
 ![20220607_19h46m23s_grim](https://user-images.githubusercontent.com/91564852/172448788-baeb7752-a15e-4b85-bffd-c56b12125a50.png)

Nos falta `docker-compose`, que podemos obtener con el siguiente comando:

`sudo apt install docker-compose`
 
- **2.- Configuración del archivo docker-compose.yml.**

Se incluye a continuación el archivo `.yml` que utilizamos en nuestra práctica y que ha resultado ser funcional. Usamos un editor de texto para crear el archivo:

![20220607_20h03m54s_grim](https://user-images.githubusercontent.com/91564852/172452101-f4a9bbce-0a49-4860-81ef-e3059bda3155.png)

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

Y añadimos el texto:

![20220607_20h04m25s_grim](https://user-images.githubusercontent.com/91564852/172453140-332c715b-7c56-4dff-90ae-94c74020f32e.png)

- **3.- Pasos para el despliegue de la aplicación.**

Arrancaremos todos los contenedores incluidos en el archivo anterior con el comando:

```
docker-compose up -d
```

Aquí podemos ver una captura en pleno proceso:

![20220607_20h17m05s_grim](https://user-images.githubusercontent.com/91564852/172454246-25f49cb8-8d49-43b8-818d-18a4637105a9.png)

Parece ser que el proceso ha sido exitoso:

![20220607_20h18m21s_grim](https://user-images.githubusercontent.com/91564852/172454415-16ddd4fc-5266-47ff-8028-6ed37f1e6e97.png)

De hecho, el comando `docker images` nos muestra las tres imágenes creadas con nuestro archivo `.yml`:

![20220607_20h26m40s_grim](https://user-images.githubusercontent.com/91564852/172456030-f3512128-96e9-4447-bf6b-f895f4eb7b88.png)



- 4- Preparación y subida de la imagen a dockerhub.

Hacemos *login* en [Docker Hub] con nuestras credenciales:

![20220607_20h23m13s_grim](https://user-images.githubusercontent.com/91564852/172455594-053934b8-ea9c-4442-881a-9eddc3549845.png)

Añadimos un `tag` a la imagen que vamos a escoger para hacer la prueba de subida a Docker Hub, y la subimos con `docker push`...

![20220607_20h33m57s_grim](https://user-images.githubusercontent.com/91564852/172456919-97cd39ce-a605-41bb-ab49-4de91241d7a7.png)

Parece que todo ha ido bien. Un `docker pull` sobre la imagen nos informará de que ésta se encuentra actualizada a la última versión, que es la que acabamos de subir.

![20220607_20h37m12s_grim](https://user-images.githubusercontent.com/91564852/172457473-31f8c135-3a74-43c5-9489-3bf18d21643c.png)


- 5- Conclusiones

Ha sido complicado encontrar un modo de hacer funcionar todo este proyecto, pero gracias al trabajo de nuestro equipo ha sido finalmente posible. Las posibilidades que tiene utilizar Docker, y el que sea un probable requisito en muchos puestos de trabajo, hacen el conocimiento, cuando menos, básico, sobre su uso algo imprescindible.

- 6- Annexos

Instalación de Docker: [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)



---

