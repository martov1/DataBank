




# Contenido


* Conceptos pevios
	* Same origin policy
	* SOP y HTTP requests
* Protocolo CORS
	* CORS protocol para simple-requests
	* CORS protocol para complex-requests (con pre-flight) 
	* CORS formas de determinar si autorizar un origen.
	* CORS headers

# Conceptos pevios

## same-origin-policy 


**Glosario:**

* **Origin** - Definido como **port, hostname, protocol**

Se trata de una serie de politicas que evitan que se realicen acciones entre dos origenes distintos. Ejemplos son:

 * Iframes con origenes distintos no se pueden hablar mediante JS
 * No se permiten AJAX requests del sitio $A$ hacia el sitio $B$
 * El JS del sitio $A$ no puede acceder al local storage, cookies, etc del sitio $B$
 * El JS de la pestaña $A$ no puede hablar con el de la pestaña $B$



## SOP y HTTP requests

El browser rechaza el envio de requests HTTP al mismo dominio de origen como parte de la politica same-origin-policy. Se puede realizar excepciones usando el **protocolo CORS** 

>Cualquier solicitud a un dominio diferente al origen puede ser sujeta al **Protocolo CORS**, que permite la relajacion del same-origin-policy si el servidor da permiso


Algunos de los requests que **no limita por default:**

* `<script src="..."></script>` - Javascript desde el HTML document con script tags
* `<link rel="stylesheet" href="...">` - CSS
* `<img>`
* `<video> and <audio>`
* @font-face
* `<frame> and <iframe>` sin un header `X-Frame-Options`


# Protocolo CORS
Especificado en https://www.w3.org/TR/cors/


El protocolo **CORS** es una forma de darle a un servidor en un origen $A$ la capacidad de indicarle a browser cuando es seguro**ignorar el same-origin-policy** y realizar requests hacia $A$ desde un sitio web en el origen $B$.

Es decir, permite a **Un servidor pueda indicarle a un browser que es seguro relajar las restricciones del Same-Origin-Policy para un request en particular**

>Notas sobre seguridad
**Este protocolo solo sirve para protejer al usuario si el servidor implementa** 
* El protocolo HTTP de forma correcta, es decir lo los verbos **GET y HEAD son safe**
* Anty CSRF (tokens/nounces o otro mecanismo) para non-safe POSTS
* Sanitizacion del header `Origin` para evitar HTTP header inyection
* Se limita el acceso a CORS a los origenes minimos necesarios (salvo que sea un public API) usando alguna base de datos o algun otro mecanismo

## CORS protocol para simple-requests

Este procedimiento se usa para aquellos requests que se conideran menos peligrosos o que los servidores en general ya tienen contramedidas para salvaguardarse.

>**A grandes razgos:** Cuando se hace una solicitud AJAX de $A$ a $B$, el browser hace la solicitud, el servidor la procesa y responde. luego el browser se fija en la respuesta si los CORS headers dan permiso de usar esa respuesta en $B$. Si dan permiso entonces el browser le da el contenido de la respuesta al JS 



**Funciona asi:**

* **REQUEST** - El sitio web en el origen `www.tuPagina.com` le pide al browser hacer un request a `www.API.com`
	* El browser indica el origen usando el CORS header  `Origin: www.tuPagina.com`
	* El browser **envia el request**
* **RESPONSE** - El browser recibe la respuesta.
	* **EVALUACION DE CORS HEADERS**- Si la respuesta tiene **CORS headers**, entonces:
		*  **Headers otorgan permiso** - El servidor dio permiso, la respuesta del request se libera al JS de `www.tuPagina.com`
		*  **Headers niegan permiso** - El servidor no da permiso, la respuesta del request NO se libera al JS de `www.tuPagina.com`
	* **AUSENCIA DE CORS HEADERS** - Si no hay CORS headers entonces el browser no permite que la respuesta sea accesible a la pagina web  

**El servidor provee permiso al sitio web:**
* Listando su `Origin` en `Access-Control-Allow-Origin`
Este metodo permite que el browser envie autenticacion automatica (cookies, http auth).
**Peligro de CSRF** si reflejas cualquier origen que te envien en lguar de 
```
	 Access-Control-Allow-Origin: www.tuPagina.com
``` 
* usando el wild-card `*`
Este metodo bloquea autenticacion automatica (cookies, http auth). 
Es **CSRF safe**
```
 Access-Control-Allow-Origin: *
```

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/aaa_1Fzg5Bq.png)

>**Simple-requests** son aquellos con los que cumplen con este **white-list**
>
* **HTTP methods**
	* GET
	* HEAD
	* POST
		* Con content-type
			*  application/x-www-form-urlencoded
	    	* multipart/form-data
	    	* text/plain
* **HTTP headers**
    * Accept
    * Accept-Language
    * Content-Language
    * Content-Type (but note the additional requirements below)
    * Last-Event-ID
    * DPR
    * Save-Data
    * Viewport-Width
    * Width
* No hay event listeners en el objeto XMLHttpRequestUpload
* No se usa un ReadableStream
>
>**NOTESE: authorization no esta entre los headers permitidos**


## CORS protocol para complex-requests (con pre-flight)

Para todos aquellos requests que no califican como "Simple requests" el **Protocolo CORS** demanda que el user agent pregunte al servidor que requests autoriza a realizar desde otros origenes **antes** de hacer el request, esto se hace mediante una **pre-flight request**

>**A grandes razgos:** Cuando se hace una solicitud AJAX de $A$ a $B$ que no es un simple request, el browser:
>* Envia previamente una solicitud al server (llamada **pre-flight**) preguntandole que clase de requests acepta en este endpoint. 
>* El server indica si $A$ puede hacer requests y que requests se pueden hacer. 
>* Si la solicitud AJAX encaja dentro de estos parametros entonces el browser la envia y la trata como un simple-requests
>	* Se usan y validan los headers  `Origin` y `Access-Control-Allow-Origin`
>	* Se cachea la respuesta del pre-flight para no tener que hacerla otra vez. el cache dura la cantidad de segundos indicada en `Access-Control-Max-Age`

**Funciona asi:**

* **REQUEST** - El sitio web le pide al browser hacer un **request fuera del origen**
* **PRE-FLIGHT** - El browser realiza **un** request usando el **metodo HTTP OPTIONS** e indicando
	*  `Origin: www.paginaQueSolicita.com ` Mi request viene de este origen
	*  `Access-Control-Request-Method: PUT` Quiero usar este method
	*  `Access-Control-Request-Headers: X-PINGOTHER, Content-Type` Quiero usar estos
* **RESPUESTA DE PRE-FLIGHT** - El servidor responde con headers indicando que tipo de solicitudes autoriza realizar a este endpoing
	*  `Access-Control-Allow-Origin: www.paginaQueSolicita.com` Autorizo tu origen.
	*  `Access-Control-Allow-Methods: PUT, POST, GET` Autorizo estos metodos en este recurso.
	*  `Access-Control-Allow-Headers: Authorize, connection` Autorizo estos headers.
	*  `Access-Control-Allow-Credentials` Autorizo el envio de cookies, certificados y Authorization HTTP headers
* **EVALUACION DE LA RESPUESTA**  El browser analiza la respuesta y se fija si el request original entra dentro de lo que autoriza el servidor
	* **REQUEST AUTORIZADO** - El request entra dentro de lo que el server autoriza 
		* **ENVIO** - el browser envia el request original **tratandolo como un CORS simple**
		`Origin: www.paginaQueSolicita.com `
		* **RESPUESTA** - Se evalua la respuesta como un simple-request
		`Access-Control-Allow-Origin: www.paginaQueSolicita.com`
	* **REQUEST DENEGADO** Los CORS headers indican que el request no se puede realizar, el browser no envia el request original
	* **AUSENCIA DE CORS HEADERS** - Si el server no responde con CORS headers entonces el browser no realiza el request
		
![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/hhh.png)

## CORS formas de determinar si autorizar un origen.

Dependiendo de lo que quieras implementar, puede ser que

* **Quieras autorizar tu API a cualquier origen**
	* Queres evitar el uso automatico de cookies/certificados/http auth (seguro) 
		* usas el wildcard 
		`Access-Control-Allow-Origin: *`
	* Queres permitir el uso automatico de cookies/certificados/http auth (**PELIGRO DE CSRF**)
		* Reflejas el valor de `origin`, habiendolo **sanitizado** pare evitar HTTP header inyection
	`Access-Control-Allow-Origin: www.paginaQueSolicita.com`
* **Queres autorizar tu API a una lista de origenes.**
	* Verificas que el `origin` exista en un array o una base de datos
		* Si existe, lo añadis al  `Access-Control-Allow-Origin:` en tu respuesta

## CORS headers

CORS actua como una extension de HTTP; usando los siguientes HTTP headers 

Los headers que un server puede poner en:


Respuestas CORS


* **Access-Control-Allow-Origin** - Permite a un origen en particular hacer este request
```
Access-Control-Allow-Origin: http://foo.example
Access-Control-Allow-Origin: * // permitir CUALQUIER origen
```
* **Access-Control-Allow-Methods** - Indica que metodos se pueden usar para hacer este request
```
Access-Control-Allow-Methods: POST, GET
```

* **Access-Control-Allow-Headers** - Indica que headers se pueden enviar con este request
```
Access-Control-Allow-Headers: X-PINGOTHER, Content-Type
```


* **Access-Control-Allow-Credentials** -  Permite que el browser envie  **Cookies, Certificados ó HTTP authentication headers**
Por default el browser NO ENVIA ninguna de estas credenciales en CORS requests.
Si el `Access-Control-Allow-Origin:` esta seteado en `*`, este header sera ignorado y el browser NO ENVIARA ninguna cookie o HTTP auth header automaticamente porque lo considera muy inseguro. 
Esto es para evitar CSRF, si estas usando una API la idea es que tengas que colocar las credenciales explicitamente en JS y no uses sistemas automaticos en el browser que puedan causar CSRF
```
Access-Control-Allow-Credentials: true
```


* **Access-Control-Max-Age** - Cuanto tiempo puede cachearse la respuesta del pre-flight en segundos. es decir, por los proximos 10000 segundos no sera necesario hacer el pre flight para este request.
```
Access-Control-Max-Age: 10000
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1MTkwMTM5Nyw2MTAxMDYwNzVdfQ==
-->