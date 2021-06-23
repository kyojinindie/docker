# docker
docker tutorial

¿Qué es Docker?

Docker es un proyecto de código abierto que permite automatizar el despliegue de aplicaciones dentro de espacios virtualizados conocidos como contenedores.

¿Qué es una imagen?

Una imagen es una plantilla para la creación de contenedores. Incluye todo el diseño y la configuración para crear contendores concretos.

¿Qué es un contendor?

Un contenedor es un espacio autocontenido el cual incluye todo lo necesario para la ejecución de aplicaciones.


Características de Docker:

Gestión centralizada de imágenes y contenedores. Docker funciona como un servicio del sistema operativo, con el que se puede interactuar utilizando el comando "docker".

Existe un repositorio centralizado conocido como Docker Hub.

El comando “docker" es un cliente que se encarga de conectarse con el servicio Docker y permite realizar todas las labores de administración disponibles en Docker.

Los contenedores en Docker admiten múltiples tipos de configuraciones, incluyendo la creación de segmentos de red independientes.

Es posible crear clusters de contenedores, crear imágenes y muchas más funciones que facilitan el trabajo de un DevOps.

Instalación de Docker

``https://docs.docker.com/engine/install/ubuntu/``

Primero desinstalar versiones antiguas

``sudo apt-get remove docker docker-engine docker.io containerd runc``

Instalar docker usando el repositorio

```shell
 sudo apt-get update

 sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Añadir clave GPG de Docker

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Añadir el repositorio

```shell
 echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Instalar Docker

```shell
 sudo apt-get update

 sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Comprobar el servicio de Docker

```shell
sudo systemctl status docker.service
```
## Configurar docker para correlo sin sudo

```shell
sudo chmod 666 /var/run/docker.sock
```
## Funcionamiento del servicio docker

Systemctl es un interface de system de que nos permite controlar los servicios instalados en el sistema,
gestiona los detalles del sistema operativo.

### argumentos

status, start, stop, restart

## Cliente de Docker

Se utiliza atrevés del comando docker

Comando básicos

Comando | Descripción 
------------ | -------------
docker ps | Sirve para ver los contenedores que actualmente se encuentran en ejecución
docker ps -a | Sirve para listar todos los contenedores
docker ps -f | Sirve para filtrar por condición determinada
docker ps -f name=name | Búsqueda por nombre
docker ps -f id=id | Búsqueda por ID
docker ps -n | Sirve para mostrar n número de contendores
docker ps -l | Sirve para mostrar el último contendor creado
docker ps -q | Únicamente muestra los ID's de los contenedores
docker run | Nos permite lanzar un nuevo comando sobre un contendor que se genera al instante
docker images ls | Lista las imágenes
docker images -a | Lista todas las imágenes
docker images -q | Únicamente muestra los ID's de las imágenes
docker images -f | Sirve para filtrar por una condición determinada
docker images --no-trunc | Muestra el hash completo de la imagen
docker image | Comando para administrar las imágenes
docker run -it contenedor bash | Crea un contenedor interactivo con una terminal del tipo tty
docker start -i ID-contenedor | Levantar un contenedor
docker stop ID-contenedor | Detener un contenedor
docker run -it -d image | Para levantar el contenedor en background
docker run -it -d --name image | Para asignar al contenedor un nombre personalizado
docker rm ID-contenedor | Elimina un contenedor
docker create | Creamos un contenedor pero no lo arrancamos
docker image save imagen -o ./nombre-archivo.tar | Guarda una imagen en un archivo .tar
docker image rm image  | Elimina  una imagen
docker logs container-name | Muestra los logs de una aplicación
docker exec -it container-name bash | Nos permite lanzar un comando contra un contenedor concreto en este caso el comando es bash
docker top container-name | Este comando nos enseña los programas que se están ejecutando actualmente en el contenedor
docker stats container-name | Para ver las estadísticas de un contenedor
docker kill container-name | Mata directamente el contenedor
docker image inspect image-name | Nos devuelve una estructura en formato JSON
``docker image inspect image-name | grep "propiedad del JSON"`` | Nos regresa una propiedad especifica del JSON
docker image inspect image-name > file-name.json | Guardamos en un archivo la información proporcionada por el comando inspect
docker pull | Descarga una imagen del repositorio sin crear un contenedor
docker container inspect container-name | Nos devuelve la información del contenedor en formato JSON
docker inspect --formar='{{.LogPath}}' container-name | Comando alternativo a grep

## Networking en Docker


Comando | Descripción
------------ | -------------
docker run -d --name container-name -p puerto-anfitrión:puerto-contenedor image| Mapea el puerto de la máquina anfitriona a un puerto dentro del contenedor
docker run -d --name container-name -p localhost:puerto-anfitrión:puerto-contenedor image | Mismo comando que el anterior pero asigna manualmente una interface de red concreta
docker run -d --name container-name -P image | Docker genera automáticamente un puerto para mapear con la máquina anfitriona
docker network | Gestiona las redes de docker
docker network ls | Lista las redes que están actualmente creadas en el servicio de docker
docker network connect | Para conectarnos a una red concreta partiendo de un contenedor determinado
docker network create nombre-red | Crea una red
docker network inspect network-name| Obtenemos información de una o mas redes
docker network prune | Eliminara todas las redes inactivas
docker run -d -p puerto-anfitrión:puerto-contenedor --network network-name --name nombre-contenedor image | Crea un contenedor y lo asigna a una red existente
docker network create network-name --subnet=ip-address/16 --ip-range=ip-address/24 | Crea una red con una subnet y un rango
docker network connect network-name container-name | Vincula el contenedor a la red
docker network disconnect network-name container-name | Desconecta el contenedor de la red
docker network rm network-name | Elimina una red

## Docker volúmenes

Comando | Descripción
------------ | -------------
sudo ls -l /var/lib/docker| Muestra los archivo donde se guarda información de configuración de docker
sudo ls -l /var/lib/docker/Hash-volume/_data | Contiene la información almacenada en el volumen
docker run -it --name container-name -v /volume-name image command | Crea un volumen dentro del contenedor
docker run -it --name container-name -v /directorio-anfitrión:/directorio-contenedor image command | Crea un contenedor con un volumen vinculado a un directorio del anfitrion
docker run -it --name container-name --volumes-from container-name image command | Crea un contenedor y vincula un volumen de otro contenedor
docker volume create volume-name| Crea un volumen
docker volume prune | Elimina todos los volúmenes que no están siendo usados por un contenedor activo
docker volume rm volume-name| Elimina un volumen
docker run -it --name container-name -v volumen-creado:/ruta-contenedor image
docker volume inspect volume-name | Muestra la información del volumen


## Creación de imagenes

Existen dos formas de crear imágenes en Docker, la primera de ellas consiste en utilizar el comando "docker commit" el cual permite
crear una imagen personalizada partiendo del estado actual de un contenedor- Esta forma es la más sencilla de todas, pero también
la menos potente y propensa a error. En algunos casos es posible que existan fugas de información, malas configuraciones o que se incluyan
librerías y dependencias innecesarias para otros contenedores que se vayan a crear a partir de dicha imagen.

La segunda forma consiste en utilizar el sistema "DockerFile" el cual incluye un conjunto muy completo
de instrucciones para la creación de imágenes personalizadas con diferentes tipos de configuraciones.


Comando | Descripción
------------ | -------------
docker commit container image-name | Crea una imagen a partir de un contenedor
docker build -t helloapp:v1 . | Crea una imagen a partir de Dockerfile

## Creación de imágenes con DockerFile

Para crear una imagen partiendo de un Dockerfile es necesario utilizar el comando "docker build" el cual se encarga de leer un fichero con nombre "Dockerfile"
en el directorio donde se ejecutara el comando o en la ubicación indicada con la opción "-f".

El comando "docker build" recibe como argumento un PATHo una URL que deberá apuntar a un repositorio GIT.
El comando se encarga de transferir todos los directorios y subdirectorios incluidos en el PATH o URL especificada de forma recursiva.
Dichos contenidos harán parte de la imagen generada.

El diseño de la imagen debe seguir un conjunto de buenas prácticas en términos de rendimiento, funcionalidad y seguridad.
Para ello es importante conocer el funcionamiento de las principales directivas que se pueden incluir en el fichero
Dockerfile

## Principales instrucciones en el fichero Dockerfile.

FROM imagen:tag

Indica la imagen base que va a utilizar para la construcción de la imagen actual. Como ocurre a la hora de crear in contenedor en Docker
, si la imagen ya descargada por parte del Docker Engine la utiliza, en cado contrario, la buscará y descargará
del registro correspondiente, por defecto de Docker Hub.

LABEL

Permite establecer metadata a la imagen, por ejemplo el autor de la misma.
LABEL maintainer="autor@mail.com"

RUN

Ejecuta cualquier comando en una capa nueva intermedia y hace un commit con los resultados, eliminando posteriormente dicha capa intermedia
si no es necesaria. Dicha nueva imagen intermedia es usada en el siguiente paso en el Dockerfile.
Se trata de una instrucción que tiene 2 modos:

Modo shell: RUN comando-simple
Modo ejecución: RUN ["ejecutable", "param1", "param2", "paramN"]

El modo shell es el más sencillo, ya que ejecuta un comando simple con el intérprete "/bin/sh".
El modo ejecución permite lanzar comandos en imágenes bases que no tienen el intérprete "/bin/bash"
así como utilizar otro intérprete como por ejemplo "/bin/bash": RUN["/bin/bash", "-c", "echo prueba"]

ENV

Permite establecer variables de entorno. Dichas variables estarán disponibles en las siguientes capas del Dockerfile y los contenedores que se creen posteriormente a partir de la imagen.

ENV variable=valor

Estas variables de entorno pueden modificarse en cada contenedor creado cuando se lance con "docker run", simplemente especificando la opción "-env"
docker run -env variable=valor

ADD

Esta instrucción copia los archivos o directorios de una ubicación en el host y los envía al contenedor en la ruta especificada.
Se pueden enviar múltiples ficheros o directorios desde el host.

ADD /home/docker/fichero/var/www/html

COPY

Funciona igual que el comando ADD, sin embargo solamente copia recursos al contenedor desde la máquina host y no permite algunas acciones que sí admite ADD,
como por ejemplo la posibilidad de carga recursos desde URL o fuentes externas o descomprimir automáticamente un fichero comprimido si es capaz de reconocer
el formato, entre otras cosas.

COPY /home/docker/webdirectory/var/www/html

EXPOSE

Expone los puertos especificados cuando se ejecute un contenedor partiendo de la imagen.
EXPOSE  no hace que los puertos puedan ser accedidos desde el host, para ello se debe mapear con
la opción "-p" del comando "docker run" al inciar el contendor

EXPOSE 80 8080 443 22

CMD Y ENTRYPOINT

Estas dos instrucciones son muy parecidas pero se utilizan en situaciones diferentes, aunque se
pueden indicar en el mismo Dockerfile conjuntamente.

Permiten especificar el comando que se va a ejecutar por defexto cuando un contenedor utilizando una imagen arranque.
Normalmente las imágenes base de sistemas operativos como Debian o Ubuntu están configuradas con estas instrucciones para ejecutar el comando /bin/bash o 
/bin/sh. Para conocer el comando indicado en la instrucción CMD de una imagen, basta simplemente con inspeccionar la imagen en cuestión cin el comando "docker inspect IMAGEN"
y buscar la sección "CMD"

## Docker Compose

Compose es una gerramienta para definir y ejecutar aplicaciones con múltiples contenedores y permite controlarlo todo utilizando un solo comando.
Compose es capaz de crear e iniciar todos los servicios desde la configuración definida en el fichero de configuración el cual tiene formato yaml y debe tener el nombre "docker-compose.yml".
El procedimiento para usar Docker Compose se describe en los tres siguientes pasos:
1- Definir el entorno con un Dockerfile
2- Definir los servicios que conforman la apolicación en el fichero "docker-comose.yml"
3- Iniciar todo el entorno utilizando el comando "docker-compose up"

## Instalación

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
