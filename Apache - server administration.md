
* DOCS: http://httpd.apache.org/docs/current/

CURSO
https://www.youtube.com/watch?v=gPOliFwMFCk&list=PLbjlI3cowd5-pvfO521ejRI1Q6abFkNQc

# Intro

## Conceptos basicos
* Apache esta armado de forma increiblemente modular, el CORE de apache es relativamente pequeño.

* Apache se configura principalmente mediante archivos de texto mediante _directivas_

## Arquitectura de apache 

Apache procesa las solicitudes de acuerdo a un **Multi-Processing Module** o  **MPM** que le indica como actuar ante multiples solicitudes paralelas


### Prefork MPM

Prefork es la arquitectura mas antigua y menos eficiente.
* Un proceso central maneja la instanciacion de otros servidores a medida que son necesarios
* Se genera una instancia de servidor (**un proceso**) que maneja una unica conexion
	* Se mantienen siempre servidores en LISTEN para procesar nuevos requests 
* Luego de terminar la solicitud se elimina el proceso.
* Cada proceso es un unico thread de procesamiento.

Este modo es util si estas usando librerias que no son compatibles con multi-threading 

**EJ:**
* APACHE - **proceso madre que spawnea servidores a medida que son necesarios**
	* Server 1- **Procesa request**
	* Server 2
	* Server 3



### Worker MPM

Worker es una arquitectura mas moderna que hace uso de multi-threading.
Funciona asi
*  Un proceso central que abre procesos servidores a medida que son necesarios.
* Cada proceso servidor crea y administra una cantidad fija de threads
* Cada thread de procesamiento:	
	* Se mantiene en **LISTEN** para tomar nuevas conexiones a penas es creado
	*  Es responsable de procesar un solo request HTTP



**EJ:**
* APACHE - **proceso madre que spawnea servidores a medida que son necesarios**
	* Server 1- **administra threads**
		* Thread 1 - **Procesa un request**
		* Thread 2
		* ...
		* Thread 200 
	* Server 2
	* Server 3
		* Thread 1
		* Thread 2
		* ...
		* Thread 200


### Event MPM

Es extremadamente similar a worker, pero intenta evitar que los threads pierdan el tiempo manteniendo conexiones categorizadas como **ESTABLISHED**  que pueden no recibir mensajes durante largos periodos de tiempo.

>Recordemos que Apache no cierra las conexiones inmediatamente si esta puesto en **KeepAlive** y esto salva mucho overhead de volver a crear la conexion TCP con cada solicitud

Con este proposito se establece **un thread por cada proceso** que esta encargado unicamente de :
* **CONOCER** 
	* Todas las conexiones en **LISTEN**
	* Todas las conexiones en **ESTABLISHED**
* **RECIBIR**  todos los segmentos TCP entrantes
* **DELEGAR** cada segmento al uno de los threads libres 

De esta manera nunca quedan threads esperando nuevos mensajes en una conexion **ESTABLISHED** cuando se **mantienen las conexiones abiertas** usando **KEEPALIVE**

# Configuracion

## Configuracion principal

La configuracion principal se encuentra en **apache/conf/httpd.conf** y contiene la configuracion global de apache.
Alguas de las directivas que contiene son:

### Directivas generales

* **ServerTokens** - Determina la info que se envia al browser sobre el servidor y sobre apache (version, etc)
* **ServerRoot** - La ubicacion en el filesystem donde esta instalado apache 
* **KeepAlive** - Permite mas de un request HTTP por cada conexion TCP
* **MaxKeepAliveRequests** - Cantidad maxima de requests HTTP por conexion TCP
* **KeepAliveTimeout** - elimina la conexion despues de N segundos de que no se realiza un request HTTP
* **L isten** - Indica a que socket TCP esta escuchando el servidor, puede especificar IP (socket especifico) o solamente puerto (socket generico)
	* listen: 111.111.111.111:80
	* Listen: 80
* **serverName** - Un nombre de dominio para este servidor, sirve para las redirecciones
* **useCanonicalName** - Si un usuario es redirigido a este server por un nombre de DNS diferente al server name, se redirige al nombre de dominio especificado en el server name
* **DocumentRoot** - Indica la carpeta publica root donde esta el contenido que el servidor puede entregar al cliente

### Worker directives
Son las directivas que le indican al worker de apache como tiene que spawnear los nuevos servidores y sus threads que procesan los http requests

>Este es un ejemplo de la configuracion para el MPM "worker", los MPM "prefork" y "event" tienen configuraciones acorde a como funcionan.

* **StartServers** - Cantidad de procesos servidor spawneados cuando apache inicia, cada proceso servidor puede spawnear threads
* **maxClients** - Cantidad maxima de clientes simultaneos
* **minSpareThreads** - Cantidad de threads que se mantienen en espera por si entran nuevas conexiones
* **maxSpareThreads** - Cantidad maxima de threads que puede haber en espera
*  **ThreadsPerChild** - Cantidad de threads que cada proceso servidor tiene.
* **maxRequestsPerChild** - cantidad maxima de requests que puede atender un proceso servidor


 
## Configuration sections

###  \<IfModule>

Permite activar una serie de directivas **solo si un modulo esta activo**, se usa mucho cuando tenes una funcion que es cumplida por modulos diferentes dependiendo de factores como:
*  sistema operativo donde este instalado apache
*    MPM activado.


### \<Directory >

Te permite aplicar directivas para ciertos directorios

    <

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY5MDgzMjMxNSwxODIyMDQwMjQ0LDUwNj
E2MzI0MywxMjIxMTM0OTQzLDE5Nzc1MzU3MDgsLTEwODg5NzYy
NDQsMzAwODE4OTU0LC00ODg4MTEwMDIsLTE2OTMyOTIxMDcsMz
I0MjI2OTMsOTMxMjMxOTM0XX0=
-->