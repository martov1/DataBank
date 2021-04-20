
* TODO:
	* Mejorar documentacion de load balancing
	* Terminar documentacion logging
	* Dejr bien claros los conecptos
	* Proofreading

**TODO:** [fumarme la referencia de dockerfile](https://docs.docker.com/engine/reference/builder/)


**TODO:** [me quede en syslog driver](https://docs.docker.com/config/containers/logging/syslog/)
network-tutorial-standalone/

# Intro y referencia


## Arquitectura

Docker se compone de 3 elementos

* **Un servidor** / daemon que administra todo
	* `dockerd`
	* Guarda sus datos en `/var/lib/docker` docker.service`
* **Un cliente** que interactua con ese servidor y le dice que hacer
	* el CLI `docker`
	* Docker REST API
* **Docker objects** que representan los elementos relevantes
	* Imagenes (un filesystem read-only)
	* Containers (un filesystem basado en una imagen, que ademas es writable y corre procesos)
	* Volumes
	* Networks


Ademas podes agrupar **containers instanciados en diferentes  daemons (osea probablemente en diferentes pcs)** a esto se lo llama **"service"** y te permiten tener  tener **Computacion distribuida**


## Images, containers y layers

* Las **IMAGES** son **un Read-only filesystem**  que son el punto de partida para crear un container
* Un **CONTAINER** es un conjunto de **procesos** corriendo en un **filesystem** que es **una copia de una imagen cuando se creo el container**

>Podes ver los containers como **instanciaciones de una imagen**, cuando creas un container estas **copando** el filesystem de una **imagen** y colocandolo en un **read/write filesystem** que ademas tiene **funcionando ciertos procesos** (el container).

El sistema docker funciona con **layers** que consisten en
*	**Una serie de imagenes**, cada una **sobreescribiendo y añadiendo** cosas de la anterior generando un filesystem final
	*	Ej una añade el SO, otra añade apache, otra añade wordpress
*	Un **contanier** que copia el **filesistem final** en un **filesystem read/write** y lo corre con ciertos **procesos**

![enter image description here](https://lh3.googleusercontent.com/5npNSbJiLcpmwCDMq2bYr_VG2BasVuv8QwJvr8Pxm4TcqiobhQAoXJ6ZYyDyWj-p22WCr8PinX61)







## Administracion 


### Best practices


* **SINGLE REPONSABILITY:** 
	* Cada container tiene una sola responsabilidad
	* Generalente implica un solo proceso
* Colocar **LABELS**
	* En **imagenes, containers, netoworks, volumes y daemons, nodes, services**
	* **convencion:** `<dominio>.tus.labels:<algun valor>`
* **LIMPIEZA**
	* `docker image prune` limpiar imagenes no usadas
* **Ver si docker esta funcionando**
	* `docker info`
* **iniciar daemon**
	* `service docker start`
	* `systemctl start docker` 



### Referencia de comandos utiles

* `docker info` Muestra el estado del servicio docker (contenedores corriendo, pausados, detenidos, imagenes, version)
* `docker ps <-param>`  Lista los containers que estan en funcionamiento
	* **-a** Muestra containers que fueron iniciados y ahora estan detenidos
	* **-q** Solo muestra los containers id
* `docker run <-param> <imagen> <comando>` Crea un container desde una imagen, si no la encuentra la descarga del repositorio
	* **-param**
		* **--name nombre** Le asigna un nombre al container que podes usar en lugar de su **ID**
		* **-it** Hace que el container sea interactivo (te conecta a su consola)
		*  **-d** run in background (daemon)
		* **`-p <hostport>:<containerport>`** mapea un puerto a otro
	* **imagen** Nombre de la imagen desde la que se crea el container
	* **comando** El comando que correr apenas el container termine de crearse. **overridea el comando default del dockerfile (CMD)**
* `docker image ls` Lista las imagenes disponibles en el OS para crear containers
* `docker container ls` Lista containers 
	* `docker container ls --all`muestra containers funcionando
* `docker logs <id>` Muestra el log de stdout de un container
* `docker container stop <id>` Detiene el contenedor gracefully
* `docker container  kill <id>` detiene el contenedor no gracefully
* `docker pull <image name>:<TAG>` descarga de dockerhub una imagen, las tags indican variaciones de una imagen
* `docker diff <id>` muestra las diferencias entre el container y su base image
* `docker commit <id>` crea una imagen del container
* `docker tag <imageId> <tuTag>` coloca un nombre (tag) a una imagen
* `docker rm <id>` Elimina un container
*  `docker rmi <idImagen>` Elimina una imagen
* `docker port <id>` muestra el mapping de puertos para un contianer
* `docker stats` Ver recursos usados por los containers



## Notas de instalacion
### Acerca del uso de SUDO

Para evitar el uso de **SUDO** es critico agregar al usuario que va a administrar docker al grupo `docker` que se crea en el sistema al instalarlo.

### IP de containers en windows

En windows no podes usar localhost para comunicarte con un container usando un puerto mapeado, tenes que usar **la ip del container y el puerto mapeado**,  la obtenes con el comando ``docker-machine ip``

### Detener contenedor en windows

En windows `CTRL-C` no detiene el contenedor, tenes que detenerlo con ``docker container stop <Container NAME or ID``





# Containers - WIP

### Crear
Una buena analogia de los containers es que son como objetos    instanciados de una clase (**la imagen**). son iguales a la imagen al momento de crearse, pero luego a lo largo de su vida son modificados.

*Si no tenes la imagen cargada entonces docker intenta bajarla de dockerhub*

Para instanciar un container desde una imagen usas.

**Instanciar y iniciar:** `docker run <-param> <imagen> <comando>`
**Solo instanciar:** `docker create <-param> <imagen> <comando>`
* **-param**
	* **- -name nombre** Le asigna un nombre al container que podes usar en lugar de su **ID**
	* **-it** Hace que el container sea interactivo (te conecta a su consola)
	*  **-d** run in background (daemon)
	* **`-p <hostport>:<containerport>`** mapea un puerto a otro
* **imagen** Nombre de la imagen desde la que se crea el container
* **comando** El comando que correr apenas el container termine de crearse. **overridea el comando default del dockerfile (CMD)**


### Nombrar

Los containers y las imagenes siempre tienen **ids** que **se ven como un hash**, pero ademas  pueden tener:
*  **nombres** en el caso de los **containers**
* **tags** en el caso de las **imagenes**

>**Donde sea que puedas usar un ID podes usar el nombre o el tag**

**Para nombrarlos** usamos el parametro **`--name`**

```
docker run --name miNombre <imagen> 
```

### Administracion


>**CRITICO:** Los containers solo funcionan si tienen por lo menos un proceso corriendo esto significa que si no tienen procesos se los considera detenidos

* **SALIR DEL CONTENEDOR:**  
	* `Ctrl + P + Q`
	* **No usar** `ctrl + C`, si es el ultimo proceso entonces detenes el contenedor!
* **ENTRAR AL PROCESO PRINCIPAL DEL  CONTENDOR:**
	Control de procesos

Podes controlar los containers que tenes usando 
* `docker container stop <id>`
	* Detiene el proceso
* `docker container start <id>`
* `docker attach <container>`
	* el **proceso principal** es el determinado en `RUN,ENTRYPOINT o CMD` y puede no ser bash 
* **ABRIR UN BASH o un proceso EN EL CONTENEDOR**
	* `docker exec -it <container> /bin/bash`
		* Aca si podes salir con `crtl + C` por que creaste un nuevo proc pause<id>`

### Container logs
El stdout de un container va a los logs de docker, accesibleso de bash separado del que ya corrie
	* `docker exec -it <container> <path a cualsde 
`docker logs <id>`

### Daemon
En produccion vas a quier ejec en el container>`
* **INSPECCIONAR CONTAINER**
	* para ver sus detalles, como **networks volumenes, etc**
	* `docker inspect <container>`
* **ISTANCIAR EN BACKGROUND**
	* `docker run -d <imagen>`
* **VER LOGS**
	* `docker logs <id>`
* **VER REURSOS USADOS**
	* `docker stats` Ver recursos usados por los containers




**Podes controlar los containers que tenes usando:** 
* `docker container stop <id>`
	* Detiene el proceso
* `docker container start <id>`
* `docker container pause<id>`

er mantener los containers funcionando como **daemons** usando  `docker run -d <imagen>`

### Conectarte con bash
Simplemente ejecutas un bash en el container y pedis que sea interactivo

```
docker exec -t -i container_name /bin/bash
```

# Images

## Mejores practicas

* Los containers deben ser **stateless** y deben poder ser detenidos, reiniciados o reinstanciados de su imagen en todo momento
* Cada container debe tener un unico **concern**

## Crear imagen - Modo Interactivo
>**CRITICO:** Los containers son **efimeros**, si el server se apaga su estado se pierde. 

Para crear una imagen
* Creas un container en base a una o varias imagenes
* haces tus cambios
* corres **`docker commit <idContainer> <tag>`** y docker guarda una nueva imagen basada en tu container (usando el `id`) con el nombre que coloques en `TAG`



## Crear imagen - DockerFile

### Overview

Docker crea las imagenes usando un CLI llamado `docker build`, este requieren una serie de instrucciones escritas en un `DockerFile`.

Una vez que tenes el `dockerFile` el builder sigue los siguientes pasos: 
* **SE ESTABLECE EL BUILD CONTEXT:** que es la carpeta donde esta el **dockerfile** , <u>los paths de tu dockerfile arrancan ahi</u>
* **SE PROCESA EL DOCKERFILE:** 
	* Se lee linea por linea
	* Para cada linea se **crea un container "intermedio"**
	* Se **corre la instruccion de esa linea** del dockerfile en el container
	*  se guarda el resultado como **imagen** o **LAYER**
	* El container de la proxima linea se **instancia** usando el **layer anterior** 
* **CACHE:** 
	* Se **guardan los layers en el cache** 
	* Se usa el cache para cada linea de dockerfile que no cambo
	* Se **invalida un layer cacheada** si:
		*  Su linea en el dockerfile cambio 
		* El checksum de los archivos que se copian con `ADD` /`COPY` cambiaron
* **RESULTADO:**  una imagen


### Resumen rapido para crear imagenes

Para crear una imagen de docker de forma programatica usamos un **dockerfile** junto con **archivos que querramos copiar al contenedor**. 

Los necesitas a todos en la misma carpeta y a esta la llamaremos **build context**.

```Dockerfile
FROM <imagen base>
RUN <comandos ej: apt-get update>
RUN <comandos ej: apt-get install -y wget>
```

>**Tips:** Conviene siempre colocar los comandos de tal forma que las cosas con menos cambios vayan arriba y las de mayor frecuencia de cambios vayan abajo. Esto permite aprovechar el **build cache** para hacer los builds mas rapidos.


**En tu dockerfile probablemente quieras:**
* **usar una imagen** oficial de base usando `FROM`
* **Copiar archivos** al contenedor usando `COPY`
* **instalar dependencias** con algun package manager `RUN` usando algun package.json que copiaste usando copy
	* apt-get
	* npm
	* pip
* **Exponer puertos** usando `EXPOSE`
* **Setear variables de entorno**
	* usando `ENV` _no recomendado_
	* copiando archivos **.sh** a  **/etc/profile.d** 

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copias cosas del directorio del dockerfile al contenedor
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]

``` 
 **Finalmente usas el dockerfile asi:**
 Para crear tu imagen entonces haces lo siguiente
**`Docker build --tag <miTag>:<version> <pathHaciaElBuildContext>`**



###  Build context
Una vez que tenes un Dockerfile podes crear tu imagen. <u>`Docker build` necesita dos cosas para crear una imagen</u>

*  EL **DockerFile** que describe que hacer
* Un **Build context** que es una carpeta con:
	* El **dockerFile**
	* Todos los **archivos que podrias necesitar** copiar al container con comandos como `COPY`, `ADD`, etc

>**EL build context agranda la imagen** (no asi el container) ya que <u>se copia todo el build context para tenerlo disponible a futuros layers que pudieran querer correr comandos como `COPY`. es por eso que **te conviene mantenerlo chiquito**</u>
>Para eso podes usar el archivo `.dockerignore` para **ignorar** los archivos que no queres que formen parte del **build context**


### Build cache, cache busting y apt-get

Docker guarda un cache de las operaciones para hacer los build processes mas rapidos. 

El cache funciona de la siguiente manera:
* Si la **base image** es la misma, uso cache
* **linea por linea del dockerfile** voy usando los layers en el cache a medida que veo que **las instrucciones fueron las mismas**
	* Para las instrucciones `COPY` y `ADD` hago un **checksum de los archivos**, si los checksums son iguales a los del cache entonces lo uso

> **NOTA IMPORTANTE SOBRE APT-GET:** Notese que esto se cachea
> ```Dockerfile
>RUN apt-get update  
>RUN apt-get install -y nginx
>``` 
> Por lo tanto cambiar el `apt-get install` **no genera** que se vuelva a correr el `apt-get update`. Te conviene entonces poner **todo junto en un comando**
> ```Dockerfile
>RUN apt-get update && apt-get install -y \
>    aufs-tools \
>   automake \
>   ETC ETC...
>``` 

### Multi-stage build

Es una tecnica para hacer que **las imagenes pesen menos** que consiste en **separar la imagen que tiene herramientas de desarrollo de la que  corre tu programa en produccion**, todo en el mismo dockerfile

**Generalmente funciona asi:**
* **STAGE 1:**
	* Usas una imagen con todas las dependencias que pudieras necesitas
	* Corres tus comandos para preparar tu codigo (`RUN`, etc)
* **STAGE 2:**
	* Creas una nueva imagen con una base image que tenga lo minimo indispensable
	* Copias los archivos compilados de la primera imagen a la segunda
* **STAGE 3, 4, ETC**

Es importante notar que podemos **pedirle a docker que construya hasta cierto stage** asi:
```bash
$ docker build --target miStage .
``` 

**EJEMPLO:**

```Dockerfile
#####
#STAGE 1: Imagen con todos los  chiches
#La llamamos "MiImagenConChiches"
#####

FROM golang:1.7.3 AS MiImagenConChiches
#Hago mi procesamiento, en este caso compila un archivo
#De GO
WORKDIR /go/src/github.com/alexellis/href-counter/
RUN go get -d -v golang.org/x/net/html  
COPY app.go    .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

#####
#EAPA 2: Imagen con lo minimo indispensable
#La lamamos "LoMinimo"
######
FROM alpine:latest  AS LoMinimo
RUN apk --no-cache add ca-certificates
WORKDIR /root/
#Copio los archivos compilados de la primera imagen en esta
COPY --from=MiImagenConChiches /go/src/github.com/alexellis/href-counter/app .
CMD ["./app"]
```





### Mas comandos de docker file
   * **`FROM:<imagen>`** Indica la imagen de base 
   * **`LABEL:<key>=<value>`** el label para la imagen, algo human friendly, <u>podes tener varios labels<u>.
	   * `key` deberia ser prefixeado por un dominio que controles (Best practice), puede tener puntos o guiones
	   * `Value` puede ser cualquier cosa (dominio, etc)
   * **`WORKDIR:<PATH>`** establece el woring directory del container desde este punto en adelante (ej `RUN` o `CMD` arrancan con ese path)
   * **`USER: <username|UID>`** indica con que usuario se correra el servicio, es para no correr el servicio como root.
	   * Precio a esto necesitas crear el usuario, ej: `RUN useradd --no-log-init -r -g postgres postgres` 
   * **`CMD <comando>`** indica un comando default que correr al iniciar el container (de bash) . 
	   * Si se corre un **comando** al iniciar el container entonces overrideas al `CMD`.  ej: `docker run <-param> <imagen> <comando>`
	   *   **solo puede haber un CMD command en todo el docker file**, si hay mas de uno entonces se corre el ultimo.
   * **`ENTRYPOING ["<command>","<option1>","<option2>"...]`** 
	   * Es como `CMD` 
	   * no se overridea al insertar un comando con `docker run`
	   * `ENTRYPOING ["wget","-o","-q"]`
	   * Lo que se coloque como comando en `docker run <-param> <imagen> <comando>` se **appendea al final del comando seteado en entrypoint**
   * **`EXPOSE <portNumber>`** expone un puerto del container al host.
   * **`ADD <path host> <path container>`** Permite copiar un archivo/directorio del host al container
   * **`COPY <path host> <path container>`** Igual que add
   * **`ENV NAME World`** define variables de entorno
   * **`WORKDIR <pathEnContainer>`** setea el working directory



# Docker networking


## Conceptos 



El networking en docker consta de dos partes

* Una o varias **REDES** 
	* Administradas por docker daemon
	* Hay 4 tipos de redes con funcionamientos diferen (`host, bridge, overlay y macvlan`
* Un **CONTAINER** que 
	* **por <u>cada red</u> a la que esta conectado** tiene:
		* Una **direccion IP**
		* Una **placa ethernet simuada**
		* Varias reglas en los archivos `hosts`, `iptable`, etc que permiten su implementacion
	* Tiene especificado que **puertos compartira con el mundo exterior**





>**IMPORTENTE:** Un container puede
>* Estar conectado a **varias redes a la vez**
>* Para cada red tiene un **network adapter diferente** y una **direccion IP** diferente

## Tipos de redes

Docker tiene 4 network drivers, es decir **4 formas TOTALMENTE DIFERENTES en las que los containers se pueden vincular con redes hacia el exterior**

>Un container puede estar conectado a muchas redes usando drivers diferentes. 

* **`HOST`**: Es la forma mas basica
	*   **usa la placa de red de su host directamente**. Es decir que tiene su ip, usa sus puertos e itercepta sus paquetes.
	* Podes tener conflictos de puertos entre las aplicaciones del host y las del container
	* El container debe ser unico en el host y debe estar en modo swarm
* **`BRIDGE`:** Es la forma mas comun, los containers en bridge:
	* Se pueden **ver entre ellos si estan en el mismo host**
	* Solo exponen al exterior los puertos declarados usando `expose`
* **`OVERLAY`:** Conecta docker daemons en diferentes hosts
	* Permite que **containers en diferentes hosts se vean**
	* Es lo que usa docker swarm para comunicarse entre varios hosts
	* Usa `Vxlan` como base de funcionamiento, que ya viene en el kernel de linux
*  **`MACVLAN`:** usa la placa de red del host para exponer su propia ip
	* **Expone varias IPs desde la placa de red del host**
	* Permite que el **container tenga su propia IP** dentro de la red del host
	* Permite facilmente migrar servicios que necesitan una IP fija para interactuar con terceros (ej legacy)
	* La placa de red tiene que soportar `promiscuous mode` (poder tener varias IPs)



## Bridge

### Conceptos
Una red `bridge` te permite la **comunicacion entre containers** dentro del mismo host.

> Internamente docker hace uso de herramientas del sistema operativo del container (ej iptables de linux el hosts file, etc) para proveer estas funnciones 


Para comunicacion entre  **containers y el mundo exterior** hace falta _publicar_ los puertos con `docker run -p` o en `dockerCompose`

* **RED BRIDGE DEFAULT:**
	* Docker crea una red `bridge` por default
	* Todos los containers dentro del host estan conectados a esa red <u>**salvo que se les especifique una o varias  user defined bridge networks**</u>
	* Para que los containers se hablen hace falta que expongan puertos explicitamente usando `EXPOSE`
	* Se acceden por **IP**
	* Se comienza  considerar legacy
* **USER-DEFINED BRIDE NETWORK:**
	* Podes crear varias redes `bridge` y colocar los containers en diferentes redes para aislarlos
	* En la red los containers exponen automaticamente **TODOS los puertos entre los containers**  y **NINGUNO al mundo exterior**
	* Se acceden por **IP** o DNS usando el **container name**
* **USE CASES**
	* BRIDGE 1: DB y Web server. Sin acceso al mundo exterior
	* BRIDGE 2: Web server. Con acceso al mundo exterior


### Administracion
Los siguentes comandos te permiten administrar las redes `bridge`:

>**CRITICO:** Los  containers creados con una red especifica NO se conectan a la red BRIDGE default por default

* **CREAR RED:**
	*  `docker network create MiRed`
* **BORRAR RED:**
	*  `docker network rm MiRed`
* **CONECTAR CONTAINER**
	* Al crearlo:
		*  `docker create --name my-nginx   --network MiRed \
  --publish 8080:80 <imagen>`
		 * En `dockerFile`  usas 		` network: MiRed`
	 * Conectar container en funcionamiento:
		 *  `docker network connect <MiRed> <MiContainer>` 
 * **DESCONECTAR:**
	 *  `docker network disconnect <MiRed> <MiContainer>`

### Exponer puertos vs mapear puertos

Los contenedores de docker normalmente son cerrados (en la red bridge default) y no pueden escuchar con ningun puerto salvo que lo **expongas** usando **`EXPOSE`**.

* **EXPONER:** expone un puerto del contenedor  para que el contenedor pueda escucharlo, solo otros contenedores pueden comunicarse con el puerto, no es accesible fuera del host.
* **MAPEAR**: Mapea un puerto **expuesto** a un puerto del host. De esta manera el contenedor puede comunicarse con el mundo exterior usando la ip y un puerto del host.

### Mapeo de puertos
Normalmente los containers pueden comunicarse con el mundo exterior **saliendo por la ip del host**, pero **el mundo exterior no puede comunicarse con ellos** (ya que los paquetes los recibe el host).

Para solucionar esto usamos **port mapping**, que es **tomar un puerto del host y mapearlo a un puerto del container**.

>**POR EJEMPLO:** podemos mapear el puerto 555555 del host al puerto 80 del container, para que los paquetes que lleguen al puerto 555555  del host sean redirigidos al container como si vinieran de su puerto 80 

**Para realizar el mapeo  usamos** 
* el flag **`--publish-all`**  para autodetectar los puertos activos del container y mapearlos automaticamente a puertos random del host
	*  `docker run <-param> --publish-all <imagen> <comando>`  
*  el flag **`-p <puerto container>:<puerto host>`**

Ahora podemos **ver los puertos mapeados** por docker para ese container usando **`docker port <id>`**.

## Overlay

### Conceptos

Es un tipo de red que hace uso de la tecnologia `vxlan` que ya viene integrada en el kernel de linux para conectar los docker daemons entre si y que **los containers puedan comunicarse aunque esten en hosts diferentes**

<u>Si necesitas que los containers entre varios hosts se comuniquen entre si simplemente pones esos containers en la misma red overlay y listo.</u>

>**CRITICO:** Necesitas tener los siguientes puertos abiertos en los hosts que van a usar overlay networks para que funcione
>*   TCP port 2377 for cluster management communications
>*   TCP and UDP port 7946 for communication among nodes
>*   UDP port 4789 for overlay network traffic


* **BENEFICIOS GENERALES:**
	* **Comunicacion entre contianers en diferentes hosts**
	* **PUERTOS**:
		* Abiertos entre containers
		* Cerrados al mundo exterior (salvo que se publquen)
	* **LOAD-BALANCING**
		* Funciona como  load balacer para los servicios en la red, diistribuyendo las solicitudes entre los nodos 

----


* **RED OVERLAY DEFAULT**
	* Se crea una red overlay default llamada `ingress` cuando **inicias el swarm mode**,  se usa para
	*  que el **swarm controller** pueda comunicarse y controlar a los **workers**
	* Comunicar los containers en todo el swarm
	* No funciona en containers que no son parte de un service
* **REDES OVERLAY USER-DEFINED**
	* Para **stand-alone containers** podes crear una overlay network asi
		* `docker network create  -d  overlay --attachable <MiRed>`
	* Para **containers en swarm services** podes crear un overlay network asi
		* `docker network create -d overlay <MiRed>`

.



### Exposicion de puertos

En un red overlay **todos los puertos estan expuestos entre los containers** pero **ningun puerto esta expuesto por default al mundo exterior**

Para exponer puertos al mundo exterior es necesario **PUBLICARLOS**


### Encriptacion

En una red overlay hay dos tipos de comunicaciones
* **Comunicaciones entre los  docker daemons**
	* Se encrptan por default
* **Comunicacion de tus aplicaciones**
	* No se encriptan por default
	* Podes encriptarlas usando `--opt encrypted`


## Inspeccionar redes

Podes inspeccionar una red para ver que contianers forman parte de ella y que caracteristicas tiene con el siguiente comando

```
docker network inspect bridge
```

## Administracion


# Data persistence


## Conceptos

Existen 5 tipos de almacenamiento de informacion en docker, sin embargo **desde el punto de vista del container son todos iguales**, lo que cambia es **como los ve el host** 
* **WRITABLE LAYER** del container
	* Es **efimero**,  cuando el container se borra los datos tambien
	* Aumenta el tamaño del container
*  **VOLUMES:** 
	* Manejados y administrados solo por docker
	* Los datos se guardan en un **archivo** en el host en `/var/lib/docker/volumes/` 
	* Persisten cuando el container se borra 
	* <u>Solo docker debe modificarlos, nadie mas</u>
	* No aumenta el tamaño del container
* **MOUNT BINDS**
	* Se monta una carpeta del host en el container
	* Puede estar en cualquier ruta
* **TPFS** 
	* Es un volumen que se guarda en la RAM del host
	* Es efimero pero rapido
	* Bueno para datos que no deben persistir (keys, secrets..)
* **Volume Driver**
	* Te permite hacer una abstraccion de un volumen a patir de
		* AWS S3
		* NFS
		* Otros servicios
	* Podes (dependiendo del servicio de base que uses) copartir el volumen entre varios containers

## Volumenes

Los volumenes son <u>La fora preferencial de guardar datos en docker</u> ya que son totalmente administrados por docker

**CARACTERISTICAS:**
* Persisten hasta ser borrados explicitamente con `docker prune <volumen>`
* Se guardan en un archivo en el host, generalmente en `/var/lib/docker/volumes/`
* Se pueden **compartir entre varios containers** y ser accedidos a la vez 
* Se pueden crear con `docker volume create`
* Al montarlos se lo puede hacer con un **nombre** o de forma **anonima** ( y se les asignara un nombre aleatorio)
* No aumentan el tamaño de los containers

**USE-CASES:**

* **COMPARTIR** archivos entre containers
* **DECOUPLING** entre el filesystem/configuracion del host y el  container (por seguridad o por falta de control sobre el host)
* **BACKUP/RESTORE/MIGRATE:**  copiando la carpeta `/var/lib/docker/volumes/` podes 
	* Tener tus volumenes backupeados 
	*  Llevarlos a otro host



## Bind mounts

Son una _carpeta compartida_ entre el host y el container, <u>**en general es preferible usar volumes**</u> pero aun asi hay casos donde podrias querer tener bind mounts


**CARACTERISTICAS:**
*  Se referencian los archivos por su path completo en el `host` (aun dentro del container)
* **PORTABILIDAD:** Requieren que el  host tenga un filesystem con una estructura especifica, osea que **no son tan portables como los volumes**
* **SEGURIDAD:** una vulnerabilidad en el container implica que tiene acceso a carpetas que existen en el host
* **SOLAPAMIENTO:** Si montas un bind en una carpeta del container **que tiene contenido este se vuelve inaccesible** por el container, solo se ve el contenido del host. 


**USE-CASES:**

* Compartir archivos de configuracion del host al container
* Compartir **codigo fuente** durante **development**
* Cuando tenes garantia de que el host tiene los archivos que necesitas

## Administracion



**TIPS:**
* Si montas un volumen en una carpeta que ya tiene datos, se crea el volumen y sincronizan esos datos en el
* Si creas un volumen en una carpeta que no existe esta se crea.

**COMANDOS:**

* **CREAR/MONTAR:**
	* `--mount 'key1=value1,key2=value2' ` con los siguientes key-value pairs
		* `type=` Selecciona el tipo de volumen
			* Volume
			* Bind
			* tmpfs
		* `source= <path |  nombreDeVolumen>` 
			* Que **volumen** montar o 
			* un path del host para el **bind**, si se omite se genera un nombre aleatorio
		* `destination=<path>` path en el container donde se monta
		* `readonly` especiica que el volumen es readonly
* **Crear un volumen:** `docker volume create my-vol`
* **Listar volumenes** `docker volume ls`
* **Inspeccionar volumenes:** `docker volume inspect my-vol`
* **Remover:** `docker volume rm my-vol` 
* **Inspeccionar volumenes en container** `docker inspect <container>`

**BACKUP DE VOLUMENES:**

Para realizar un backup basicamente lo que haces es copiar sus datos a un bind mount usando un container (lo logico).

 **Un metodo para hacerlo en un solo comando es:**
* Montas un container que se auto-destruye cuando termine de correr un poceso
* Montas el volumen y un bind para copiar su contenido al host
* Usas `tar` para copiar el volumen al bind
```bash
$ docker run 
		#Autdestruir container al terminar comando
	--rm 
	#montar volumenes de Micontainer
	--volumes-from <MiContainer>
	#Hacer un bind mount 
	-v <path en host>:/miBackuop 
	#la imagen a usar
	ubuntu 
	#Tar datos del volume al Bind
	# para recuperarlos despues
	tar cvf <path>/backup.tar /miVolumen

```



## Volume drivers

Te permiten mediante **plugins** montar servcios (**NFS, S3, etc**)  como si fueran volumenes de docker. Esto permite compartir volumenes entre containers de manera totalmente transparente. **los drivers funcionan como intermediariios entre el container y el filesystem**


# Distributed / load balancing - WIP
# Volumenes

>**CRITICO:** Es importante tener en cuenta que los volumenes compartidos no se commitean como parte de una imagen

### Entre host y container (permanente)
Para montar un directorio del host  como un volumen en un container podes hacer:

* `docker run <-param> -v path/en/el/container:path/en/el/host<imagen> <comando>` 
* Podes agregar permisos `docker run <-param> -v path/en/el/container:path/en/el/host:rw- <imagen> <comando>` 

Esto te permite tener **archivos pemanentes** que no se eliminan si el container se detiene.

### Entre containers

Podes compartir los volumenes de un container con otros, incluso si este no esta corriendo.

Para crear un volumen compartible usas el siguiente comando
* `docker run <-param> -v path/en/el/container <nombreDeVolumen> <imagen> <comando>` 

Para usar los volumenes de otro container
* `docker run <-param> -volumes-from <containerId> <imagen> <comando>` 


## Docker compose - WIP

Docker compose te permite instanciar y configurar multiples contenedores desde un solo archivo denominado **dockerCompose** en el formato **.yml**

En lugar de ejecutar `docker run <-param> -volumes-from <containerId> <imagen> <comando>`  manualmente para cada container declaras 

```yml
version: 2 #Version de sintaxis de dockercompose
#Declaras una red de load balancers (opcional)
networks: 
  nombreDeLoadBalancer:
#Declaras servicios
services:
	# Cada servicio es un contenedor, en este caso 
	#"web" y "database" 
	web:
	  name: "nombre del contenedor" #como --name
	  image: "miwilfly:7" #imagen usada
	  ports: #el mapeo de puertos
	   - "80:8000"
	   - "21:300"
	  links: ·#aliases
	   - basedatos:miAliasVisibleParaWeb
	  volumes: 
	   - "<path en container>:<pathHost>"
	  deploy:
	    placement: #ej Solo correr en swarm manager
	      constraints: [node.role == manager]
	  command: <comando, equivalente a CMD>
	  networks: 
	    - nombreDeLoadBalancer
	basedatos:
		image:"mysql:lastest"
		ports:
		 - "3306:3306"

```



## DockerHub

Dockerhub funciona como github pero para containers.
* **Push** - podes publicar tus imagenes tagueandolas  con el nombre de usuario de dockerhub, tu repositiorio y un tag para identificarlo (una version posiblemente)
	```
	docker tag <imagen> username/repository:tag
	docker push username/repository:tag
	```
* **Pull** - Podes tomar imagenes tuyas o de otro repositorio haciando un pull con la sintaxis `username/repository:tag`
	```
	docker run -p 4000:80 username/repository:tag
	```


# Distributed / load balancing




### Conceptos
Distributed systems se basa principalmente en el concepto de **services** o de **micro-services**, es decir dividir el sistema en varias partes que sea stateless y corran en diferentes servidores. **cada servicio consiste en uno o varios containers funcionando en paralelo con la misma imagen**


**Nomenclatura:**
* **SWARM WORKER** nodo con un docker daemon que corre algunos o todos los tasks de uno o varios services. se comunica mediante DOCKER API
* **SWARM MANAGER** computadora que dirige el swarm y le dice a cada node que task de cada servicio instanciar. se comunica mediante DOCKER API
* **SWARM:** conjunto de nodes que corren services
* **NODE:** computadora que esta corriendo un docker daemon
* **STACK:** Conjunto de services. configurado en **dockerCompose**
* **SERVICE:** Conjunto de containers:
	*  instanciados desde la misma imagen 
	* configurados con dockerCompose
	* Manejados por un swarm manager
* **TASK:** un container que forma parte de un service
* **LOAD-BALANCER:** El sistema que se encarga de distribuir los requests entre ciertos containers



###  Overview

**CONFIGURACION:** 


Desde un archivo `dockerCompose`  se definen las cosas basicas necesarias para que el swarm funcione:
* **Una lista de servicios**, cada uno tiene:
	* Una imagen que se va a instanciar 
	* La cantidad de instancias que mantener activas en el swarm (**tasks**)
	* Las redes a las que se los contecta
	* Los puertos que exponen
* **Una lista de redes**
* **Una lista de volumenes**


**OPERACION:**

*  se inicia un **swarm manager** y se unen los **workers** a el.
* El **swarm manager** entonces instancia 
	* Los **tasks** en los **workers** segun lo indicado en cada **servicio**La descripcion de cuantos tasks de **una misma imagen** se deben mantener instanciados a lo largo del swarm en todo momento (ej 10 apache servers). configurado en **dockerCompose**.
* **TASK:** un container 
	*  Las **redes** 
	*  Los **volumenes**
* Cuando llega un request a **cualquiera** de los hosts del swarm
	* Se define a que servicio pertenece dependiendo del puerto
	* Se entrega el request a uno de los tasks en algun host del swarm instanciados para ese servicio(**load balancer**)
	* Ese task puede comunicarse con otros containers
		* Si estan en la misma red `overlay`
		* Si estan en el mismo host y misma red `bridge`
	* El taks puede responder por los puertos `expuestos`


**LOAD-BALANCER:** El sistema que se encarga de distribuir los requests entre ciertos containers

### Consideraciones previas

Necesitas que cada host  tenga abiertos los puertos
-   Port 7946 TCP/UDP for container network discovery.
-   Port 4789 UDP for the container ingress network.

### Usando docker compose y swarm - wip

#### Generar el swarm

* Para transformar este nodo en un **swarm manager** hacemos
	*  ```docker swarm init	```
	* El comando devolvera un comando ```docker join --token <token> <ip>	``` que podemos usar para **unir workers al swarm**
* Para ver los nodos hacemos ``docker node ls``
* para **apagar docker swarm** haces `docker swarm leave --force`


>Una vez creado el swarm todos tus **comandos de docker** los vas a realizar en el **swarm manager** y este se encargara de coordinar los **workers**
#### Configurar el stack
DockerCompose te permite  **configurar  un stack** indicando  **servicios** que se componen de una **cierta cantidad de contenedores instanciados de la misma imagen** de ciertas **caracteristicas** y con ciertas **limitaciones** 

```yml
version: "3"
##Listado de los servcios:
services:
  ##Servicio 1, llamado "web" y su descripcion
  web:
    image: username/repo:tag
    deploy:
      replicas: 5 #Correr 5 contenedores
      resources:
        limits:
          cpus: "0.1" # cada uno usa max 10% de 1 CPU core
          memory: 50M # cada uno usa max 50mb ram
      restart_policy:
        condition: on-failure # Reiniciar si hay error
    ports: #Mapeo de puertos
      - "4000:80"
    networks: #Web va a usar el load-balancer "webnet"
      - webnet
   #Aca colocarias otro servico
  otroServicio:
networks: #Defino el load-balancer network llamado "webnet"
  webnet:
  

```

#### Desplegar el stack en el swarm

* Para **desplegar un stack en el swarm** hacemos 
```docker stack deploy -c docker-compose.yml <nombreDelSwarm>```
* Para **eliminar** el stack haces `docker stack rm getstartedlab`

#### Ver servicios, tasks, nodes y stacks activos en swarm

Podes ver los **servicios corriendo en un stack** asi
```
docker stack services <nombreDelSwarm>
```
Para ver los **tasks corriendo en un service**, haces
```
docker service ps getstartedlab_web
```

Para ver los **tasks corriendo en un stack**
```
docker stack ps <stackname>
```

Para ver los **nodos** hacemos 
```
docker node ls
```

#### Escalar y distribuir

Podes escalar el servicio cambiando la cantidad de replicas en el docker-compose y corriendo:

```
docker stack deploy -c docker-compose.yml <nombreStack>
```

No hay necesidad de hacer nada mas, **los contenedores se distribuiran en todo el swarm y el load balancer va a distribuir la carga equitativamente.**

#### Acceder

Podes acceder con la ip de cualquier **worker** o el **swarm manager**, el **load balancer** se va a hacer cargo de todo


#### shared files y volumes


Si necesitas compartir archivos entre los containers (ej archivos subidos por suers) tenes que tener **un container en un solo nodo que tenga un volumen compartirdo con ese nodo**

Ejemplo de docker-composer
```yml
redis:
    image: redis
    ports:
      - "6379:6379"
    volumes:
      - "/home/docker/data:/data"
    deploy: ##Solo existira en el swarm manager
      placement:
        constraints: [node.role == manager]
```






# Logging - WIP

## Overview


existen 3 niveles de logging que nos pueden interesar
* **Swarm level**
	* Cuando tenes servicios funcionando en un swarm
* **Daemon level**
	* Logs de lo que sucede en el daemon (instanciacion, containers, etc)
* **Containaer level**
	* Lo que sucede en el container y las aplicaciones en su interior
	* Los procesos deben escribir sus logs en `stdin` y `stderr`
	* Luego son procesados por un **log driver** en el **daemon** que los guardara de una forma determinada



Existen diferentes formas/drivers para guardar los logs, los que vienen con docker por default se integran con `docker CLI` y esto permite ver los logs desde la consola con facilidad.

Generlmente especificas un solo driver para el **docker daemon** y lo usas para todos los containers del host, pero podes tener log drivers especificos para cada container en particular

>**IMPORTANTE:** algunos log drivers podrian enviar los datos a una DB, una aplicacion externa, etc. En estos casos no podes ver los logs desde la consola


## Daemon logs


* **LOGGING NIVEL DAEMON:**
	* Podes encontrar los logs del daemon aca
		* Red hat `/var/log/messages`
		* Debian `/var/log/daemon.log`
		* Ubuntu/cenOs `journalctl -u docker.service`


## Container logging


### Administracion


Existen diferentes formas/drivers para guardar los logs, los que vienen con docker por default se integran con `docker CLI` y esto permite ver los logs desde la consola con facilidad, estos son:
-   `local`
-   `json-file`
-   `journald`

Generlmente especificas un solo driver para el **docker daemon** y lo usas para todos los containers del host, pero podes tener log drivers especificos para cada container en particular

>**IMPORTANTE:** algunos log drivers podrian enviar los datos a una DB, una aplicacion externa, etc. En estos casos no podes ver los logs desde la consola

 El output aparece como si lo estuvieras viendo en la consola

* **VER LOGS**
	* **De Container**
  `docker logs <container>`
	* **De containers en un service**
   `docker service logs <service>`
*  **UBICAR EL LOG DRIVER**
	* **De daemon**
		Aparecen en `docker info`
	* **De container especifico**
	 Aparece en `docker inspect <container>`
* **LOG DRIVER ESPECIFICO PARA UN CONTAIER**
	* `docker run -it --log-driver <TuDriver> alpine ash`

### Configuracion


Para guardar logs en docker es importante entender que el docker daemon espera que los containers escriban toda la informacion relevante de logs a  la consola (es decir `/dev/stderr` y `/dev/stdout`)

Una vez que esto sucede, el daemon docker lee la informacion y actua en base a lo que le indique el **log driver** que este configurado, este puede por ejemplo guardarlo en un archivo, en una DB, etc.

La configuracion del daemon se puede encontrar en `/etc/docker/daemonjson`

* **LOGGING DEL CONTAINER:**
	* **EN CONTAINER:**
		*  Tenes que configurar tus plicaciones para que arrojen sus logs a: 
			* `/dev/stderr`
			* `/dev/stdout`
		* Podes indicar un logger driver especifico diferente para un container asi 
			* `docker run -it --log-driver none alpine ash`
	* **EN HOST:**
		* Elegir el **`log driver`**  que el daemon usara para guardar los logs, configurado en `/etc/docker/daemon.js`, ej: 
			```json 
			{
			#el driver
			  "log-driver": "json-file",
			  #Sus opciones (opcional)
			  "log-opts": {
			    "max-size": "10m",
			    #Todos son strings, no hay ints ni bools
			    "max-file": "3", 
			    "labels": "production_status",
			    "env": "os,customer"
			  }
			}
	```


### Tagging
Notese que en una de las lineas de configuracion esta el key `labels`, este te permite configurar lo que precede a la linea de log (ej el nombre del container, la fecha, etc). 

**Toma este markup language:**

* `{{.ID}}` - The first 12 characters of the container ID.
* `{{.FullID}}` - The full container ID.
*`{{.Name}}` - The container name.
* `{{.ImageID}}` - The first 12 characters of the container’s image ID.
* `{{.ImageFullID}}`- The container’s full image ID.
* `{{.ImageName}}` - The name of the image used by the container.
* `{{.DaemonName}}` - The name of the docker program (`docker`).


### Drivers disponibles
**Los drivers disponibles son:**

* **SYSLOG**
	* Escribe los logs en el syslog del host
	* `"log-driver": "syslog"` 
* **LOCAL**
Guarda los logs en un archivo   optimizado para usarse con docker, normalmente hasta 100mb de logs en 5 archivos de 20mb y compresion automatica
	* **Opciones**
		* `max-size:20m`  Cantidad max de logs en `k`,  `m`,o  `g`. Default es 20m.
		* `max-file` Max cantidad de archvios antes e rotacion. Default 5.
		* `compress` habilitar compresion, default true
	* **JSON-FILE** Guarda los logs en un archivo  json facilmente leible por humanos
		```json
		{
		  "log-driver": "json-file",
		  "log-opts": {
		    "max-size": "10m",
		    "max-file": "3" 
		  }
		}
		```
		* **Opciones**
		* `max-size` maximo tamaño de cada archivo
		* `max-file`Cantidad maxima de archvios antes de rotar
		* `labels` Tags que se colocan (hostname, container name, ip, fecha, hora)
		* `env` Applies when starting the Docker daemon. A comma-separated list of logging-related environment variables this daemon accepts. Used for advanced  [log tag options](https://docs.docker.com/config/containers/logging/log_tags/).
		* `env-regex` Similar to and compatible with`env`. A regular expression to match logging-related environment variables. Used for advanced  [log tag options](https://docs.docker.com/config/containers/logging/log_tags/).
		* `compress` Compresion, `disabled` por default


* `"log-driver": "json-file"` el default
	* `"log-driver": "fluentd"` usa fluentd
	* varios otros
	* 


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NzU0ODMyNzJdfQ==
-->