


# contenido

* Arquitectura de las RFC
* URI
* Basics de HTTP
* representation y representation metadata
* HEADERS
	* Algunos headers
	* Headers de requests 
	* Headers de response
* HTTP methods
	* Que y cuales son
	* Safe methods
	* Idempotent Methods
	* Definicion de metodos
		* GET
		* POST
		* PUT
		* DELETE
		* CONNECT
		* OPTIONS
* Status Codes 
* Chunks y streaming
* Asociacion entre request y response
* Manejo de conexiones
* Content negotiation
	* Desde el cliente
	* Respuesta del server
	* MIME types
* Conditional requests
	* Validators 
	* Headers para conditional requests
* Range request
	*  Solicitud del cliente
		* Range unit 
		* Accept-ranges
	* Respuesta del servidor
* Caching
	*  Viabilidad de cacheo de una respuesta
	*  header fields que se usan para el cacheo
* Autenticacion
	* Funcinamiento general
		* Generalidades
		* Codigos de respuesta
		*  Headers
	* Bearer token (Oauth rfc6750)
		* funcionamiento desde el cliente
		* respuesta del server
		* Consideraciones de seguridad



# Arquitectura de las RFC


  * RFC 7230, HTTP/1.1: Message Syntax and Routing 			**LISTO**
  * RFC 7231, HTTP/1.1: Semantics and Content			**LISTO**
  * RFC 7232, HTTP/1.1: Conditional Requests	**LISTO**
  * RFC 7233, HTTP/1.1: Range Requests			**LISTO**
  * RFC 7234, HTTP/1.1: Caching						**LISTO**
  * RFC 7235, HTTP/1.1: Authentication				**NO EMPEZADO**
  * RFC 7540, HTTP 2						**NO EMPEZADO**




# URI

las  Uniform Resource Identifiers (URIs) [RFC3986] son usadas por HTTP para identificar recursos

Sintaxis:

````
"protocol:" "//" authority path-abempty [ "?" query ] [ "#" fragment ] 
````

donde:
* **protocol** - indica el uso de HTTP o HTTPS u otro (ftp etc)
* **authority** - es un host identifier y opcionalmente un puerto TCP, indica quien tiene la autoridad de responder a este mensaje, basado en TCP
* **path-abempty** -  Es un path, ya sea **ab**soluto o **empty**, indica un target resource
* **query** - opciona, asiste en indicar un target resource
* **fragment** - opcional, asiste en indicar un resource secundario 



# Basics de HTTP

El objetivo del protocolo HTTP es acceder a un **recurso**, para ubicar el recurso se utiliza una **URI**,

El mensaje HTTP esta dividido en un **header** y un **message**, el header se procesa primero y **dependiendo de lo que este indique se ignorara o se leera el message**

Toda conexion comienza con una solicitud del cliente que contiene:

**Header:**
* Metodo (GET, POST)
* URI
* Version del protocolo (HTTP 1.1)
* Headers
* Client information
* Representation metadata

**Linea en blanco para representar fin del header**

**Message:**
* Payload body

Ejemplo: 
![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/2016-02-09_05-59-06.png)
El server responde con lo mismo, pero ademas añade un **success o error code** en el header

Client request:

     GET /hello.txt HTTP/1.1
     User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
     Host: www.example.com
     Accept-Language: en, mi


   Server response:

     HTTP/1.1 200 OK
     Date: Mon, 27 Jul 2009 12:28:53 GMT
     Server: Apache
     Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
     ETag: "34aa387-d-1568eb00"
     Accept-Ranges: bytes
     Content-Length: 51
     Vary: Accept-Encoding
     Content-Type: text/plain

     Hello World! My payload includes a trailing CRLF.



# Representation y Representation Metadata


## Que son

**Representation:**

>el **estado actual o deseado de nuestro recurso**, es decir:
>* Si haces un **get** la representacion es lo que obtenes, que **simboliza el estado del recurso en el server**
>* Si hacers un **post** la representacion es lo que deseas, **simboliza el estado futuro del recurso en el server**
>* Basicamente es **lo que sea que este en el body**

* **Representation metadata** - son headers que ayudan al cliente a interpretar la representacion que obtiene del server  


## Representation metadata

Permite que el cliente sepa como interpretar la representacion que se le envia.

Consiste en los siguientes **Headers**

* ** Content-Type** - Indica el tipo de contenido. ej `text/html;charset=utf-8`
* **Content-Encoding** - Indica si hay encoding, por ejemplo compresion gzip
* **Content-Language** - Indica el lenguaje del usuario (mi, en, da)
* **Content-Location**
  
# Headers

## Algunos headers

### Transfer-Encoding

indica como esta encodeado el mensaje
````
//El payload esta comprimido!
Transfer-Encoding: gzip, chunked
````

El encoding provee la informacion necesaria para indicarle al cliente cuando termina el mensaje, entonces no hace falta colocar un **Content-Length**

### Content-Length

Cuando no tenes un **transfer-encoding**, el campo **content-length** puede anticipar eltamaño del mensaje, en la implementacion se usa para saber cuando termina el mensaje.

### Location 

Le indica al navegador que debe redireccionarse a esa ubicacion
````
location: www.redirigirAca.com
````


## Headers de requests

* **Expect** - indica al servidor que necesita tener soporte de algo para comprender el mensaje. No hay mayores especificaciones.
* **Conditionals** - permite al cliente especificar alguna condicion en el estado del recurso - mas info en **RFC7232**
* **Accept** - indica al server que tipo de media-type son aceptables como respuesta
* **Accept-Encoding** - indica al server que encodings son aceptables
* **Accept-Language** - indica al server que lenguajes humanos son aceptables
* **Authorization** - contiene credenciales de autenticacion
* **From** - sirve para enviar una direccion de correo electronico
* **Referere** - URI desde la que se fue redigirigo a este recurso
* **User-Agent** - Informacion del user agent, como el browser
* **Host:** - indica el dominio, sirve para que el server diferencie entre varios dominios que dirigen a una misma IP
* **via** - indica en forma de lista los protocolos usados por cada proxy para retransmitir el mensaje hasta el cliente, y los proxys que lo hicieron
* **connection** - le indica al servidor si deberia cerrar la conexion TCP
* **upgrade** - sirve para transicionar a otro protocolo, en la practica HTTP 2
* **range** - especifica que partes del recurso se estan solicitando,generalmente una cantidad de bytes, ver range request


## Headers de response

* **Date** - fecha y hora en la que se origino el mensaje
*  **location** - se usa para especificar una ubicacion
	*  **en codigo 201 (created)** - especifica la ubicacion del nuevo recurso
	*  **en codigo 3xx (redireccion)** - especifica hacia donde redireccionar
* **Retry-After** - indica cuanto tiene que esperar el cliente antes de reintentar
* **Allow** - Lista los verbos HTTP validos para este endpoint
* **Server** - provee informacion del software del server
* **via** - indica en forma de lista los protocolos usados por cada proxy para retransmitir el mensaje hasta el cliente y los proxys que lo hicieron 
* **Accept-Ranges** - el servidor indica que acepta range requests y en que unidad. ver range requests
* **Content-Range** - Indica el sector de la representacion que se esta enviando. ver range requests
* **last-modified** - Indica cuando fue modificado por ultima vez esta representacion, sirve para flushear caches
* **ETag** - Provee de un numero que cambia cuando la representacion es modificada, suplementa o reemplaza a last-modified
* ** Content-Type** - Indica el tipo de contenido. ej `text/html;charset=utf-8`
* **Content-Encoding** - Indica si hay encoding, por ejemplo compresion gzip
* **Content-Language** - Indica el lenguaje del usuario (mi, en, da)
* **Content-Location**
* **WWW-Authenticate** - El servidor esta indicando que tenes que autenticarte, en este header se indica que sistema de autenticacion se espera (token, basic, etc)



# HTTP methods

### Que y cuales son
Los metodos HTTP indican **que se desea hacer con el representation**

* **GET** - Transferir una representacion actual del recurso
* **HEAD** - Igual que GET, pero solo transfiere el status y el header
* **POST** - Realizar un procesamiento sobre el payload enviado
* **PUT** - Reemplazar la representacion del resource con lo que se envia en el payload
* **DELETE** - Remover la representacion del resource
* **CONNECT**
* **OPTIONS**
* **TRACE**


### Safe methods

Los methods se consideran **safe** si su semantica admite unicamente la **lectura de recursos y no la escritura**. Estos son los metodos que pueden usar los web crawlers por ejemplo

Son:
* GET
* HEAD
* OPTIONS
* TRACE

### Idempotent Methods

Son metodos que se pueden repetir sin temor de generar un resultado diferente al deseado.pueden repetirse automaticamente en caso de fallo sin temor a generar resultados no deseados

son:
* PUT
* DELETE
* TODOS LOS SAFE METHODS

## Definicion de metodos

### Get

Sirve principalmente para **obtener informacion** del estado de ese recurso.
El **payload **  para get **no esta definido** y no deberia usarse.

### HEAD

Es identico a GET, solo que **el server no debe responder con un message body**
El **payload **  para HEAD **no esta definido** y no deberia usarse.

### POST

Sirve para **enviar informacion al recurso para su procesamiento**, muchas veces se usa para **Crear representaciones de un recurso en el servidor**, por ejemplo crear un post nuevo en un foro, que da como el nuevo recurso `www.sitio.com/numer-de-post`, por ese motivo a veces queres **redireccionar al usuario al nuevo recurso usando tu respuesta HTTP**


* **Se han creado recursos ó representaciones** como resultado del post (un post de un blog por ej):
	* El server debe enviar un **codigo 202 created**
	* El server puede **redireccionar al navegador al nuevo recurso** mediante un **location header**
* Si el recurso que se intento crear **ya existe**
	* El server puede **rediracciona el navegador** al recurso ya existente con un **codigo 303** y un **Location header**


### PUT

Sirve para **crear o reemplazar totalmente el estado de un recurso** con el **payload suministrado**

>**Notese que PUT  es INDEPODENT, si lo llamas 6 veces tiene que hacer el mismo resultado, a diferencia de POST. esa es la diferencia principal**

* **exito al REEMPLAZAR** -> el server debe **devolver codigo 200 OK**
* **Exito al CREAR** -> El server debe **devolver codigo 201 created**
* **Error**
	* **El payload no es adecuado** -> responder con **409 conflict ó 415 unsupported media type** 	

### DELETE

Sirve para **Eliminar un recurso**
El **payload **  para get **no esta definido** y no deberia usarse.


* **Exito al BORRAR** -> el server debe:
	*  **devolver codigo 202 accepted** - si la accion probablemente sea realizada en el futuro cercano
	*  **Devolver codigo 204 no content** - si la accion se realizo y no hace falta devolver ninguna informacion
	*  **Devolver codigo 200 OK** - si la accion se realizo y hace falta devolver informacion para describir el estado actual

### CONNECT

Se utiliza unicamente para **realizar solicitudes a un proxy**, no suele estar implementado en servidores normales.

Genera un **tunel**, las solicitudes al servidor final quedan encapsuladas en una burbuja de HTTP enviada al proxi, el cual remueve el encapsulamiento y reenvia la solicitud al servidor de destino.

### OPTIONS

Se utiliza para **preguntar las capacidades de un resource** mediante **algun payload**
Se utiliza normalmente en el protocolo CORS


# Status codes

A groso modo, los **Status codes** se separan por el primer digito

* **1xx** - **Informativo** - la solicitud fue recibida, el proceso continua
* **2xx** - **exito** - la solicitud fue aceptada, recibida, comprendida
* **3xx** - **Redireccion** - Hacen falta otras cosas para completar el request
* **4xx** - **Error del cliente** - Hay un prolema con la solicitud o no se puede cumplir
* **5xx** - **Error del server** - hay un problema con el server o la solicitud


# Chunks y streaming


HTTP permite transferir cosas en partes o chunks, permite transferir cosas de tamaña indefnido.

Podes definir que vas a usar chunks/streaming si:
* Si colocas `Transfer-Encoding: chunked`
* si omitis `Content-Length` los servers suelen agreChunks y streaminggar `Transfer-Encoding: chunked` solos

Los mensajes se envian en una sola respuesta HTTP cuyo contenido esta dividido en partes separadas por /r/n y el numero de octetos que tiene el chunk.

**Aclaraciones** 
* El protocolo de la **capa inferior**, por ejemplo **TCP**, se encargara de dividir la respuesta en **paquetes mas pequeños** y enviarlos a lo largo del tiempo
* desde el punto de vista de **HTTP** es **una sola respuesta muy larga**.



# Asociacion entre request y response

HTTP no contempla como asociar entre un request y un response, por ende se asume que **el response mas cercano al request es el que corresponde**, eso implica que puede haber dos implementaciones:

* Que el cliente no haga requests HTTP en paralelo al mismo destino
* Que el server  devuelva las multiples requests en orden inverso (PIPELINING) 
* Que se hagan multiples requests HTTP paralelas en conexiones paralelas, usando el algotirmo de la capa inferior para diferenciarlas (TCP)


# Manejo de conexiones

HTTP no es responsable de mantener las conexiones, esto es trabajo del protocolo inmediatamente abajo (generalmente TCP) pero puede informarle al server sobre si seria conveniente dejar la conexion abierta o cerrarla. **es estandar dejarla abierta** y dejar que TCP decida cuando cerrarla.

Podes indicarle esto al server mediante

````
connection:keep-alive

connection: close

````



# Content negotiation

Un recurso puede tener varias representaciones en varios formatos (JPG, PDF, HTML, etc), el cliente y servidor pueden comunicarse para saber **que formatos hay disponibles o son aceptables**. tambien se usa para solicitar contenido en **determinado lenguaje**

**La negociacion se realiza a traves de headers. **

### Desde el cliente


> #### Sintaxis:
>Podes **listar varios** types, charsets o encodings y otorgarles una **prioridad**.
>
>* Para indicar **multiples**, separalos con **coma**
>* Para indicar "**todos** los posibles", usa **`*/*`**
>* Para indicar **prioridad**, usas **Q-value** (mas alto es mas prioritario) despues de la representacion separandolo con un punto y coma. 
por ejemplo `application/xml;q=0.9, */*;q=0.8`. indica mas prioridad para **application/xml** y menos prioridad para **todos los otros** types


* **Accept** - Este header es usado por el cliente para indicarle al server que representaciones son aceptables. **utiliza MIME types y subtypes**. 
````
 Accept: text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8
````
* **Accept-Charset** - Permite indicar al cliente que charsets son aceptables
* **Accept-Encoding** - Permite al cliente indicar que encodings son validos (gzip, chunk, compress,`*` )
````
  Accept-Encoding: gzip;q=1.0, identity; q=0.5, *;q=0
````
* **Accept-Language** - Permite al cliente indicar el idioma preferido
````
 Accept-Language: da, en-gb;q=0.8, en;q=0.7
````


### Respuesta del server

Si el server:
* **No puede honrar la peticion** - code **406 not acceptable**
* **Puede honrar la peticion** - code **200 OK**

### MIME types

Los types estan predefinidos y **dependiendo del type de una respuesta el cliente sabe como reaccionar** (Mostrar un PDF, descargar un archivo, ver un sitio HTML, ejecutar JS, etc)

Por ejemplo, los tags <video src="URLdelrecurso"> o <img src="URLdelrecurso"> pueden **no funcionar** si el **servidor HTTP no devuelve el type correcto** cuando se hace la solicitud a la url del recurso

**Algunos de los types son**

* Datos de **Forms**
	* **application/x-www-form-urlencoded** - los form controls son agregados en orden de aparicion, todo se encodea de forma rudimentaria
	* **multipart/form-data**  - Mas eficiente para enviar datos binarios
* Otros
	* text/plain
	* text/html
	* image/jpeg
	* image/png
	* audio/mpeg
	* audio/ogg
	* audio/*
	* video/mp4
	* application/octet-stream 

---

# Conditional requests

Son solicitudes condicionales que puede hacer HTTTP basandose en la **fecha de la ultima modificacion** de la representacion o de un identificador **Etag**


Muchas de estas condiciones se usan para **permitir un cacheo eficiente de los datos**

### Validators

Los validators se usan para poder identificar y comparar el estado actual de la representacion del servidor con el estado actual de la representacion del cliente.

El servidor muchas veces utilizara esto para saber cual es la representacion que posee el cliente y compararla con la mas actual.

Hay dos headers que se usan con este proposito cuando el servidor contesta un request

* **Last-Modified** - La fecha de la ultima modificacion de la representacion del servidor
* **ETag** - Entity tag, indica un identificador unico que cambia cuando la representacion del servidor cambia.


## Headers para conditional requests

### If-match

Le pide al servidor que:

* devuelva la representacion con un **Etag** particular
* modifique la representacion del servidor en caso de que el **Etag** sea el actual, caso contrario no lo modifica

EJ de uso: se suele usar cuando un recurso puede ser editado por muchas personas en paralelo., si el **Etag** de lo que se desea modificar no es el mas nuevo significa que el usuario esta tratando de modificar un documento que ya fue modificado entre que lo solicito y lo edito
````
If-Match: "xyzzy"
````

Si la condicion evalua como falsa entonces:
* Responder con **code 412 precondition failed**

### If-None-Match

Al reverz de If-Match, la request se procesa solo si no hay una representacion con un **Etag** en paricular.
Tambien se puede usar con un asterisco para indicar que solo se debe procesar el request **si no hay representaciones** en el recurso.

Si el request es **GET o HEAD**
	* Respuesta **code 304 not modified** - 
Si es otro request
	* respuesta **code 412 precondition failed**

### If-Modified-Since

Solo se usa con **GET o HEAD**

Responder con **code 304 not modified** si la fecha de modificacion del recurso es igual o anterior a la de este campo. caso contrario porcesar el request.

### If-Unmodified-Since

Inverso al If-Modified-Since.

Se utiliza para evitar que cuando hay varios usuarios modificando el mismo recurso, estos se pisen sin saberlo.


### If-Range

Se usa cuando haces un HTTP range request
Utiliza un **Etag** o **modification date** como valor, si el cliente esta haciendo range requests pero el **validador cambia durante los range requests** entonces el server envia la representacion entera otra vez. 


# Range request

Es una **implementacion opcional de HTTP** que permite solicitar y recibir parte de una representacion en condiciones en las que no se desea la totalidad de la representacion.

Ademas permite al cliente realizar varias solicitudes HTTP para obtener una representacion en varios pedazos, esto permite **descargas reanudables y pausables**.


### Solicitud del cliente
Por ejemplo: **pedir una parte de un gran documento, pedir solo las dimensiones de una imagen y no su contenido**, permitir una **descarga larga reanudable**. para eso se utiliza el header **range** donde:

* **unit** es la unidad utilizada 
* **range start** es desde donde se solicita el documento
* **range end** es hasta donde se solicita el documento
* **se pueden repetir mas secciones**

````
Range: <unit>=<range-start>-<range-end>
````

Ejemplo:
````
//se solicitan varios rangos
Range: bytes=200-1000, 2000-6576, 19000-
````


### Range unit

Dependiendo de el tipo de representacion (texto, imagen, audio) sera particionada usando unidades distintas, el tipo de unidades aceptadas sera indicado por el cliente con el header **range-unit**. sus valores pueden ser:

* **bytes** - La cantidad de bytes que se desean de la representacion

### Accept-ranges

Es un header que le permite al server especificar que soporta range requests para ese resource y en que unidad
````
Accept-Ranges: bytes
````

### Respuesta del servidor


* **EXITO, se solicito un solo rango** 
	* CODIGO **206 partial content** indicando que el server logro cumplir
	* header **Content-Range** indicando que parte de la representacion se esta enviando
* **EXITO, se solicitan varios rangos** 
	* CODIGO **206 partial content** 
	* el **media-type** sera **multipart/byteranges**
	* En el **payload** cada rango esta acompañado de un parametro  **Content-Type **y **Content-Range**
* **FALLO - el rango excede al recurso**
	* **codigo 416 range not satisfiable** - el rango solicita partes que no existen
	* tal vez devuelva todo el recurso y responda con **200 ok**


Ejemplo de respuesta ante solicitud de varios rangos

````
  HTTP/1.1 206 Partial Content
     Date: Tue, 14 Nov 1995 06:25:24 GMT
     Last-Modified: Tue, 14 July 04:58:08 GMT
     Content-Length: 2331785
     Content-Type: multipart/byteranges; boundary=THIS_STRING_SEPARATES

     --THIS_STRING_SEPARATES
     Content-Type: video/example
     Content-Range: exampleunit 1.2-4.3/25

     ...the first range...
     --THIS_STRING_SEPARATES
     Content-Type: video/example
     Content-Range: exampleunit 11.2-14.3/25

     ...the second range
     --THIS_STRING_SEPARATES--
````

---

# Caching


En general los caches almacenan solo los requests **GET** y usan como identificador el **URI**. tambien podria tener un identificador secundario con los valores requeridos para el **content negotiation**. de esta forma si el recurso tiene varias representaciones entonces el cache puede proveer la que es adecuada.

### Seguridad

Un cache no debe guardar respuestas con:

* **Authorize** - el header-field lleva una credencial, no debe cachearse esta respuesta.


## Viabilidad de cacheo de una respuesta

Las respuestas son viables de cacheo si:

* **no hay un headers que lo impidan** - cache-control, authorize, etc
* **Es fresca** - no a pasado su tiempo de expiracion
* **Puede refrescarse** - la respuesta no ha cambiado
* **El server de origen no responde** - Se envia la ultima respuesta del server y se debe avisar al cliente con **code 1xx**


### Freshness
Es una respuesta que no ha pasado su **tiempo de expiracion**, esta no necesita ser validada para ser usada como buena.

* El **Tiempo de expiracion** es indicado por el servidor original mediante el header **Expires**
* Si el servidor original **no indica una expiracion** el intermediario cache puede **adivinar uno con heuristica**


````
Expires: Wed, 21 Oct 2015 07:28:00 GMT
````



### Age

El campo **age** sire para que el cache pueda indicarle al cliente cuanto tiempo hace que fue cacheada la respuesta que esta recibiendo.

### Refreshing o revalidation

El cache puede **Refrescar** una respuesta si el servidor contesta con un **Code 304 not modified** usando un nuevo validador si fuera necesario.

### Invalidacion

Cuando se envia un **non-safe request (POST, PUT..)** a una **URI**, lo mas probable es que la representacion del server cambie, entonces el cache debera invalidar lo que tenga cacheado de ese recurso e intentar refrescarlo.


## header fields que se usan para el cacheo :

### De ambos:
* **cache-control** - Permite al server o cliente especificar como desea que sea cacheada esa request o response, o si no desea que sea cacheada.
	* **no-cache** - indica que este mensaje no debe ser cacheado
	* **no-store** - indica que este mensaje y su respuesta no deben ser cacheados


### Del server ó cache:

* **Age** - indica cuanto tiempo paso desde que se valido esa respuesta, su preencia implica que la respuesta salio de un cache y no del server original (en segundos)
* **Max-age** - indica que la respuesta debe expirar despues de esta cantidad de segundos
* **s-maxage** - Indica que si la respuesta esta guardada en un cache publico debe expirar despues de esta cantidad de segundos.
* **Expires** - Indica cuando debe expirar la respuesta, o sea no ser considerada fresca. **Max-age y s-maxage toman presedencia sobre esto**
* **cache-control** - Permite al server o cliente especificar como desea que sea cacheada esa request o response, o si no desea que sea cacheada.
	* **Must-revalidate** - Le indica al cache que cuando la respuesta no sea fresh no la utilice, incluso si el servidor original queda offline, en lugar de eso debe responder con **CODE 504 gateway timeout**
	* **Public** - indica que esta respuesta se puede cachear publicamente aunque normalmente el cache sea privado.
	* **Private** - Indica que esta respuesta solo puede ser cacheada para este usuario en particular y no debe ser compartida con otros.

### Del cliente
* **max-age** - El cliente no aceptara respuestas con un age mayor a este valor en segundos.
* **max-stale** - el cliente esta dispuesto a aceptar una respuesta no fresca que haya excedido su frescura en esta cantidad de segundos
* **min-fresh** - el cliente quiere una respuesta que aun sera fresca cuando pasen la cantidad de segundos especificada en este campo
* **cache-control** - Permite al server o cliente especificar como desea que sea cacheada esa request o response, o si no desea que sea cacheada.
	* **only-if-cached** - Indica que el cliente desea una respuesta que venga de un cache y no del server



---
# Authentication

## Funcinamiento general

### Generaliades

> Recorda que HTTP es stateless, **entonces vas a tener que transferir tus credenciales, un token o algo en todas tus requests**. 
* Si envias **tokens que caducan**es mas dificil que alguien los pueda robar y usar. 
* Si la **comunicacion no esta encriptada** con algun otro protocolo encima de HTTP entonces todas las **credenciales van en plain text**

	
>**HTTP** solamente indica **como transferir los datos de autenticacion**, pero hay muchas formas de usarlo para autenticarse y estas no estan descriptas por HTTP (Oauth, basic, etc.)

Cuando el cliente intenta acceder a un recurso protegido:
* El cliente solicita acceso a un recurso sin enviar credenciales.
* El server debe hacerte un challenge usando un **Code 401 unauthorized**, enviando tambien un header **www-authenticate** conteniendo un challange.
* El Cliente debe responder con al respuesta del challenge en un header **authorization**
	* El server responde con **200 OK** y devuelve lo solicitado
	* El server responde con **401 unautorized** si las credenciales estan mal
	* el server responde con **403 forbidden** si esas credenciales no dan acceso a ese recurso en particular.

### Codigos de respuesta

El funcionamiento elemental de las respuestas del server es el siguiente

* **401 unauthorized** - no hay credenciales validas para usar este recurso
	* **www-Authenticate** debe ser enviado como field en la respuesta indicando que estrategia de autenticacion se utiliza (**token, basic, etc**) 
* **407 proxy authentication** - igual que 401 pero para proxys

### Headers

* **WWW-Authenticate** - El server responde con esto si el cliente no pudo autenticarse correctamente o no dio credenciales, el campo indica las estrategias de autenticacion que son aceptadas por el server (token, basic, etc)
* **Proxy-Authenticate** - Identico a WWW-Authenticate, pero para proxys
* **Authorization** - El cliente envia credenciales en este campo en cada solicitud para poder acceder a una respuesta protegida

## Bearer token (Oauth rfc6750, rfc6749)

**Descripcion de Oauth**: rfc6749
**Uso con HTTP**: rfc6750

> **Esta seccion describe la forma correcta de transferir tokens** de un cliente a
> un server y viceversa, asi como los campos esperados en los paquetes HTTP
> **no describe como funciona la autenticacion de tokens en el servidor o que contienen**
> 


### funcionamiento desde el cliente
La autenticacion con tokens funciona de la siguiente forma

* El cliente envia usuario y contraseña **una vez**
* El server envia un **token** con una fecha de **expiracion**
* El cliente se **acredita usando el token** en las futuras requests
* El token **expira** y el cliente debe renovarlo, enviando alguna de las siguientes:
	* **Token de renovacion** que tiene una expiracion mas larga 
	* **usuario y contraseña** nuevamente


Hay 3 formas de enviar el token:

1) en el **http request header** llamado **authorization** usando el prefijo **Bearer**
````
 GET /resource HTTP/1.1
 Host: server.example.com 
 Authorization: Bearer mF_9.B5f-4.1JqM
````

2) en el **request body**, usando 
* **Content-Type: application/x-www-form-urlencoded**
* usar el parametro **access_token** con el token
* no usar **get** ya que no tiene body

````
 POST /resource HTTP/1.1 
 Host: server.example.com 
 Content-Type: application/x-www-form-urlencoded 
 
 access_token=mF_9.B5f-4.1JqM
````

3) URI query parameter
* es **insegura de usar**, ya que la URI podria ser logueada por alguien en el medio
* Usa **GET**

````
 GET /resource?access_token=mF_9.B5f-4.1JqM HTTP/1.1 
 Host: server.example.com
````

### respuesta del server

#### Fallo
* Si se intenta acceder a un recurso sin autenticacion o el token es insuficiente, el server debe responde con **WWW-Authenticate Response Header Field**
````
 HTTP/1.1 401 Unauthorized Autenticacion
 WWW-Authenticate: Bearer
````
* Si se envio un access token pero no se pudo autenticar, el server debe enviar un **error attribute** explicando porque
````
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer ,
				  error="invalid_token",
				  error_description="The access token expired"
````
* El server puede enviar alguno de los sigueintes status codes: **400, 401, 403, or 405**

#### Exito

````
    HTTP/1.1 200 OK
     Content-Type: application/json;charset=UTF-8
     Cache-Control: no-store
     Pragma: no-cache

     {
       "access_token":"mF_9.B5f-4.1JqM",
       "token_type":"Bearer",
       "expires_in":3600,
       "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA"
     }
````

### Consideraciones de seguridad

* no guardar el token en cookies para evitar leaks
* Los tokens deben expirar rapidamente (implmentado desde el server)
* No transmitir token en la URI
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUzMjg5NTkxNl19
-->