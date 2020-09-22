**FALTARIA HABLAR DE**
* Endmills conicos / taped
	* Genera bordes en un angulo
* Fishtail endmills


**Me quede en este ultimo de herramentas**
https://www.youtube.com/watch?v=Wks3Zf0Khec&t=59s

**despues ver recubrimiento de herramientas**
https://www.youtube.com/watch?v=nY6o04ODJ3U

**Ver rapidamente este de seleccion de herramientas**
https://www.youtube.com/watch?v=Bupr_IR-_Pk&list=PLzc0Bm2I_0pn1lfdvG2xIG_z4-YiaTq1H

**Ver es**
**te de herramientas y speed and feed**
https://www.youtube.com/watch?v=ip2jm_6aUyk

**Seguir viendo**
https://www.youtube.com/watch?v=_HGGkCaYMVA&list=PLY67-4BrEae9m8v20LNARIRl9Pd9bdFRZ&index=3

**Fortalecer con**
https://www.youtube.com/watch?v=15p1Kerb4N8&list=PLNvVbYXgJCEU2yqoOpEHB0mbDEttFgH7j
# Introduccion
## Seguridad

Para manipular una fresa es necesario:
* Pelo corto o atado
* Proteccion ocular
* mangas cortas
* Sin anillos, joyas, cadenas ni nada colgando
* No acercar las manos a la maquina mientras este girando o moviendose

## Comandos y partes de la fresa - WIP
![IDENTIFYING MACHINE PARTS, CONTROLS, AND THEIR FUNCTIONS – Cad cam  Engineering WorldWide](https://cadcamengineering.net/wp-content/uploads/2015/02/IDENTIFYING-MACHINE-PARTS-J-3.jpg)


Las operaciones que requieren rigidez se hacen con las cranks (knee vertical, traverse) y bloqueamos el quill feed hand lever para aumentar la rigidez 

Si necesitas hacer operaciones rapidas de agujereado, podes usar el quill feed hand lever que funciona como un taladro

## Ajuste y nivelado previo de maquina

[fuente](https://www.youtube.com/watch?v=YkTgyvaYn0M&list=PLY67-4BrEae9m8v20LNARIRl9Pd9bdFRZ&index=2)


La alineacion de las partes de la fresa con gran precision es crucial.

Un problema de nivelacion en la mesa de trabajo se transfiere a la morsa que se transfiere a la pieza y se amplifica con movimientos en los ejes $XY$ de la herramienta, la cual tambien es afectada por la nivelacion de la cabeza!

**Todo tiene que estar bien alineado**



### Ajuste: nivelacion de cabeza de la fresa

La cabeza de la fresa debe estar  perpendicular a la mesa, para ajustarlo la cabeza esta sobre dos ejes que permite rotarla en dos direcciones

![](https://i.imgur.com/6W1zosB.png)



Para determinar si el ajuste fue exitoso usamos un instrumento de medicion de altura, lo pegamos a una varilla y medimos la diferencia de altura desde el husillo hasta un extremo de la mesa y el extremo diagonal opuesto, esto maximiza los errores de alineacion y los hace mas evidentes.

 Si no hay diferencia de altura entre un extremo de la mesa y el otro entonces estamos alineados. ($\text{diferencia}<0.025mm$) 


![](https://i.imgur.com/EEvo2aD.png)

###  Ajuste: alineacion de Morsa

Pasos:
Sacar la morsa, desarmarla, limpiarla y sacarle la grasa.


Revisar base de la morsa y remover picos en la base de la morsa con una piedra, ya que introducen error. lo mismo con la mesa de trabajo.

![](https://i.imgur.com/iqMGuzn.png)

Colocar **cuidadosamente** la morsa en la mesa

Ajustar la morsa de tal manera que este paralela a la mesa, para eso usamos un instrumento de medicion en **la cabeza de la fresa** y medimos dos puntas de la fresa para verificar que dan el mismo valor, caso contrario ajustamos.


![](https://i.imgur.com/jvd9PYz.png)




## Conceptos de fresa 

### Direccion de giro

**SIEMPRE** tendremos en cuenta que la herramienta esta diseñada para girar **en una sola direccion**. **INTENTAR CORTAR CON UNA HERRAMIENTA GIRANDO EN LA DIRECCION INCORRECTA LA PARTIRA**

La herramienta **salvo en casos particulares** debe girar en la direccion de la espiral, siempre consultar el manual o las indicaciones del fabricante

![Top 8 Milling Tools for New CNC Machinists - Fusion 360 Blog](https://www.autodesk.com/products/fusion-360/blog/wp-content/uploads/2018/05/1-rotation-direction.png)

### Direccion de corte (climb /conventional )

Recordemos que el filo y la forma de la herramienta afecta una serie de factores a la hora de cortar, por ejemplo la direccion hacia donde sale la viruta y la direccion del filo.

Dicho esto, normalmente **intentaremos que la direccion del corte sea igual que la direccion de giro de la herramienta**

* Se le llama al corte en direccion  contraria al giro de la herramienta **conventional cutting**
	* Requiere mucha menos energia y fuerza por parte de la maquina
	* Puede cortar mayor cantidad de material en una pasada
* Se llama al corte en direccion del giro de la herramienta.
**climb cutting**
	* Requiere mucha mas energia para hacer el corte, **no** lo usamos con cortes de mucho material o con maquinas chicas
	* Produce un mejor acabado
	* Bueno para cortes de terminacion.
	* la herramienta mordera fuertemente la pieza, si esta no esta firmemente sujeta podria salir despedida si se esta maquinando mucho material
		* Para minimizar este efecto, que el corte siempre este paralelo a la morsa

**En una maquina CNC siempre preferimos usar el climb cutting**

Video coparacion para clase
https://www.youtube.com/watch?v=galm5_6SUcM

### Calcular velocidad de giro y avance - WIP

En una fresa debemos colocar una velocidad de giro y de avance tales que no rompan la herramienta y corten el material lo mas rapido y eficientemente posible.

para eso tenemos que **ver las especificaciones del fabricante para la herramienta que tenemos segun el material que tenemos**

El fabricante nos dara
* **IPT  o chip load** Inches per tooth, pulgadas de material a morder por un diente. es decir, el **tamaño de una viruta por cada diente**
* **SFM** Surfice foot per min. Superficie de la herramienta por minuto

**Criterios:**
* Podemos variar el **IPT** dentro de algo razonable (15%)
	*  **IPT muy bajo** hace que el cortador resbale y genere friccion
	* **IPT muy alto** fuerza la herramienta y podria quebrarla

### Chatter / Vibraciones

[fuente](https://www.youtube.com/watch?v=rKPxfzx3sxE)

**chatter** es cuando la maquina vibra generando **problemas en el acabado de la pieza** y un **ruido muy molesto**.


![](https://i.imgur.com/UOgZO76.png)



 esto es causado por 
**CAUSAS:**
* **falta de rigidez** a lo largo de la maquina
* **Resonancia**

 Para evitarlo:

* **Sujecion**
	* La pieza debe estar perfectamente agarrada a la morsa
	* No debe haber partes que sobresalgan de la morsa
* **Herramienta**
	* Se debe usar el menor largo de herramienta posible para aumentar la rigidez
	* Elegir el menor largo de flute posible
	* Elegir el mayor ancho posible para aumentar la rigidez
* **avance y velocidad**
	* Usar el avance y velocidad correctos
* **Resonancia**
	* La herramienta y la pieza o la morsa pueden llegar a resonar, causando chatter, Si sucede variar levemente la altura de la herramienta para eliminar la resonancia
	* **Reducir/aumentar la velocidad**
		* Si la pieza resuena probar apretando el boton de **+-20%  speed** de la maquina y ver si deja  de vibrar

## Operaciones - WIP


# Herramientas

[videos fuente](https://www.youtube.com/watch?v=EB7B1zq8AM8)

A diferencia de los drill bits, que estan diseñados para **perforar hacia abajo**, los endmills estan diseñados para **cortar hacia los costados**



## Geometria general

### Largo y ancho

**largo**
* Cuanto mas larga la herramienta menos rigidez ( mas distancia entre el motor y la punta de corte)  y mas posibilidad de **chatter**
* **siempre elegir la herramienta mas corta posible**
* Siempre tratar de cortar con **todo el largo de la herramienta** para permitir un desgaste parejo
* Mas corto es mas barato

EL largo **utilizable** de una herramienta de fresado va desde la  punta hasta el final del angulo de la flute
![](https://i.imgur.com/tRfjT1I.png)


**Ancho**
* Cuanto mas ancho **mas rigidez** y  por ende menor posibilidad de **chatter**
* Cuanto mas ancho **mas precio**
* Cuanto mas ancho **mas rapido come material**

### Helicoidalidad de Flutes

#### Helicoidales normales
La forma de espiral de los flutes sirve para
* Evacuar la viruta
* Tener los filos
* Mantener una fuerza constante sobre la pieza (mientras un filo esta cortando, otro empieza a cortar, entonces **nunca "golpetean"** como sucederia si fueran filos rectos)
* Dividir la **fuerza de corte** en dos componentes, uno paralelo y uno perpenndicular. permitiendo mayor resistencia que si los filos fueran rectos
	* Cuantos **mas flutes**, se entiende que el material a cortar sera mas duro y tendran mayor angulo para transferir mas fuerza hacia abajo.



![](https://i.imgur.com/p7k4cRx.png)
_Division de fuerzas causado por la helicoidalidad_

![](https://i.imgur.com/kjPJQEa.png)
_Distribucion de la fuerza a lo largo del tiempo para evitar golpeteo y chatter_

Diferentes angulos de flutes, a **mayor cantidad de flutes** se interpreta que el **material a cortar sera mas duro** entonces el **angulo de la helicoidal es mas pronunciado** para **transferir mas fuerza hacia abajo en vez de hacia el costado** y **EVITAR QUE SE PARTA**

![](https://i.imgur.com/jkDTF0P.png)
_Diferentes angulos de helicoidales para mayor o menor distribucion de la carga hacia abajo_
#### Helicoidales especiales

Existen **flutes sin forma helicoidal** pero son muy poco comunes
Son **MUCHO** mas propensos a generar chatter debido a que generan un golpeteo con una cierta frecuencia muy pareja que puede ser similar a la de todo el sistema
![](https://i.imgur.com/Zyz6pbo.png)

![](https://i.imgur.com/51nRnCD.png)
_fuerza de corte a lo largo del tiempo para flutes rectos, notese que habra golpeteo_ 

Hay endmills que se diseñan para materiales laminados, que **evitan deslaminar el material** haciando un **sanguchito de fuerzas** con **helicoidales opuestas**, entonces **parte del material empuja para arriba y parte empuja para abajo**

![](https://i.imgur.com/CHoz0xk.png)

Existen tambien **helicoidales invertidas**, es decir  helicoidales que **cortan clockwise** pero **van counterclockwise**
Esto permite que **el flute empuje la pieza para abajo en vez de para arriba**, hay **materiales fragiles que lo requieren**

![](https://i.imgur.com/sEorwi1.png)


### **Cantidad de flutes**

[fuente](https://www.youtube.com/watch?v=Pm1N3ApOGlw)


A grandes razgos

* **Mas flutes**
	*  Mejor terminado
	* Mas filos sigifica que podemos tener **mas velocidad de avance** y entonces **cortar mas rapido** que con menos flutes
	*  Peor chip clearing
		* Si el material es duro, tenes chips mas chiquitos
		* En materiales blandos esto implica mas friccion entre chips, eso puede **derretir plastico** o **fundir aluminio** en lugar de cortarlo
* **Menos flutes** 
	*  Mejor chip clearing
		* Bueno si el chip es grande  por que el material es blando!
	*  Peor terminado

En terminos generales usamos

* **1 - 2 flutes**
	* Plastico
	* Madera
	* Metales blandos (aluminio)
* **3 - 4 flutes**
	* Detalles
	* Metales duros
* **>6**
	* Fibra de carbono
	* Acero de herramientas

### Angulos 
**Geometria de la punta**
La punta tiene un angulo llamado **rake angle**, este angulo puede estar 
* **Hacia el material (Positivo +)**
* **perpendicular al material (0 o neutral)**
* **Alejandose del material (negativo -)**

![](https://i.imgur.com/YrqE8Gb.png)

**Geometria del largo**
De la misma manera, los filos del largo tambien tienen rake angles que pueden ser


* **Hacia el material (Positivo +)**
* **perpendicular al material (0 o neutral)**
* **Alejandose del material (negativo -)**

![](https://i.imgur.com/4cZFjcR.png)


**ENTONCES:**
 * Un **rake angle positivo en ambas caras** 
	 * sirve para elementos blandos, ya que  los cortara con el filo.
	 * Toma menos potencia usarla (por que corta con el filo)
	 * El filo va a ser mas fino y por ende mas endeble
 * Un **rake angle negativo en ambas caras** surve para elementos mas duros
     * el filo no corta, sino que **raspa** el material
	 * El filo es mas grueso, y por ende mas fuerte
	 * Se usa en materiales mas duros
	 * toma mas fuerza


### enter/non-center cutting
[fuente](https://www.youtube.com/watch?v=eH50t7kUx6c)

**Center cutting endmill**

Son endmills que tienen la capacidad de cortar hacia abajo en el eje $Z$ sin moverse en $XY$, Tienen **un filo unferior** en **ROJO** y huecos para **evacuar la viruta** en **AZUL**

![](https://i.imgur.com/uE5AY1C.png)


**Non-center cutting**

Son endmills que cortan por cortadores radiaales pero en el centro no cortan.
![](https://i.imgur.com/3f5frqP.png)
Eso implica que **no podemos taladrar con ellos**, sino que tenemos que hacer agujeros de manera helicoidal. y una velocidad de avance en el eje $Z$ baja comparada con $XY$

## Geometrias especiales

### Rougth cutting endmills

Son endmills diseñados para **Cortes de gran profundidad**, tienen un patron de **zig-zag** sobre los flutes que sirve para **romper la virtua** de manera mas efectiva, ya que  los **cortes profundos generan virtuas largas dificiles de extraer**

![](https://i.imgur.com/neV67EE.png)

### Square endmill

 Este tipo de endmill tiene bordes a 90 grados, eso hace que los bordes del corte queden muy **rectos**. tiene la desventaja de que **esto hace que ese borde sea fino y entonces fragil, por lo que tiende a romperse**
![](https://i.imgur.com/sSiy9E6.png)

### radius endmills

Tienen el borde redondeado.

En un endmill normal, las puntas son filosas y finas, esto las hace mas propensas a romperse y a tener menor fuerza. 

* Las puntas tienen mayor fuerza
* Los bordes del fondo del agujero seran redondeados en lugar de rectos
* Preferido para **rougthing** por que al ser mas fuerte durara mas

![](https://i.imgur.com/gg4JH6I.png)

### ball nose  endmill

Son endmills con puntas redondeadas.

Sirven para maquinar cualquier  superficie que no sea perpendicular a la herramienta.
**siempre que se pueda se corta de low a high, ya que  el centro de la punta de la esfera no tiene mucha capacidad de corte**

EJ:
* Radios internos/externos
* formas curvas que no estan en el eje $XY$

![](https://i.imgur.com/fR1et6S.png)

Es un **center-cutting endmill**, se puede apreciar como dos de los flutes forman el filo
![](https://i.imgur.com/ooJrekl.png)




## Material de la herramienta


[fuente](https://www.youtube.com/watch?v=EB7B1zq8AM8)


**Acero rapido**


* **No tan duro**
	* Solo corta cosas mas blandas que acero
 	* se parte menos facilmente por no ser tan rigido
* **Filo**
	* En vez de partirse, se desafila
	* Si el feed and speed no estan bien, la herramienta sobrevive y solo se desafila
	* Filo poco duradero
	* Muy filoso y se puede afilar mucho
	* Al ser mas filoso requiere menos fuerza de maquina
	* Corta muy limpiamente materiales blandos debido al gran filo
* **Afilado y economia** 
	* Barato de adquirir
	* Reemplazo o afilado frecuente, por lo que es caro para la produccion en masa de piezas


**Acero rapido con cobalto**

* Un poco mas duro que el high speed steel
* Un poco mas caro

**Powdered metal tooling**
* Mas duro que high speed steel, pero menos duro que el tungsten
* Menos fragil que el carbide
* Se usa mucho en cortes gruesos


**Tungsten carbide**

* **Durisimo**
	* Corta cualquier material duro
	*	Puede hacer cortes mas profundos
* **Filo** 
	* No puede ser muy afilado mucho por que se parte el filo debido a la  fragilidad		
	* La falta de filo evita que corte limpiamente materiales blandos
	* La falta de filo hace que necesite mas fuerza de maquina
	* Al ser tan duro no se desafila con facilidad, por lo que duran mucho usadas correctamente
*	**Fragil**
	*	 Se parte con facilidad total o parcialmente
	*	 No se desafila, se parte
	*	Si el feed y speed no estan bien, se parte el filo
* **Economia**
	*	Caro de adquirir
	*	Dura mucho, asi que es economico para la produccion en masa
	*	Se reemplaza de manera poco frecuente si estan bien los feeds y speeds

## Coatings de la herramienta

Las herramientas pueden estar recubiertas de diferentes materiales para extender su vida util y su filo




## Face mills


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY3Nzg0MzkwMSw3MjQwMDQ1ODMsLTMxOT
A5NTUxNCwxOTgxMjg2NjM3LC03OTQ0Njc3NzcsLTM5NDMxNTk5
NCw4MDYzODAxMjMsOTY4MzkxMjUzLDEwMzE1MDkzNDEsMjAzNT
U3NDU4MCwxODI1ODg0MTY4LC04NTgwOTMwODcsLTE3NTAzODYz
MDgsNjk3NjAwNjIxLC02Njg3MDkzNjQsLTE2OTc4OTQ0OTQsLT
E3MDEyNDk5NTUsMzA0MDg3NjUwLDExMTU0Mzk1MzMsMTMzOTE3
ODkxM119
-->