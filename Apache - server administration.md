
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

Prefork es la arquitectura mas antigua y menos eficiente, 


### Worker MPM



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

### Worker directives
Son las directivas que le indican al worker de apache como tiene que spawnear los nuevos servidores y sus threads que procesan los http requests



* **StartServers** - Cantidad de procesos servidor spawneados cuando apache inicia, cada proceso servidor puede spawnear threads
* **maxClients** - Cantidad maxima de clientes simultaneos
* **minSpareThreads** - Cantidad de threads que se mantienen en espera por si entran nuevas conexiones
* **maxSpareThreads** - Cantidad maxima de threads que puede haber en espera
*  **ThreadsPerChild** - Cantidad de threads que cada proceso servidor tiene.
* **maxRequestsPerChild** - cantidad maxima de requests que puede atender un proceso servidor


 
## Configuration sections

###  \<IfModule>

Permite activar una serie de directivas **solo si un modulo esta activo**, se usa mucho cuando tenes una funcion que es cumplida por modulos diferentes dependiendo del sistema operativo donde este instalado apache.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA5NDkyMzU5MywzMjQyMjY5Myw5MzEyMz
E5MzRdfQ==
-->