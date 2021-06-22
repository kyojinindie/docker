# docker
docker tutorial

¿Qué es Docker?

Docker es un proyecto de código abierto que permite automatizae el despliegue de aplicaciones dentro de wapacios virtualizados conocidos como contenedores.

¿Qué es una imagen?

Una imagen es una plantilla para la creación de cntenedores. Incluye todo el diseño y la configuración para crear contendores concretos.

¿Qué es un contendor?

Un contenedor es un espacio auto-contenido el cual inclute todo lo necesario para la ejecución de aplicaciones.


Caraterísticas de Docker:

Gestión centralizada de imágenes y contenedores. Docker funciona como un servicio del sistema operativo, con el que se puede interactuar utilizando el comando "docker".

Eciste un repositorio centralizado conocido como Docker Hub.

El comando "docker" es un cliente que se encarga de conectarse con el servicio Docker y permite realizar todas las labores de administración disponibles en Docker.

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
## Funcionamiento del servicio dockerd

systemctl es una interface de system de que nos permite controlar los servicios instalados en el sistema,
gestiona los detalles del sistema operativo.

### argumentos

status, start, stop, restart

## Cliente de Docker

Se utiliza atravez del comando docker

Comando básicos

Comando | Descripción 
------------ | -------------
docker ps | Sirve para ver los contenedores que actualmente se encuentran en ejecución
docker ps -a | Sirve para listar todos los contenedores
docker ps -f | Sirve para filtrar por condición determinada
docker ps -f name=name | Busqueda por nombre
docker ps -f id=id | Busqueda por ID
docker ps -n | Sirve para mostrar n número de contendores
docker ps -l | Sirve para mostrar el último contendor creado
docker ps -q | Unicamente muestra los ID's de los contenedores
docker run | Nos permite lanzar un nuevo comando sobre un contendor que se genera al instante
docker images ls | Lista las imagenes
docker images -a | Lista todas las imagenes
docker images -q | Unicamente muestra los ID's de las imagenes
docker images -f | Sirve para filtrar por una condición determinada
docker images --no-trunc | Muestra el hash completo de la imagen
docker image | Comando para administrar las imagenes
docker run -it contenedor bash | Crea un contenedor interactivo con una terminal del tipo tty
docker start -i IDcontenedor | Levantar un contenedor
docker stop IDcontenedor | Detener un contenedor
docker run -it -d image | Para levantar el contenedor en background
docker run -it -d --name image | Para asignar al contenedor un nombre personalizado
docker rm IDcontenedor | Elimina un contenedor
docker create | Creamos un contenedor pero no lo arrancamos
docker image save imagen -o ./nombre-archivo.tar | Guarda una imagen en un archivo .tar
docker image rm image  | Elimina  una imagen