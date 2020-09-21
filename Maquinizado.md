**viendo**
https://www.youtube.com/watch?v=_HGGkCaYMVA&list=PLY67-4BrEae9m8v20LNARIRl9Pd9bdFRZ&index=3

**despues ver para lathe**
https://www.youtube.com/watch?v=H6Dnmd3lDzA&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN

# Fresa
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

La herramienta debe girar en la direccion de la espiral, siempre consultar el manual o las indicaciones del fabricante

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



## Operaciones - WIP


## Herramientas

[videos fuente](https://www.youtube.com/watch?v=EB7B1zq8AM8)

A diferencia de los drill bits, que estan diseñados para **perforar hacia abajo**, los endmills estan diseñados para **cortar hacia los costados**

### Largo y ancho

* **largo**
	* Cuanto mas larga la herramienta menos rigidez ( mas distancia entre el motor y la punta de corte) 
	* **siempre elegir la herramienta mas corta posible**
	* Siempre tratar de cortar con **todo el largo de la herramienta** para permitir un desgaste parejo
	* Mas corto es mas barato
* **Ancho**
	* Cuanto mas ancho **mas rigidez**
	* Cuanto mas ancho **mas precio**
	* Cuanto mas ancho **mas rapido come material**

### **Cantidad de flutes**

A grandez razgos

* **Mas flutes**
	*  Mejor terminado
	*  Peor chip clearing
		* En materiales blandos esto implica mas friccion entre chips, eso puede **derretir plastico** o **fundir aluminio** en lugar de cortarlo
* **Menos flutes** 
	*  Mejor chip clearing
	*  Peor terminado

En terminos generales usamos

* **1 - 2 flutes**
	* Plastico
	* Madera
	* Metales blandos
* **3 - 4 flutes**
	* Detalles
	* Metales duros
* **>6**
	* Fibra de carbono

### Material de la herramienta


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

### Coatings de la herramienta

Las herramientas pueden estar recubiertas de diferentes materiales para extender su vida util y su filo

### Geometria

* Endmills Rectos
	* Genera bordes perfectamente rectos
* Endmills conicos / taped
	* Genera bordes en un angulo
* Fishtail endmills
* Ball-nose
	* Se usan mucho para hacer moldes 

## Seleccion de herramienta / Endmill - WIP

Tipos de herramientas
* Center cutting
* 






# Tornos
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTM4Nzg2MDM2LC0xNTMyNDcyMzY3LC00Mj
c0OTY5MzQsLTEzOTMwNjY2MjgsODIzOTAxNjE5LC0yMTAxNzUw
MDg2LC03MzI0MzA3NTMsLTEyMjQzODMyNzMsNzg2MzYxOTY0LC
0xODA3OTkyMDUyLDExNDc1MTQyMTksNzQ2Mzk4Njg2LC0xOTc0
Njc3NDU1LDI5MDgzMTc5OCwtMTkzMjUyNTU4OCwtMzMxODk1Nz
Q1LDE2MzI3OTMzNzgsMTM0MjY3NzczNSw5NjEwODYyNzUsNTg3
ODk5NDYxXX0=
-->