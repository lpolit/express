## DOKCER

### Que es Docker

Docker es un software de código abierto utilizado para desplegar aplicaciones dentro de contenedores virtuales.Permite a los usuarios crear entornos independientes y aislados para desplegar sus aplicaciones (CONTENEDORES)

### ¿Por qué utilizar Docker como desarrollador?

- Docker es rápido. A diferencia de una máquina virtual, tu aplicación puede iniciarse en pocos segundos y detenerse igual de rápido.

- Docker es multi-plataforma. Puedes lanzar tu contenedor en cualquier sistema.

- Los contenedores pueden construirse y destruirse más rápido que en una máquina virtual.

- Se terminaron las dificultades para configurar tu entorno de trabajo. Una vez configurado tu Docker, no tenes  que volver a instalar tus dependencias manualmente. Si cambias de PC o si alguien nuevo lo requiere, solo tendrás que darle tu configuración (Dockerfile).

- Tu espacio de trabajo siempre limpio, ya que cada uno de tus entornos estará aislado y podes eliminarlo en cualquier momento sin que afecte al resto.

- Será más fácil desplegar tu proyecto en tu servidor para ponerlo en línea.

### Instalacion

https://docs.docker.com/get-docker/

-------------------------------------------------------

## DOCKERIZANDO MI APLICACION

### DockerFile

Lo primero que hay que hacer cuando queres crear tu Dockerfile es preguntarte qué queremos hacer. Nuestro objetivo es lanzar una aplicacion con Node.

Para ello nuestro Docker debe contener todas las dependencias necesarias para lanzar NODE (Un LINUX con NODE y listo)

El Primer paso para crear el Dockerfile es entrar a DockerHub.(Este sitio contiene muchas imágenes prediseñadas para ahorrarte tiempo) y buscar la imagen que contenta nuestras precondiciones. Ej: https://hub.docker.com/_/node

### Contenido

FROM => Define la imagen base
RUN => para instalar dependencias
WORKDIR /app => creamos directorio de trabajo
COPY => Copia contenido
EXPOSE => Expone puerto
ENTRYPOINT ["node"] (opcional)  => Ejecutar dentro del contendor
CMD ["node", "index.js"] (opcional) => Ejecutar dentro del contendor

### Diferencia entre RUN, CMD y ENTRYPOINT

RUN

- Corre cuando se esta construyendo la imagen

CMD

- Comando por default
- Puede llevar parametros
- Facilmente Sobrescribible

ENTRYPONT

- Se define SOLO el comando
- Sin parametros
- No se puede sobreescribir
- Misma version de imagen para cualquier app se llame como se llame

## IMAGEN DOCKER

### Que es una imagen docker

Una imagen de Docker, es un archivo ejecutable e independiente que se utiliza para crear un contenedor. Esta imagen contiene las bibliotecas, dependencias y los archivos que el contenedor necesita para ejecutarse.

### Construyendo la imagen

``` bash
    docker run build -t mi_imagen .
```

### Ver las imagenes creadas

``` bash
docker images
```

### Arrancar la aplicacion

``` bash
docker run -p 8080:3000 mi_imagen index.js
```

### Entrar al contenedor

``` bash
docker ps
docker exec -it b7bff /bin/bash

```

## SUBIR IMAGEN A DOCKER HUB

Crearse una cuenta
crearse un repositorio
renombrar la imagen con el nombre de ese repo
docker tag local-image:tagname new-repo:tagname
docker login
docker push new-repo:tagname

## DEPLOY

### Deployar aplicacion

Vamos a deployar en un servidor gratuito llamado RENDER (https://render.com/)
Para ello los pasos son:

##### Deploy de mi repo GITHUB:

- Nos logueamos con la cuenta de github
- New -> Web Service
- Seleccionamos la opcion "Build and deploy from a Git repository"
- Selecionamos el repositorio github que queremos desployar
- cargamos los datos necesarios:
        *Runtime: NODE
        *Build Command: "NPM install"
        *Start Command: "NODE index.js"
        *Opcion FREE

##### Deploy de la imagen publicada en DOCKERHUB

- Nos logueamos con la cuenta de github
- New -> Web Service
- Seleccionamos la opcion "Deploy an existing image from a registry"
- cargamos los datos necesarios:
    Image URL: lpolitano/mi_imagen:1.0.5
    Environment variable: PORT = 3000
