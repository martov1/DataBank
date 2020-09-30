


**Atencion:**
**Para ver como aplicar Oauth 2 como METODO DE AUTENTICACION tenes que ver el documento AUTENTICACION en la carpeta SEGURIDAD**

# Contenido

* Motivacion y objetivo 
* Punto de vista del usuario 
* Nomenclatura
	* Nombres generales
	* Tokens
	* Endpoints 
* "Authentication code" flow 
	* Funcionamiento
		* Setup previo 
		* Authenticacion
* "Implicit" flow 
* "Resource Owner Password Credentials Grant" flow
* "Client Credentials Grant" flow
* Endpoints 
	* Authorization Endpoint
	* Redirection Endpoint
	* Token Endpoint
	* Obtencion de datos
* Checklist de Consideraciones al implementar
	* **Los refresh tokens son optativos**	 	
	* User experience y redireccion
	* Edge cases a tener en cuenta
* Seguridad
	* Client identification (client secret, client ID)
	* Code inyection attack
	* Cross site request forgery
	* Almacenamiento en bases de datos



# Motivacion y objetivo

Referencia: https://tools.ietf.org/html/rfc6749

>### OAUTH ES UN PROTOCOLO DE __AUTORIZACION__, NO ~~AUTENTICACION~~
	
_

>**Es un protocolo permite que un cliente:**
> * Use un tercer servicio a nombre del usuario
> 	* Asegurando que el usuario dio consentimiento 
> 	* Sin  que el usuario le de sus credenciales del servicio al cliente
> 	* Limitando los permisos que se le dan al cliente sobre el servicio
> 	* Permitiendole al usuario en cualquier momento revocarle el permiso al cliente
> 	* Manteniendo siempre el control de su cuenta en el tercer servicio
> 	
> 	
>**NO FUE DISEÑADO ORIGINALMENTE COMO UN PROTOCOLO DE AUTENTICACION**
>
> Oauth 2.0 se puede usar para autenticar al usuario con los datos de un tercer servicio (EJ: numero de usuario unico de facebook/Google)

**Ventajas para el usuario:**

El uso de Oauth para que un tercero acceda en nombre del usuario a un servicio le da al usuario algunas ventajas de seguridad.
* **Rol limitado** - El acceso al servicio es limitado (scope)
* **Revocabilidad** - El acceso al servicio es revocable
* **Seguridad** - Robo del token no implica perder el control de la cuenta del usuario

## Punto de vista del usuario:

Ejemplo con google y miSitio

* El usuario aprieta un boton en miSitio y es redirigido a google.
* En google coloca sus credenciales
* Google consulta al usuario que permisos desea otorgarle a miSitio
* El usuario es redirigido nuevamente a miSitio y
*  MiSitio tiene acceso a servicios de Goole en nombre del usuario
	* Estos servicios pueden permitir a MiSitio autenticar al usuario (Ej id unico de facebook)  

---

## Nomenclatura:

### Nombres generales
* **Resource owner** - el usuario de google que es dueño del recurso al que miSitio desea acceder
* **Client** - miSitio, el sistema que desea que se realize una autenticacion
* **Authorization server** - Google, el sistema que realiza la autenticacion
* **Resource server** - Google, el sistema que tiene el recurso que miSitio desea, por ejemplo google Places API
* **Redirect URI** - el lugar a donde es redireccionado el usuario despues de aceptar otorgarle permisos a miSitio
* **scope** - Los permisos que miSitio solicita que el usuario autorice en el authorization server (ver perfil, publicar,etc)
* **Back channel** - La comunicacion entre servidores
* **Front channel** - La comunicacion entre el usuario y un servidor



### Tokens

* **Authorization grant** - Un token que prueba que el usuario acepto dar permisos a miSitio, se usa luego para obtener el access token
	* Caduca maximo a los 10 minutos
	* Un solo uso 
* **Access token** - lo que miSitio obtiene del proceso, y que usa cada vez que le solicita a Google datos de este usuario
	* Tiene poco tiempo de validez
	* puede usarse multiples veces
* **Refresh token** - miSitio puede usar un refresh token provisto al mismo tiempo que el access token para obtener un nuevo access token cuando el anterior caduque
	* Mas tiempo de validez



### Endpoints
* Google
	* **Authorization Endpoint**
		Donde el usuario es autenticado por google mediante usuario y contraseña
	* **Token Endpoint**
	Donde MiSitio solicita tokens. MiSitio se autentica con ID y client secret
* MiSitio
	* **Redirection endpoint  **
	Endpoint de MiSitio donde google redirecciona al usuario con el Access grant (en Authentication code flow) o el Access token (en implicit flow) como parametro de la URL


---
## Authentication code flow 

Es un medio de operacion que sigue los siguientes pasos basicos

* **Authorization Endpoint** - El usuario es redirigido a google
	* google autentica al usuario
* **Redirection endpoint** - google redirige al usuario a miSitio con un **Authorization grant** en la URL
* **Token Endpoint** - miSitio recibe el **Authorization grant** y lo usa para para obtener un **token**
* miSitio usa el token para obtener los datos del usuario con la API de google


## Funcionamiento

Antes de poder autenticar con Oauth, hay que registrarse con el **Authorization server**, esto se hace una unica vez cuando  estas implementando Oauth con un **Authorization server** nuevo.


### Setup previo:
* **registras manualmente miSitio con el authenticatio server, tenes que darle:**
	* Nombre de la aplicacion de MiSitio
	* Dominio de la aplicacion de Misitio
	* **Redirection Endpoint** donde se redirige al usuario al terminar de autenticar
		* Podes tener varias, la que vas a usar la especificas en el momento en el paso **Authorization Endpoint**	 
	* **Scope** - los posibles scope que podrias llegar a pedir


* **el Authorization server te devuelve:**
	* **Client ID** que tenes que usar para identificarte, como si fuera tu usuario
	* **Client secret key** - que tenes que usar para identificarte, como si fuera tu contraseña

### Authenticacion:
* **Authorization Endpoint** - Redirigis al usuario a una URL del authorization server especifica, con los siguientes parametros
	*  **Scope** - Los scopes que pedis para este usuario
	*  **Redirect URI** - la redirect URI de miSitio que vas a usar
		* En el setup podrias haber registrado mas de una  
	*  **client_ID** - indica que miSitio es el que hace la solicitud


* **Consentimiento** - En el authorization server el usuario se loguea y da consentimiento al scope pedido


* **Redirection Endpoint** - Google redirige al usuario al RedirectURL de miSitio
	*  Como parametro de URL, google te envia un **Authorization grant** 
		* Expira en 10 min
		* Uso unico  
	*  El usuario esta en una url de miSitio y ve una pantalla de espera


* **Token Endpoint** - miSitio Envia el Authorization grant a google y recibe los tokens
	* Envias:
		* Authorization grant
		* credenciales de miSitio  
	* Recibis
		* Google responde con el **Access token**
		* Google puede proveer un **refresh token**
	* Ocurre en el back channel 
		* Mientras tanto el usuario sigue en la pantalla de espera 


* **Obtencion de datos** - Usas el **Access token** como HTTP Bearer token para entrar a la API del servicio en nombre del usuario
	* Se solicita a google algun dato de identificacion con este token
		* Id unico de usuario/nombre/etc  


* **Refresh del token (OPCIONAL)** - El Access token **expiro**.
	* Envias el **refresh token** a Google usando el **Token Endpoint**
	* Google responde con un nuevo **Access token** y **Refresh token**


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/fotomila_8TGnEu2.jpg)


---

## Implicit flow 

Es una forma de tuilizar Oauth cuando **no tenes un backend** y necesitas que todo el proceso funcione en el **front channel**. Es menos segura y por consiguiente no orotga refresh tokens, solo access tokens de duracion limitada.

> EJEMPLO DE USO:
> **WEB APP QUE CORRE TOTALMENTE EN EL BROWSER DEL USUARIO, Y POR ENDE NO HAY SERVIDORES**

**Funciona asi:**

* El usuario es redirigido a google
* google autentica al usuario
* google redirige al usuario a miSitio con un access token
* miSitio puede usar el token para 
	* FRONTEND usar la API de google
	* BACKEND Enviar el token al server para determinar la identidad del usuario

**Diferencias con el authorization code flow:**
* No utiliza un backend
	* no utiliza el **token endpoint** 
	* No utiliza **client secret**
* No utiliza refresh tokens
* Los tokens se obtienen directamente del **authentication endpoint**
	* El usuario es redirigido al **redirection endpoint** con el **Access token como un URI fragment** 
		* Alli vuelve a cargar la **web app**
		* Los fragmentos no se envian al server (HTTP spec) asi que tendra que ser **leido localmente por el frontend** de la web app
		* La web app actua de **cliente**, pidiendo los datos al **authorization server**
* El usuario tiene acceso al Access token de forma directa (inevitable)
* No se autentica al cliente (misitio), es inevitable

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/oauth2-and-spring-security-15-638.jpg)


---

## Resource Owner Password Credentials Grant


Este flow **se usa muy poco** y solamente en aplicaciones muy privilegiadas (OS del telefono, etc).

**funciona asi:**
* mediante el **token endpoint**
	* El **cliente** envia el **usuario y contraseña** del usuario al **authentication server**
	* El **authentication server** responde enviando 
		* Un **Access token** 
		* Opcionalmente un **refresh token**

---
## Client Credentials Grant

Este flow **se usa poco**, el cliente (miSitio) puede obtener un token **solamente con sus credenciales** (EJ: client_id y client_secret) sin tener que preguntarle nada al usuario ni pedirle consentimiento.

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/image001_eP3CK8y.png)



---


## Endpoints

### Authorization Endpoint

> Este endpoint se usa
> * **Solo en el front channel**
>
>
> * **Se usa en los flows:**
> 	* **Authentication grant flow**
> 	autentica y devuelve un access grant
> 	* **Implicit flow**
> 	autentica y devuelve un access token

El **Authorization Endpoint** es una **URL del authorization server** a donde el **resource owner** es redirigido para pedirle que:

* **Se autentique** con el authorization server
	En general esto es loguearse a su cuenta de google/facebook
* **Provea su consentimiento** para que miSitio acceda a partes del servicio en su nombre 
	En general esto implica una pantalla de "desea que miSitio acceda a: "lista de contactos, datos....." 
 
Este endpoint en general se provee en la **Documentacion del authorization server**


**El endpoint acept los siguientes parametros:**

````
https://google.accounts/o/oauth2/auth?
	client_id = blabla // Id provisto por google para saber quien soy
	redirect_uri= https://miSitio.com/callback
	scope=contacts.readonly, postStuff  //El scope que solicito
	response_type=code		//que deseamos del endpoint
	state=foobar	//Esto se devolvera tal como lo escribas, evita CSRF
````

* **Client_id** - Un identificador unico de miSitio, 
	* Funciona efectivamente como el "nombre de usuario" de miSitio
	* Provisto por el Authorization server durante el setup/registro previo
	* Permite al authorization server saber quien hace la solicitud
	* Los authorization grants solo seran validos en el **token endpoint** si los pide el mismo client_ID
* **redirect_uri** - El Redirection endpoint donde el authorization server debe redirigir al usuario
	* Es opcional si al momento del setup/registro se agrego solo un redirection endpoint
	* Es obligatorio si al momento del setup se registraron varios redirection endpoints
* **Scope** - te permite pedir accesos reducidos
	* En el momento del registro, miSitio pidio cierto scope
	* Al momento de pedir una autorizacion puntual, podes pedir MENOS scope usando este parametro.
* **response_type**    
	* **code** - Solicita al authorization server un access grant, se usa en el "**authorization code flow**"
	* **token** - Solicita al authorization server un token directamente, se usa en el "**implicit flow**"
* **state** - Un valor que sera devuelto al redirection endpoint. debe chequearse que el valor sea el mismo para evitar  cross-site request forgery

---

### Redirection Endpoint

> este endpoint se usa
> * **Solo en el front channel**
>
>
> * **Se usa en los flows:**
> 	* **Authentication grant flow**
> 	informa de un access grant
> 	* **Implicit flow**
> 	informa de un access token

Una vez que el usuario **dio consentimiento**, el **Authorization server** lo redirige al **redirection endpoint** de miSitio.

**El redirection endpoint permite:**
* Devolver al usuario nuevamente a miSitio
* Darle a miSitio el codigo que pidio, ya sea
	* **Authorization code** - en el "authorization code flow" 
	* **Access token** - en el "implicit flow" 
	 

se ve asi:

**Exito;**
````
GET https://miSitio.com/callback?
	code = blabla //El Authorization grant (Authorization code flow) ó 
					// el access token (implicit flow)
	scope= blabla
	state=foobar
````

Los query strings que coloca el **Authorization server** son los siguientes

* **code**
	* Si el **request_type** pedido en el **Authorization Endpoint** era `"code"` entonces Devuelve un **Authorization grant**
	* Si el **request_type** pedido en el **Authorization Endpoint** era `"token"` entonces Devuelve un **Access token**
* **scope** -  El usuario puede haber consentido a un subconjunto del scope que miSitio pidio. Si el scope otorgado es diferente al scope que pediste en el authorization endpoint entonces en este parametro aparece el scope otorgado
* **state** - Un valor que fue provisto en el authorization endpoint y ahora es devuelto al redirection endpoint. debe chequearse que el valor sea el mismo para evitar  cross-site request forgery


>Cuando ello haya sucedido, **el sitio que cargaste con la redirect URI debera hacer que el usuario espere hasta que el proceso de autenticacion termine, y otorgarle al usuario una sesion**

**Error:**

En caso de que google no haya podido autenticar al usuario, devolvera al callback un menaje de error
````
GET https://miSitio.com/callback?
	error = Access_denied //El Authorization grant
	error_description=the user did not consent
````

* **error**
	* **invalid_request** - parametros faltantes, invalidos, repetidos, etc
	* **unauthorized_client** - miSitio no esta autorizado a hacer este request
	* **access_denied** - El usuario no dio consenitmiento
	* **unsupported_response_type** - el flow solicitado no esta soportado
	* **invalid_scope** - miSitio pidio un scope invalido
	* **server_error** - server internal error, existe porque un redirect (3xx) no puede a la vez tener codigo 5xx
	* **temporarily_unavailable**
* **error_description** - OPCIONAL, error en human-friendly format
* **error_uri** - OPCIONAL, sitio web con documentacion sobre el error
 

---

### Token Endpoint

>Este endpoint se usa
>
>* **Solo en el back channel**
>* **Solo con datos encodeados usando application/x-www-form-urlencoded**
>
>
> * **Se usa en los flows:**
> 	* **Authentication grant flow**
> 	* **Resource Owner Password Credentials Grant flow**
> 	* **Client Credentials Grant**

**Este Endpoint tiene varios usos:**

* **Obtener Access tokens**
	* **Authorization code flow**
	Provees el access grant y las credenciales del cliente (misitio) para obtener un access token y refresh token
	* 	**Resource Owner Password Credentials Grant flow** 
	Provees el usuario y contraseña del usuario final y obtenes un acces token y refresh token 	
	* **Client Credentials Grant**
		El cliente envia sus credenciales y el scope deseado, el Authorization server devuelve un token


* **Renovar tokens con un Refresh token**
	Cuando un **Access token** caduca (o cuando miSitio lo desee) se puede utilizar el **Refresh token** para pedir un nuevo **Access token y refresh token**
	
>**Autenticacion:**
El token endpoint esta protegido con autenticacion, el **client (miSitio) debe autenticarse**, esto puede suceder con:
* Parametros en el request (**client_id y client_secret**)
* **Bearer token**
* Cualquier otro metodo de autenticacion.

	
	
 **Solicitud que hace miSitio:**
 
````
 POST www.googleapis.com/Oauth2/v4/token
 	Content-Type: application/x-www-form-urlencoded
 	
	//**SI QUERES USAR UN ACCESS CODE **
	code = blablabla  
	//**SI QUERES USAR UN REFRESH TOKEN**
	refresh_token=tGzv3JOkF0XG5Qx2TlKWIA 	
	
	client_id = blabla // un identificador unico que te dio google al registrarte
	client_secret= blabla // una clave secreta que te dio google al registrarte
	grant_type=authorization_code
	scope="blabla" //OPCIONAL - el scope que pedis, podes pedir scopes mas pequeños
					// de los que te autorizo google para requests puntiales
	redirect_uri = "www.misitio/callback" // solo si se especifico redirectURI en el 
										  //Authorization Endpoint
	
````

**Parametros en Authorization code flow:**

* **El request es un POST**
* **code** - un **Access grant** (NO USAR SI USAS REFRESH TOKEN)
* **refresh_token** - un **Refresh token** (NO USAR SI USAS UN ACCESS CODE)
* **client_id** - un identificador unico de miSitio que el **Authorization server** provee al momento del setup inicial / registro
	* Funciona como el "nombre de usuario" de miSitio
* **client_secret** - (OPCIONAL) Funciona como contraseña de miSitio
	* La autenticacion tambien podria ser por HTTP bearer token	 
	* Si un refresh token es robado, sera inutil sin este client_secret
* **grant_type** - puede ser 
	*  **"authorization_code"** - si estas usando el "authorization code flow"
	*  **"password"** - si estas usando resource owner "password credentials grant flow"
	*  **client_credentials** - si estas usando Client Credentials Grant flow
* **redirect_uri** 
  Si se especifico un redirect_uri en el Authorization endpoint entonces tambien debe ser colocado en el token endpoint al solicitar el token, y ambos valores deben ser identicos.
 
 > Si se usa el **Resource owner password credentials grant flow**, los parametros son
 > * **Grant type** - "password"
 > * **username** - el nombre de usuario que identifica al resource owner en el servicio
 > * **password** - la contraseña del resource owner en el servicio
 > * **scope**
 >
 >So se usa el **Client Credentials Grant flow**, los parametros son
 >
 > * **grant_type** - "client_credentials"
 > * **scope**
 > Ademas vas a tener que autenticarte, ya sea con bearer token o otro sistema


**Recibis el access token:**
````
     HTTP/1.1 200 OK
     Content-Type: application/json;charset=UTF-8
     Cache-Control: no-store
     Pragma: no-cache

     {
       "access_token":"2YotnFZFEjr1zCsicMWpAA",
       "token_type":"example",
       "expires_in":3600,
       "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
       "example_parameter":"example_value"
     }


````


---

### Obtencion de datos

 Ahora podes **interactuar con la API con la que querias interactuar**, en nombre del usuario, **usando el token como http bearer token**
 
>Podes **usar estos datos para autenticar al usuario**, por ejemplo podes usar un userID unico que te provee facebook o google
 
````
 GET api.google.com/some/endpoint
 Authorization: Bearer MiToken
````


---
## Checklist de Consideraciones al implementar

### Los refresh tokens son optativos

**Solo necesitas refresh tokens si vas a acceder al servicio cuando el usuario no esta usando la aplicacion**, sino es perfectamente aceptable volver a hacer el flow, ya que el **authorization server** no volvera a pedir consentimiento y volvera a enviar un nuevo token al **redirect url**. 


>**RECORDA: Si estas solamente autenticando con Oauth**, simplemente podes devolverle al usuario una sesion que guardes que no tenga nada que ver con oauth ni con los tokens y asi lo dejas autenticado por la duracion que vos quieras (puede ser por siempre), entonces **solo necesitas autenticar con oauth una vez por sesion**

### User experience y redireccion:

* Hasta que la comunicacion en el back channel termine, el usuario vera:
	* una pantalla de carga (**redirigis a una parte puntual de tu SPA que le pregunte al server si logro autenticar**) 
	* una pantalla en blanco hasta ser redireccionado (**HTTP request que eventualmente sera respondido con un 303 redirect y una cookie**)

### Edge cases a tener en cuenta:

* **Redireccion 2 / Callback URL**
	* Manejar el caso en el que el **authentication server** no logre autenticar y devuelve un error mediante el callback url


* **Solicitud de datos:**
	* Manejo de expiracion del token
		* El usuario esta usando la aplicacion 
			* Volver a mandar al usuario a travez del flow (facil)
		* El usuario no esta usando la aplicacion 
			* Refrescar usando refresh token (menos facil)
	* Manejo de expiracion ó invalidez del refresh token (optativo)
		* Volver a mandar al usuario a travez del flow   
		
		
### Comunicacion continua con tercer servicio:

Este flujo es para aplicaciones que necesitan **constantemente comunicarse con el tercer servicio y por algun motivo no queres volver a hacer pasar al usuario por el authentication flow**.

**ES INNECESARIAMENTE COMPLEJO SOLAMENTE PARA SOLAMENTE AUTENTICAR AL USUARIO**



* **JWT o encripted cookie con los Oauth tokens**
	* Podes guardar el token y refresh token encriptados, el user los manda en cada interaccion
		* Desencriptas y usas para pedile al 3er servicio los datos (pedir auto a uber?)
		* Si caduco el access token
			* Refrescas tokens con refresh token
			* Envias nuevos tokens al cliente en forma de cookie/JWT 


**Ventaja**: Evitas guardar tokens en tu DB, es stateless.


* **JWT/cookie con sesion o tokens propios**
	* Guardas los Oauth tokens en tu base de datos junto con el usuario
	* Te ocupas de refrescar los tokens del lado del server
	* EDGE CASE: Si los tokens caducan le pedis al user que vuelva a pasar por el flow

**Ventaja:** tenes tokens validos aunque el usuario no este cerca.

---

## Seguridad


### Client identification (client secret, client ID)

* **Client secret** 
	* **Proteccion de refresh tokens** El token endpoint pide un client secret para inutilizar el robo de refresh tokens.
Si roban un Refresh token y no tienen la client_secret entonces no pueden usar el token endpoint para pedir un nuevo token.
	* **Proteccion de access grants** El access grant viaja por el **front channel** y podria ser robado, Si necesitas un client secret para usarlo en el Token endpoint entonces el robo del access grant es inutil
	* **Rotacion de credenciales/ Recuperarse de ser vulnerado** - podes cambiar facilmente los client ID y client secret si un sitio web es vulnerado, y los mismos Refresh tokens que tenias siguen siendo validos ya que aunque otro los tenga, si no tiene tu nuevo client_secret entonces no le sirven.


* **Client ID** El server pide un client ID en el authorization endpoint ya que asi sabe la lista de Redirection endpoints a la que es valido redirigir al usuario.

### Code inyection attack

Deberias sanitizar todo

### Cross site request forgery

Con cada request que se realice desde el **front channel** hay que tener cuidado de que no se trate de un **CSRF**, esto se hace mediante el parametro **state** de los endpoints que **pueden ser usados por el front channel**

Simplemente con emitir un valor criptoseguro y luego verificar que ese valor es el que vuelve en la respuesta alcanza.

[mas info](https://www.youtube.com/watch?v=vRBihr41JTo)

### Almacenamiento en bases de datos

* Si guardas el access/refresh token en la base de datos, **encriptalo**
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTU3MjkwMzQyLC0xMTUxMjU4NTMwXX0=
-->