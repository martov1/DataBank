


# Descripcion

**T**ransmision **C**ontrol **P**rotocol

Es el **Protocolo de capa 2 mas usado**, y provee de:

* **Reliability** - asegura que la informacion llego al receptor
* **Order** - asegura que el orden de la informacion sea correcto
* **Error-checking** - Verifica que la informacion llego correctamente sin errores

TCP tiene **una interfaz superior** que utiliza como comunicacion con los niveles por encima de el, a su vez se espera que el protocolo de capa inferior (EJ **IP**) tenga algun tipo de interfaz que permita que  TCP se comunique de maera asincronica con el.

TCP **No asume casi nada** de las capas inferiores o superiores, principalmente.
*  **no asume que la red tenga ningun tipo de confiabilidad**, por lo que puede funcionar en enlaces muy pobres o con mucha interferencia.

## Puertos, Sockets y conexiones

TCP utiliza **puertos** para diferenciar ente los diferentes data streams emitidos por o de un host.

**PUERTO**: Un numero que identifica los distintos data streams que puede haber entre dos hosts. El sistema operativo puede dirigir datos que llegan de diferentes puertos a diferentes procesos internos del sistema.
**SOCKET**: la combinacion de  **direccion de host (ej:IP)** y **puerto**
**CONEXION:** Una cantidad de informacion que dos procesos comparten para poder comuicarse, una conexion es **identificada por dos sockets** 

>Las conexiones pueden enviar datos desde y hacia ambos sockets, osea que son **FULL DUPLEX** 



## Arquitectura y tipos de conexiones
TCP opera **como un servicio SINGLETON**, es decir que **es compartido entre varios procesos que desean realizar conexiones**.


Un proceso puede pedirle al servicio tcp la apertura de **dos clases de conexiones**

* **Conexion activa** - Se pide una conexion desde el **socket 1** al **socket 2**
	* El receptor de la conexion debe contestar iniciando otra **conexion activa** 
	*  es decir que se conocen las direcciones IP y puertos de los dos interlocutores (Browser, cliente FTP)
* **Conexion pasiva** - Se pide una conexion desde el **socket 1** a **cualquier otro socket**, y se solicita que se notifique cuando una conexion se inicie
	* Otro interlocutor inicia una conexion iniciando una **conexion activa** al host que mantiene una **conexion pasiva**  
	* Es decir, un servidor que espera conexiones entrantes de desconocidos (FTP server, Apache HTTP server) 


## Numeros de secuencia

Indica el **numero total de bytes transmitidos  desde el socket 1 al socket 2** en el momento en el que se envio ese paquete.

Sirve para:

* Indicar el **orden de los segmentos al receptor** 
* Que el receptor indique **que bytes recibio correctamente en un ACK** 
* Que el receptor indique **cuandos bytes puede recibir**
.
>* **En una conexion tenes dos numeros de secuencias**
>	* Bytes enviados de $A \Rightarrow B$
>	* bytes enviados de $B \Rightarrow A$ 
>
## Acknowledgement - ACK y retrotransmision

El **ACK** es una herramienta que tiene TCP para indicarle al emisor hasta que punto durante la conexion **Se recibio correctamente la informacion**. 

>Se hace usando el **numero de secuencia**, que indica los bytes recibidos con exito **desde que comenzo la conexion hasta ahora**. es decir que es **ACUMULATIVO**
>
>Un **ACK** con numero de secuencia $M$ indica que **todos los segmentos con numeros $N<M$ fueron recibidos con exito**

TCP envia un ACK al emisor con el numero de secuencia que considera que tiene que recibir del emisor, de esta forma el emisor sabe **hasta que bytes recibio el receptor**  y puede reenviar los bytes que no hayan llegado.

>basado supuestamente en: 
RFC - 1122
RFC 2581

Cuando TCP recibe un paquete:
* Con el numero de secuencia esperado $N$
	* Aguanta un tiempo para ver si se recibe el segmento siguiente
		* **Recibe** el segmento inmediatamente siguiente, con numero $Q$: 
			* manda un **ACK** con numero $Q$, indicando que recibio $N$ y $Q$
		* **No recibe:** mas segmentos, envia **ACK** con numero $N +1$, indicando que recibio todos los bytes hasta $N$ correctamente 
*  Con un numero de secuencia mayor que el esperado $M>N$
	*  Se procede de acuerdo con el algoritmo de retrotransmision implementado
		*  [RFC - 793 - Timout ](https://tools.ietf.org/html/rfc793.html)
		* [RFC - 2581 - Fast retransmit heuristic ](https://tools.ietf.org/html/rfc2581.html)
		* [RFC - 2018 - TCP Selective Acknowledgment (SACK)](https://tools.ietf.org/html/rfc2018) 
* Con numero de secuencia menor al esperado $M<N$
	* Envia **ACK** con numero de secuencia $N$ 


![enter image description here](https://lh3.googleusercontent.com/vfKtLrlE8VXKFg9LpkSG2astxZTbbDqTkTOKZbH83MpBrd9pQqRrHFVNULZ0E9qsiSk9t9Gr0-W1)
# Protocolo

## handshake

>El handshake consiste en **sincronizar numeros de secuencia**, por eso se inicia con el flag **SYN**.
Esto implica simplemente **intercambiar dos numberos arbitrarios que serviran como numero de secuencia iniciales** del socket 1 al socket 2 y viceversa.


* **Host $A$:**
	* Un proceso llama a la funcion OPEN de TCP especificando un socket del host $A$
	* **ENVIA segmento con:**
		* flag **SYN** 
		* Un numero de secuencia inicial para **contabilizar los bytes** de $A \Rightarrow B$
* **Host $B$:**
	* **Si** hubo un pedido de OPEN de **conexion pasiva** o **activa al socket 1** por parte del  usuario
		* **ENVIA segmento con:**
			* flags **SYN** y **ACK**
			* Un numero de secuencia inicial para $A \Leftarrow B$
			* **Confirma** con el **ACK** el numero de secuencia $A \Rightarrow B$
	* **NO** hubo un pedido de OPEN de **conexion pasiva** o **activa al socket 1**
		* No abre una conexion  
* **Host $A$:**
	* Envia **ACK**  confirmando que recibio el numero de secuencia  para $A \Leftarrow B$
* **LISTO: $A$ y $B$ sincronizaron numeros de secuencia y estan listos para transmitir datos** 

![enter image description here](https://lh3.googleusercontent.com/g4NJoKyKTSm6HKK5RMVWHsWuIFYbppY3FYymquvVB3dsWOoKjVI5GKCe_-HkaHP2A3Kw2kNo0f7K)


## Envio de datos

* **Transferencia de datos** - El host 1 llama al proceso TCP con una serie de datos como argumento
	 *  TCP divide los datos en **segmentos**  
	* TCP coloca a cada segmento un **numero de sequencia** que es **la suma de:** 
		 *  El numero de secuencia inicial acordado en el handshake
		 * Todos los bytes transferidos en esta conexion hasta el momento + 1 
	 * TCP coloca un checksum a cada segmento para asegurar su integridad
	 * TCP marca para enviar aquellos **segmentos con numero de secuencia:**
		 *  **MAYOR** que  el **numero de secuencia** $N$ confirmado por el **ultimo ACK del host 2**
		 *   **MENOR** que el **window** indicado por el host 1  mas el **numero de secuencia** $W+N$
	 * TCP envia esos segmentos al protocolo IP para que este lo envie y maneje su fragmentacion
 * **Recepcion de datos** -   El host 2 procesa el datagrama IP y envia el segmento a TCP
	 * TCP verifica el checksum
	 * TCP envia un ACK para indicar que recibio el paquete justo con el numero de secuencia
		 * ademas puede envia un "window" indicandole al emisor **que segmentos puede enviar**, y lo hace prediciendo los numeros de sequencia que faltan. de esta forma el receptor puede tener **flow control** 


![enter image description here](https://lh3.googleusercontent.com/PmAW7mcGdiL25ZayYsVyKrJnGx36EIbXLspaPDRl33NSOfZTGRQ48GsuscbkLcxeXiq0g260Jzzc)


### Window - Flow control

En una comunicacion, el host $A$ puede indicarle al host $B$ **cuantos mas bytes despues del numero de secuencia esta preparado para recibir**.
A esto se lo llama **Window**, el emisor enviara a su discrecion todos los segmentos con numero de secuencia que sea:
* **MAYOR** Al ultimo numero de secuencia que el receptor indico que recibio con un **ACK**
* **MENOR** Al numero de secuencia + el window indicado por el host $B$

Ejemplo de la cola de segmentos que TCP debe enviar:

![enter image description here](https://lh3.googleusercontent.com/TXnjf4FiS56sb6KDfhJ3p8-g1TJiSMgo5H7JKTSfk80S5OZxtZUuzrHbvSdd3XzC7ZCLxpef1IEe)


Grafico de funcionamiento del fow control y el seteo del window
![enter image description here](https://lh3.googleusercontent.com/wGoshZ4AwEJZom3V1hCc-mKeVLiHqYmcvmRMeU9onrvo3Y859RcBbrfKD2WjE_PKEEKx1iLMgcuG)


## Manejo de erores

###  Perdida de segmentos u orden

>Existen estrategias mas modernas para el manejo de estas situaciones, como por ejemplo:
>
>* **TCP fast retransmit heuristics** - RFC 2581
>* **TCP selective acknowledgements** - RFC 2018
 
Si sucede un problema durante la transimicion, TCP detecta que le faltan segmentos con numeros de secuencia, TCP enviara **ACK** con el ultimo numero de secuencia que esperaba recibir, en el emisor todos los segmentos con numeros de secuencia posteriores llegaran al timeout y seran vueltos a enviar

El emisor reenviara aquellos segmentos que lleguen al timeout.

![enter image description here](https://lh3.googleusercontent.com/mmOHorsTPfbTBCgm8pxBYKCy8zK0B-GBkAKS74fJoKcM3q0448SPlmqI3mVo8pSb8-RpecOyVvuW)

### Perdida de la sincronizacion y  Half-connections

**Una conexion deberia ser reiniciada si:**
* **Perida de sincronizacion:** Uno de los dos hosts pierde el numero de sincronizacion
* **Half connection:** host $A$ tiene la conexion como ESTABLISHED y host $B$ tiene la conexion como CLOSED


Si el Host $B$ por algun motivo **pierde  la sincronizacion** con el host $A$, por ejemplo si crashea el servicio TCP, $B$ puede pedirle a$A$ que vuelva al estado **LISTEN** y arrancar desde cero haciendo el handshake para volverse a sincronizar.

**EJ 1 :**
* $A$ mantiene una conexion en estado **ESTABLISHED** con $B$
* $B$ intenta conectarse con $A$ enviando un **SYN**
* $A$ envia flag **RST** por que se da cuenta que hay un **half-connection**
* $B$ cambia el estado de su conexion a **LISTEN**
* $A$ y $B$ comienzan el three way handshake

**EJ 2 :**
* $A$ mantiene una conexion en estado **ESTABLISHED** con $B$
* $B$ no tiene conexion activa con $A$ (**CLOSED**)
* $A$ envia datos a $B$ pensando que estan conectados
* $B$ no acepta los datos y envia un segmento con flag **RST** por que detecta un half-connection
* $A$ cambia el estado de su conexion a **LISTEN**
* $A$ y $B$ comienzan el three way handshake


# Especificaciones 

## TCP segment

![enter image description here](https://lh3.googleusercontent.com/aB6nl8JSFeHpwZwfDZCA37ZZR9BTl_ORVJoXrvG34nzRnEA1B3krwp14pVan8oEgTkiUMeCjHVUq)

* **source port:**  - Puerto de origen
* **destination port** - Puerto de destino
* **sequence number** 
	* La suma de El numero de secuencia inicial y  Todos los bytes transferidos en esta conexion hasta el momento + 1
	* si el flag **SYN** esta presente: Un numero de secuencia inicial arbitrario  
* **Header hegith** - Indica el tamaño del header para que el receptor sepa donde comienzan los datos.
* **control bits**  - Aca se indican los FLAGS
	* **URG** - Le indica al receptor que el paquete es urgente, no esta especificado en TCP que hacer
	* **ACK**
	* **PSH** - El user indico que se envien los datos de forma inmediata.
	* **RST** - Reiniciar la conexion
	* **SYN** - syncronizar numeros de secuencia 
	* **FIN** - Terminar la conexion, no envies mas datos.
* **window** - Sequence number hasta el cual el receptor aceptara datos desde este paquete, permite que el receptor controle el flujo de datos. 
* **Checksum**-  el checksum de los datos

	 
## Manejo de las conexiones

### Etapas de una conexion

La conexion TCP para por varios "estados", estos son **estados internos que no se comunican entre las dos partes**. Simplemente indican en que etapa se encuentra la conexion desde cada extremo

Los estados de las conexiones son:
* **Listen** - Conexion pasiva abierta, a la espera de conexiones activas de un socket desconocido.
* **Syn-sent** - Se envio una solicitud de sincronizacion (asi inician todas las conexiones activas), se esta esperando la respuesta.
* **Syn-received** 
	*  Se recibio un pedido de sincronizacion y por ende se tiene el numero de secuencia de $A \Rightarrow B$
	*  se envio un ACK con el numero de secuencia propio $B \Rightarrow A$
	* se espera el ACK para confirmar que $B$ tiene el numero de secuencia de $A$
* **ESTABLISHED** - TCP intercambio numeros de secuencia y esta listo para recibir o enviar datos
* **FINWAIT_1** - TCP envio una solicitud de cierre de conexion con flag **FIN** y esta esperando la respuesta 
* **CLOSE-WAIT** - TCP recibio un flag **FIN** y esta esperando la confirmacion del usuario para enviar su propio segmento con flag **FIN** para confirmarle al otro host que van a cerrar la conexion
* **FINWAIT_2** 
	*  TCP recibio un **ACK** indicando que el otro host recibio el flag **FIN**
	* TCP esta esperando que el otro host envie su propia solicitud de cierre de conexion con un flag **FIN** 
* **LAST-ACK** 
	* TCP  ya envio su propio segmento con flag **FIN** y cuando reciba el **ACK** cerrara la conexion.  

![enter image description here](https://lh3.googleusercontent.com/f8IH3qB2uIpxoCxVPyBAPtMB5uiJNYwBQK9t27F871HDV9JxkyvU9x2AAzl2obBSGw39fFLBCu_P)


### Cierre de la conexion

Las conexiones TCP son **full duplex**, osea que pueden enviar y recibir datos al mismo tiempo, sin embargo el cierre de conexiones es **SIMPLEX**.

>Un host $A$ puede **cerrar su conexion para envios** y **mantener su capacidad de recibir datos** hasta que el host $B$ **cierre la conexion de su lado**
>
>Por este motivo es necesario que para terminar totalmente una conexion ambos interlocutores **envien el flag FIN a su contraparte**

Una vez que TCP cerro su conexion **SIMPLEX**, no le permitira al usuario seguir enviando informacion, pero recibira los segmentos siguientes hasta que el otro host cierre su conexion.


## Interfaz


La interfaz **entre el usuario y TCP** esta bien definida por el protocolo, mientras que la interfaz entre **TCP y el protocolo de capa inferior** sera espericificado por el protocolo de capa inferior


### OPEN

Pide la apertura de una conexion desde el socket $A$ al socket $B$

* **Si la apertura es pasiva:** la conexion se abre como **LISTEN**
* **Si la apertura es activa:** se inicia el **handshake**
* **Timeout:** Si se coloca un timeout, la conexion sera abortada si luego del transcurso del timeout no se recibio respuesta del host $B$
```
 OPEN (
	 local port,
	 foreign socket, 
	 active/passive, 
	 [timeout],
	 [precedence],
	 [security/compartment]
	 [options]
 ) -> local connection name
```

### SEND

Envia una pieza de datos a travez  de una conexion ya establecida.

* **PUSH flag** - Los datos se envian inmediatamente
* **No PUSH flag** - Se espera para ver si se acumulan mas datos para enviar en esta conexion y se envian todos juntos para aumentar la eficiencia de la red.

```
 SEND (
	 local connection name, 
	 buffer address, // La direccion de los datos a enviar 
	 byte count, 
	 PUSH flag, 
	 URGENT flag, 
	 [timeout]
 )
```

### CLOSE


Inicia el proceso de cierre de la conexion

* Todos los paquetes que quedan en cola seran enviados con sus respect
```
 CLOSE (local connection name)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTA3Mzg3NTE5LC02NTgzMDY4NTksMTY2ND
k2MzczMCwtNTA2OTMzNjc3XX0=
-->