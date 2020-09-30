


**Me quede en**
min 23
https://www.youtube.com/watch?v=lND9yuxnwc0

VER
no hay buenas soluciones para revocar certificados, pero algunas son:
https://www.youtube.com/watch?v=q1OF_0ICt9A min 23
**CRL**
**protocolo OCSP**


6.  The TLS Record Protocol
http://www.rfcreader.com/# rfc5246_line666


# Contenido


* Intro
	* Conocimientos previos necesarios. 
	* Conceptos basicos
		* Handshake y record protocols
		* Connections y sessions
* Descripcion basica 
	* Handshake protocol
		* Detalles
		* Necesidad de la Pre-master key
		* Handshake corto usando sesiones
	* Record protocol 
	
* Fuentes 
	



# Intro

## Conocimientos previos necesarios. 

Todos definidos en el documento de seguridad/criptografia.

* **Stream/block ciphers** - que son, diferencias
* **Modos de operacion de block ciphers** - cuales son, como funcionan
* **RSA** - Idea fundamental de como funciona
* **AES** - Idea fundamental de como funciona
* **Diffie-Hellman** - Idea fundamental y como funciona
* **SHA256** - que es y que hace
* **HMAC** - Idea fundamental de como funciona
* **Digital signatures** - Que son y como funcionan
* **Certificados** - Idea fundamental de que son y como funcionan



## Conceptos basicos

**Definido en:**

* [RFC5246 -    The Transport Layer Security (TLS) Protocol](http://www.rfcreader.com/# rfc5246)


**Obejtivos:**


* **Prevenir Eavesdropping** - que un tercero pueda leer los mensajes
* **Prevenir Tampering** - que un tercero pueda modificar los mensajes en camino
* **Prevenir Falsificacion** - que un tercero pueda generar un mensaje que aparenta haber sido creado por otro.

**Flexibilidad:**

El protocolo TLS esta **concebido para ser super flexible**, es decir que puede usar una **gran variedad de encriptaciones, hashes, MACs, etc**. esto hace que sea **poco especifico y a veces bastante complejo**



### Handshake y record protocols

>Hace uso de **Criptografia asimetrica**, (la cual es bastante lenta) para realizar el **intercambio inicial** de **keys simetricas** que se usan luego para intercambiar los mensajes de forma rapida usando **criptografia simetrica**
>la integridad de los mensajes se verifica usando **HMAC**.

**En otras palabras el protocolo esta dividido en**

* **Handshake protocol** - el intercambio de keys simetricas a ambos lados mediante el uso de criptografia asimetrica. 
	* **Sus propiedades son:**
		* **Authenticacion** - La identidad de por lo menos uno de los interlocutores es autenticada con criptografia asimetrica (**RSA**, DSA o similar, **certificados** )
		* **Negociacion** - segura via criptografia asimetrica (**RSA**) de una clave simetrica para usar en el record protocol.
		* **Confiabilidad de negociacion** - Los mensajes no pueden ser modificados sin que esto sea detectado


* **Record protocol** - El uso de las keys simetricas para encriptar y desencriptar los mensajes con criptografia simetrica. 
	* **Sus propiedades son:**
		* **Privacidad** - la conexion es encriptada usando criptografia simetrica (**AES**,RC4 o similar)
		* **Confiabilidad** - los mensajes son checkeados por integridad usando **HMAC**
		* **Encapsulacion** - Se usa para encapsular otros protocolos, como HTTP 



### Connections y sessions

 >**Las conexiones TCP** entre un cliente y un server que estan usando **TLS** se agrupan en lo que se llama una **SESION**, ya que **las conexiones comparten un gran numero de variables que hacen posible la encriptacion**

Despues del **handshake protocol** todas las constantes necesarias parala comunicacion se guardan a nombre de:

* **LA SESION:** todo aquello que se comparte entre conexiones para lograr la encriptacion( **IDs, certificados, tipo de compresion, ciphers, claves simetricas, etc**)

* **LA CONEXION:** todo lo que no se comparte con otras conexiones pero que es necesario para la encriptacion (**IVs, MAC secrets, random values**)

---

# Descripcion basica:

## Handshake protocol


El handshake protocol se divido en 3 partes:

* **Hello**
	* se acuerda que ciphers se usaran
	* Se acuerda quienes presentaran certificados
* **Pre-master key exchange**
	* Se comparte una clave con algun algoritmo, a partir de esta se computan las otras claves que se usaran (MAC, AES, IV, etc)
* **Change cipher spec**
	* El cliente y el server acuerdan usar de ahora en mas los ciphers que acordaron anteriormente. de este momento en adelante todo se encripta. 

### Detalles

A continuacion se detallan las 3 partes de forma mas detallada

* **Hello**
	* El cliente envia un hello y: 
		* Random 28 bytes
		* Accepted cipher suites (EJ: RSA-AES128--CBC-SHA256)
		* Accepted compression methods (zip, null)
	* El server responde con hello y:
		* Random 28 bytes 
		*  El cipher suite elegido
		*  El compression method elegido
		*  Un certificado (el cliente lo verificara por su lado)(opcional)
		*  Solicitar certificado al cliente (opcional)
	* El cliente responde con certificado (opcional)  



* **pre-master Key exchange**
	* El server envia datos para el key exchange (si es **DH**)
		*  **firmado con la clave privada que es autenticada con la clave publica dentro de el certificado enviado al cliente**
	* El cliente  envia datos para el key exchange (si es **DH**)


* **Procesamiento interno, aca no hay intercambio de informacion**
>* **Obtener master a partir de Pre-master**
> * El cliente y el server usan la **pre-master** que se intercambiaron y en conjunto >con los **random bytes** del hello, hashing y otras tecnicas, generan un **master key** 
>
>
>* **Obtener keys a partir de master**
>	* A partir de la **master** se generan todas las **keys que hagan falta**
		* **HMAC keys**
			* Un $\text{MAC}_1$ del client al server
			* Un $\text{MAC}_2$ del server al client
		* **IV** para el CBC mode 	
			* un $IV_1$ del client al server
			*  un $IV_2$ del server al client 	
		* **AES keys** 
			*  Un $\text{AES}_1$ del client al server
			*   Un $\text{AES}_2$ del server al client
		
* **Change cipher spec protocol**
	* El server envia un mensaje indicando que de ahora en mas usaran los ciphers que han acordado. 
	* El server envia un **new session ticket**
	* El client responde con finished (mensaje encriptado)


 

![](https://github.com/martov1/DataBank/blob/master/imagenes/fotomila_qoiTSZ8.png)

### Necesidad de la Pre-master key

> **Porque una pre-master key?**
> 
> TSL es muy flexible y admite muchos algoritmos, tales como variantes de Diffie-Hellman y RSA.
> **Si intercambiaran claves directamente entonces no tendrias siempre claves del mismo largo.**
> Como concecuencia, para estandarizar el largo de las claves, **TSL demanda la generacion de una shared secret de un largo determinado, y usa como seed la pre-master key y otros parametros**
> 
> [fuente](https://security.stackexchange.com/questions/54399/whats-the-point-of-the-pre-master-key)

### Handshake corto usando sesiones

Una vez que el handshake fue realizado, se establece una sesion usndo el session ticket, esto implica que la proxima vez (dentro de un lapso de tiempo) que **por cada nueva conexion** del cliente con el servidor,**el handshake sera mucho mas corto** (solo **hello**) y **se reutilizaran las keys del handshake anterior**

## Record protocol

>El record protocol es el **encargado de enviar y recibir mensajes usando criptografia simetrica** una vez que se logro **establecer un handshake y crear una clave simetrica.**

**Los pasos son los siguientes:**

* **Division** - Se divide lo que se quiere enviar en **Fragmentos**
	* Si se usa un block cipher, el tamaño debe ser compatible con el tamaño de block del block cipher usado
* **Compresion** - Se **comprimen** los fragmentos **(OPCIONAL)**
* **MAC** - Se computa un **MAC** sobre el fragmento y se lo añade el mismo
* **Encriptacion** - Se encripta el fragmento con **criptografia simetrica**
* **SSL header** - Se añade un **SSL RECORD HEADER**

![](https://github.com/martov1/DataBank/blob/master/imagenes/fotomila_qCa7bek.png)




# Fuentes


* css322 thammasat university
https://www.youtube.com/watch?v=lND9yuxnwc0
https://www.youtube.com/watch?v=hYxtjtfwhqk

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1ODc3OTc5NzldfQ==
-->