
Viendo
https://www.youtube.com/watch?v=g3HPqpe3kes&list=PL35sMcDwCf0iXK_K4H_m_V-8HbmI8MS55&index=3


Ver:
https://www.youtube.com/watch?v=KO3_SfZo_QE&list=PLaCDmykyjVw8cABQfqSll18S65kkfNBN9

 **setup de cnc mill**
https://www.youtube.com/watch?v=4HWuhbhySpw&list=PLpl7LvSkK4IFDD4G638p6_Sr-BUl20Ocn
**CNC lathe programming**
https://www.youtube.com/watch?v=o9vXeH8lCjQ&list=PL35sMcDwCf0iL-pMqxzclnKoLpCGShkI7

# Intro



Las computadoras en lineas generales funcionan leyendo una lista de instrucciones escrita en un lenguaje que sepan interpretar.

Los sistemas CNC (tornos, fresas, impresoras 3d, maquinas de corte, etc) funcionan con un lenguaje que esta estandarizado internacionalmente, es decir que utilizan el mismo lenguaje, denominado "codigo G"

El "codigo G" es una lista de instrucciones que le dice a la maquina a donde moverse, cuando cambiar de herramienta, cuando encender el laser, cuando girar la pieza en el torno, con que velocidad avanzar, etc.

Conociendo codigo G nosotros podemos explicarle a cualquiera de esas maquinas como fabricar una pieza que nosotros queramos, Existen ademas programas en los que podemos diseñar una pieza en 3d y nos devolvera el codigo G para subirlo al torno.

**aun sabiendo eso, debemos leer el manual del usuario de la maquina, ya que hay ligeras diferencias entre cada maquina que hace que no podamos meter cualquier programa en cualquier maquina**

Comenzaremos programando maquinas simples y gradualmente iremos a las mas complicadas, con ejercicios practicos en un simulador para practicar en cada una. Las maquinas en cuestion son:

* **2 ejes:** cortadoras laser, plasma
* **3 ejes** fresas, tornos e impresoras 3D
* **5 ejes** fresas


# Maquinas 2D- WIP

En esta unidad hablamos de maquinas de corte laser donde no usamos valores de profundidad (eje $Z$) ni tenemos que preocuparnos por giro de una herramienta, profundidades de corte ni tamaño de la herramienta




## Coordenadas

Hay algunas cosas que tenemos que decirle a la maquina antes que empecemos a mover nada.
La maquina va a usar coordenadas $(X,Y)$ para desplazarse, coordenadas que nosotros pondremos en el  codigo $G$.

La maquina conoce un punto particular, al que llamamos **cero maquina** o **home point** y corresponde a la coordenada $(0,0)$

La posicion en cualquier momento de la maquina siempre esta determinada por el centro del porta herramienta, independientemente del diametro de la misma.

En el caso de una herramienta de corte laser o plasma 2D, la **coordenada se corresponde con el lugar de corte**. no asi en un torno o fresa.

### Coordenadas absolutas y relativas

Existen en lineas generales dos tipos de coordenadas

* **Coordenadas absolutas**  las coordenadas siempre son con respecto a un $(0,0)$ fijado desde un principio por la maquina
	* `G90; de aca en adelante se usan coord. abs`
* **Coordenadas relativas** Las coordenadas siempre son con respecto a la posicion actual de la maquina, el $(0,0)$ es donde estas parado
	* `G91; desde ahora se usan coord. relativas`

**Critico: es super importante verificar que estamos en el sistema de coordenadas correcto antes de correr un programa!**

### Unidades

Las maqunas CNC pueden tener sus coordenadas en **milimetros** o en **pulgadas**. para indicarle a la maquina que tipo de unidades utilizamos utilizamos 

    G20; para pulgadas
    G21; para milimetros

**Siempre debemos indicarle a la maquina en que unidades vamos a trabajar al inicio de cada programa**


## Movimientos
### movimiento linear 2D

El movimiento recto desde la **posicion actual de la herramienta** al punto $(1,1.1)$ 


**MOVIMIENTOS RAPIDOS:**

para hacer cortes rapidos que **no son para corte, sino solo para mover la herramienta en el aire** 
* se indica en codigo $G$ con la instruccion `G0`seguido de las coordenadas del punto al que me quiero mover.
	* ejemplo `G0 X1 Y1.1` 

**MOVIMIENTOS LENTOS DE CORTE:**
para hacer cortes lentos  que **si son para corte de material** 
* Se indica la velocidad de corte en **unidades por minuto**con el comando `F` y la velocidad
* Se indica en codigo $G$ con la instruccion `G1`seguido de las coordenadas del punto al que me quiero mover, opcionalmente junto con la **velocidad de avance en unidad/min** 
	* Recordamos que las unidades estan seteadas desde antes por `G20` o `G21`
* ejemplos
	*   `G1 X1 Y1.1 F10;`
	* ``` 
			F10;
			G1 X10 Y10;
			G1 X20 Y30;
			```
	*  una vez indicada la **velocidad de avance** esta queda configurada para todo `G1`hasta la proxima vez que se invoque `F`
		 


#### ejercicio simplificado

![](https://i.imgur.com/N4skT1B.png)

    
    (estoy parado en X0 Y0 antes de iniciar mi programa)
    G21;
    F10;
    G1 X1 Y1;
    G1 X2 Y1; moverte a la posicion 2,1 a vel. de corte
    G1 x2 Y3; movete a la posicion 2,3 a vel. de corte
    G2 X1 Y3;
    
### movimiento curvo 2D

El movimiento curvo desde la **posicion actual de la herramienta** al punto $(1,1.1)$ haciendo un radio de $0.5mm$ de radio

**Posibilidad 1**
* para hacer cortes lentos  **en direccion de las agujas del reloj** que **si son para corte de material** se indica en codigo $G$ con la instruccion `G2`seguido de las coordenadas del punto donde terminara nuestro arco, seguido del radio de giro indicado con $R$
	* ejemplo  `G2 X1 Y1.1  R.5` 
* Para hacer cortes **en direccion contraria a las agujas del reloj** utilizamos la misma estructura pero con la instruccion `G3`
	* ejemplo  `G3 X1 Y1.1 R.5`

**Posibilidad 2**
Algunas maquinas en lugar de utilizar la  instruccion $R$, utilizan las instrucciones $I$ y $J$, que indican donde esta el centro del circulo con respecto a la herramienta

Si quiero indicar un arco desde mi posicion actual al punto $(1;1.1)$ y  que el centro de mi arco esta a $5mm$ de mi posicion actual en el eje $X$ y a $3.4mm$ de mi posicion actual en el eje $Y$ lo hago de la siguiente manera
* `G2 X1 Y1.1 Z0 I5 J3.4`

#### ejercicio simplificado

Usando una herramienta de 0.5mm de diametro, decida una serie de coordenadas para trazar la siguiente pieza.
Recuerde que todas las coordenadas tienen que tener un offset de 0.25mm, ya que ahi esta el borde de corte de la herramienta

![](https://i.imgur.com/kgIuHBM.png)


### Back home

En cualquier momento podemos indicarle a la maquina que mueva el husillo a la posicion $(0,0)$ de **la maquina**. Esto ignora cualquier offset.

    G28; volver a la posicion home

## Coordenada cero maquina

Al encender la maquina, pueden pasar dos cosas:

* **maquinas caras:** Algunas maquinas automaticamente buscaran el punto $(0,0)$, moviendose en una direccion en cada eje hasta tocar un sensor
* **maquinas hobbistas:** El $(0,0)$ estara en el lugar donde apenas se enciende la maquina, aunque muchas veces existe un mecanismo para llevarla a un cero mas util



## Work offsets

#### teoria
El work offset sirve para **cambiar el sistema de coordenadas**, en lugar de que el punto $(0,0,0)$ este en la posicion default de la maquina, lo especificamos para que este en otro lado, por ejemplo **en un lugar cercano a la pieza donde queremos empezar a trabajar**.

Lo especificamos con un punto desde desde el $(0,0)$ de la maquina hasta el punto que nosotros queramos, ese sera el **nuevo origen** $(0,0)$ de ahi en adelante

![](https://i.imgur.com/T0k6gRv.png)



 los offsets muchas veces se colocan en una hoja de offsets en la maquina para evitar necesitar especificarlo en cada programa

Podemos tener varios work offsets diferentes programados tanto en la maquina como en nuestro programa.

#### Practica codigo G
Para programarlos utilizamos las instrucciones `G54` al `G59`, es decir que podemos tener **8 offsets** de la siguiente manera

* Si el offset ya esta programado en la maquina directamente usamos
  *  `G54; Colocar el (0,0) en el offset 52 ej en (1,1)`
 * Si el offset no esta programado, entonces lo especificamos
	 * `G54 X1 Y1; el nuevo 0,0 desde ahora esta en 1,1`

**Ejemplo:**
 
 Offset colocado dentro del codigo

    G40; Desactivo todos los offsets
    G0 X0 Y0; Me muevo al cero default de la maquina
    G54 X1 Y1; Indico nuevo sistema de coord. 0,0 en 1,1
    G0 X0 Y0; La maquina se movera al punto 1,1
    
offset ya programado en la tabla 

    G40; Desactivo todos los offsets
    G0 X0 Y0; Me muevo al cero default de la maquina
    G54; Indico nuevo sistema de coord. ej 0,0 en 1,1
    G0 X0 Y0; La maquina se movera al punto 1,1
    


## manejo de la herramienta - WTF

En el caso de las maquinas de corte 2D, nuestra herramienta es un **laser** o una **cortadora de plasma**

* **abrir puerta**
* **Encender laser/cortadora**
* **apagar laser/cortadora**
* **Volver a la posicion home (0,0)**


## Instrucciones modales y no-modales

Las instrucciones modales son aquelllas que una vez que se dictan quedan guardadas en la maquina hasta que otra instruccion las cambie.

 ejemplos son:
* `F` velocidad de avance
* `S` Velocidad de giro
* `G20` y `G21` unidades mm o pulgadas

Otras instrucciones no son modales y solo cambian las lineas 

## La linea de seguridad

Para todos nuestros programas siempre queremos evitar accidentes.
Cosas como que la maquina no este en coordenadas absolutas, 

Un ejemplo de una  linea de seguridad para maquinas 2D de corte laser seria 


```
G21; usaremos milimetros
G90; coloco la maquina en cood abs
G28; volver a la posicion (0,0)
G94; avance por  minuto
```

## Estructura de un programa basico -WIP

```
G21; usaremos milimetros
G90; coloco la maquina en cood abs

```
    


# Maquinas 3D - Fresa - WIP

En esta unidad introducimos el tercer eje y las complejidades de programar una fresa, tales como situar la herramienta donde nosotros queremos, tener en cuenta el tamaño de la herramienta, la altura de la herramienta, etc.


## Unidades

Tenemos algunas unidades nuevas, principalmente por que ahora tenemos cosas que **giran**, y tenemos **avances `G1`** que pueden ser utiles en realacion al **tiempo** o al **giro**


    G94; avance por minuto, muy commun para FRESAS
    G95; avance por revolucion, muy comun para TORNOS


## Movimientos en 3D

### Movimientos rectos en 3D

Son iguales que en 2d pero incorporamos el eje  $Z$
	
	F5
    G0 X0 Y0 Z0;
	G1 X1 Yx Z1;

### Movimientos curvos en 3D - WTF

Si tenemos 3 ejes entonces podemos hacer movimientos curvos en varios planos y formas!. esto añade un poco mas de complejidad a nuestro comando `G2` y `G3`

### Back home

#### G28 - punto intermedio
**Atencion: el comportamiento de G28 varia fuertemente de maquina a maquina!**

En el caso de las maquinas 3D, siempre queremos asegurarnos de que la maquina **se aleje de la pieza en el eje Z** antes de moverse en los demas ejes al volver a la posicion $(0,0)$ para **evitar que golpee contra la pieza**

Para eso usamos

    G28 <posicion intermedia>;

`<posicion intermedia>` por default es el $(0,0,0)$ del **work offset**, esto **PUEDE OCASIONAR UN CRASH**


Queremos que la maquina se mueva hacia arriba en $Z$ sin importar su posicion en $X,Y$ (que es lo que queremos) entonces usamos la **coordenadas relativas** con $G91$


    G28 G91 x0 y0 Z30; volver a la posicion home
    ;pero antes ir a Z3 (osea elevar
    ; el usillo 30mm para arriba )
	G90; Volver a modo absoluto


**CRITICO:**
El uso de $G91$ nos asegura que estemos llendo hacia arriba y no nos movamos en ninguna otra direccion, sin importar el **work offset** o el sistema de coordenadas que usemos. Caso contrario las coordenadas seran con referencia al **work offset**

#### G28 - unico eje 
La maquina tambien puede aceptar el siguiente comando


    G28 G91 Z0;

Que implica que no te moves en ninguna direccion, pero **solo vas a home en el eje  $Z$**

#### G53 - Recomendado

   `G53` me permite hacer un movimiento en la linea en la que es llamado usando como referencia el **cero maquina** e **ignorando todos los offsets**
   
Puedo usarlo para volver al **home** asi

    G53 G0 G90 Z0; ir al Z0 de la maquina primero
    G53 G0 G90 X0 Y0; ir al cero maquina.



## Diferencias con fresa manual
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


## Manejo de herramientas - WIP

La fresa CNC tiene en general una serie de codigos basicos que manejan la herramienta o la maquina en general

* `M1` pausa opcional - Permite detener la maquina en este paso si el operario esta presionando un boton
* `M30` fin del programa



### Cambio de herramienta 

Para cambiar de herramienta debemos
* **Alejarnos** de la pieza para asegurarnos de no chocarla
* **Seleccionar** la herramienta que queremos con `T3` donde `3` es el numero de la herramienta, en maquinas grandes esto hace que la maquina prepare la herramienta para el cambio
* **hacemos el cambio** con el comando `M6`

EJ:
	
	G28 G91 Z0; anda a home en el eje Z para no chocar
    T3M6; cambia la herramienta


### Giro de la herramienta

* `S200` indica una velocidad de giro de 200 unidades/min
* `M3` comienza el giro de la herramienta clockwise
* `M4`comienza el giro de la herramienta counter-clockwise (menos comun)
* `M5` detener el giro de la herramienta


### Otros

* `M8` activa flujo de enfriante/lubicante
* `M9` detiene el flujo de enfriante/lubricante





## Offsets

### Cutter compensation

#### Teoria

Podemos indicarle a la maquina el radio de nuestra herramienta para evitar tener que programar las coordenadas teniendo en cuenta ese radio.

Generalmente programaremos el diametro de cada herramienta en el panel de la maquina, con lo que la maquina sabra de antemano que radio correspondera a cada herramienta.
![](https://i.imgur.com/nak8vo5.png)


![](https://i.imgur.com/BqBX6Vt.png)
![](https://i.imgur.com/Kw6enDk.png)

 Para eso utilizaremos

* `G41` El ajuste para cuando el material esta a la izquierda de la herramienta
	* `G41 P0.5` puedo indicar que el radio de ajuste es de 0.5 si es que no lo configure en el listado de herramientas de la maquina
	* `G41 D1` indico que use el offset 1 de la tabla, generalmente corresponde a la herramienta numero 1
* `G42` El ajuste para cuando el material esta a la derecha de la herramienta
	* `G42 P0.5` puedo indicar que el radio de ajuste es de 0.5 si es que no lo configure en el listado de herramientas de la maquina
	* `G42 D1` indico que use el offset 1 de la tabla,generalmente corresponde a la herramienta numero 1
* `G40` Desactivar ajuste
	* **SIEMPRE** desactivamos el ajuste cuando terminamos de cortar y estamos lejos de la pieza
	
	

**CRITICO:**
en cuanto doy el comando $G41$ , $G42$  o $G40$ la maquina ajustara en **ese instante** la herramienta.
* osea **no que puedo estar al lado del material** por que lo voy a cortar sin querer o partir la herramienta 

![](https://i.imgur.com/X6gE1Pj.png)

#### Ejercicio

![](https://i.imgur.com/N4skT1B.png)
En maquinas donde no hay table

   
    G42 P3; mi herramienta tiene un radio de 3mm
    G0 X0 Y0; movete con ese offset a la posicion de inicio
    G1 X1 Y1;
    G1 X2 Y1; moverte a la posicion 2,1 a vel. de corte
    G1 x2 Y3; movete a la posicion 2,3 a vel. de corte
    G2 X1 Y3;
    G40; desactivo el offset
    G0 X0 Y0; vuelvo a la posicion de reposo

En maquinas donde quiero usar un offset que esta configurado en una tabla de la maquina

    G42 D1; Use el offset numero 1
    G0 X0 Y0; movete con ese offset a la posicion de inicio
    G1 X1 Y1;
    G1 X2 Y1; moverte a la posicion 2,1 a vel. de corte
    G1 x2 Y3; movete a la posicion 2,3 a vel. de corte
    G2 X1 Y3;
    G40; desactivo el offset
    G0 X0 Y0; vuelvo a la posicion de reposo


### Work offsets


Operan igual que en 2D pero en 3 dimensiones

![](https://i.imgur.com/T0k6gRv.png)


Usamos las mismas instrucciones

* Si el offset ya esta programado en la maquina directamente usamos
  *  `G54;ir al offset 52`
 * Si el offset no esta programado, entonces lo especificamos
	 * `G54 X1 Y1; el nuevo 0,0 desde ahora esta en 1,1`
    
#### Practica con jogfinder

La maquina puede detectar su posicion en cualquier momento, por lo que podemos encontrar las coordenadas de cualquier punto de la pieza moviendo manualmente la maquina (torno o fresa) hasta encontrar el punto. Para esto se usa un aditamento para tal fin

https://www.youtube.com/watch?v=_kZlQdr7iJ0

### Tool length offsets

#### Teoria

Por defecto las coordenadas siempre son con referencia a la punta del mandril que sostiene la herramienta, esto es muy incomodo.

El tool offset nos permite indicarle al cnc **donde esta la punta o el filo de la herramienta**. de esta manera todas las coordenadas que coloquemos seran siempre con referencia a la punta o filo de la herramienta y no al mandril.

![](https://i.imgur.com/JWqlRIY.png)

#### Practica: codigo G

Dado que hemos configurado el tool offset en una de las paginas de la maquina para cada herramienta y los hemos guardado en una lista numerada, para elegir un offset usamos

    G43 H1; donde 1 es el numero del offset


#### Practica: Hallar altura de la herramienta 
minuto 11
https://www.youtube.com/watch?v=_kZlQdr7iJ0



### Movimiento ignorando todos los offsets (G53)

Si queres hacer un movimiento en la maquina ignorando **todos** los offsets (tool, work, cutter, etc) usas $G53$

    G53 G0 G90 X0 Y0 Z0

## Safety line

Usamos una linea de seguridad al comienzo de cada programa para asegurarnos evitar accidentes.

* `G0` por si estabamos en otro modo de movimiento
* `G17` nos pone en el plano $XY$ (sirve si la maquina es de 6 ejes)
* `G40` apagar cutting compensation
* `G49` apagar tool offset
* `G80` cancelar cualquier ciclo que este en proceso
* `G90` colocar la maquina en coord absolutas
* `G94;` avance por  minuto
* `G21` setear la maquina en milimetros


y elevamos la maquina en el eje $Z$
.

    G0 G17 G40 G94 G49 G80 G90 G21;
    G28 G91 Z0;

## Estructura de un programa basico 


Juntamos todo lo aprendido para hacer un programa elemental que haga una hendija de 1mm de profundidad en una sola pasada.

```
(linea de seguridad)
 G0 G17 G40 G94 G49 G80 G90 G21;
(Herramienta arriba)
G28 G91 Z0; 
(cambiar a herramienta numero 1!)
M06 T1;
(cutter comp. para la herramienta 1)
G41 D1;
(cargar el segundo work offset, G54 a G59)
G55;
(velocidad de avance y de giro)
F10;
S300;
(nos paramos encima de la pieza)
G0 X10 Y10 Z2;
(cortamos)
G1 X10 Y10 Z-1;
G1 X20 Y10 Z-1;
G1 X20 Y20 Z-1;
(elevamos la herramienta)
G28 G91 Z0;
(Guardamos la herramienta)
G28 X0 Y0 Z0;
(Fin del programa)
M30;  
```


## Canned cycles

Un canned cycle es una funcion del CNC que permite hacer tareas repetitivas con poco codigo. por ejemplo

* Hacer multiples agujeros
* Hacer multiples roscas

### G80 - Cancelar canned cicle

Siempre que terminemos de usar un canned cycle, tenemos que cancelarlo para no tener inconvenientes despues. Para eso usamos `G80`




### G81 - introduccion, Perforaciones

#### Simples
Para hacer una serie de agujeros en una pieza podemos usar el canned cicle de perforaciones. 
Su funcion es tener un comando corto y comodo para:
*  Posicionarse en un lugar
* Taladrar el aguero
* Subir la mecha encima de la pieza
* Repetir las veces necesarias


Para usar comodamente G81 conviene que las **work coordinates** esten prolijamente seteadas, principalmente $Z=0$ en la superficie de la pieza


`G81` espera los siguientes parametros:
* `X Y` indican la posicion del agujero en **work offset**
*  `Z` indica el final del agujero en **work coordinates**, si $Z=0$ esta en la superficie de la pieza, entonces indica la **profundidad del agujero**
* `R` indica a que altura en $Z$ debe subir la herramienta en **work coordinates** al finalizar un agujero
* `F` indica la velocidad de avance (mm/min o inches/min)
* `P` pausa entre un agujero y el otro en milisegundos (opcional)

```
	(agujero en 50,30 con final en -10 y velocidad 50mm/min)
	(al terminar ir a Z=1)
    G81 X50.0 Y30.0 Z-10.0 R1.0 F50.0;
	G80; terminar ciclo
```
#### Multiples
Podemos usar el comando para hacer todos los agujeros que queramos. Las coordenadas siguientes son en **coordenadas relativas** o **incrementales**
```
    G81 X50.0 Y30.0 Z-10.0 R1.0 F50.0;
    (aca van los demas agujeros)
    (en coordenadas INCREMENTALES)
    X20 Y20; otro aguj. 20mm abajo y a la derecha del prim.
    X20 Y20; otro mas, 20mm abajo y a la derecha del segund.
    X0 Y40; otro, 40mm abajo del anterior
    X0 Y40 Z-5; otro, 40mm abajo del anterior y profund. 5mm
	G80; terminar ciclo
```
### G98 - G99 Ciclo con evasion de obstaculo

Si tenemos pedazos de pieza que hay que evadir entre un agujero y el otro usaremos los codigos `G98` y `G99`

**la evasion se puede usar en casi cualquier tipo de ciclo**

* `G99` nos permite usar la altura $Z$ previa al llamado de `G81` para poner la herramienta en un lugar seguro
* `G98` nos permite usar la coordenada $R$ tal como se hace normalmente

```
	(estoy lejos de la pieza, por que Z=30!)
	G00 X10 Y10 Z30;
	(uso G98 para decirle a la maquina: acordate de Z=30)
    G81 G98 X50.0 Y30.0 Z-10.0 R1.0 F50.0;
    
    (maquina se separa 1mm de la pieza dps de cada agujero)
    (por que R=1mm)
    X20 Y20; 
    X20 Y20;
    
    (Aca hay que evadir un obstaculo! me elevo a mi)
    (Z anterior al ciclo que era Z=30) 
    X0 Y40 G98;
    
    (ahora sigo usando mi altura R=1mm como antes)
    (indico esto con G99)
    X0 Y40 G99;
    
    (sigo haciendo agujeros con mi R=1mm)
    X0 Y40;
    X0 Y40;
	G80; terminar ciclo
``` 

### G83 - Perforacion c/pecking c/ retraccio total

Identico a `G81` pero cada cierta profundidad el taladro sube hasta $Z>0$ (idealmente en **work coordinates** para que este sobre la superficie de la pieza) para sacar la viruta del agujero

Todo lo que era valido para `G81` se puede hacer en `G83` (evasion de obstaculo con `G98-G99`, diferentes profundidades, etc)
 
 se agrega un nuevo parametro
 
 * `Q 3`  la cantidad de mm de perforacion entre cada vez que el taladro sube para sacar la viruta. ej `3`mm 
 
```
	(identico a G81 pero con un valor Q)
    G83 X50.0 Y30.0 Z-10.0 R1.0 F50.0 Q5;
    X20 Y20;
    X20 Y20;
    X0 Y40; 
    X0 Y40;
	G80; terminar ciclo
```


### G73 - Perforacion c/pecking c/ retraccio parcial

Identico a `G83`, pero en lugar de subir sobre la pieza cada cierto intervalo para sacar la virtua, sube una pequeña distancia para romperla y quebrarla. la **pequeña distancia** en general **no es cofigurable**

Este ciclo es compatible con todo lo que se puede hacer con `G81` (evasion de obstaculo, alturas diferentes, perforaciones multiples, etc)
```
	(identico a G81 pero con un valor Q)
    G73 X50.0 Y30.0 Z-10.0 R1.0 F50.0 Q5;
    X20 Y20;
    X20 Y20;
    X0 Y40; 
    X0 Y40;
	G80; terminar ciclo
```


### G74 - G84 - Tapping / Roscado

Para roscar un agujero usamos:

* `G84` para rosca derecha
* `G74` para rosca izquierda



Inicalmente se ve igual a un agujero comun con `G81`, la diferencia principal es que
* **CRITICO:** Las **revoluciones por minuto** que colocaremos dependeran del material, y la herramienta. ver info del fabricante de la herramienta! (el macho)
* **CRITICO:** En base a esa velocidad, debemos calcular cuidadosamente la **velocidad de avace** para lograr una rosca con el macho que estemos utilizando!
* Al finalizar el agujero, la instruccion gira en reversa para volver a subir sin romper la rosca creada.

**Pasos:**
* Determinar que macho vamos a usar, esto puede **[afectar nuestra programacion de profundidad](https://www.youtube.com/watch?v=bkrUzGooA9k)**!!
* Determinar las $\text{RPM}$ recomendadas por el fabricante del macho que vamos a usar para el material que vamos a usar
* calcular la velocidad de avance 
	* **Roscas en pulgadas:**
		* ej: rosca $\text{UNC} \frac{ 1}{2} -13$
			* Tiene 13 hilos por pulgada
		* $\frac{\text{hilos por pulgada}}{ \text{RPM} }= \text{avance}\frac{in}{min}$
		* Si la maquina esta en $mm$, hacemos la conversion
			* $1in=25.4mm$
	* **Roscas milimetricas**
		* ej: rosca $M12 \text{ X } 1.75$
			* Tiene 1.75mm entre cada hilo
		* $\text{mm por hilo}. \text{RPM }= \text{avance}\frac{mm}{min}$
* Programar la maquina con 
	* esas $RPM$ 
	*  ese $\text{avance}$
	* La direccion de giro correcta `G74`o`G84`

Nuevamente, es compatible con todas las alteraciones que le podemos hacer el `G81` (evasion de obstaculos, multiples agujeros, etc)

Ejemplo:

```
(Estoy haciendo una rosca de M16x0.5 hilos por mm, osea 0.5
mm entre cada hilo, si voy a 40 rev/min entonces
0.5*40= 20mm/min de avance)

S40; vel. de giro a con 40rev/min
G0 X10 Y10 Z5; Voy a donde quiero hacer el agujero
G84  Z-10 R1 F20; avanzo a 20mm/min
x0 Y20; hago otro
G80; salgo del ciclo
```


# Maquinas de 6 ejes - WIP

https://www.youtube.com/watch?v=LfAxkMOvEgk&list=PL35sMcDwCf0iXK_K4H_m_V-8HbmI8MS55&index=8




<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEwNzY4ODc3NSwxNTkzMzY4MTQ2LC0zNT
IwMzUxMDMsMTA2MTExNTY4NV19
-->