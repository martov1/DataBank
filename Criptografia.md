



https://www.youtube.com/watch?v=bMC_OuHReA8&list=PLvifRcqOOwF-z2sfMb3w0uQzd7PfaLFlU

**Lectures Introduccion a la criptografia:**
https://www.youtube.com/playlist?list=PL6N5qY2nvvJE8X75VkXglSrVhLv1tVcfy


**Forward secrecy**
https://crypto.stackexchange.com/questions/31291/why-use-diffie-hellman-key-exchange-over-rsa-or-any-public-key-encryption

Clases analizadas y documentadas bien:

- [ ] lecture 1: introduction
- [ ] Lecture 2: Modular Arithmetic and Historical
- [x] Lecture 3: Stream Ciphers, Random Numbers and the One Time Pad 
- [x] Lecture 4: Stream Ciphers and Linear Feedback Shift Registers
- [ ] Lecture 5: Data Encryption Standard (DES): Encryption 
- [ ] Lecture 6: Data Encryption Standard (DES): Key Schedule and Decryption
- [ ] Lecture 7: Introduction to Galois Fields for the AES
- [ ] Lecture 8: Advanced Encryption Standard (AES) 
- [x] Lecture 9: Modes of Operation for Block Ciphers 
- [ ] Lecture 10: Multiple Encryption and Brute-Force Attacks
- [x] Lecture 11: Number Theory for PKC: Euclidean Algorithm, Euler's Phi Function & Euler's Theorem 
- [x] Lecture 12: The RSA Cryptosystem and Efficient Exponentiation
- [x] Lecture 13: Diffie-Hellman Key Exchange and the Discrete Log Problem
- [ ] Lecture 14: The Generalized Discrete Log Problem and the Security of Diffie-
- [ ] Lecture 15: Elgamal Encryption Scheme
- [ ] Lecture 16: Introduction to Elliptic Curves
- [ ] Lecture 17: Elliptic Curve Cryptography (ECC) 
- [x] Lecture 18: Digital Signatures and Security Services
- [ ] Lecture 19: Elgamal Digital Signature
- [ ] Lecture 20: Hash Functions
- [ ] Lecture 21: SHA-1 Hash Function
- [ ] Lecture 22: MAC (Message Authentication Codes) and HMAC
- [ ] Lecture 23: Symmetric Key Establishment and Kerberos
- [x] Lecture 24: Man-in-the-middle Attack, Certificates and PKI 

**Elgamal encription**
https://www.youtube.com/watch?v=tKNY1zhK3sQ&index=15&list=PL6N5qY2nvvJE8X75VkXglSrVhLv1tVcfy

**generalizacion sobre DH y encontrar buenos discrete log problems :**
minuto 43
https://www.youtube.com/watch?vc=IGqrbM52wtg

**Comprender cuando se usa el algoritmo Square and multiply en RSA y en DH**

**Digital signature algorithm**
https://www.youtube.com/watch?v=PQ8AruHaoLo


# Contenidos

* Conceptos basicos
	* Random number generators 
	* Criptografia simetrica
	* Criptografia asimetrica
	* Ciphers	
		* Confusion y difusion
		* Stream ciphers 
		* Block ciphers
	* Hashing 	
* Algoritmos criptograficos de encriptacion
	* RSA 
		* Principio de funcionamiento 
		* Ejemplo
		* porque es asi?
		* Generacion de claves
		* Calculo de $\phi()$
		* Implicaciones de seguridad
	* AES
		* Funcionamiento basico 
		* Longitud de la clave
		* Expansion de clave
		* Funcionamiento detallado
	* DES 
	* Diffie-Hellman Key exchange
		* Funcionamiento basico 
		* Porque funciona
		* Implicaciones de seguridad
* Modos de operacion de block ciphers
	*   Coneptos basicos
	*   ECB
	*   CBC
	*   OFB (block cipher como stream cipher)
* Algoritmos criptograficos de hashing
	* Algoritmos Legacy
		* SHA-1 (legacy)
		* MD5 y MD4
	* Algoritmos usados
		* SHA-256
		* SHA-3 (draft)
* Criptographic checksums
	* MAC 
	* HMAC
* Digital signatures
	* Funcionamiento basico
	* Funcionamiento con RSA
* Certificates 
	* Funcionamiento
	* Anatomia de un cerificado
* Ataques
	* Man-in-the-middle
		*  Diffie-Hellman
		*  Generalizacion a cualquier Asimetric key encription
* Fuentes




# Conceptos basicos



## Random number generators

Muchos algitmos criptograficos utilizan **RNG** o **R**andom **N**umber **G**eneratos para partes de sus procesos, la **aleatoriedad de los generadores es fundamental para mantener la seguridad** ya que se suelen usar para **crear claves secretas**

### Usos comunes:

* **Criptografia simetrica** - se usa para crear una clave secreta
	* AES 
* **Criptographic checksums** - se usa para crear una clave secreta
	* MAC
	* HMAC 
* **Criptografia asimetrica** - Es la base sobre la cual se calculan las claves publica y privada
	* RSA 


### Tipos de RNGs:


* **TRNG** - **T**rue **R**andom **N**umber **G**enerator, en general usan algun metodo fisico para generar numeros realmente aleatorios. EJ: tirar una moneda, medir los movimientos del mouse, tiempo entre teclas al tipear, etc.
* **PRNG** - **P**seudo **R**andom **N**umber **G**enerator. no son realmente aleatorios, son deterministicos, se podrian llegar a recrear. **NO DEBEN USARSE EN CRIPTOGRAFIA**
* **CSPRNG** - **C**riptographically **S**ecure **P**seudo **R**andom **N**umber **G**eneratos.EJ: [node.js randomBytes()](https://nodejs.org/api/crypto.html# crypto_crypto_randombytes_size_callback), la [instruccion RdRand del procesador intel](https://en.wikipedia.org/wiki/RdRand)

>**Solo se deben usar TRNGs y CSPRNGs para generar claves**, nunca PRNGs como por ejemplo la funcion rand del lenguaje $C$




## Criptografia simetrica



>Ejemplos:
> * AES
> * DES
> * 3DES


Es el tipo de criptografia mas elemental y es usada en las comunicaciones porque es rapida. ambos interlocutores usan la misma clave secreta para encriptar sus mensajes. 

en general **Las claves son strings largos aleatorios provenientes de un fuerte algoritmo generador de numeros aleatorios**

**consta de:**

* Una **clave** que es **compartida por ambos interlocutores**, generalmente proveniente de un **R**andom **N**umber **G**enerator.
* El mensaje es **encriptado y decriptado** usando esa clave
* 


**Problemas:**

* **El dilema del huevo y la gallina:** 
	* Para generar una **conexion segura** tenes que **enviar la clave** al otro interlocutor por lo menos una vez, para que pueda **encriptar y desencriptar tus mensajes**.
	* Para **enviar la clave** de forma segura **necesitas** que tener **una conexion segura**.
* Necesitarias de una clave **distinta para cada interlocutor** con el que te comunicas.

Entonces para enviar la clave se usa otro metodo menos rapido llamado criptografia asimetrica.


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/wWhbYNz.png)



## Criptografia asimetrica

>Hay 3 familias:
 * RSA
 * Discrete log
 	*  Diffie Hellman
 	*  Elgamal encription
 * Elliptic curve



En la criptografia asymetrica permite **resolver el problema del huevo y la gallina que presenta la criptografia simetrica**.



Generas **dos claves** y  lo que **una clave encripta** solo puede ser **desencriptado por la otra**. una clave no puede ser obtenida a partir de la otra.

De esas dos claves:
* Una es compartida o **publica**
* Otra es reservada o **privada**


Esto en la practica se usa para:

**AUTENTICACION: El emisor es quien dice ser**
> Un tercero que tiene tu clave publica puede desencriptar tus mensajes que encriptaste con la clave privada. Con eso **se asegura que sos vos el que la escribio**, ya que solo la **persona con la clave privada pudo haberlo encriptado**. es decir, te aseguras que el emisor es quien dice ser.

**PRIVACIDAD: solo el receptor puede leer los mensajes**

> Un mensaje enviado a un tercero y **encriptado la clave publica de ese tercero**  solo puede **desencriptarse con la clave privada de ese tercero**, es decir, solo el receptor lo podra leer.


	





## Ciphers

En criptografia un **cipher** es un algoritmo que sirve para encriptar y desencirptar datos.

### Confusion y difusion

Para que un **cipher** sea **dificil de descifrar** necesitas dos propiedades basicas

* **Confusion:**
La relacion entre el plaintext y el ciphertext esta obscurecida, por ejemplo con un lookup table y substituciones
* **Difussion:**
 La modificacion de un bit del plaintext debe repartirse a lo largo de gran parte del ciphertext. EJ: Permutaciones

>un **cipher fuerte** tiene **multiples** combinaciones de **confusion y difusion**

### Stream ciphers

Son un metodo de **encriptacion simetrica** que **Encripta bit por bit**, es decir, no necesitas dividir al archivo en _bloques_, sino que podes encriptar los bits a medida que son generados. 

**Ejemplos:**

* Llamadas de voz
* Streaming de video

**Funcionamiento basico:**

>Funciona simplemente **sumando cada  bit de la clave simetrica con cada bit de mensaje**. como **un bit es binario** solo los podes sumar haciendo **$\mod 2$**, es decir:
>
> $1+1 = 0 \text{  dos bits con valor 1 sumados dan un bit 0}$ 
> $1+0 = 1$ 
> $0+1 = 1$


* **Dados**:
	*   $S_i \text{ - Clave compartida en binario }$ 
	*   $E_i \text{ - Mensaje encriptado en binario}$ 
	*   $D_i \text{ - Mensaje desencriptado en binario}$ 
	*   $\text{El subfijo }_i \text{ implica un bit puntual del mesnaje/clave}$

* **Encriptacion:**
Se **encripta** simplemente **sumando el bit $_i$ del mensaje con el bit _i_ de la clave**.
$$
\text{Encriptacion}
\\
E_i=D_i+S_i \mod 2
$$ 
* **Desencriptacion**
	Se **desencripta** realizando el mismo proceso, **sumando el bit $_i$ del mensaje encriptado con el bit _i_ de la clave**. al ser $\mod 2$ volves a donde empezaste.
	
	$$
\text{Desencriptacion}
\\
D_i=E_i+S_i \mod 2
$$ 

* **Ejemplo de encriptacion:**
$$
\begin{bmatrix}D = 1,0,0,0,0,0,0,1\\ S = 0,1,0,1,0,1,0,1 \\ \hline  E= 1,1,0,1,0,1,0,1 \end{bmatrix}
$$


>#### Seleccion de clave simetrica:
>
>Si tuvieras una clave simetrica con la misma cantidad de bits que tus datos, entonces lograrias un codigo inquebrantable (llamado **One time pad** ó **OTP**), pero la clave pesaria lo mismo que el mensaje.
>
Esto es muy inpractico, como concencuencia en general se usa una tecnica que es menos segura pero mas facil de usar en la practica, llamada **Linear Congruential Generators** ó **LCGs**
>
**Linear Congruential Generators / Key Stream Generators:**

>Los interlocutores utilizan una **shared key** para alimentar un **PRNG**. al usarse la misma clave vas a generar los mismos numeros. luego estos numeros son los que se usan como **clave simetrica de encriptacion y desenriptacion**. de esa manera podes transmitir una clave mas pequeña pero encriptar con una mas larga.
> **Ambos interlocutores deberan usar un PRNG que devuelva los mismos numeros dado ese seed**

### Block ciphers

Los block ciphers **pueden ser aplicados con criptografia simetrica o asimetrica**

Su principio de accion es que **encriptan la informacion de a bloques**. La mayoria de los algoritmos de encriptacion funcionan de esta manera, y **si los bloques son pequeños entonces pueden usarse para hacer streaming, por ejemplo de video, sin recurrir a un stream cipher**

Algunos ejemplos son:
* Criptografia asimetrica
	* RSA
* Criptografia simetrica
	* DES
	* AES  



## Hashing

El hashing o una hash function es un procedimiento que puede usarse para **mapear datos de cualquier tamaño a una serie de datos de un largo determinado.** 

### Propiedades:
* Es **improbable** que dos **archivos diferentes** tengan el **mismo hash**
* Dos **archivos iguales** siempre tienen el **mismo hash**
* Los hash siempre tienen **un tamaño determinado** independientemente del tamaño del archivo
* **No** se puede **recuperar el archivo original** usando el hash
* Debe ser **razonablemente rapido** pero no **extremadamente rapido** porque permitiria  artificialmente crear documentos con un hash determinado
* Con un bit de diferencia el hash sera completamente diferente
* Debe ser imposible **crear un archivo que tenga un hash arbitrario**, de esta forma no podes armar archivos que artificialmente tengan el mismo hash que otro archivo

La idea es que podes correr un hash function sobre un archivo, entrada de datos, etc y el hash que devuelve puede usarse para identificar ese dato. estadisticamente **solo dos archivos iguales produciran el mismo hash**, por lo que


>si te proveen de un **hash** y un **archivo**, podes correr el hash function sobre el archivo y compararlo con el que te dieron, si son iguales entonces sabes que **el archivo no fue modificado**

### Usos:
* Chequeo de **integridad** de datos/descargas/etc
* Corroborar que **un archivo no fue alterado** 
* Utilizarlos como **index** en bases de datos
* **Comparacion de contraseñas**. en lugar de almacenar contraseñas almacenas sus hashes





# Algoritmos criptograficos de encriptacion

## RSA



**R**ivest **S**hemir **A**delman

Es un sistema de **encriptacion asimetrica** que utiliza **Aritmetica Modular** para encriptar y evitar que otros decripten mensajes.
Tambien se puede usar para crear **Firmas digitales**

>Comprension de este doc basada en
https://www.youtube.com/watch?v=wXB-V_Keiu8&t=872s

### Principio de funcionamiento



En la practica funciona de esta manera:

1)Se transforma el mensaje en numeros
2) se elevan esos numeros por otro numero (**clave 1**) y se toma el modulo por **un numero arbitrario** $N$. este es el **mensaje encriptado**
3) Ahora existe un numero (**clave 2**) al que podemos elevar el **mensaje encriptado** y al sacar el modulo de $N$, obtenemos el **mensaje desencriptado**

>Parte del algoritmo **RSA** es como obtener tato las **claves 1 y 2** como el **numero arbitrario**.
>Los conjuntos de Clave 1 ó 2 y  $N$ seran las**claves privada y publica.**
>
>EJ:
>**Clave publica:** ${(clave 1 ,N)}$ 
>**Clave privada:** ${(clave 2 ,N)}$ 




### Ejemplo:

* Mensaje inicial codificado en numeros: **2**
* Numero arbitrario: **14**
* Clave 1:  **5**
* Clave 2: **11**

#### Encriptacion:

Elevas el **mensaje** a la potencia de la **clave 1** y haces el modulo por el **Numero arbitrario** seria:

$2^5(\mod 14)= 4$

te queda el cyphertext **4**, que  es el **mensaje encriptado**


#### Decriptacion:

Elevas el mensaje cifrado a la potencia de la **clave 2** y haces el modulo por el **numero inicial**, te queda el mensaje.
$4^{11}(\mod14)=2$

#### Identidad

Notamos que se **eligieron 5,11 y 14 tal que:**

$2^{5*11} (\mod 14) = 2$

Fijate que es importante que 5 y 11 sean coprimos

### Porque es asi?

RSA funciona conociendo una funcion que es **facil de calcular** cuya inversa es **dificil de calcular** un ejemplo de esto es la **aritmetica modular**.
Si elegirmos **numeros lo suficientemente grandes** entonces una computadora **tardaria años** en resolverlo.


Imaginemos
$$
M: \text{Mensaje}\\
C: \text{Mensaje encriptado}\\
E: \text{algun numero}\\
D: \text{algun numero}\\
$$

$$
\text{FACIL HACIA UN LADO Ó ENCRIPTAR}
\\
M^E \mod N \equiv ?
\\
$$

$$ 
\text{DIFICL HACIA EL OTRO Ó DESENCRIPTAR} 
\\
?^E \mod N \equiv C
$$
[RSA problem: find exponent of the message, modulo a composite number N whose factors are not known](https://en.wikipedia.org/wiki/RSA_problem)

**Entonces si le proveemos a un tercero de numeros $E, N$ el puede encriptar un mensaje y no podra ser leido.**


Necesitas un **trapDoor o key** que te permita de alguna manera **evitar esa dificultad** cuando vos desees **desencriptarlo**.

$$
\text{por la identidad, sabemos que existe algun E y D tal que}
\\
M^{D*E} \mod N \equiv M \Rightarrow \\
M^{E} \mod N \equiv C  \  \land 
C^{D} \mod N \equiv M\\
$$

**Entonces tenemos que encontrar dos numeros $E,D$ tales que $M^{E*D}$ nos provea de la identidad** (devuelvan $M$), **esto no es trivial** 

>Incluso si el atacante conoce $M$, encontrar $D$ para
> $C^{D} \mod N \equiv M$
> Es muy dificil y requeriria fuerza bruta

El **teorema de euler** nos provee de una manera de **encontrar $D$ y $E$ que satisfagan la identidad**.
Para eso requiere del  calculo de $\phi(N)$, que es convenientemente **dificil de calcular a menos que conozcas la factorizacion de N de antemano, cosa que ya conocemos al crear N** 

Como concecuencia **el que creo N** puede calcular $\phi(N)$ con facilidad, obtener el exponente identidad y despejar $E$ y $D$. Pero **cualquier otro necesita factorizar N para calcular  $\phi(N)$, cosa que no toma tiempo razonable**





$$
\text{Obtener el exponente identidad:}
\\
~
 \\
 \text{Por teorema de euler}
 \\
 M^{\phi(N)} \equiv 1 \mod N  \quad \quad \small  \text{Mientras M y N sean coprimos  }
 \\ 
  \text{si multiplicamos de ambos lados por M } 
\\
 M.M^{\phi(N)} \equiv M.1 \mod N
\\
 \text{entonces} 
\\
 M^{1+ \phi(N)} \equiv M \mod N
\\
 \phi(N) \text{ implica factorizar N a menos que tengas mas informacion, }
 \\
 \text{nosotros conocemos } \phi(N) \text{porque creamos N }
 \\
 \text{ (ver calculo de } \phi(N)  \text{ para mas informacion) }
$$

###### [Teorema de euler - Wikipedia](https://en.wikipedia.org/wiki/Euler%27s_totient_function#Euler's_theorem)


$$\text{Despejar E y D a partir del exponente identidad:}
 \\
~
 \\
 \\
M^{1+ \phi(N)} \equiv M \mod N \qquad \land \qquad M^{E*D} \equiv M \mod N
\\
\qquad \text{ Euler}  \qquad  \qquad  \qquad  \qquad \qquad \qquad \text{ Identidad}
\\
$$

$$
\text{fijate que el exponente deberia ser igual en ambos ya que da el mismo resultado}
\\
\phi(N)+1 = E*D
$$
**Esto implica que si elegiimos una clave publica $E$ cualquiera (Dentro de ciertos parametros que la hacen segura, generalmente se elige $65537$) entonces podemos despejar nuestra clave privada $D$**

$$
\text{Nuestra clave privada D seria:}
\\
D={\phi(N)+1 \over E}\\
\small
\text{que tambien se puede escribir como:}\\
\small{
ED=1 \mod \phi(N) \\
\text{ ya que eso implica que existe K tal que } \\
ED= 1 + k\phi(N) }
$$

###### [equivalencia](https://crypto.stackexchange.com/questions/56259/relationship-between-equivalent-ways-of-computing-rsa-private-key/56262#56262)

Como **nadie** va a lograr calcular $\phi(N)$ ni tampoco resolver $C^{D} \mod N \equiv ?$ en tiempos razonables si **N** es lo suficientemente grande (**Ya que ambos problemas requieren factorizacion**) la unica forma factible de desencriptar es **Conocer D** y la unica forma factible de ecriptar es **conocer E**

>En realidad tendrias que agregar una multiplicacion por cualquier constante $K$ quedando $M^{1+ \phi(N)K} \equiv M \mod N $. ya que el teorema de euler [tiene esa propiedad](https://en.wikipedia.org/wiki/Euler%27s_theorem)
>###### [computo de claves](https://www.youtube.com/watch?v=t5lACDDoQTk&t=161s)

### generacion de claves:

>**Aclaracion:** una lista de numeros **cooprimos** es una lista de numeros que **no tienen** factores comunes salvo el 1

* Elegir 2 numeros primos **con un generador de numeros aleatorios**
* Hacer el producto de ambos. este sera el **numero arbitrario** $N$
* Se calcula la **cantidad** de numeros **cooprimos** del $N$. esto se conoce como funcion $\phi(N)$. **hay dos formas de hacerlo y aca reside la seguridad del algoritmo**
* Se eligen las claves 1 y 2, para eso usamos teo euler  $M^{\phi(N)} = 1 \mod N$
* Se elije la **Clave 1** $C_1$, que debe ser
 * Entre 1 y $\phi(N)$
 * **Coprimo** con $N$ y $\phi(N)$
 * Muchas veces se elige $65537$ por convencion, si es posible.
* Se elije la **Clave 2** $C_2$ eligiendo algun  resultado valido de [alguna de estas equaciones](https://crypto.stackexchange.com/questions/56259/relationship-between-equivalent-ways-of-computing-rsa-private-key/56262# 56262):
	*  $C_2={\phi(N)+1 \over C_1}$
	*  $C_1* C_2=1 \mod \phi(N)$





### Calculo de $\phi(N)$

La funcion $\phi(N)$ es una funcion que determina la **cantidad de numeros menores a $N$ que son cooprimos entre si**. hay dos formas de calcularlo, una facil y una dificil.

Aca **reside la seguridad de RSA**,

* **Forma 1 -DIFICIL**
   * se **hace una lista** de todos los numeros anteriores a $N$
   * Se **eliminan** de la lista los numeros que tengan **factores comunes** con $N$
   * se **eliminan** de la lista los dos **numeros primos del paso 2**, que son siempre **factores de $N$** porque este el el producto de esos dos.
   * Contas la cantidad de numeros en la lista.
   * Con un $N$ grande podria **tomar siglos calcular esto** 
* **Forma 2 - FACIL** 
	* Sabiendo que $N$ es el producto de dos numeros primos $P_1$ y $P_2$, podes usar esta formula $\phi(n)=(P_1 -1)(P_2-1)$
	* Destruis $P_1$ y $P_2$ para que nadie pueda revertir el proceso
	* Independientemente del tamaño de $N$, esto es **trivial de calcular**
  

 
 ### Implicaciones de seguridad
 
* RSA **no garantiza que dos computadoras no generen las mismas claves**, pero se usan numeros tan grandes que es **estadisticamente improbable** que eso suceda.
* Calcular $\phi(N)$ sin los dos numeros originales podria tomar decadas, porque factorizar es costoso.

>**Para romper RSA podrias intentar:**
>
* Brutforcear $D$ conociendo un mensaje $M$ en  
	$C^D \mod N = M$
>  Parece ser aun mas dificil que el [discrete logarithm problem](https://crypto.stackexchange.com/questions/56242/difference-between-the-math-of-rsa-problem-and-dh-problem/56243?noredirect=1#comment124467_56243) ya que los factores de N no se conocen
* Factorizar $N$ para calcular $\phi(N)$ de la **forma 1** y despejar $D$ de 
	$D={\phi(N)+1 \over E}$
>
* Factorizar $N$ en primos para encontrar $p$ y $q$. 
 usarlos para calcular $\phi(N)$ de la **Forma 2**
>
 Todas estas formas son **computacionalmente infeasibles**
 [Otros ataques](https://crypto.stanford.edu/~dabo/pubs/papers/RSA-survey.pdf)


## AES

> La comprension de este algoritmo esta basada en:
> https://www.youtube.com/watch?v=K2Xfm0-owS4&t=22s
> https://www.youtube.com/watch?v=7uRK9iOk4uk
> https://www.youtube.com/watch?v=dRYHSf5A4lw
> https://www.youtube.com/watch?v=bERjYzLqAfw
> https://www.youtube.com/watch?v=4pmR49izUL0

> En este documento hay varias transformaciones que usan constantes que son **matrices aparentemente arbitrarias**. existe un motivo para la eleccion de estas matrices en lugar de otras, pero el motivo de esta eleccion escapa al scope de este documento

Es un algoritmo de **Encriptacion simetrica** usado universalmente. tiene las siguientes propiedades
* **universalmente aceptado** - las CPUS estan diseñadas y optimizadas para computar AES nativamente
* **Extremadamente rapido** -  para encriptar y desencriptar
* **Seguro y testeado**
* Basado en **difusion y confusion usada multiplies veces**
* Es un **block cipher**




### Funcionamiento basico

El algoritmo basicamente es asi: 

* Se precisa una **clave simetrica** que se usa para encriptar o desencriptar
* Se divide el archivo en **bloques de 128 bits/16 bytes**
* Cada bloque es tratado como una matriz de 4x4 bytes
* Cada bloque se encripta de la misma manera usando la clave simetrica
	* Se **expande** la clave simetrica pare generar varias claves
	* Se **encripta multiples veces** el mensaje con las varias claves.
		* Cuanto mas **larga la clave**, mas claves se genera y mas veces se encripta el mensaje 
		 

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/PIu5hyb.png)

### Longitud de la clave


La **seguridad de AES** esta en gran medida influenciado por **el largo de la clave** ya que mientras mas larga la clave **mas rondas de encriptacion recibe el mensaje**

| largo de clave        | ciclos de encriptacion           | uso  |
|  |::| :|
| 128 bits     | 10 ciclos | Muy frecuente, ecriptacion rapida |
| 192 bits      | 12 ciclos      |   no tan frecuente |
| 256 bits | 14 ciclos      |    encriptacion lenta, muy seguro |

### Expansion de clave

Se usa la **clave original** como semilla para crear **tantas claves diferentes como ciclos de encriptacion correspondan**, es decir que **cada ciclo de encriptacion tiene su propia clave**

**Es una funcion recursiva**, la clave inicial atraviesa este **algoritmo de tres pasos** y sale una nueva clave, esta nueva clave atraviesa el algoritmo nuevamente y sale otra clave, y asi sucesivamente.

* Se separa la clave en 4 bytes, y en cada segmento se aplica:
	* **Rotate** - se rota cada byte una posicion a la izquierda (onda ciclic group)
	$[B_1, B_2, B_3, B_4] => [B_2, B_3, B_4, B_1]$
	* **S-Box** - Se reemplaza cada byte por su valor en la [matriz de Rijndael  S-box](https://en.wikipedia.org/wiki/Rijndael_S-box)
	* **RCon** - se reemplaza cada byte por su valor en [la matriz RCon](https://en.wikipedia.org/wiki/Rijndael_key_schedule# Rcon)
* **Recursion**- Se toma la nueva clave de 16 bytes y se vuelve a pasar por el mismo algoritmo recursivamente 

### Funcionamiento detallado

> Todas las operaciones corresponden al concepto de **diffusion** ó **confusion**, los pasos se realizan multiples veces para solapar ambos procesos y generar un **cipher fuerte**

El algoritmo tiene:
* **Una ronda inicial** - unica al principio del algoritmo
* **Muchas Rondas intermedias** - La cantidad de rondas depende del largo de la clave
* **Una ronda final** - unica, al final del algoritmo

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/A9jcSvg.png)

Pasos del algoritmo: 

* **Initial Round** - Ocurre al inicio de la encriptacion de cada **bloque de 128 bits / 16 bytes**.
	* **AddRoundKey** - Operacion **bitwise XOR** entre cada byte de la clave con cada byte del bloque de 16 bytes
* **Rounds** - Ocurre una cantidad de veces, dependiendo del largo del la clave
	* **SubBytes** - utiliza una matriz predeterminada llamada [Rijndael  S-box](https://en.wikipedia.org/wiki/Rijndael_S-box). cada Byte, representado en hexadecimal es reemplazado por su correspondiente substitucion en la tabla
	* **ShiftRows** - Se colocan los 16 bytes que estamos encriptando como una matriz de 4x4 y se rota cada row como si fuera un ciclic group.
	$$\begin{pmatrix}
1 & 2 & 3 & 4\\\
5 & 6 & 7 & 8\\\
9 & 10 & 11 & 12\\\ 
13 & 14 & 15 & 16\\\
\end{pmatrix}$$
		* La primera columna se deja como esta
		* La segunda se shiftea una posicion a la izquierda $[5,6,7,8]=> [7,8,5,6]$
		* La tercera dos posiciones $[9,10,11,12]=> [11,12,9,10]$
		* La cuarta 3  $[13,14,15,16]=> [16,13,14,15]$
	* **MixColums** - se hace el **dot product** entre nuestro estado representado por una matrix de 4x4 y una [matriz predefinida](https://en.wikipedia.org/wiki/Rijndael_MixColumns# Step_3:_matrix_representation)
	 $$\begin{pmatrix}
	1 & 2 & 3 & 1\\\
	5 & 6 & 7 & 8\\\
	1 & 1 & 2 & 3\\\ 
	3 & 1 & 1 & 2\\\
	\end{pmatrix}$$
	* **AddRoundKey** 
* **Final round** - Ocurre al final de la encriptacion de cada bloque de 128 bits
	* **SubBytes**
	* **ShiftRows** 
	* **AddRoundKey** 




## DES

**D**ata **E**ncription **S**tandard. Desarrollado por la NSA.

* Hoy **no se considera seguro** a menos que se realice 3 veces seguidas, denominado **3DES**
* Es el **antecesor de AES**
* Similar a AES
* Es un **block cipher**
* Usa **Clave simetrica**

### Funcionamiento

> El funcionamiento basico de **DES** consiste en dividir el mensaje y la clave en dos y realizar 16 rondas dee difusion y confusion permutando la clave y mezclando las mitades con el mensaje

Utiliza:

* **Simmetric key** - 64 bits
* **Mensaje dividido en bloques** - De 64 bits

Algoritmo:

* **Division:**
	* **De input:** Se divide el primer bloque en dos partes de 32 bits
	* **De clave:** Se divide la clave en 2 bloques de 28 bits
* **Rondas** - Se pasa  la segunda mitad del mensaje por una funcion recursiva y el resultado se suma (**XOR**) con la primera parte del mensaje **->quede aca<-**
	* **swapping** - Se intercambia la primera mitad del mensaje con la segunda y se vueve a alimentar la funcion





## Diffie-Hellman Key exchange

Es un algortimo que **Permite que dos partes acuerden de forma segura una clave privada sobre un canal inseguro, por ejemplo intenret**.
En general se usa para que dos computadoras **acuerden una clave simetrica** para despues usar AES

>El siguiente ejemplo es _una forma_ de Diffie hellman. **Diffie-Hellman se puede usar en cualquier grupo donde la [Diffie-hellman assumption](https://en.wikipedia.org/wiki/Computational_Diffie%E2%80%93Hellman_assumption) exista.** _los reales modulo un numeor primo_  ( $\Bbb{Z}\mod P$ ) son un ejemplo donde la Diffie-hellman assumption  existe.

**Funciona bajo dos pincipios:**
* [Discrete logaritm problem](https://www.youtube.com/watch?v=aeOzBCbwxUo)
>$$
\text{Given: }P, G \in Z_P^*, \text{the primitive element A.}
\\
\text{find x for}\\
A^x \equiv G \mod P \\
\text{alternativamente}\\
A \equiv G^x \mod P
$$
###### [Alternativa](https://www.youtube.com/watch?v=YEBfamv-_do)
* $A^{bc}=A^{cb}$


### Funcionamiento basico

El funcionamiento es muy simple.

* Ambos interlocutores acceden a usar **dos numeros publicos** $G$ y $P$
* Cada interlocutor **elige una clave privada** $a$ ó $b$
* Cada interlocutor**genera una clave publica** $A$ ó $B$ con su clave privada:
	* $A=G^a \mod P$ 
	* $B=G^b \mod P$
* los interlocutores **intercambian sus claves publicas**
* los interlocutores usan sus **claves privadas como exponentes**, ambos **obteniendo el mismo resultado**, que sera su clave compartida $S$
	* $A^b=G^{a^b} \mod P= G^{ab} \mod P = S$ 
	* $B^a =G^{b^a} \mod P= G^{ba} \mod P= S$ 

>La eleccion de $G$ y $P$ debe ser un poco particular para formar un grupo que no tenga una buena soluion en el problema de [Discrete logaritm problem](https://www.youtube.com/watch?v=aeOzBCbwxUo).
>
>Lo minimo y basico es que
> * El$P$ debe ser un primo
> * El $G$ debe ser un generador de un grupo $ Z_P^*$


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/SvtOXfx.png)


### Porque funciona

Un atacante podria intentar calcular $S$ sabiendo $G,P,A,B$, ya que fueron transmitidos en un canal inseguro.	
	
* Si conocemos $a$ ó $b$ podemos hacer $B^a$ ó $A^b$ y sacar la clave
* Queremos despejar $a$ de aca:
$A = G^a \mod P  $
* Despejando $a$ nos queda
$ a = log_G A \mod P$
	 
Computar este logaritmo se conoce como [**Resolver el Discrete Log Problem**](https://en.wikipedia.org/wiki/Discrete_logarithm) que en la practica es muy dificil con un numero $N$ muy grande


### Implicaciones de seguridad

Algunas formas de atacarlo son 

* **Fuerza bruta**
	* Evitable con $P,G>2^{80}$
* **Baby step-Gigant step**
* **Polland's rho method**
Podemos evitar que sean practicos on un $P,G>^{160}$
* **Index-calculus attack**
Se puede evitar con $P,G>^{1024}$





# Modos de operacion de block ciphers

Los block cipher encriptan bloques, eso implica que **necesitas una estrategia para encriptar datos que sean mas grandes que un bloque.** Estas estrategias que existen son algoritmo-agnosticas, es decir, **no dependen de si usas AES, DES, 3DES, etc**. Mientras estas usando un block cipher estas estrategias tendran sentido.

Algunas entrategias incluso te permiten usar **Block ciphers como si fueran stream ciphers!**

>**Podes dividir los modos de operacion asi:**
>
* Deterministicos
	* ECB
* Probabilisticos
	* Block cipher como block cipher
		*  CBC
	* Block cipher como stream cipher
		* OFB
		* CFB
		* Counter mode 


> * **Determinisitico:** implica que para un **plaintext A** siempre obtenes un **ciphertext B** si usas **la misma key**
> * **Probabilistico:** implica que **no es deterministico**, generalmente mediante la combinacion de un metodo deterministico y un **RNG**


## ECB

**E**lectronic **C**ode **B**ook

Es la estrategia mas **basica e insegura** que hay para encriptar usando block ciphers. consiste en **encriptar un bloque despues de otro**sin conectar sus encriptaciones entre si.

>**Advertencia de seguridad:**
>Tiene el problema de que **si dos bloques son iguales entonces seran encriptados mapeandolos al mismo ciphertext**, y esto puede usarse por un atacante que conozca partes repetidas del mensaje para vulnerar el sistema **sin vulnerar el block cipher**. (Ej: modificar un mensaje reemplazando un bloque encriptado por otro bloque encriptado previamente por el server cuyo valor es conocido por el atacante. por ejemplo reemplazar el numero de cuenta de destino en una transaccion realizada por un tercero por el numero de una cuenta propia cuyo valor encriptado conocemos porque hicimos una transaccion de prueba)


**Funcionamiento**

Cada bloque se encripta con el algoritmo de encriptacion usando la clave privada.

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/kihwZae.jpg)


## CBC

**C**ipher **B**lock **C**haining

Es una estrategia de utiliza **Probabilistica** para evitar los **problemas de seguridad de ECB**. principalmente intenta **evitar que se encripte dos veces el mismo plaintext con el mismo ciphertext**



**Su objetivo es**: 

* **Encriptar dos bloques iguales, genere dos ciphertexts distintos**


**Para lograrlo:**

* Hace que la **encriptacion de bloques sea Probabilistica mediante un RNG**
*  **Combina la encriptacion de varios bloques**


**Funcionamiento:**

>Funciona Sumandole (XOR) al primer bloque un numero aleatorio de un RNG (de ahi la parte **Probabilistica**) y encriptandolo. A cada bloque siguiente se le suma el bloque encriptado anterior y se encripta esa suma.

$$
\text{DADO: }\\
B_n: \text{Bloque de plaintext } n\\
C_n: \text{bloque de ciphertext } n\\
IV: \text{Initial Vector}\\
AES: \text{El algoritmo de encriptacion}\\
\oplus \text{Suma mediante XOR }
$$

El algoritmo funciona asi:

* Usando un **RNG, counter ó date** Se genera un numero denominado $IV$ ó **I**initial **v**ector 
* Se **envia** el $IV$ al otro interlocutor en plain text, **no es secreto**.
* **Encriptacion del primer bloque:** 
	* Se **suma** (XOR) el primer bloque con el **IV**
	* Se encripta esa **suma** usando el algoritmo de encriptacion
	$C_1 =AES( B_1 \oplus IV)$
* **Encriptacion de los siguientes bloques:**
	* Se **suma** el bloque siguiente  con el ciphertext del bloque anterior
	* Se encripta esa suma
	$C_n= AES( B_N \oplus C_{n-1})$

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/2EIs3sA.jpg)

* **Desencriptacion:**
	* **Primer bloque** 
		* se desencripta ciphertext $C_1$ con la key
		* se hace un XOR con il $IV$
	* **siguientes bloques**
		* Se desencripta el ciphertext $C_N$ con la key 
		* Se hace un XOR con el ciphertext no desencriptado del bloque anterior  


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/MyTPbeR.jpg)


>**CONCLUSIONES:**
> 
> * **No tenes el problema de ECB. Un bloque de plaintext no sera mapeado siempre al mismo ciphertext porque:**
> 	* el $IV$ cambia seguido
> 	* Cada bloque de ciphertext cambia dependiendo de los anteriores
>
**Condiciones para ser vulnerable:**
* Mismo $IV$ en dos mensajes
* Mismos bloques anteriores al bloque que se desea reemplazar por un valor conocido por el atacante
>
**Sobre el** $IV$:
* No es secreto
* puede provenir de un **RNG**
* Para evitar generar **IVs repetidos** y asi evitar vulnerabilidad
	* Puede usarse un **counter**
	* Puede usarse un **high precision date** 
* Solo se usa una vez

## OFB

**O**utput **F**eed**b**ack mode

Es una estrategia que:

* Te permite usar un block cipher como un stream cipher
	* **Usa el block cipher como un stream key generator** 
* Es probabilistica

**Funcionamiento:**

>Basicamente **OFB** encripta recursivamente un valor inicial $IV$ con un block cipher , el string de datos generado se usa como **Key Stream Generator** en un **stream cipher**.

Aunque el $IV$ sea publico, la clave secreta con la que se lo encripta con el block cipher no lo es, por lo que un atacante no puede recrear  **Key Stream Generator** aunque conozca el $IV$

* Usando un **RNG, counter ó date** Se genera un numero denominado $IV$ ó **I**initial **v**ector 
* Se **envia** el $IV$ al otro interlocutor en plain text, **no es secreto**.
* **Encriptacion de los primeros $N$ bits:** 
	* Se **encripta** el $IV$ con un block cipher, generando $N$ bits (128bits si es $AES$).
	* Se hace un **stream cipher** con esos primeros $N$ bits. es decir, se hace una **XOR** entre los primeros $N$ bits del mensaje con los $N$ bits del $IV$ encriptado
* **Encriptacion de los bits despues de $N$ bits:** 
	* Se toma el $IV$ encriptado enteriormente y se lo **vuelve a encriptar**, cenerando un **nuevo ciphertext**, este a su vez se usa en un **stream cipher** para encriptar los siguientes $N$ bits y asi sucesivamente 


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/D4jKT13.png)

>**El proceso de desencriptacion** es dentico al de encriptacion, en virtud de que es un stream cipher, entonces una operacion XOR se revierte haciendo la misma operacion.


# Algoritmos criptograficos de hashing

## Algoritmos Legacy


### SHA-1 (legacy)


>SHA-1 es un algoritmo legacy diseñado para, a partir de un imput, producir un output de exactamente 20 bytes/160 bits. la idea es que podes **reproducir localmente el algoritmo** en un archivo o en datos y **compararlo** con el resultado esperado, **proveniente de otro lado**. al ser ambos iguales podes probar que el archivo no fue modificado.
>
> Fuente:
> https://www.youtube.com/watch?v=DMtFhACPnTY


**Funciona asi:**

* Arrancas con un **estado inicial** de 20bytes/160bits dividido en 4 _palabras_ de 32 bits
* **Loopea** agarrando 512 bits del archivo a la vez hasta que se acaba el archivo
	* Se coloca en una **funcion de compresion** el estado inicial y el primer perazo de 512 bits, devuelve **otro estado**
	* Recursivamente se coloca ese **estado** en la **funcion de compresion** con el siguiente pedazo de 512 bits hasta que el archivo termina



### MD5 y MD4

Son simples de romper y ya no seben ser usados



## Algoritmos usados

### SHA-256

Similar a **SHA-1**, es considerado seguro al dia de hoy

**es el estandar**

### SHA-3

Aun no es usado globalmente



# Criptographic checksums

Los Criptographic checksums son algoritmos que **permiten a un receptor de un mensaje verificar que el mensaje no ha sido modificado cuando estaba siendo enviado**.

Suelen usarse en conjunto con un algoritmo criptografico que encripta el contenido del mensaje, pero no es necesario. Pueden usarse para corroborar que mensajes enviados en texto plano no fueron modificados

El mecanismo principal de accion es la**creacion y envio de un codigo (hash)** junto con el mensaje, que pueda ser recreado por el receptor pero dificilmente falsificado por un atacante.Con este proposito se pueden usar **Claves simetricas**

**El Envio seguro de la clave simetrica no es parte del trabajo de estos algoritmos
**
## MAC

**M**essage **A**uthentication **C**ode

El mecanismo es muy simple:

* **Se comparte una clave secreta** entre el emisor y el receptor (se crea de un **RNG**)
* **Se computa un hash** de los datos enviados + la clave
* **Se envia el mensaje y el hash**
* **El receptor recibe el mensaje** y computa nuevamente el hash usando la clave que le compartieron en el primer paso
* **El receptor compara el hash del mensaje y el que computo**, si coinciden el mensaje no fue modificado

Dependiendo de la funcion de hashing que uses, se nombra al algoritmo:
* **MAC-MD5**
* **MAC-SHA1**
* **MAC-SHA256**

## HMAC
 
 [RFC 2104 - HMAC informatinal memo]( https://tools.ietf.org/html/rfc2104)
 **H**ashed **M**essage **A**uthentication **C**ode (**MAC**).
 
 Es extremadamente similar a **MAC**, pero se utiliza la clave como semilla para armar dos claves, y con ellas se computa el hash recursivamente dos veces, y este se envia.
 

 
**Comenzas con:**
 
 * **Tu mensaje**- el cual queres asegurar que no fue modificado
 * **Una shared key** - que es compartida entre ambos interlocutores
 
**Consiste en:**

* **se generan dos keys** - A partir de la shared key original 
* Se computa el **hash del mensaje con una de las keys agregada al mensaje**, denominado _inner hash_
* Se computa el **hash de ese hash on la otra key agregada** denominado _outer hash_
* **Se envian** tanto el mensaje como el _outer hash_
* El receptor realiza el mismo proceso de hashing ya que posee la  **Shared key**, si **el outer hash que computó es identico al que recibio en el mensaje**entonces el mensaje **no fue alterado**

Dependiendo de la funcion de hashing que uses, se nombra al algoritmo:
 * **HMAC-MD5**
 * **HMAC-SHA1**
 * **HMAC-SHA256**


>A diferencia del algoritmo **MAC**, en **HMAC** Se realiza el hashing dos veces para proteger de [Length extension attacks](https://en.wikipedia.org/wiki/Length_extension_attack)




# Digital signatures

Las firmas digitales son sistemas que permiten **autenticar que un mensaje proviene o fue creado por un usuario en particular**. Solo ese usuario puede crear firmas digitales que lo autentiquen. Ademas en general tambien proveen de **verificacion de integridad**

>A diferencia del HMAC o MAc, que solo verifica la integridad del archivo, las firmas digitales proveen de **veryficacion de integridad** y ademas de **verificacion de la identidad del emisor** y  **no repudiacion**

**La digital signature nos asegura:**

* **Integrity** - El mensaje no fue modificado mientras viajaba
* **Autentication** - El mensaje proviene de quien dice provenir
* **Non-repudiation** - El emisor del mensaje no puede negar que el lo creo, porque solo el tiene la clave privada.

### Funcionamiento basico:

En general hacen uso de un **Hash** y **Criptografia asimetrica** para generar las firmas. por ejemplo:

* Computar un **hash** del archivo o mensaje
* **Encriptar el hash** con una clave privada. **Esta es la firma**
* Enviar al receptor el mensaje y la firma
* El receptor usa la **clave publica** para desencriptar el mensaje, de esta forma:
	* Save que proviene del emisor, ya que **solo alguien con la clave privada podria haber creado un mensaje que pueda desencriptarse con la clave publica**.
	* Puede verificar la**integridad del archivo enviado** usando el hash.

> Solo el emisor tiene la clave privada, entonces nadie puede falsificar un mensaje y decir que el emisor lo envio.

### Funcionamiento con RSA

En general se elige la clave publica $e=3$ y $N=2^16$ para que la verificacion sea muy muy rapida, como concecuencia la generacion de clave privada es muy muy lenta



# Certificates


Los certificados son herramientas que te permiten **Evitar el Man In The Middle.**.
**Su objetivo es lograr que las claves publicas de los servidores sean inequivocamente las correctas para que nadie pueda inpersonarlo**

>Son  **Claves publicas (RSA, ECC, Elgamal) de un interlocutro**  que pueden **verificarse mediante la firma digital de un tercero**, llamado **Certificate authority** ó **CA**.
>
>  **la clave publica  del CA usada para la firma digital se conoce de antemano y esta instalada en el browser.**

### Funcionamiento

* El certificado contiene
	* **Una clave publica**
	* **Su identificacion** (asocia la clave publica con un interlocutor, ej el dominio)
	* **Una firma digital** de todo lo anterior creada con la **clave privada del CA**
		* Las claves publicas de los **CA** se **conocen de antemano**.


> Los browsers son adversos a incorporar nuevas clves publicas de **CA** por poarte del usuario, generalmente estos se añaden cuando los browsers son actualizados (nuevas versiones de chrome o firefox). **entonces no suele haber un handshake que un man in the middel pueda usar para inyectar una clave publica de CA falsa.**

Cuando te queres comunicar con Alguien:

* Interlocutor $A$ envia su certificado
* Intelocutor $B$ Utiliza la **public key** del **CA** $Pk_{CA}$, que se conoce de antemano, para **verificar la firma digital** del certificado de $A$
	* Si se verifica, entonces la**clave publica del certificado** $PK_A$ de $A$ se usa para la comunicacion.
	* (**OPCIONAL**) Se usa $PK_A$ con criptografia asimetrica para intercambiar claves simetricas  
	*  (**OPCIONAL**) Se usa $PK_A$ con criptografia asimetrica para firmar futuros mensajes


### Anatomia


Los certificados vienen encodeados en base64 o similar para hacerlos mas pequeños.

Un ejemplo de un certificado
```
[
[
  Version: V3
  Subject: CN=XRamp Global Certification Authority, O=XRamp Security Services Inc, OU=www.xrampsecurity.com, C=US
  Signature Algorithm: SHA1withRSA, OID = 1.2.840.113549.1.1.5

  Key:  Sun RSA public key, 2048 bits
  modulus: 19206033826534342682632495828927635123439157609676562039233563572917876078114513457600390696700174083679538456341758334592481978420826404729506737215833914255666540175886267037531139889297685722237821599692475307789891460460008671693614845469374688701701501064727144031911232620141585054553781093869650227378770758792265520056647803100678126503550873048172060275942837201956025959406518395708902210113120347995651316264691475966254483476718976671182789398533801136648349011545024832126941120907644302936106853445768208783246887871215301823193787493054151937651027156908432190206937447512518393703893091583344190018661
  public exponent: 65537
  Validity: [From: Mon Nov 01 17:14:04 UTC 2004,
               To: Mon Jan 01 05:37:19 UTC 2035]
  Issuer: CN=XRamp Global Certification Authority, O=XRamp Security Services Inc, OU=www.xrampsecurity.com, C=US
  SerialNumber: [    50946cec 18ead59c 4dd597ef 758fa0ad]

Certificate Extensions: 6
[1]: ObjectId: 1.3.6.1.4.1.311.20.2 Criticality=false
Extension unknown: DER encoded OCTET string =
0000: 04 06 1E 04 00 43 00 41                            .....C.A


[2]: ObjectId: 1.3.6.1.4.1.311.21.1 Criticality=false
Extension unknown: DER encoded OCTET string =
0000: 04 03 02 01 01                                     .....


[3]: ObjectId: 2.5.29.19 Criticality=true
BasicConstraints:[
  CA:true
  PathLen:2147483647
]

[4]: ObjectId: 2.5.29.31 Criticality=false
CRLDistributionPoints [
  [DistributionPoint:
     [URIName: http://crl.xrampsecurity.com/XGCA.crl]
]]

[5]: ObjectId: 2.5.29.15 Criticality=false
KeyUsage [
  DigitalSignature
  Key_CertSign
  Crl_Sign
]

[6]: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: C6 4F A2 3D 06 63 84 09   9C CE 62 E4 04 AC 8D 5C  .O.=.c....b....\
0010: B5 E9 B6 1B                                        ....
]
]

]
  Algorithm: [SHA1withRSA]
  Signature:
0000: 91 15 39 03 01 1B 67 FB   4A 1C F9 0A 60 5B A1 DA  ..9...g.J...`[..
0010: 4D 97 62 F9 24 53 27 D7   82 64 4E 90 2E C3 49 1B  M.b.$S'..dN...I.
0020: 2B 9A DC FC A8 78 67 35   F1 1D F0 11 BD B7 48 E3  +....xg5......H.
0030: 10 F6 0D DF 3F D2 C9 B6   AA 55 A4 48 BA 02 DB DE  ....?....U.H....
0040: 59 2E 15 5B 3B 9D 16 7D   47 D7 37 EA 5F 4D 76 12  Y..[;...G.7._Mv.
0050: 36 BB 1F D7 A1 81 04 46   20 A3 2C 6D A9 9E 01 7E  6......F .,m....
0060: 3F 29 CE 00 93 DF FD C9   92 73 89 89 64 9E E7 2B  ?).......s..d..+
0070: E4 1C 91 2C D2 B9 CE 7D   CE 6F 31 99 D3 E6 BE D2  ...,.....o1.....
0080: 1E 90 F0 09 14 79 5C 23   AB 4D D2 DA 21 1F 4D 99  .....y\#.M..!.M.
0090: 79 9D E1 CF 27 9F 10 9B   1C 88 0D B0 8A 64 41 31  y...'........dA1
00A0: B8 0E 6C 90 24 A4 9B 5C   71 8F BA BB 7E 1C 1B DB  ..l.$..\q.......
00B0: 6A 80 0F 21 BC E9 DB A6   B7 40 F4 B2 8B A9 B1 E4  j..!.....@......
00C0: EF 9A 1A D0 3D 69 99 EE   A8 28 A3 E1 3C B3 F0 B2  ....=i...(..<...
00D0: 11 9C CF 7C 40 E6 DD E7   43 7D A2 D8 3A B5 A9 8D  ....@...C...:...
00E0: F2 34 99 C4 D4 10 E1 06   FD 09 84 10 3B EE C4 4C  .4..........;..L
00F0: F4 EC 27 7C 42 C2 74 7C   82 8A 09 C9 B4 03 25 BC  ..'.B.t.......%.

]
```



# Ataques

## Man-in-the-middle

### Diffie-hellman
Un ataque ante el cual Diffie-Hellman no puede protegerte es el denominado **Man In The Middel** ó **MITM**.

>Consiste en que un atacante intercepte los paquetes durante el intercambio de claves e inplante sus claves en lugar de las de los interlocutores.
>Requiere un **Atacante activo que pueda modificar los paquetes**

* **Los interlocutores creen que hablan entre si**, pero en realidad hablan con el atacante
* **El atacante habra generado las claves simetricas** para la comunicacion con los interlocutores
* Una vez que comienza la comunicacion con una clave simetrica
	* El atacante **podria forwardear las comunicaciones entre los interlocutores**, osea que estos nunca se darian cuenta que los **mensajes estan siendo leidos**
	* El atacante podria **no forwardear la comunicacion**, logrando un **Denial-Of-Service** 

#### Solucion con certificados
> Se puede **firmar digitalmente** el **intercambio de parametros de Diffie-Hellman** usando la **clave privada que puede ser verificada por el certificado**
> De esa manera **evitas el man-in-the-middle**
> Si usaras RSA directamente para encriptar, no tendrias [forward secrecy](https://crypto.stackexchange.com/questions/31291/why-use-diffie-hellman-key-exchange-over-rsa-or-any-public-key-encryption)

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/qToc8Eh.jpg)




### Generalizacion a cualquier Asimetric key encription

Con cualquier **Asymetric key** un atacante puede interceptar la comunicacion y darte **Su clave publica en lugar de la del interlocutor** ya que no tenes forma de verificar que esa clave publica realmente es de la persona que crees.

**Para solucionar esto se usan certificados, que son claves publicas abaladas por un tercero**


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/mOLH81p.jpg)


# Fuentes

* Introduction to Cryptography by Christof Paar
  https://www.youtube.com/watch?v=2aHkqB2-46k&list=PL6N5qY2nvvJE8X75VkXglSrVhLv1tVcfy
* RSA khan academy
  https://www.youtube.com/watch?v=wXB-V_Keiu8&t=872s
* AES
	https://www.youtube.com/watch?v=K2Xfm0-owS4&t=22s
	https://www.youtube.com/watch?v=7uRK9iOk4uk
	https://www.youtube.com/watch?v=dRYHSf5A4lw
	https://www.youtube.com/watch?v=bERjYzLqAfw
	https://www.youtube.com/watch?v=4pmR49izUL0
* SHA-1
  https://www.youtube.com/watch?v=DMtFhACPnTY
* MAC y HMAC
  https://www.youtube.com/watch?v=wlSG3pEiQdc
  https://tools.ietf.org/html/rfc2104
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxNDQ0MjEwMDcsLTk5ODY2ODU1MV19
-->