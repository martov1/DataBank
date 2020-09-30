



**CNIT 129S 2016**

- [x] CNIT 129S: Securing Web Applications Ch 1-2	
- [x] CNIT 129S: Ch 3: Web Application Technologies Part 1	
- [x] CNIT 129S: Ch 3: Web Application Technologies, Part 2	
- [x] CNIT 129S: Ch 3: Web Application Technologies Part 3 of 4	
- [x] CNIT 129S: Ch 4: Mapping the Application (Part 1 of 2)	
- [x] 129S ch4b	
- [x] CNIT 129S: Ch 5: Bypassing Client-Side Controls (Part 1 of 2)	
- [x] CNIT 129S: Ch 5: Bypassing Client-Side Controls (Part 2 of 2)	
- [x] CNIT 129S: Ch 6: Attacking Authentication (Part 1 of 2)	
- [x] CNIT 129S: Ch 6: Attacking Authentication (Part 2 of 2)	
- [x] CNIT 129S: Ch 7: Attacking Session Management (Part 1 of 2)	
- [x] CNIT 129S: Ch 7: Attacking Session Management (Part 2 of 2)	
- [x] CNIT 129S: 8: Attacking Access Controls	
- [x] CNIT 129S: PHP Security Problems	
- [ ] CNIT 129S: 9: Attacking Data Stores (Part 1 of 3)	**Ver cuando sepa SQL**
- [ ] CNIT 129S: 9: Attacking Data Stores (Part 2 of 3)	
- [ ] CNIT 129S: 9: Attacking Data Stores (Part 3 of 3)	
- [ ] CNIT 129S: 10: Attacking Back-End Components (Part 1 of 2)**cuando sepa linux**
- [ ] CNIT 129S: 10: Attacking Back-End Components (Part 2 of 2)	
- [x] CNIT 129S: 11: Attacking Application Logic	
- [x] CNIT 129S: 12: Attacking Users: Cross-Site Scripting (Part 1 of 2)	
- [x] CNIT 129S: 12: Attacking Users: Cross-Site Scripting (Part 2 of 3)	
- [x] CNIT 129S: 13: Attacking Users: Other Techniques (Part 1 of 2)	
- [x] CNIT 129S: 13: Attacking Users: Other Techniques (Part 2 of 2)
 


 **Otros:**
 
 - [ ] [SQL inyection](https://www.youtube.com/watch?v=BR-VeQUoRCw&list=PLZOToVAK85Mr4CzRimmw4KD84yUjkEAEw)
- [ ] [OWASP CSRF recomendations PROTEGE CONTRA XSS Y CSRF A LA VEZ, ESTA BUENO PARA LOS REST TOKENS](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)_Prevention_Cheat_Sheet#Double_Submit_Cookie) 
 
**Libros:**

- [ ] [JavaScript Web Application Secure Coding Practices](https://checkmarx.gitbooks.io/js-scp/file-management/)
* [web app hacked handbook](https://leaksource.files.wordpress.com/2014/08/the-web-application-hackers-handbook.pdf)
	- [ ] Chapter 9 - SQL inyection chapter

**Seminarios 2018**:

- [x] [Web Application Security Risks: A Look at OWASP Top Ten 2017](https://www.youtube.com/watch?v=avFR_Af0KGk)
- [x] [Modern Web Security Standards](https://www.youtube.com/watch?v=j-0Bj40juMI)


**Esperar a que salga el cap 13 otra vez**
**VER:** https://www.youtube.com/watch?v=jDE0cntjOq8


**Volver a ver SQL inyection despues de ver SQL**
https://www.youtube.com/watch?v=0gCYar3GAmw
https://www.youtube.com/watch?v=vCAn9qBlpls


**Volver a ver back-end cuando sepa linux**

Curso:

https://owasp-academy.teachable.com/courses

https://www.udemy.com/webhacking/





## Problematicas


Las web apps tienen como mayor problematica que **El usuario puede realizar inputs**

Por consiguiente, cuando desarrollas una web app, tenes que:


* Asumir que todos los user inputs son maliciosos
	* Un atacante puede modificar HTTP headers, cookies o cualquier parte de las solicitudes.
* Los client-side controls cant be trusted

* No poner confidential data en el source code
* Considerar las vulnerabilidades de las librerias y servicios de terceros que usas
* Loguear logins, key transactions, credit card payments, cambios de contraseña, authentication events. Si queres mucha seguridad, loguea todo
	* Los logs son SENSITIVOS. por ahi quieras ponerlos en otro server 
	* Un atacante intentara borrar los logs, deberian ser read-only



## Seguridad de un servidor HTTP

### Usar HTTPS y cookies bien configuradas

El servidor debera:

* Usar **HTTPS** y **certificados** SSL para poder garantizar la seguridad de los datos en transito
* Usar **cookies** con los parametros **safe** y **HttpOnly** para ayudar a protegerlas del robo.
	* Evitar que el **servidor envie cookies en http** (puede hacerlo aunque la cookie este setada como safe) 


### Obscurecer informacion del servidor

Los servidores (apache, Ngnix, etc) tienen vulnerabilidades conocidas en determinadas versiones, proveerle al atacante la informacion de que servidor estas corriendo puede ser darles una ventaja. para evitarlo:

* Proveer mensajes vagos en el HTTP HEADER **server**
* Proveeer**mensajes de error vagos** que no den mucha informacion interna.
* Evitar proveer file extensions.


### Recavar informacion del atacante

Los logs sirven para btener infromacion del ataque, pero tambien pueden contener datos sensibles que un atacante podria intentar robar.

* **Loguear** por lo menos los authentication events
* Si realmente podes, Loguea todo
* Mantene los **logs encriptados**

### Configuracion de CORS


CORS permite que **Un servidor pueda indicarle a un browser que es seguro relajar las restricciones del Same-Origin-Policy para un request en particular**

Lo importante aca es que **Si no lo necesitas, no lo habilites** y si lo necesitas entonces tene en cuenta estas notas:

>Notas sobre seguridad
**Este protocolo solo sirve para protejer al usuario si el servidor implementa** 
* El protocolo HTTP de forma correcta, es decir lo los verbos **GET y HEAD son safe**
* Anty CSRF (tokens/nounces o otro mecanismo) para non-safe POSTS
* Sanitizacion del header `Origin` para evitar HTTP header inyection
* Se limita el acceso a CORS a los **origenes minimos necesarios** (salvo que sea un public API) usando alguna base de datos con los origenes permitidos o algun otro mecanismo
>
>Si **no necesitas** que tu API/HTTP server responda a requests de otros dominios, entonces **NO HABILITES CORS**, por default si no hay CORS HEADERS entonces los browsers van a rechazar los HTTP requests que se generen desde otros dominios hacia el tuyo.



## Identificacion de vectores de ataque

Los posibles vectores de ataque mas comunes son todos aquellos donde:

* se pueda colocar un input arbitrario en la aplicacion.
* Se puede obtener informacion sobre posibles vulnerabilidades

* **HTTP entry points**
	* URL Query strings
	* POST data
	* Cookies
	* HTTP headers 
	* Server banner
	

* **Encontrar pistas sobre el stack usado**
	* Estructura de URL (Wordpress, drupal, CMS)
	* Custom HTTP headers  
	* Fingerprinting software (httprint o otros) que intentan descubrir el stack
	* Mapear URLs para ubicar
		* File extensions
		* Folder directories
		* Otras pistas sobre la tecnologia usada
	 

* * **Intentar generar errores para obtener informacion**
	* Illegal characters en URL o querys 
	* Enviar Illegal requests en APIs tratando de generar errores


* **Los frameworks suelen ser seguros, busca el custom code del desarrollador**
	* Cosas que no encajan con el framework usado (naming conventions, GUI)
	* CAPCHAS, Debug functions
	* Parametros con nombres fuera del naming convention 
	* Comentarios en el source code

* **Web app attack vectors**
	* Client side validation (donde el server no valida el input)
	* Sql inyection
	* File uploading/downloading
	* Display de user-generated data (XSS)
	* Dynamic redirects (cuando la redireccion depende de algun parametro que un atacante podria modificar)
	* Session state
		* Predictable tokens
		* Insecure token handling
	* Weak authentication  
	* Known vulnerabilities on the stack
	* Email interaction (lograr inyectar un correo que no es)
	* Hidden fields que pueden ser modificados


## Bypassing Client-side controls

Si los datos son controlados unicamente por el client-side y no por el server-side, entonces un atacante puede aprovechar esto para inyectar parametros no controlados.

Esto es simple de evitar. **NO CONFIES EN EL CLIENT SIDE VALIDATION**

**Esto es trivial**

EJ:

* Hidden form values
	* Colocar el precio en el form de forma oculta y pedirlo de vuelta
* Confiar en el form verification (Email, phone y otros standard client side verifications)
* Disabled form elements 
* JS form validation


## Broken authentication

**Los problemas basicos son:**

* Contraseñas muy cortas o blank
* Contraseñas que son dictionary words
* Contraseñas en valores default
* Contraseñas identicas al username
* Error conditions que dan pistas
* Broken vulnerable password change system
* no hay proteccion para brute-force attacks
	* Capchas
	* **lock out** 
* Session ids predecibles
* Los admin panels no estan protegidos con autenticacion, solo con una URL que se espera que los usuarios no encuentren

**Los pasos minimos para asegurar la web app son:**

* **Lock out** Bloquear al usuario despues de una cantidad de intentos fallidos.
	* La logica del lock out debe estar en el server
* **Minimal password complexity** 

### Cambio de contraseñas

* Cuando te piden la contraseña antigua para el cambio de contraseña y las error conditions te dan idea si esta bien o mal.

* Cuando no tiene las protecciones de la pagina de autenticacion que evitan bruteforcing (por ej **lockout**)

* Cuando no notificas al usuario via email que se cambio la contraseña

### Forgotten password

* Preguntas de seguridad que se pueden bruteforcear
* Preguntas de seguridad escritas por el usuario

### Logging e identificacion de ataques

El servidor debe ser capaz de identificar los ataques a las interfaces de autenticacion

* Loguear los logins exitosos y fallidos
* Alertar sobre multiples intentos desde la misma IP
* Alertar sobre multiples intentos de login al mismo usuario

## Cross-site-scripting (XSS)

Consiste en **utilizar los medios que el sitio web tiene para que los usuarios publiquen contenido** (seccion de comentarios, posts, etc.) para colocar **HTML o JS** que sera **interpretado por los navegadores de terceros**. 

Posiblemente:
* **Robando sus cookies**
	* Accediendo a sus sesiones 
	* enviandolas a un server bajo el control del attacker
* **Engañando a los usuarios con contenido falso**
	* Phishing
	* Scamming 
	* Popups 
* **Usando JS como Keylogger** 


**Solucion minima:**
santitizar con alguna libreria para **XSS**
* **Inputs** de los usuarios al server
* **Outputs** del server que no deberian contener HTML o JS


### Reflected XSS attack

Es cuando podes colocar como input algo que el server devuelve sin sanitizar (**Refleja**).
Es posible reproducirlo e inyectar JS o HTML, si logras que la victima haga este request (ej, le mandas el link con una URL que lo hace) entonces la victima ejecutara el codigo de XSS

* Un mensaje de error que devuelve el input
* Parte de la URL que se refleja en la pagina web

> http://www.miforo.com/mensaje=<script>enviar cookie a otro dominio</script>

### DOM XSS attack

Explicacion: https://www.youtube.com/watch?v=j4nNx6IpWnk

Es cuando la pagina web permite la inyeccion local de codigo que refleja en el pagina.

El ejemplo mas comun es un fragmento en la URL, los fragmentos nunca se envian al server, pero si la web app lo usa para agregar algo al sitio web, entonces podes enviarle a la victima una URL con un fragmento artificial que se mostrara en la pagina web, y puede contener HTML o JS malicioso

> http://www.miforo.com/mensajeDeAlerta#<script>enviar cookie a otro dominio</script>

### Stored XSS attack

Es cuando guardas algo en el server (un comentario por ejemplo) que se ejecuta en los browsers de terceros

### XSS segun contexto

A veces no podes correr codigo arbitrario porque las defensas (filtros) de la aplicacion te lo evitan, pero tal vez parte del codigo esta en un tag que podes atacar (un img src por ejemplo)

### XSS - Deteccion

Podes detectar ocurrencias de XSS colocando un string en cada input, HTTP header y request y buscando en la respuesta si el string vuelve integro. A partir de eso tenes que ver en que contexto se usa ese string para ver si podes aprovecharlo para vulnerar la aplicacion.

### XSS - evasion de filtros

Aca hay data sobre diferentes trucos para evadir filtros de XSS
Cosas como encodear partes del script tag o event handler en **base64, hexa, html characters, unicode, etc**
https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet

### same-user XSS

Es cuando el ataque XSS esta restringido a una pagina que solo un usuario puede ver.
Inicialmente parece poco peligrosos, pero si el atacante logra inyectar su cookie a otro usuario o lograr que se autentique como el entonces el browser de la victima ejecutara el XSS


## Broken Session management


La **sesion** es la informacion que permite al usuario tener una experiencia personalizada, ademas permite identificar al usuario despues de la autenticacion.



### Tipos de sesiones
#### Cryptographic session

Es cuando la sesion se guarda encriptada en el client side, y solo puede ser desencriptada en el server side (**JWE**).


**Problemas principales:**

* La encriptacion debe ser segura 
* El cipher block mode of operation debe ser seguro
* Modificaciones pequeñas en el token podrian hacer que sea desencriptado como el userID de otro usuario 
* No debe ser posible modificar el token sin que esto sea detectable por el server
* No caducar las sesiones (en aplicaciones sensibles)
* **Si se filtra la key con la que encriptas los tokens, es catastrofico**
* **No reutilizar el algoritmo de encriptacion en otro lado**

**Soluciones**

* **Lock out**al probar varios tokens invalidos
	* **Firmar** los tokens y bloquear IPs que intentan ingresar con ifrmas invalidas

#### Session token / ID

La sesion se guarda en el server-side y se le da al client side un identificador unico que permite asociar al client side con esa sesion.

**Problemas principales:**

* El token que usas para identificar la sesion es:
	* Muy corto y se puede brutforcear
	* Predecible
		* Es una secuancia de numeros
		* Tiene que ver con fechas o el tiempo
		* Usa un RNG debil ó no criptografico 
* El token se maneja de forma poco segura 
	* Mal manejo de cookies
	* No usar https
* No caducar los tokens
* **No usar TLS**

**Soluciones**
* Usar un token **largo y un RNG fuerte**
* Caducar los tokens
* Guardar los tokens en client side en lugares seguros
	* Cookies con httpOnly y Secure 
* **Firmar** los tokens para poder detectar intentos de login con tokens invalidos y bloquear la IP 


### Ataques y vulnerabilidades

#### En general


* **Mal manejo del token o sessionID**
	* No usar un token y guardar la sesion en plaintext en el user agent
	* No proteger contra el robo de token via **XSS**
	* No proteger contra **CSRF**
	* No colocar tokens en logs que podrian ser roabados
	* No usar HTTPS en todos lados
	* No usar **HttpOnly** y **secure** cookies
	* No invalidar las sesiones del lado del server al hacer logout
	* Poner session IDs en la URL


* **Token o sessionID vulnerable**
	* Predecible
	* Desencriptable
	* Modificable facilmente 
	* Facil de brutforcear/ sin lock up automatico
	* No proveer un nuevo session ID en cada login


#### SessionID brutefrocer

Los ataques que consisten en intentar muchos SessionIDs son ataques de fuerza bruta.
Hay varias formas de determinar que los sessionIDs son aleatorios y no son SessionIDs viejos.

* **Firmar** el token, para verificar que el servidor no fue quien lo creo.

### Session fixation

Es cuando el browser tiene un session token  (en una cookie por ejemplo) y al loguearse nuevamente al sitio web, el servidor valida **ese mismo token** para esa sesion **en lugar de asignar un nuevo token**

Si logras **inyectar un session ID** conocido entonces podes esperar a que el usuario se loguee y tenes acceso a su cuenta usando ese session ID.

**La inyeccion se puede hacer mediante:**
* **XSS** Si el ID esta en una cookie sin HttpOnly
* **XSRF** Si 
	* El session ID esta en un hidden form value
	* El session ID esta en la URL

**Solucion:**
* Cambiar el token en cada login
* Invalidar el token viejo


### Logout y token/cookie reuse

Es el uso de tokens viejos para acceder a la cuenta de un usuario si es que todavia son validos del lado del server. Muchos servicios nunca invalidan sus tokens

Los sessionIDs deben ser **borrados del server o invalidados**, no solo borrados del client side.

* **Log out** - Deberia invalidar el token en el server
* **Expiracion** - Si el token expira en el cliente tambien deberia expirar al mismo tiempo en el server

## Access control

Consiste en saber en todo momento quien es el usuario, y limitar sus capacidades dependiendo de su rol. 

**El codigo de Access control debe estar centralizado** en el codebase que ejecuta el servidor para: 

* Evitar que el desarrollador tenga que **copiar codigo para implementarlo** en cada endpoint/pagina
* Mantener el **Access control uniforme** en toda la aplicacion


**Un buen access control:**
* Verificar la **identidad** del usuario en cada request
* Verificar las **capacidades** del usuario para cada request

Los ataques sobre el acces control son:

* **Vertical** priviledge escalation
	* Permitirle a un usuario mas privilegios de los que deberia tener (user a admin)
* **Horizontal** priviledge escalation
	* Permite al usuario privilegios de otro usuario   (user1 a user2)


### Unsecured direct object access

Consiste en tener un recurso no protegido  asumiendo que mientras la URL no sea conocida, no sera usado por los usuarios.

* Admin panels
* Admin function
* Imagenes, docs,pdfs con URLs

## Inyection


Es la inyeccion de codigo en alguno de los Input fields de la aplicacion que puede luego ser mal interpretado por el servidor.

https://www.youtube.com/watch?v=0gCYar3GAmw


### SQL Inyection

Es cuando se inyecta codigo SQL inesperado en un input field.


#### Parametrized querys

Los Adaptadores entre lenguaje y base de datos tienen la capacidad de generar "prepared statements"
SQL prepared statements / parametrized statements

#### ORMs

Muchos frameworks tienen ORMs que evitan el sql inyection

#### Privilegios

Las querys deben correr con los privilegios minimos necesarios para hacer su tarea, de esta forma si un atacante logra inyectar codigo, los daños seran limitados

### NOSQL Inyection

Entender mongoDB

### Shell Command inyection

Es una vulnerabilidad que se da cuando la aplicacion envia algun input a un shell del server, es re picante

Entender sobre linux server administration
https://www.youtube.com/watch?v=MM5HdaxqXvg

### Command inyection

Es cuando podes inyectar codigo arbitrario, por ejemplo cuando se coloca algo sin sanitizar como parametro en PHP.

Ej:
Podes inyectar valores no esperados en el query, que son evaluados por PHP
> http://retentionpanel.com/view_order.php?submit=4;exit()


### SMTP Inyection

Cuando tenes un from que envia un email, el protocolo SMTP es muy simple y si estas alimentando con el imput del usuario el mail entonces un atacante podria usarlo para enviar spam.

Principalmente se deben **filtrar los new lines** para evitar crear strings que puedan ser interpretados por SMTP como varios mails

## Back-end attack

Ver cuando sepa Linux administration y apache

https://www.youtube.com/watch?v=MM5HdaxqXvg&list=PL7gCgFw1RV1M6vJFX1RPDhgPZbg9qU3ub&index=18

https://www.youtube.com/watch?v=mgDcP6bXtJE&list=PL7gCgFw1RV1M6vJFX1RPDhgPZbg9qU3ub&index=19

## Site Request Forgery 

Se trata de una familia de ataques que consisten en hacerle pensar al browser que el usuario desea realizar una accion con un sitio, entonces el browser envia la cookie de ese sitio.

>Este ataque solo puede efectuarse cuando se usa **autenticacion automatica** mediante **cookies, HTTP basic o cualquier cosa que pueda hacer que el browser envie automaticamente credenciales.**
>Los **REST APIS**, que usan tokens como parametros, **NO SON VULNERABLES A REQUEST FORGERIES**

En general **las contramedidas ya estan siendo usadas por frameworks**

### On-Site-Request-Forgery (OSRF)

Es una forma de aprovechar un ataque **stored XSS** para realizar un ataque de request forgery.

Estos ataques suceden dentro del sitio que se desea atacar

* Se añade, via XSS, algo que haga que el browser haga un **request que el usuario no solicito.**
	* **Img tag** con `src=/cambiarMail?nuevoMail=owned@owned.com `
	* **Un link** al que el usuario apreta y lo manda a `/cambiarMail?nuevoMail=owned@owned.com `

**Soluciones**
* Validar siempre el user input
* Filtrar caracteres especiales `/ . \ ? & =`


### Cross-Site-Request-Forgery (CSRF)


**El atacante crea un sitio web con un link/form que se submitea sola/js/img con src/otra cosa que genera un request al sitio atacado.**
El browser envia la solicitud con la cookie que corresponda, autorizando el request, que podria cambiar una contraseña, mail, comprar algo, etc

**Solucion:**
* Agregar un token aleatorio que cambia con cada refresh a cada form
* Enviar el token cuando se submitea el form
* Verificar que el token enviado es el mismo que el recibido

Mientras el atacante no pueda determinar el valor del token con anticipacion, no podra hacer ataques de CSRF

![](https://i.imgur.com/goHbK6P.jpg)

### UI redressing

Se trata de ataques que escondel el UI de la pagina victima y coloca algo encima que hace que el usuario haga algo que no desea

#### ClickJacking

Se coloca la pagina victima como un **Iframe transparente** por encima de la pagina del atacante. se colocal UI de tal forma que la victima haga clicks en el UI de la pagina atacada para realizar acciones que no eran las deseadas. (Hacer compras, etc)

**Solucion:**
El HTTP header **X-Frame-Options** con valor
* X-Frame-Options: DENY
* X-Frame-Options: SAMEORIGIN

Evita que la pagina sea cargada como un Iframe 

#### Reverse strokeJacking

Es cuando hay un Iframe transparente que tiene el focus, y usa JS para detectar las teclas que apretas, a su vez JS añade tus inputs en los campos adecuados, para que parezca que todo funciona normalmente

## HTTP header inyection / HTTP Response Splitting

Los servidores HTTP modernos no son vulnerables a esto, pero nuevos trends (**node con express por ejemplo** pueden ser vulnerables.

Se da cuando alguna parte de la aplicacion permite que el usuario agregue _algo_ como un header 

>EJ: 
>* Parametros o preferencias del usuario guardados en una cookie
>* Un producto con un nombre malicioso, con un carrito de compras implementado con cookies

Si este es el caso entonces un atacante podria escribir mucho mas que el header, ya que si podes poner **line breaks** entonces podes inyectar todos los headers que quieras o incluso **una pagina web entera**

### Combinacion con same-user XSS

Si es posible hacer XSS hacia uno mismo, y aemas existe un HTTP header inyection vulnerability, entonces podes **inyectar tu sesion a un tercero y van a ejecutar el codigo del XSS**


## Open redirects

Es cuando la pagina web usa alguno de los siguientes para determinar a donde redirige

* User inputs
* URL
* JS (via XSS)
* HTML (via la <meta> tag, usando XSS)


Por ejemplo, cuando un parametro de la URL o un HTTP Header indica a donde redirigir.
Un atacante podria proveer un link al sitio atacado que redirija a un sitio de phishing.

**Soluciones:**
* No tener open redirects
* Filtrar el user input para no permitir absolute URLs (urls que empiecen con HTTP, www, etc. solo que empiecen con **/**)
	* No recomendable. blacklisting en general es choto




## window.Opener hijacking

Cuando abris un link en una pestaña nueva, [Window.opener](https://developer.mozilla.org/en-US/docs/Web/API/Window/opener) permite que la nueva pestaña tenga algunos controles sobre la anterior, estre estos puede **redireccionar la pestaña anterior**, esto se puede usar para phishing (cuando el usuario cierre la pestaña y vuelva a la pestaña anterior, se encontrara con otra pagina)

**Solucion:**
En el anchor tag, usar siempre **rel="noopener"** para evitar que el sitio al que mandamos al usuario tenga control sobre nuestra pestaña.

## Unsafe deserialization 

[Ejemplos con PHP](https://www.owasp.org/index.php/PHP_Object_Injection)
La serealizacion es el proceso de transformar un objeto/array/funcion/clase en un string que se pueda guardar en una base de datos (un campo string en SQL por ejemplo) o que se pueda enviar por una red.

Cuando Deserealizas, transformas ese string nuevamente en un objeto/array/funcion/clase con el mismo nombre que tenia antes, basicamente estas **inyectando una nueva variable/clase/funcion**

Esto significa que un atacante puede instanciar una clase del programa (esto requiere saber de antemano que tenes que sobreescribir).


Si el atacante puede inyectar arbitrariamente datos que seran deserealizados sin sanitizar, y esos datos son ejecutados (ej instancias un objeto con un constructor ), el atacante tendra la posibilidad de **inyectar codigo arbitrario**

## Unrestricted file upload

Permitir que los usuarios suban archivos al servidor implica un gran riesgo, ya que si esos archivos son luego accesibles a los usuarios, un atacante podria **inyectar codigo malicioso** que el servidor pordia ejecutar.  Esto implica que **es facil escalar de unrestricted file upload a code execution**

Algunas formas de controlar los archvios subidos al server son:

* **Evitarlo totalmente** - No permitir uploads
* **Tercerizarlo** - No tener los archivos en el server, usar algun servicio (AWS S3)
* **Guardarlo localmente** - Guardar el archivo en el servidor
	* **Descartar el nombre del archivo** 
		*  Podria tener una extension peligrosa o un nombre que intente aprovechar el filesystem para hacer path traversal.
		*  Renombrarlo a un hash sin extension, guardar el nombre en una base de datos asociado a ese hash para poder recuperarlo luego
	* **Guardar fuera del webroot** - Guardar los archivos fuera del directorio publico del servidor para evitar que intente ejecutarlos
	* **Guardar en carpeta sin permiso de ejecucion** 
	* **Verificar la extension del archivo con un whitelist**
	* **Colocar un tamaño maximo**
	* **Escanearlo con un AV para sumarle seguridad al usuario que lo descargue**



## Browser enforced security


### same-origin-policy 


**Glosario:**

* **Origin** - Definido como **port, hostname, protocol**

Se trata de una serie de politicas que evitan que se realicen acciones entre dos origenes distintos. Ejemplos son:

 * Iframes con origenes distintos no se pueden hablar mediante JS
 * No se permiten AJAX requests del sitio $$A$$ hacia el sitio $$B$$
 * El JS del sitio $$A$$ no puede acceder al local storage, cookies, etc del sitio $$B$$
 * El JS de la pestaña $$A$$ no puede hablar con el de la pestaña $$B$$


#### Iframes y Cross-document messaging

Un Iframe que tiene un origen distinto al de la pagina que la contiene esta protegida por la same-origin-policy.
**El browser no le permitira al JS de la pagina contenedora acceder al Iframe y modificar su contenido.**

>Esta defensa **se puede circumventar** de forma segura con [la funcion postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage), que genera eventos en el child iframe que el parent iframe puede escuchar. tambien sirve para pop-ups. 
>
>Al usar esta funcion, Se deben tomar los siguientes pasos para evitar generar una vulnerabilidad
>*  **validar el origen** con la propiedad _event.origin_ del evento
>* **Indicar el destino**  con el segundo parametro de la funcion postMessage
> 	* postMessage(mensaje, DESTINO)
>
>Si no lo haces, cualquiera podria, desde cualquier origen, abrir tu pop-up o Iframe y recavar los datos que querias enviar a TU parent
> $$\scriptsize{\href{(https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage}{\text{Fuente}}}\\
\scriptsize{\href{(https://www.youtube.com/watch?v=XTKqQ9mhcgM}{\text{Video explicativo}}}$$


#### HTTP requests

El browser rechaza el envio de requests HTTP a un dominio diferente al dominio de origen como parte de la politica same-origin-policy. Se puede realizar excepciones usando el **protocolo CORS** 

>Cualquier solicitud a un dominio diferente al origen puede ser sujeta al **Protocolo CORS**, que permite la relajacion del same-origin-policy si el servidor da permiso


Algunos de los requests que **no limita por default:**

* `<script src="..."></script>` - Javascript desde el HTML document con script tags
* `<link rel="stylesheet" href="...">` - CSS
* `<img>`
* `<video> and <audio>`
* @font-face
* `<frame> and <iframe>` sin un header `X-Frame-Options`




---

###  Content security policy

Su proposito es proteger al usuario de XSS, CSRF e inyeccion de contenido mediante


* Un **HTTP header con atributos llamados directiva** que le indican al browser
	* **Desde que origenes se puede cargar contenido**  indicandole al browser mediante headers de que origenes se pueden cargar recursos (scipts, css, imagenes, etc)
		* Incluidos los in-line scripts, que son desactivados por default 
	* **A que origenes se puede enviar requests** EJ: Desde la pagina de LOGIN, solo enviar POSTS a `www.miSitio.com`
	* **A donde reportar** si hay un error en estas politicas.


**POLITICAS EN EL HEADER:**

**Este HTTP Header contiene la politica** a utilizar por el browser,
en forma de **directivas** separadas por `;`, los Atributos de cada directiva estan separados por un espacio
```
Content-Security-Policy: directiva1 atributo 1  atributo 2;directiva2;directiva3;
//Line breaks añadidos para facilitar lectura
Content-Security-Policy: default-src 'self' WWW.ejemplo.com www.google.com;
						img-src *; 
						media-src media1.com media2.com;
						script-src userscripts.example.com
```
Podes tener **multiples headers**, si las politicas de ambos se contradicen, entonces se usara la directiva **mas restrictiva**
```
Content-Security-Policy: connect-src 'none';	//Esta toma presencia por ser mas
												//restrictiva
Content-Security-Policy: connect-src http://example.com;
```

**POLITICAS EN EL HTML DOCUMENT:**

**Alternativamente** se pueden colocar CSP utilizando el `<meta>` tag
```
<meta http-equiv="Content-Security-Policy"
content=" directiva 1; directiva 2; directiva 3;"
>
```

#### Scope de CSP

**Las CSP tienen un scope que se limita a la pagina abierta en ese momento.** es decir que
 `www.ejemplo.com/index.html` y `www.ejemplo.com/login.html` **pueden tener diferentes SCP directives**

CSP bloquea por default los **in-line scripts**



#### Politicas disponibles

Las siguientes politicas (tambien llamadas **"directivas"**) se pueden colocar tanto en el `Content-Security-Policy` **header** como en el `<meta>` tag.
	
A menos que se indique lo contario, **TODAS** las constantes de SCP pueden utilizarse como parametros para las directiva.

>**Las directivas se dividen en 5 grupos**
>* **Fetch** - Indican al browser a donde puede ir a buscar recursos (img, scripts, css)
>* **Document** - Indican propiedades de la pagina web.
>* **Navegation** - indican a donde se puede ir desde esta pagina web y quienes pueden colocarla en un Iframe
>* **Reports** - Indican como realizar los reportes
>* **Miscelaneas** - Dan otras indicaciones


**DIRECTIVAS DE FETCH:**

Estas directivas indican de donde puede solicitarse un recurso.
* **default-src** - Sirve como fallback para todos los resource que no tengan una directiva definida (imagenes, scripts, etc)
* **frame-src** - Indica que origenes se pueden embeber en un Iframe
	* 'none' es particularmente util aca
* **worker-src** - Indica Origenes validos para web-workers
* **connect-src** - Indica a que URLs se puede conectar AJAX, webSocket y EventSource
* **font-src** - Indica origenes validos para @font-face 
* **img-src** - Indica origenes validos para imagenes y favicons
* **manifest-src** - Indica origenes validos para manifest files
* **media-src** - Indica origenes validos para `<audio>`, `<video>` y `<track>`
* **object-src** - Indica origenes para `<object>`, `<embed>` y `<applet>`
* **script-src** - Indica origenes validos para javscript
	* **'report-sample'** - Si los reportes estan activados, Envia una muestra del codigo junto con el reporte de violacion de directivas
* **style-src** - Indica origenes validos para CSS


**DIRECTIVAS DE DOCUMENT:**

Estas directivas limitan ciertas propiedades del HTML document

* **base-uri** - Indica que origenes se pueden usar como `base-uri`
* **sandbox** - Solicita un sandbox para esta pagina, esto limita las acciones de la pagina. Los siguientes permisos seran negados salvo que esten explicitamente escritos
	*  **allow-forms** - Permite que la pagina submitee forms
	*  **allow-modals** - Permite que la pagina abra modals
	*  **allow-orientation-lock** - permite que la pagina evite la rotacion de la pantalla en mobiles
	*  **allow-pointer-lock** - Permite el uso del pointer lock API
	*  **allow-popups** - permite popups (`window.open`, `target="_blank"`, `showModalDialog`)
	*  **allow-popups-to-escape-sandbox** - Permite que los popups abiertos no esten en el sandbox
	*  **allow-presentation** - Permite el uso del [Presentation API](https://www.w3.org/TR/presentation-api/)
	*  **allow-same-origin**
	*  **allow-scripts** - Permite el uso descripts
	*  **allow-top-navigation**
* **disown-opener** - Solicita al browser que, si abre nuevas ventanas desde esta ventana, NO provea a la nueva ventana una referencia a la ventana anterior mediante `window.opener`. esto evita el ataque conocido como **window.Opener hijacking**
 

**directivas DE NAVEGATION:**

Estas directivas indican a donde puede navegar el browser desde esta pagina.

* **form-action** - Indica a que Origenes se puede hacer submit a un form
* **frame-ancestors** - Indica quienes pueden embeber esta pagina en un Iframe. es similar a **X-Frame-Options**
* **navigation-to** - Indica a que origenes puede navegar el navegador desde esta pagina (mediante window.location, window.opener, <a>, form submit o cualquier otro metodo)

**DIRECTIVAS DE REPORTS:**

Le indica al browser a donde enviar un report si alguna de las directivas tuvo que ser activada.

* **report-uri / report-to** - Indica a que URL enviar el reporte. report-to reemplazara a report-uri en el futuro
	* Json object que indica como hacer el reporte (en report-to)


**DIRECTIVAS MISCELANEAS:**

* **block-all-mixed-content** - Bloquea todo contenido que no este en HTTPS
* **require-sri-for** - Bloquea todos los recursos que se llamen sin un [hash de integridad](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)
``` 
<script src="EJ.com/script.js"
integrity="sha384oqVuAfXRKap7fdgcCYblablabla">
</script>
```
* **upgrade-insecure-requests** - Carga todos los recursos con HTTPS aunque tengan su src en HTTP. si no estan disponibles en HTTPS entonces no los carga. No modifica los anchor tags



#### Propiedades utilizables en las directivas



* **URL** - una o varias urls
```
default-src: www.google.com www.ejemplo.com www.otro.com
```
* **'self'** - Indica el dominio del que viene el documento
```
default-src: 'self'
```

* **wildcards** - Indica subdominios o cualquier dominio, dependiendo del contexto
```
default-src: 'self' *.miDominio.com // Indica un subdominio
default-src: * // Indica cualquier dominio
```

* **Combinado** - Una combinacion de cualquiera de los 3 anteriores
```
default-src: 'self' www.google.com *.api.com // Cualquiera de estos
```


* **'none'** - Indica ninguno.
```
default-src: 'none'
```



*  **Schemes** - Indica el protocolo del cual se puede cargar el recurso
	*   'http:', 'https:'
	* 'data:'
	* 'mediastream'
	* 'blob'
	* 'filesystem'
	* 'self'
```
default-src: 'https' *.miDominio.com // solo cargar cosas en HTTPS y en mi dominio
default-src: 'https' //solo cargar cosas en HTTPS
```

* **Permisos para recursos in-line**
	*  **'unsafe-inline'** - Indica que permite in-line scripts ó styles
	*  **'unsafe-eval'** - Indica que permitel uso de `eval()`
	*  **'nonce-valorCriptograficoAcaBase64'** - Usa el NumberUsedOnce indicado despues del guion como indicador de que un in-line script/stype es seguro
```
	Content-Security-Policy: connect-src 'nonce-2726c7f26c'
	<script nonce="2726c7f26c">var inline = 1;</script>
```
	*  **un Hash** - El hash del inline script/style, el browser computara el hash del in-line script y lo comparara con este valor.
```
	  Content-Security-Policy: script-src 'sha256-B2yPHKaXnvFWtRChIbabYmUBFZdVfKKXHbWtWidDVF8='
```
	* **'strict-dynamic'** - Implica que los scripts cargados por aquellos in-line scripts autorizados con un hash o un nonce seran de confianza por el browser




#### SCP reports 

>report-uri esta **depricated**, use **report-to** en su lugar cuando consideres que report-to tiene suficiente traccion en todos los navegadores y existe buena documentacion de como usarlo.


**Se puede configurar al browser de tal forma que envie un reporte cada vez que ocurra una violacion a las SCP**.

El reporte sera enviado automaticamente en forma de **JSON** a una URL especifica usando la directiva **report-uri**.

```
Content-Security-Policy: 
				default-src 'self'; 
				report-to http://reportcollector.example.com/collector.cgi
```

**Reporte:**
```
{
  "csp-report": {
    "document-uri": "http://miSitio.com/signup.html",
	"disposition":"enforce"
    "referrer": "",
    "blocked-uri": "http://example.com/css/style.css", // URL bloqueada por CSP
    "violated-directive": "style-src cdn.example.com",
    "original-policy": "default-src 'none'; style-src cdn.example.com; report-uri /_/csp-reports"
  }
}
```

**Los siguientes elementos pueden aparecer en el reporte, dependiendo de la configuracion de report-uri:**
* **blocked-uri** - La url bloqueada (Ej: el src de una imagen, el src de un script tag
* **disposition** - Indica si la CSP que genero el reporte esta en modo de prueba o no
	* **"reporting"** - PRUEBA, Causado por `Content-Security-Policy-Report-Only`
	* **"enforce"** - REAL, Causado por `Content-Security-Policy`
* **document-uri** - URL de la pagina donde ocurrio la violacion
* **effective-directive** - el nombre de la directiva que corresponde a la violacion
* **violated-directive** - El nombre y parametro de la directiva que fue violada
* **original-policy** - Las directivas activa en la pagina al momento de la violacion
*  **referrer** - El campo HTTP referer de la pagina donde ocurrio la violacion
*  **script-sample** - Los primeros 40 chars del script o estilo que causo la violacion
*  **status-code** - El HTTP code dela pagina


#### SCP testing


Se puede configurar las SCP para que no sean efectivas, sino que unicamente generen repotes de error, esto sirve para evitar romper el sitio al introducir nuevas politicas.
Para esto usamos **Content-Security-Policy-Report-Only:**
```
Content-Security-Policy-Report-Only:: default-src 'self';
```

### HSTS - Strict Transport Security

Indicada en [  HTTP Strict Transport Security (HSTS) - RFC 6797](https://tools.ietf.org/html/rfc6797)

>**HSTS** es un mecanismo que tiene un sitio web de indicarle al browser que **nunca debe conectarse a este dominio mediante HTTP**, sino unicamente mediante HTTPS


#### HSTS Header
El servidor indica al user-agent que tiene prohibido intentar comunicarse mediante HTTP usando el HTTP header  Strict-Transport-Security.
```
Strict-Transport-Security
```

**HSTS SE PUEDE CONFIGURAR CON LAS SIGUIENTES DIRECTIVAS:**

* **max-age** - Tiempo en segundos en el que expirara la politica de HSTS.
	* un valor de **0** indica al user agent que debe remover a este host de su lista de hosts que usan HSTS
```
	strict-Transport-Security: max-age=31536000
```
* **includeSubDomains**- Indica al browser que la politica de HSTS aplica a los subdominios tambien
```
	 Strict-Transport-Security: max-age=15768000 ; includeSubDomains
```

#### Funcionamiento 

**USER AGENT:**

Al intentar ingresar a un sitio mediante HTTP, el user agent:

**Funcionamiento del user agent:**

* **User agent intenta entrar a un sitio con HTTP**
	* Esta en la lista de hosts conocidos que indicaron HSTS
		* Intenta entrar mediante HTTPS
		* si no lo logra entonces **no entra al sitio.**
	* Si no esta en la lista, 
		* **entra al sitio**  
		
		
* **User agent conecta mediante HTTPS sin errores y recibe header HSTS** 
	* Agrega al sitio a la lista de HSTS hosts si no estaba ahi.
	* Actualiza el max-age y includeSubDomains que tenga almacenados usando el header


* **User agent conecta mediante HTTP y recibe header HSTS**
	* User agent **ignora** el header. 


**SERVER:**

* **Intento de conexion con HTTP**
	* Respuesta con permanent redirect **CODE 301** al mismo sitio pero con HTTPS.


### Referrer-Policy

El Referrer-Policy es un header que permite al servidor indicarle al browser que colocar en el HTTP header "referer" cuando es redirigido de esta pagina.


>El objetivo principal de Referrer-Policy es **mantener la privacidad** del usuario, Y en algunos casos evitar **Filtrar urls con tokens**
>
Ejemplos: 
* Si apretas en un link en facebook a otro sitio, no queres que se envie la URL de tu perfil
* Si entras en una URL que es un token (password reset, etc) no queres que el usuario la filtre navegando a otro lado

* **Referrer-Policy** - El HTTP header que el server envia.
	*  **origin**
	Solo enviar el origen como referer (https://example.com/ en lugar de https://example.com/page.html)
	*  **no-referrer** -	 Indica al browser nunca colocar referrer
	*  **[DEFAULT] no-referrer-when-downgrade** 
	Indica al browser no colocar referrer si pasa de HTTPs a HTTP
	*  **strict-origin** - Envia el origin como referrer, no envia nada si pasas de HTTP a HTTPS
	*  **strict-origin-when-cross-origin** 
	Enviar referer a paginas del mismo dominio, enviar origen a paginas de otro dominio salvo que pasen de HTTPS a HTTP
	* **origin-when-cross-origin**
	Enviar referer completo al navegar a paginas en este dominio, enviar solo origin al navegar a paginas de otro dominio
	* **same-origin** - No enviar referer al navegar a otro dominio
	* **[NO SEGURO] unsafe-url** - Enviar toda la URL como referer siempre 

[FUENTES](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)

**Ejempos:**
```
Referrer-Policy: no-referrer
Referrer-Policy: no-referrer-when-downgrade
Referrer-Policy: strict-origin-when-cross-origin
Referrer-Policy: unsafe-url
```

### XSS Auditor

Algunos browsers (chrome, IE, Opera) tienen sistemas de defensa contra XSS integrados llamados **XSS Auditor** que en general estan **activados por default**, pero pueden ser **activados y configurados por el servidor** con el HTTP Header **X-XSS-Protection**.

Funciona principalmente buscando script tags en los requests enviados que sean reflejados en las respuestas del usuario.

**Niveles de proteccion:**

* **0** - Proteccion XSS Desactivada
* **1; mode=block** - Proteccion activada, en caso de deteccion bloquear la pagina
* **1; report=URL-Para-Enviar-Reporte [SOLO CHROME]** 
Proteccion activada, en caso de deteccion sanitizar la pagina y reportar el incidente, usa el mismo mecanismo que la CSP report-uri.

EJ:
```
X-XSS-Protection: 1; mode=block
```


## Logging y monitoring

### Eventos a loguear

La aplicacion que crees debe tener logging para los eventos de seguridad que sean relevantes, y de ser necesario enviar alertas.

* **Error de validacion** - Se encontro un valor que se tuvo que sanitizar o que se rechazo
* **Autenticacion exitosa o fallida**
* **Se denego el acceso a un recurso** - Authorization (access control) failures
* **Error de sesion management** - SessionID invalido o modificado
* **Errores de la aplicacion** - syntax errors, runtime errors, file system errors, etc
* **Startup y shutdown** - Cuando la aplicacion es iniciada o terminada,cuando inicia el logging, inicio, pausa y detencion de sistemas perifericos, base de datos, etc
* **Funciones de alto riesgo** 
	* Añadir, editar o remover usuarios
	* Cambios de privilegios
	* asignar, añadir o remover tokens
	* Uso de privilegios administrativos
	* Accesos al admin backend de la aplicacion
	* Pagos, acceso a informacion de pagos
	* Cambios de claves criptograficas o uso de criptogriafia dentro de la app
	* Importar/exportar datos
	* Subida de archivos o otro user generated content
* **Uso excesivo**  


### Proteccion de logs

Los logs suelen tener **informacion sensible** y deben ser protegidos.

Es indispensable que el medio  donde se guardan los logs no tenga la capacidad de **lectura ni borrado, El unico permiso necesario es de escritura**

Dependiendo del medio donde se guarden, las estrategias pueden ser diferentes:

* **Filesystem**
	* Una carpeta con unicamente permiso de escritura para la web app.
	* Fuera del webroot, no accesible desde internet.
* **Database**
	* Una cuenta solo con permisos para agregar logs, no para editar ni borrar
	* Sin capacidad de tocar ninguna otra tabla, funciones o comandos
	* Ninguna otra cuenta accesible a la web app debe ser capaz de tocar los logs 


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU5MDE3NjQwNSwtMTY3MzgyNDY3Nl19
-->