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

 
- 2- Configuración del archivo docker-compose.yml.


- 3- Pasos para el despliegue de la aplicación.


- 4- Preparación y subida de la imagen a dockerhub.


- 5- Conclusiones


- 6- Annexos (si lo consideráis necesario)
