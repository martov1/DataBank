

URI rfc
https://tools.ietf.org/html/rfc3986

Clarificacion (?
https://tools.ietf.org/html/rfc3305




# URL

[Uniform Resource Locator RFC 1738 - 1994](http://www.rfcreader.com/# rfc1738)

**Uniform Resource Identifier:** Describe la sintaxis y semantica de un string que representa un recurso accesible a la internet. Son usadas para **Localizar recursos**.

## Encoding

Cada caracter de la URL (Que consiste en un byte, osea un octeto) se puede representar con:

* Los caracteres US-ASCII
* Un simbolo **%** seguido de **dos valores exadecimales** (0123456789ABCDEF) Cuando:
	* El simbolo no este en US-ASCII
	* No sea seguro usar el simbolo
		* Espacios pueden ser agregados o quitados por word processors
		* **#** se usa como fragment/anchor y no debe transmitirse
		* **%** se usa para encodear
		* etc
	* El simbolo esta reservado
		*   **";", "/", "?", ":", "@", "=" and "&"** ya se usan como delimitadores de URL, si la URL en si misma los usa entonces deben estar encodeados.



## Estructura


La estructura de la URL es la siguiente
```
<scheme>:<scheme-specific-part>
```

### Scheme

Indica el protocolo utilizado

Donde **scheme:**
  * **ftp** -    File Transfer protocol
  * **http** -    Hypertext Transfer Protocol
  * **gopher** -    The Gopher protocol
  * **mailto** -    Electronic mail address
  * **news** -    USENET news
  * **nntp** -    USENET news using NNTP access
  * **telnet** -    Reference to interactive sessions
  * **wais** -    Wide Area Information Servers
  * **file** -    Host-specific file names
  * **prospero** -    Prospero Directory Service

### Scheme-Specific-Part

Depende del protocolo a utilizar, pero **todos los protocolos que hacen 
uso del protocolo IP usan una sintaxis comun**

**Sintaxis:**
```
//<user>:<password>@<host>:<port>/<url-path>
```

**DONDE:**
* **//** implica que esta **url es compliant con esta sintaxis comun**
* **Los sigueintes podrian ser EXCLUIDOS**:
	* **"<user>:<password>@"** - Indica que no hay usuari y pas
	* **":<password>"** - Indica contraseña como empty string
	* **":<port>"**	- Indica que el port es default para ese scheme
	*  **"/<url-path>"** - Indica usar un path default
* **@** Implica que **un usuario y contraseña fueron decladaros** (aunque sean un string vacio) 
* **<host>** - El nombre de **dominio** totalmente calificado o la **IP**
* **<port>** - Numero del **puerto TCP**
* **<url-path>** El resto del locator, es **especifico a cada Scheme**.

## Schemes de la actualidad

### FTP

* **<user>:<password>@**
	* La ausencia de un **usuario** se toma como el **usuario anonimous**
	* La presencia de un **usuario** y ausencia de **contraseña** debera triggerear que el user agent pregunte la contraseña al usuario
*  **<url-path>**
	*    ```<cwd1>/<cwd2>/.../<cwdN>/<name>;type=<typecode>```
		* **cwd** son comandos de FTP en el orden de ejecucion, separados por **/**
		* **name** Nombre del archivo con el que se interactua
		* **<typecode>** es omitible, Puede tener valor:
			* **"d"** - Ejecutar comando NLST con <name> como argumento
			*  **"a" ó "i"** - Ejecutar el comando FTP TYPE con "a" ó "i" como parametro



### HTTP

En HTTP:

* **<port>** -  Es omitible, si no esta se defaultea a 80
* **<url-path>** - Toma la forma de **<path>?<searchpart>**
* **El uso de usuario y contraseña no esta permitido**


### MailTo

Es una forma de implicar una direccion de email, no implica nada mas que eso, no indica como debe ser usado. En general los user agents abren un cliente de correo y le sugieren comenzar la escritura de un nuevo correo a esa direccion
Toma la forma
```
 mailto:<rfc822-addr-spec>
```
 
 donde:

 **<rfc822-addr-spec>** es la direccion de coreo segun RFC822
 
### Telnet

En general toma la forma 
```
 telnet://<user>:<password>@<host>:<port>/
```


### Files

Designa la ubicacion de un archivo en una computadora.
**No suele usarse para designar recursos accesibles desde internet**, ademas 
**no implica como debe navegarse o abrirse los archivos, su interpretacion es interna a cada sistema de archivos o SO**

```
 file://<host>/<path>
```


# URI

Definida en [ Uniform Resource Identifier  - RFC3986](http://www.rfcreader.com/# rfc3986)

## Intro y definicion
Define una sintaxis general de todos los Uniform Resource Identifiers (lo cual incluye a las URLs). La sintaxis especifica dependera de cada resource.

>**Su objetivo:** Tener un **sistema de nombres** lo suficientemente **flexible** como para poder **identificar los recursos de diferentes protocolos y sistemas**, incluso aquellos que aun no se han inventado. y mantener esos nombres dentro de una esturctura comun facil de parsear.

Las caracteristicas de las **URI**s son:

* **Uniform** - Permite tener identificadores uniformes (iguales o muy parecidos) a lo largo de diferentes mecanismos de recursos, protocolos y contextos (HTTP, FTP, FILE, etc), esto ademas permite usar los mismos  identificadores en diferentes contextos.

* **Resource** - Las URIs no limitan que se denomina como **_recurso_**, sino que se usa como un termino vago para llamar a aquello que esta siendo identificado por la URL.
No necesita ser algo accesible mediante la URI, podria ser una empresa o una persona.

* **Identifier** - Implica que contiene la informacion necesaria para distinguir un recurso de cualquier otro.


Ejemplos de URIs:

> ftp://ftp.is.co.za/rfc/rfc1808.txt
 http://www.ietf.org/rfc/rfc2396.txt
 ldap://[2001:db8::7]/c=GB?objectClass?one
 mailto:John.Doe@example.com
 news:comp.infosystems.www.servers.unix
 tel:+1-816-555-1212
 telnet://192.0.2.16:80/
 urn:oasis:names:specification:docbook:dtd:xml:4.1.2

## URL como subset de URI

Las URL son el subconjunto de las URIs que ademas de identificar un recurso Permiten acceder a ese recurso describiendo el mecanismo de acceso.


## Encoding

Muchos caracteres estan reservados como delimitadores de URIs, por consiguiente si se desea usarlos en la URI entonces deben ser **encodeados simbolizando su byte como dos numeros hexadecimales precedidos de un signo %**

## Sintaxis, las 5 partes del URI

Una URL tiene las siguientes partes, pero todas son opcionales.
```
Scheme: //authority/path1/path2/pathN  ?query # fragment
```


Ejemplo de partes opcionales:
![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/dsfsdf.jpg)

### Scheme:

Indica como sera construida la URI, muchas veces esta ademas vinculada a un protocolo (HTTP, FTP) el cual dicta como debe ser la URI

### //Authority

**Esta precedida por dos barras //, si estas no estan entonces LA URL NO TIENE AUTHORITY**
Identifica una autoridad jerarquica donde esta el recurso, desde la cual se extiende un path, puede ser relativamente complicada dependiendo del scheme, o puede no estar presente:
* //Dominio
* //host
* //IP
* //user:password@hostname:port 
* sin authority `tel:+1-816-555-1212`


### /path

**Identifica jerarquicamente la ubicacion del recurso** dentro del contexto del scheme ó de una authority (si aplica).


* Si le sigue a un authority, debe empezar con **/**
* Si la URI no tiene authority, el path NO debe empezar con **//**
* cada Path segment se separa con **/**
* Cada Path Segment tiene jerarquia, de izquierda a derecha son mas a menos importantes


### ?query


El segmento query contienen datos no jerarquicos que junto con el path sirven para **identificar el recurso dentro de la URI y del contexto del scheme.**

**Su inicio se indica con ?**


### # Fragment


El segmento Fragment **identifica un recurso secundario** relacionado al recurso principal (una parte del recurso principal por ejemplo). su contexto depende del **media type** del recurso obtenido (parte de la pagina HTML, minuto x de video, minuto x de audio, etc), por tal motivo:

* El fragment siempre es **interpretado por el user agent**
* El fragment es **independiente del scheme**
* El fragment es **dependiente del media type**
* **Tiene como objetivo permitir a un cliente enviar ó compartir en forma de URIs partes especificas de un recurso a otro cliente**

**Su inicio se indica con #**


## Relative URIs

Es una URI que, **dado el contexto de otra URI, hace referencia a un recurso**. 
Es identificada por tener un path sin tener un scheme.

EJ: dado el contexto `C:/carpeta/carpeta2` se puede considerar la **relative URI** `../carpeta3`

##  Same-Document Reference

Cuando se pasa de una URI a otra cuya **unica diferencia es el fragment** deberia ser interpretada como una **accion de navegacion dentro del recurso que ya fue obtenido, y no deberia comenzar una nueva accion de obtencion del recurso** (Ej deberia hacerte scrollear dentro de la pagina web, no deberia volver a bajarla y despues hacerte scrollear.)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc3ODM1NjkwOF19
-->