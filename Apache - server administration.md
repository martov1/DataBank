
* DOCS: http://httpd.apache.org/docs/current/

CURSO
https://www.youtube.com/watch?v=gPOliFwMFCk&list=PLbjlI3cowd5-pvfO521ejRI1Q6abFkNQc

# Intro

## Conceptos basicos
* Apache esta armado de forma increiblemente modular, el CORE de apache es relativamente pequeño.

* Apache se configura principalmente mediante archivos de texto mediante _directivas_

* El proceso central de Apache se denomina **httpd** 

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

# Configuracion CORE

## Conceptos iniciales

Apache se configura colocando **_directivas_** en archivos de texto, las directivas pueden ser colocadas dentro de **_secciones_** que indican en que circunstancias la directiva tiene que tomar efecto

### Filesystem y URLs

Apache por default lee el contenido de la directiva **DocumentRoot**, (_que contiene la URL donde se supone que esten los documentos publicos para los usuarios_), a partir de ahi mapea las urls a los documentos presentes en el filesystem,

### Configuracion principal y sus directivas

La configuracion principal se encuentra en **apache/conf/httpd.conf** y contiene la configuracion global de apache. Estas configuraciones se aplican a la totalidad del servidor

>Apache solo lee el archivo de configuracion global al iniciarse, es necesario **reiniciar el servicio para actualizar la configuracion global** si esta se cambia

Alguas de las directivas que contiene por default son:


* **ServerTokens** - Determina la info que se envia al browser sobre el servidor y sobre apache (version, etc)
* **ServerRoot** - La ubicacion en el filesystem donde esta instalado apache 
* **KeepAlive** - Permite mas de un request HTTP por cada conexion TCP
* **MaxKeepAliveRequests** - Cantidad maxima de requests HTTP por conexion TCP
* **KeepAliveTimeout** - elimina la conexion despues de N segundos de que no se realiza un request HTTP
* **Listen** - Indica a que socket TCP esta escuchando el servidor, puede especificar
	*  IP (socket especifico) 
	* Puerto (socket generico)
	* Nada:  si no esta configurado escucha todos los puertos
	* Protocolo (http, https, etc)
	* EJ:
		* listen: 111.111.111.111:80
		* Listen: 80
		* Ausente: escucha TODOS los sockets
		* Listen 111.111.111.111:80 https
* **serverName** - Un nombre de dominio para este servidor, sirve para las redirecciones
* **useCanonicalName** - Si un usuario es redirigido a este server por un nombre de DNS diferente al server name, se redirige al nombre de dominio especificado en el server name
* **DocumentRoot** - Indica la carpeta publica root donde esta el contenido que el servidor puede entregar al cliente
* **ErrorLog** - Indica el path donde apache creara y mantendra el error log


### Directivas de MPM
Son las directivas que le indican al MPM  de apache como tiene que spawnear los nuevos servidores y sus threads que procesan los http requests

>Este es un ejemplo de la configuracion para el MPM "worker", los MPM "prefork" y "event" tienen configuraciones acorde a como funcionan.

* **StartServers** - Cantidad de procesos servidor spawneados cuando apache inicia, cada proceso servidor puede spawnear threads
* **maxClients** - Cantidad maxima de clientes simultaneos
* **minSpareThreads** - Cantidad de threads que se mantienen en espera por si entran nuevas conexiones
* **maxSpareThreads** - Cantidad maxima de threads que puede haber en espera
*  **ThreadsPerChild** - Cantidad de threads que cada proceso servidor tiene.
* **maxRequestsPerChild** - cantidad maxima de requests que puede atender un proceso servidor

## Archivos .htaccess

Los archivos **.htaccess**  te permiten tener una configuracion descentralizada del servidor.

* Pueden estar presentes en cualquier carpeta del directorio publico
* Son leidos en cada request
* Las directivas que contienen son efectivas en esa carpeta y todas las subcarpetas
* Pueden tomar precedencia de la configuracion global dependiendo de la directiva **AllowOverride**


>Los archivos .htaccess **pueden llamarse de cualquier manera** si se lo define usando la directiva **AccessFileName**

## Configuration sections

Las configuration sections te permiten coordinar cuando una directiva tiene que tomar efecto.

>**Las secciones pueden ser anidadas para lograr mas control**

### Secciones que usan RegEx

Muchas configuration sections pueden usar regex, ademas podes usar los selection groups dentro de la configuracion

    <DirectoryMatch  "^/var/www/combined/(?<SITENAME>[^/]+)">
     require ldap-group "cn=%{env:MATCH_SITENAME},ou=combined,o=Example"  
     </DirectoryMatch>

###  \<IfModule>

Permite activar una serie de directivas **solo si un modulo esta activo**, se usa mucho cuando tenes una funcion que es cumplida por modulos diferentes dependiendo de factores como:
*  sistema operativo donde este instalado apache
*    MPM activado.


### \<Directory >

Te permite aplicar directivas para ciertos directorios

Podes usar **Regex** con **Directorymatch**

    <directory /bla/bla/public>
    //Cosas que se aplican solo en esta carpeta
    </directory>
    
### \<Files >
Te permite aplicar directivas  todo archivo con un nombre especifico (en la carpeta y subcarpetas si esta en htaccess o en todo el server si esta en la configuracion global).

Podes usar **RegEx** con **FilesMatch**


    <Files  "private.html">
	    Require all denied
    </Files>
_Podes anidarla dentro de la directiva `<directory>` para mayor control._

### \<Location > 

Te permite aplicar directivas sobre una URL
Tambien podes usar **\<LocationMatch\>** para usar **RegEx** en el computo de la URL

    <Location  "/server-status">
      SetHandler server-status 
    </Location>
Con regex:

    <LocationMatch  "^/private">
      Require all denied 
      </LocationMatch>

### \<IfDefined >

Las directivas toman efecto solo si existe una variable (o parametro cuando apache se inicio en command line con `-DParametro`)

    <IfDefine  Variable>
    	 Redirect  "/"  "http://otherserver.example.com/"
    </IfDefine>
    
### \<IfVersion >
Las directivas toman efecto solo si la version de apache cumple con el requisito

    <IfVersion  >=  2.4>  
    \# Hacer cosas
    </IfVersion>

### \<If >
Las directivas toman efecto si se cumple una operacion booleana
Podes hacer pleno uso de las environment variables
EJ: si el referrer header es igual a un dominio en particular.


    <If  "!(%{HTTP_REFERER} -strmatch 'http://www.example.com/*')">  
    Require all denied 
    </If>

## Directivas


### Sintaxis

* **Orden:**
	* Una sola directiva por linea
	* **Indentacion:**
		*  Los **espacios en blanco** detras de la directiva son ignorados, asi que podes indentar las directivas
		* Las **lineas en blanco** son ignoradas 
* **argumentos:**
	* Se separan con un whitespace
	* Si el argumento tiene espacios, va entre comillas 
* **Case sensitivity**
	* Las directivas son **case insensitive** 
	* sus argumentos pueden ser **case sensitive**
* **Comments** 
	* Comienzan con **#** 
	* NO pueden compartir la linea con una directiva


### Lista de directivas varias

Las siguientes son las directivas propias de **CORE**, otros modulos tendran otras directivas.

* **Include** - Permite incluir otros archivos de configuracion al archivo de configuracion actual

		Include  /usr/local/apache2/conf/ssl.conf
* **Redirect** - Te permite redireccionar  una solicitud que va a un lugar del filesystem (cualquiera sea la URL)  hacia otra URL
	```
	Redirect permanent "/foo/"  "http://www.example.com/bar/"
	```
* **RedirectMatch** - Igual que redirect pero acepta RegEx
	```
	RedirectMatch permanent "^/$"  "http://www.example.com/startpage.html"
	```
* **Alias** - Te permite mapear URLs a carpetas que no estan en la carpeta publica del server
	```
	Alias  "/docs"  "/var/web"
	```
* **AliasMatch** - Igual que alias pero soporta RegEx
	```
	AliasMatch  "^/upages/([a-zA-Z0-9]+)(/(.*))?$"  "/home/$1/public_html/$3"
	```
* **DirectoryIndex** - Marca el archivo que sera cargado si la URL no especifica un archivo en el directorio (por default index.html)
* **ErrorDocument** - Te permite especificar la pagina a donde va si apache devuelve un error HTTP CODE 404

* **AllowSymlinks** - Apache seguira los symlinks como si fueran archivos reales
* **AllowOverride** - Indica si deben ser cargados los archivos .htaccess presentes en un directorio (debe estar dentro del section `<Directory>`)
## Variables

### Locales
Podes **definir una variable** con la directiva Define
	
	Define nombreDeVariable Valor

Podes **tomar decisiones** si una variable esta definida:

    <IfDefine TEST> 
     Define servername test.example.com
     </IfDefine>

Podes **usar una variable** en la configuracion usando la sintaxis ${Variable}

    DocumentRoot  "/var/www/${miVariable}/htdocs"

### Environment variables del SO

Apache puede leer las variables de la consola con la directiva `PassEnv`

	PassEnv LD_LIBRARY_PATH

### Envoronment variables locales

Podes **setear** una variable de environment para apache y todos sus modulos asi:

	SetEnv SPECIAL_PATH /foo/bin

Podes **quitar** una variable de environment interna asi

    UnsetEnv LD_LIBRARY_PATH


## Virtual hosts

Los virtual hosts te permiten tener multiples sitios en un solo servidor, apache decide en base al nombre de dominio solicitado que archivo servir.

Definis el virtual host con una Ip o un nombre de dominio en la section 

```
<VirtualHost miDominio:miPuerto>
  ServerAdmin webmaster@host.example.com 
  DocumentRoot  "/www/docs/host.example.com"  
  ServerName host.example.com 
  ErrorLog  "logs/host.example.com-error_log"  
  TransferLog  "logs/host.example.com-access_log"
</virtualHost>
```



## Logging

Apache tiene la capacidad de loguear un monton de cosas
Es importante **no colocar los logs en lugares accesibles por los usuarios** para evitar problemas de seguridad (logs sensibles, inyeccion de codigo en el log,etc)


Algunas directivas que afectan el logging: 
* **ErrorLog** - Indica la ubicacion del log de errores
* **ErrorLogFormat** - Te permite modificar el formato de lo que se loguea
* **LogLevel** - Te permite establecer niveles (info, warning, error) a los logs de modulos especificos

### Access log

El access log loguea todos los request procesados por el server, su ubicacion y contenido es controlado por la directiva **CustomLog** mientras que su formato es controlado por **LogFormat**

**EJ:** especificas el formato "miFormato"  y lo usas para loguear el acceso, el log se guarda en logs/access_log

    LogFormat  "%h %l %u %t \"%r\" %>s %b" miFormato 
    CustomLog logs/access_log miFormato

>Si especificas muchos **CustomLog** diferentes, creas multiples logs que pueden tener diferentes formatos

#### Logging en virtual host

Si las directivas se colocan dentro de la section \<virtualHost\> entonces se guardara solo el log respectivo a ese virtual host en el archivo declarado en ese **CustomLog**

## Modulo  Mod_rewrite

El modulo mod_rewrite permite utilizar regular expressions para parsear una URL y redirigirla a otra URL, un PATH del file system o un proxi interno. el parsing se realiza en cada nuevo HTTP request.

Mod_rewrite permite tener una cantidad ilimitada de reglas y cada regla puede tener una cantidad ilimitada de condiciones que pueden estar basadas en **variables del server, de environment, HTTP headers o time stamps**

### Logging
Podes loguear las acciones de Mod_rewrite asi 

	LogLevel alert rewrite:trace3
>Los log levels van desde trace0 a trace9, no uses para produccion nada mayor a trace2 por que va a ralentizar el server
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzMDAyMTI5MCwxNTQ5MTA0MTYxLDE1OD
U4MzU2NzQsMTI3OTQ2MzY4NywtMjI2NjI0MDYwLC0yMDc2MTQ2
OTQsLTg3NTc4MzMxNiwyODg2OTQ4ODIsMTM5NTAwODYyMCwtOT
U4NzM1OTczLC0xODc4Mjg0NTM5LDE5NDg2OTA2ODEsLTc4NzUw
ODU1NywxODEwOTI4MTc4LDQ2NDg4NjM3NywxODI2MjE2OTkxLC
04NDc0NDIyMTksOTg0NDAzMDI4LDExOTk1Nzc1OTEsMTY5NjYx
NjY0M119
-->