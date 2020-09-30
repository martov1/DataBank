
# Introduccion


Las HTTP cookies estan definidas en [RFC6265](http://www.rfcreader.com/# rfc6265).
Son una manera de hacer que HTTP, un protocolo **stateless** tenga la capacidad de tenr **state**

>Las cookies son **parametros HTTP adicionales** que el**servidor le da al user agent** y el **user agent devuelve en cada request**

Muchas veces se usan para

* Identificar a las computadoras que visitan tu sitio
* Guardar Sessions IDs
* Guardar datos no sensibles


## Headers usados 

* **El Servidor** - Envia una respuesta con el header **set-cookie** para pedirle al user agent que guarde una cookie y sus atributos 
```
 Set-Cookie: NombreDeLaCookie=ElValorQueQUierGuardar;
```
* **El User-Agent** - Usa el header **cookie** en cada HTTP request para reenviar la cookie al servidor
	``` 
	Cookie: SID=31d4d96e407aad42
	```
	
## Multiples cookies en al misma respuesta

Podes tener varios **set-cookie** headers en el mismo http response.
cada cookie tiene un **nombre**, por lo que podes colocar varias.



Ejemplo:

**El server coloca varias cookies:**
```
 Set-Cookie: SID=31d4d96e407aad42;
 Set-Cookie: lang=en-US; Path=/; Domain=example.com	 
```

**El cliente devuelve varias cookies**
```
 Cookie: SID=31d4d96e407aad42; lang=en-US
```

# Parametros de las cookies

>El servidor puede colocar varios atributos a una cookie, tales como su expiracion, a donde puede ser enviado y de que manera

* **Enviado por el servidor**
	* **set-cookie**  - Podes tener varios en la misma respuesta HTTP
		* **name:value pair** - Nombre de la cookie y el valor que se desea guardar
		* **expires** - Fecha de expiracion de la cookie, se puede colocar en el pasado para pedirle al user agent que la elimine
		* **max-age** - Indica la vida de la cookie en segundos, toma presedencia sobre expires
		* **domain** - Indica a que dominios se enviara la cookie al hacer http requests
		* **path** - Pide al user agent que solo envie la cookie a ciertos paths del dominio
		* **secure** - Pide al user agent que envie la cookie solo por canales seguros (HTTPS)
		* **httpOnly** - Pide al user agent que solo use cookies para http (JS no puede tocarlas)



* **Enviado por el user agent**
	* **cookie** - Contiene el valor de la cookie


## Atributos de Set-cookie 
* **Nombre y valor**
	El servidor Debe **identificar la cookie con un nombre** y **asignarle el valor** o la informacion que desea guardar en ella.
```
Set-Cookie: NOMBRE=VALOR;
// nombre: SID, valor: 31d4d96e407aad42
Set-Cookie: SID=31d4d96e407aad42;
// nombre: lang, valor: en-US
Set-Cookie: lang=en-US; 
```


* **expires**
	El servidor puede especificar hasta cuando la cookie es valida usando el atributo **expires**. Si no se especifica entonces el user-agent expira al finalizar la sesion (esto sucede cuando el user agent lo considere, ej: cuando cerras la pestaña del browser que tenia ese sitio) 
```
 Set-Cookie: lang=en-US; Expires=Wed, 09 Jun 2021 10:18:14 GMT
```

* **max-age**
	Cantidad de segundos hasta que la cookie expira, tiene presedencia sobre _expires_

* **Domain** 
Especifica **a que dominios puede enviarse la cookie**, incluye a los subdominios
	* Si se omite entonces el user agent devolvera la cookie **unicamente** al servidor de origen.
	* El user agent **rechaza cookies** cuyo domain no incluya el servidor de origen
```
 Set-Cookie: lang=en-US; HttpOnly; Domain=mozilla.org 
```


* **path**
 Permite limitar el envio de la cookie a ciertas rutas dentro del dominio
```
 Set-Cookie: lang=en-US; path=/docs
```
	
* **Secure**
	Le pide al user agent que envie esta cookie solo por canales seguros (que es un canal seguro lo define el user agent, en general implica **HTTPS**)
```
 Set-Cookie: lang=en-US; secure; 
```
	
* **HttpOnly**
	Pide al user agent que solo use las cookies en HTTP requests.
	esto **evita que javascript pueda acceder a las cookies**
```
 Set-Cookie: lang=en-US; HttpOnly; 
```

### Ejemplo

```
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly
```


# Limites

La implementacion de las cookies **puede tener** los **siguientes limites** en el user agent

* **4Kb de almacenamiento** (entre nombre, valor y atributos)
* 50 cookies por dominio
* 3000 cookies en total

# Sobreescribir cookies



El servidor puede sobreescribir una cookie para cambiar su valor, pero esto solo sucede si

* La cookie tiene el mismo nombre
* La cookie tiene el mismo path
* La cookie tiene el mismo dominio

**Seteo de cookie en un request**
```
Set-Cookie: miCookie=VALOR1; path=/docs; Domain=mozilla.org 
```

**Actualizacion del valor de la cookie en otro request**
```
Set-Cookie: miCookie=VALOR2; path=/docs; Domain=mozilla.org 
```


# Revocar cookies


El servidor puede solicitarle al user agent que **descarte una cookie** simplemente **cambiando su valor de expiracion a una fecha en el pasado**

```
Set-Cookie: miCookie=en-US; Expires=Wed, 09 Jun 1992 10:18:14 GMT
```


# Privacidad

Muchos sitios web usan contenido de un **tercer servidor** (publicidad, imagenes, etc).

**Si muchos sitios web utilizan el contenido de este tercer servidor, entonces el tercer servidor, a travez de colocar cookies en cada solicitud, tiene la capacidad de saber a que sitios fue el usuario.**

El **tercer servidor** puede entonces **enviar una cookie con un identificador unico**, y para rastrear al usuario, puede:
* Leer el HTTP header "referer" que indica de que sitio web viene la solicitud
`Referer: http://websiteA.com`
* El sitio original puede darle la informacion el tercer servidor cuando se realiza la solicitud mediante una url especifica
```
<iframe src="http://websiteB.com/ad.html?referer=websiteA.com">
```


# Seguridad


* El contenido de las cookies puede ser alterado por un atacante, debe ser tratado como **contenido posiblemente malicioso**.
* el servidor podria **firmar digitalmente** el contenido de la cookie
* El contenido de la cookie podria **encriptarse** (si es algo mas que un session ID) 
* Las cookies deben ser usar los atributos **secure** y **httpOnly**
* Las cookies pueden ser leidas y seteadas por todos los puertos del mismo server
* Las cookies **no deben almacenar contenido sensible**
* Las cookies deben ser siempre enviadas en **HTTPS/TLS** para evitar cookie stealing
* Las cookies pueden ser usadas en **ataques XSRF** si el sitio web es vulnerable a ese ataque
* Que una cookie este **marcada como secure** no evita que **EL SERVER LA ENVIA EN HTTP**
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU3MzA4MjQ3Ml19
-->