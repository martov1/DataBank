 
**Oauth y vulnerabilidades**
https://www.youtube.com/watch?v=x8F9ms-uMbU

**VER:**
* Peppering the password
	*  https://security.stackexchange.com/questions/3272/password-hashing-add-salt-pepper-or-is-salt-enough

**Formas de autenticacion**
https://docs.google.com/spreadsheets/d/1tAX5ZJzluilhoYKjra-uHbMCZraaQkqIHl3RIQ8mVkM/edit#gid=0


# User and password

## Mecanismo

En una conexion con TLS, el usuario envia mediante HTTP el usuario y la contraseña.
El server, mediante un salted hash, lo guarda o lo compara en la base de datos.
En caso de que se admita el acceso, se provee al usuario una sesion que dura un tiempo X, para evitar que tenga que volver a enviar las credenciales con cada solicitud.

Las funciones minimas de seguridad son:
* **Minimum password complexity**
* **Account lockout after X tries**

## Almacenamiento de contraseñas 

>Fuentes
>https://www.youtube.com/watch?v=8ZtInClXe1Q
https://security.stackexchange.com/questions/211/how-to-securely-hash-passwords
https://crackstation.net/hashing-security.htm

Un almacenamiento correcto de las contraseñas evita que, en caso de que la base de datos sea comprometida, un atacante tenga acceso a las contraseñas de los usuarios

**Para esto, las contraseñas no deben:**
* Almacenarse en plain text
* Encriptarse (la key estaria en el server, seria accesible al atacante)
* Hashearse y almacenar el hash (con ningun algoritmo)
* Hashearse con un salt usando una fucion de hashing normal (son muy rapidas)

**Las contraseñas deben:**
* Almacenarse como **salted hashes** usando **algoritmos para ese fin**, los cuales son
	* **lentos** - para evitar ataques de procesamiento
		* Brute force 
		* Dictionary attacks
	* **con salts largos y criptoseguros** - Para inutilizar las tablas precomputadas 
		* Rainbow tables
		* Rash tables
		* Hellman's tables


**Algunos ejemplos de estos algoritmos son**
* **PBKDF2**
* **bcrypt**
* **scrypt**



## Ataques Online

Un servidor puede ser atacado sin much dificultad mediante **Fuerza bruta** o **contraseñas populares**, por eso es importante limitar la velocidad con la que se pueden probar contraseñas. Colocar **un limite** de $$X$$ contraseñas cada $$T$$ tiempo ayuda a mitigar esto. Es importante elegir  $$X,T$$ de tal forma que no generen con facilidad un ataque de **DDOS**



## Ataques offline

Si un atacante logra vulnerar la base de datos (mediante SQL inyection por ejemplo) y logra s**ubstraer el listado de usuarios y sus respectivos hashes de contraseñas y salts si los hubiera**, es posible que pueda intentar extraer las contraseñas a partir de esos hashes. esto se hace en su propia computadora sin conexion al servidor.

Si las contraseñas usaron algoritmos lentos y salts de forma correcta entonces la base de datos sera resistente contra estos ataques.

### Paralelismo y time-space tradeoff

 * **Paralelismo** 
 Ver un hash existe en alguna entrada de la base de datos robada es muy rapido.
 El atacante puede generar hashes con valores conocidos, cada hash puede ser buscado en toda la base de datos robada muy rapido. Esta ventaja se puede evitar con un **salt**
 
 Un **salt diferente para cada contraseña remueve el paralelismo**, entonces tenes que intentar crackear las contraseñas una por una, generando un candidato a contraseña, agregandole uno de los salts en la base de datos y probando todas las combinaciones posibles de contraseñas.
 
 * **time-space tradeoff** - Es mas rapido buscar hashes en una tabla precomputada que computarlos en el momento. 

### Brute force 

Consiste en calcular hashes de todas las combinaciones de caracteres posibles e ir buscandolos en la base de datos. 

* El **paralelismo** y la **velocidad de la funcion de hashing** hace que este ataque sea mucho mas factible.
* Un **salt** remueve el paralelismo, entonces tenes que intentar crackear las contraseñas una por una.

### Diccionario y Diccionario con reglas 

Consiste en calcular hashes de palabras, combinaciones de palabras o palabras con modificaciones predecibles (L337, mayusculas alternadas, numeros atras y adelante)

* El **paralelismo** y la **velocidad de la funcion de hashing** hace que este ataque sea mucho mas factible.
* Un **salt** remueve el paralelismo, entonces tenes que intentar crackear las contraseñas una por una.

### Hash table

Consiste en utilizar gran poder de computo durante mucho tiempo para crear tablas que consisten en posibles contraseñas y sus respectivos hashes, en general son prohibitivamente grandes salvo para contraseñas de pocos caracteres

>* El uso de **un salt unico por contraseña** hace que este ataque sea irrelevante, porque tendrias que crear una tabla con todas las posibles contraseñas para cada salt, y seria prohibitivamente grande.
>>* El uso de **un salt unico** (ej si tenes solo una contraseña) hace que el atacnate tenga que computar una tabla nueva (muy muy costoso, es mas facil hacer brute force)
>
* La **velocidad de la funcion de hashing** permite que estas tablas puedan computarse en tiempos relevantes.


### Hellman's time-memory trade-off tables

[Ver mas aca](https://en.wikipedia.org/wiki/Rainbow_table#Precomputed_hash_chains)

Como los hash tables pueden tener tamaños que no pueden ser almacenados en el hardware moderno, esta tecnica consiste en ** en un punto medio entre:** 

*  Las **hash tables**, que utlizan **memoria**,
* Los ataques que utilizan **tiempo** como **brute force, diccionario y diccionario con reglas**.

Son, en sintesis, una forma de **guardar un hash table de una manera que ocupe poco espacio a cambio de sacrificar tiempo de procesamiento**

>* El uso de **un salt unico por contraseña** hace que este ataque sea irrelevante, porque tendrias que crear una tabla con todas las posibles contraseñas para cada salt, y seria prohibitivamente grande.
>>* El uso de **un salt unico** (ej si tenes solo una contraseña) hace que el atacnate tenga que computar una tabla nueva (muy muy costoso, es mas facil hacer brute force)
>
* La **velocidad de la funcion de hashing** permite que estas tablas puedan computarse en tiempos relevantes.


Su medio de operacion es el siguiente.

**Se crea una tabla de la siguiente manera:**

* se tiene la hash function $$H()$$
* se tiene una reverse function $$R()$$ que mapea valores de hash space (ej 256 bits) a password space (ej 8 caracteres). esta funcion no es una inversa, solo devuelve algo que **podria** ser una contraseña.
* se preparan una lista de  candidatos de contraseñas.
* se genera una cadena de un largo fijo $$K$$ para cada candidato asi:
	* Se hace $$H()$$ al candidato
	* Se hace $$R()$$ al hash del candidato (recordemos que esto no devuelve el candidato original sino otro)
	* Se hace $$H()$$ al resultado anterior
	* Se hace $$R()$$ al hash del resultado anterior
	* y asi $$K$$ veces
* Se guardan en una tabla los candidatos y el ultimo hash de cada cadena. de esta forma **podes recrear las cadenas cuando vos quieras sin tener que guardarlas enteras**. 


**Se intenta vulnerar un hash:**

S**e crea una cadena con el hash que se quiere vulnerar**, cada vez que se calcula un nuevo hash se lo compara los hashes de la tabla, que son los finales de las cadenas.

Si en algun momento alguno de los hashes de esta cadena es igual a alguno de los hashes de las cadenas que fueron computadas al crear la tabla, entonces **al continuar la cadena eventualmente se llegara al mismo valor que el final de una de las cadenas de la tabla**, indicando que la contraseña esta en esa cadena. 

Para encontrarla reconstruis la cadena y buscas que plaintext corresponde al hash que estas intentando vulnerar.

>**Este metodo tiene varios PROBLEMAS:**
>
>**1) Colisiones**
>como $$R$$ mapea elementos de 256 bits a elementos de 8 caracteres, va a haber muchos hashes que lleguen a las mismas contraseñas, esto se conoce como **colision**.
>
>por la forma como funciona esta tabla , si tenes una colision (el mismo valor en algun punto, en dos cadenas) entonces todos los valores subsuiguientes van a ser exactamente los mismos, entonces **vas a tener los mismos valores en dos cadenas a la vez y eso es espacio desperdiciado**. **Una solucion son las rainbow tables**
>
> 
>**2) nada garantiza que la contraseña este en la tabla**
>
>**3) un salt hace que el ataque sea imposible.**
> Ya que un hash grande agrandaria enormemente el password space y tornaria la tabla demasiado grande.
>**Tambien tiene varias VENTAJAS**
>
>**1) Podes elegir la relacion espacio-tiempo**
>Si tenes **cadenas mas largas** entonces **minimizas la cantidad de espacio** pero aumentas la cantidad de veces que tenes que realizar el hashing de la contraseña original para llegar a algun final de alguna cadena. **(menos space, mas time)**
>Si tenes **cadenas cortas** entonces cada vez mas **se parece a un hash table**, y tenes que hacer menos veces el hashing.(menos time, mas space)


### Rainbow tables

Las rainbow tables **son una evolucion de las Hellman's time-memory trade-off tables** y su unico objetivo es usar menos espacio **reduciendo las concecuencias de las colisiones**

El problema de las colisiones en las tablas de hellman es que una vez que se produce una colision, el resto de los valores de una cadena son identicos a los valores que hay en otra cadena, esto hace que haya **muchos valores duplicados**.

Las rainbow tables usan **una funcion $$R$$ distinta en cada eslabon de la cadena**, entonces si en dos cadenas diferentes tenes una colision (el mismo valor), salvo que la colision suceda en el mismo punto en ambas cadenas (el mismo eslabon, y por ende la misma funcion $$R$$), seran procesados por funcones $$R$$ distintas que evitaran que los valores de las dos cadenas se repitan

![](http://i.markdownnotes.com/Sin_t%C3%ADtulo_A81cvZi.png)

![](http://i.markdownnotes.com/Rainbow_table_collisions_explained.jpg)
**Habra de igual manera colisiones y repeticiones, pero ahora una colision no implica (generalmente) que el resto de la cadena tambien esta repetido en otra cadena.**




>* El uso de **un salt unico por contraseña** hace que este ataque sea irrelevante, porque tendrias que crear una tabla con todas las posibles contraseñas para cada salt, y seria prohibitivamente grande.
>>* El uso de **un salt unico** (ej si tenes solo una contraseña) hace que el atacnate tenga que computar una tabla nueva (muy muy costoso, es mas facil hacer brute force)
>
* La **velocidad de la funcion de hashing** permite que estas tablas puedan computarse en tiempos relevantes.


# Oauth 2.0 como autenticacion 



Oauth te permite obtener **algun dato unico que te permita identificar al usuario**, PERO **ES UN PROTOCOLO DE AUTORIZACION, NO DE AUTENTICACION**.


**BENEFICIO:**
No necesitas implementar una base de datos de usuarios y contraseñas, no necesitas tener un sistema de "olvide mi contraseña" ó two factor authentication, etc. No tenes que manejar nada de eso. Lo unico que tenes que hacer es que el usuario se loguee en otro servicio, recibir el token y usarlo para saber quien es esa persona y ya la autenticaste.



>**CRITICO:**
Una vez autenticado, podes darle al usuario una sesion manejada por vos (cookie/jwt) con la duracion que vos quieras. **NO NECESITAS OAUTH PARA MANTENER LA SESION ABIERTA**



## Implicit flow automatizado por javascript

Los grandes autenticadores con Oauth (google y facebook por ejemplo) tienen librerias que se encargan de hacer un **Oauth 2.0 implicit flow** en el browser de forma automatica. 
Como resultado **recibis un token en el browser**

**Es indispensable que pases este token al server para ver la identidad del usuario, y que no envies sus datos (user id, mail, etc) directamente al server ya que no se puede confiar en ellos**

### [Google sign-in con javascript](https://developers.google.com/identity/sign-in/web/)

### [Facebook sign-in con javascript](https://developers.facebook.com/docs/facebook-login/web)


>Uso de facebook SDK
>https://stackoverflow.com/questions/21294534/how-to-verify-user-login-when-using-facebook-javascript-sdk

https://stackoverflow.com/questions/14186146/how-to-securely-authorize-a-user-via-facebooks-javascript-sdk


### Patron de implementacion

>**El siguiente patron es para el login clasico con facebook/google/etc. una vez que el usuario se autentico no se vuelve a hacer uso del token, sino que se maneja la sesion por otros medios.**

* **Obtener token** - Conseguir un access token mediante Oauth
* **Autenticar usuario** - Usar el token para obtener un identificador unico del servicio (facebook/google user id)
* **Verificar registracion** - Ver si el identificador esta en mi DB
	* No esta - El usuario se esta registrando, añadirlo como nuevo usuario.
	* Si esta - El usuario se esta logueando
* **Proveer sesion** - En el **Redirection endpoint** 
	* **Proveerle al usuario de una sesion** mediante cookie o  jwt que lo mantenga logueado por el tiempo que sea necesario.
	* **Redireccionar** al usuario a una pagina principal (script o HTTP 3xx), donde ya tiene acceso a su sesion debido a la cookie o JWT


# Cookies and tokens

La autenticacion se puede lograr si el usuario esta en **posesion** de un token que pueda identificarlo, generalmente este token se otorga al usuario **despues de ser autenticado incialmente con USUARIO y CONTRASEÑA ya que es un metodo simple de recordar, mientras que un token es largo y dificil de recordar** 

## Stateful session cookie ó Random token

Consiste en un **numero aleatorio llamado SESSION ID** almacenado en el cliente mediante una **cookie** o el almacenamiento local(**token**). El server **vincula el numero con un usuario en particular**.

* El SESSION ID debe ser lo suficientemente largo y aleatorio como para ser imposible encontrar una session mediante azar.
* El servidor puede guardar no solo el vinculo entre el SESSION ID y usuario en particular, sino tambien guardar otros datos (ej carrito de compras)
* Los SESSION IDs deben caducar
* Deben ser transferidos mediante HTTPS
* Si se usan cookies, se debe asegurar con SECURE, HttpOnly y CSRF tokens
* Si se usa el local storage, se debe tener cuidado con XSS
* Se pueden firmar para encontrar intentos de brutforceo de sestiones
* ** El SESSION ID se debe enviar en cada request**

## Stateless (signed) session cookie ó Criptographic token (JWT, JWE)


Consisten en cookies ó tokens que contienen la informacion de la sesion (por ejemplo el nombre del usuario, etc) y que estan firmados digitalmente para probar que fue el server el que los creo. de esta forma **no pueden ser adulterados** ya que **no se puede crear una firma falsa para un token adulterado**


* Se puede colocar toda la informacion de la sesion en una signed cookie o en un JWT y asi **lograr que el servidor no tenga que almacenar nada.**
* **Se debe enviar la cookie o token en cada request**
* La **perdida de la clave privada** es grave y compromete todos los tokens.
* La revocacion de tokens es dificil
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDg2MjA4OTddfQ==
-->