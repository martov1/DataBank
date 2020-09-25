**FALTARIA HABLAR DE**
* Endmills conicos / taped
	* Genera bordes en un angulo
* Fishtail endmills


**Seguir viendo**
https://www.youtube.com/watch?v=5V0s6fLyRH0&list=PLY67-4BrEae9m8v20LNARIRl9Pd9bdFRZ&index=

**Fortalecer con**
https://www.youtube.com/watch?v=15p1Kerb4N8&list=PLNvVbYXgJCEU2yqoOpEHB0mbDEttFgH7j

**mas detalles**
https://www.youtube.com/watch?v=p4JpLKNPs9U&list=PLups-28TmUhLod3H0vhIDHl_qXPfWikfn


**Detalles copados**

https://www.youtube.com/watch?v=bKksH9UAbO8&list=PL6015CA604E06A0C6

**entender esto de zig zag**
https://www.youtube.com/watch?v=KNwAHE73SHk&list=PLzc0Bm2I_0pn1lfdvG2xIG_z4-YiaTq1H&index=7

## Seguridad

Para manipular una fresa es necesario:
* Pelo corto o atado
* Proteccion ocular
* mangas cortas
* Sin anillos, joyas, cadenas ni nada colgando
* No acercar las manos a la maquina mientras este girando o moviendose

## Comandos y partes de la fresa
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

### Width of cut/ length of cut

* **Width of cut:** que porcentaje de la herramienta esta embutida en el material. Intentar alrededor de **30%** para 
	* una mejor evacuacion de chips.
	* Menor temperatura
	* Menor necesidad de lubricacion 
	* Reduce riesgos de atrapamiento de viruta y consecuente desafilado
	* Podes tener mayor width of cut (100%) pero hay que tener cuidado de que evacues los chips (lubricante, aire comprimido, geometria del material etc que permitan evacuar chips)

.

* **Deepth of cut:** que profundidad del largo util de la herramienta esta ebutida en el material, intentar que sea **100%** para 
	*  Un desgaste parejo de la herramienta


### Direccion de corte (climb /conventional )

Recordemos que el filo y la forma de la herramienta afecta una serie de factores a la hora de cortar, por ejemplo la direccion hacia donde sale la viruta y la direccion del filo.

Dicho esto, normalmente **intentaremos que la direccion del corte sea igual que la direccion  giro de la herramienta**

* Se le llama al corte en direccion  contraria al giro de la herramienta **conventional cutting**
	* Requiere mucha menos energia y fuerza por parte de la maquina
	* Puede cortar mayor cantidad de material en una pasada

.
* Se llama al corte en direccion l giro de la herramienta.
**lib cutting**
	* Requiere mucha mas energia para hacer el corte, **no** lo usamos con cortes de mucho material o con maquinas chicas
	* Produce un mejor acabado
	* Bueno para cortes de terminacion.
	* la herramienta mordera fuertemente la pieza, si esta no esta firmemente sujeta podria salir despedida si se esta maquinando mucho material
		* Para minimizar este efecto, que el corte siempre este paralelo a la morsa
		* a maquina necesita de gran rigidez

**Conclusiones**
* **Climb cutting**
	* Lo preferimos en maquinas CNC o maquinas grandes, por que son mas rigidas
	* En maquinas manuales lo usamos para la terminacion
	* Necesitas gran rigidez en todo (pieza, maquina, todo)
* **Convenitional cutting**
	* En maquinas manuales lo usamos para casi todo 

Video coparacion para clase
https://www.youtube.com/watch?v=galm5_6SUcM

### Chip load - tamaño de viruta por diente (IPT)

**IPT  o chip load:** Inches per tooth, pulgadas de material a morder por un diente. es decir, el **tamaño de una viruta por cada diente**

![](https://i.imgur.com/6lTNVRV.png)

El chipload  determinara
* El esfuerzo que tiene que hacer la maquina al cortar
* El calor que se generara durante el corte
* El desgaste de la herramienta
* La velocidad a la que se puede comer material
* El  acabado del material


**CRITICO:** tenemos que tener un chip load **acorde a la herramienta que tenemos**, el **fabricante de la herramienta nos dara un  recomendado** Podemos variar el **** dentro de algo razonable (15%)
*  **IPT muy bajo** 	
	* hace que el cortador resbale y genere friccion
	* Desafila la herramienta
* **IPT muy alto** 
	* fuerza la erramienta 
	* podria quebrarla
	* Mal acabado
	* Mas calor

la conclusion de esto es que **TENER UNA BAJA VELOCIDAD DE AVANCE NO HACE QUE LA HERRAMIENTA DURE MAS, TODO LO CONTRARIO!**

### Cutting speed  (SFM o M/min)

distancia recorrida por los filos de ta sobe el material en un minuto, es decir **superficie de erma oca el material por minuto**

**Cada herramienta de cada fabricante tiene un CUTTING SPEED recomendado para cada material**

Podemos usar un **CUTTING SPEED** menor S recomendado sin problemas en materiales blandos como aluminio E fariante  SCUTTING SPEED** para maximizar nuestra productividad pero no siempre podemos lograrlo con la maquina que tenemos, y eso es normal.

En materiales **duros** como **acero o titanio** es necesario usar **exactamente el CUTTINGPEel fabicnt**. En materiales blandos como aluminio, es opcional.

EL cutting speed puede venir en
* $\frac{metros}{min}$
* $\frac{pies}{min}$ o **Surfice Feet Min**

**Nomenclatura**
Los fabricantes usan estos nombres en sus tablas y formulas
* $RPM=n$
* $\frac{metros}{min}$ ó $SFM=V_c$
* $D=$ Diametro

### Obtener cutting speed y chip load 


Los manuales de los fabricantes de eetaican que **Chip load** y **cutting speed** se debe usar para **cada herramienta** en combinacion con **el material a cortar**

Para eso cada fabrcante coloca una serie de materiales en diferetes categorias y te indica tin eehip load** para cada material dentro de cada categoria y subcategoria.

![](https://i.imgur.com/LxCBhPB.png)

Buscamos la combinacion de 
* Herramienta
* Material a cortar
* Operacion

Si  no estas seguro siempre podes **llamar a n  ae de  herramienta**
lco aules e abricante onl

usmanua rcndeheramientas te an a da  l menos o arametros de **Cuttingetrse tn speed** y **Chip lo y ad** dependiendo de la **operacion a realizar**

* Uno para *  ar*Slotting**
* Uno para **Side milling**

T n para deillambien se pueiad

ara lo
* Si minaiene uden poer**amasespeciios*  a recomdacioa eeifis*  a mnains paraacess y aieros  palas 

![](https://i.imgur.com/w.png)

### Calcular velocidad de giro y avance 

[fuente pulgadas](https://www.youtube.com/watch?v=zzzIpC39WUg)
[fuente mm](https://www.youtube.com/watch?v=gTnkNHB7dss)

En una fresa debemos colocar una velocidad de giro y de avance tales que no rompan la herramienta y corten el material lo mas rapido y eficientemente posible.

para eso tenemos que **ver las especificaciones del fabricante para la herramienta que tenemos segun el material que tenemos**

Para una herramienta determinada y un material  nos dara
* **Chip load** 
* **Cutting speed**

A partir de eso nosotros debemos determinar **Feed y RPM**


#### pindle RPM 

as $RPM$ o $n$ dependeran del **Cutting speed** de la herramienta en cuestion para el material en cuestion, segun determine el fabricante

No es dificil ver que si me dan un **cutting speed** entonces probablemente pueda calcular mis $RPM$ usando algo asi
$$RPM=\frac{\text{perim por min recomendado x fabric}}{\text{permi de una vuelta de  mi herramienta}}$$

Notamos que
$\text{permi de una vuelta de  mi herramienta}=\pi Diametro$ 

Perim  minimo recomendado por el fabriante tiene que estar en la unidad de diametro para hacer la division. osea que:

Dada la siguiente nomenclatura de catalogos
$n=$ RPM, lo que queremos obtener
$V_c$= Cutting speed, sale del catalogo
$D$= Diammetro de la herramienta en mm, sale del catalogo

**Formula version pulgadas**

$$n=\frac{12V_c}{\pi D}$$

Por que me dan la **velocidad de corte** o $V_c$ en **SFM** y $12 inches =1feet$


**Formula version milimetros**

$$n=\frac{1000V_c}{\pi D}$$

Por que me dan la **velocidad de corte** o $V_c$ en metros y $1000mm=1m$

#### Avance / Feed para milling

El avance se calcula despues de haber calculado las $RPM$ y de la siguiente manera

Dado 
* **Chipload** Inch per tooth o mm per tooth, a veces indicado como $f_z$
* Numero de dientes del endmill, indicado como $Z_n$
* Las $RPM$ que obtuvimos, indicado como $n$

Calculamos el avance tal que **Cada diente en la herramienta coma lo que tiene que comer en las RPM elegidas**

**tanto para mm como para inches**
$$\text{avance}\frac{in}{min}=f_zZ_nn$$




#### Avance / Feed para drilling
En el caso de tener que taladrar con una mecha de taladro, no se usa **IPT (inch per tooth)** sino **IPR (Inch per revolution)** el calculo sera


$V_f=f_nn$

donde

* $V_f$ es velocidad de feed
* $f_n$ es feed por revolucion
* $n$ es $RPM$


### Chip control

Queres evitar tener virtuta cerca del cortador, ya que

* En elementos blandos, la friccion y el calor pueden derretirlos
* En elementos duros, las chips pueden calentarse tanto que se templan y son aun mas duras que el material original, volver a cortarlas con la herramienta genera problemas
* Estresa y desafila la herramienta sin necesidad

Para evitarlo
* Si la maquina tiene fluido enfriante, usalo
* Si la maquina tiene soplador de aire comprimido, usalo
* Sino soplalas con aire comprimido o apaga la maquina y usa un cepillo
* **No tocarlas, son filosas y calientes**

![](https://i.imgur.com/eMwbjQwwgWGvzL.png)

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

### Face/side milling

Es la operacion de hacer una cara **PLANA**, muchas veces arrancamos nuestro trabajo haciendo **face milling** en **todas las caras de nuestro material** para llevarlo a escuadra y a una dimension aproximadamente cercana a nuestra pieza inicial.


![](https://i.imgur.com/2Hf7Hjv.png)_Comparacion de un bloque de aluminio face milled y uno cortado con una sierra de mano_


* Para hacer **face milling** podemos usar un **enndmill** o un **facemill**
* 
### Side milling

Es la operacion de cortar a 90 grados de la herramienta

Demanda mas fuerza de la maquina, por lo que dependiendo de la potencia tal vez tengas que cortar con menor **Cutting speed**
Podes hacer **Side milling** solo con un **endmill**

![](https://i.imgur.com/psvfKIa.png)

### Plunging

Plunging es usar el **endmill como una mecha de taladro** para **cortar hacia abajo**

Hay que **evitarlo siempre que sea posible!** 
* Siempre que sea posible **usa un drill bit y despues cambia a un endmill**
	* Si hace falta **achatar el fondo** del agujero, usas un endmill en el fondo del agujero
* No siempre se puede evitar 
	*  Solo se puede hacer con **center cutting endmills**
	* el endmill **no esta diseñado para evacuar viruta hacia arriba**
	* Usar una herramienta con **menor cantidad de flutes**, ya que evacua mejor y ademas generalmente solo dos de las flutes realmente cortan abajo

### Chip diagnostics

Podes determinar en base a tu viruta si estas haciendo una operacion correctamente

* Face milling
	* Chips cortitas
* Side milling
	* Chips alargadas como agujas
* Baja velocidad de corte y tool rubbing o desafilada
	* Chips que son como polvo
* Chips negras
	* Alta temperatura, tal vez se templaron (puede o no ser normal, indicador de que necesitas cooling)

![](https://i.imgur.com/E4kPdxc.png)

## Accesorios - WIP

### Paralelos - WIP

Son dos piezas de metal perfectamente paralelas (hasta una precision muy elevada) y a 90 grados para elevar la pieza encima de la altura de la morsa manteniendola co un agarre de 90 grados.

![](https://i.imgur.com/tV8oSw7.png)

# Endmill
# Herramientas

[videos fuente](https://www.youtube.com/watch?v=EB7B1zq8AM8)

A diferencia de los drill bits, que estan diseñados para **perforar hacia abajo**, los endmills estan diseñados para **cortar hacia los costados**



## Geometria general

### Largo y ancho

**largo**
* Cuanto mas larga la herramienta menos rigidez ( mas distancia entre el motor y la punta de corte)  y mas posibilidad de **chatter**
* **Siempre es preferible que el corte sea lo mas profundo posible**
* **siempre elegir la herramienta mas corta que tenga la profundidad de corte adecuada**
* Siempre tratar de cortar con **todo el largo de la herramienta** para permitir un desgaste parejo
	* **si usas solo la punta de una herramieta que no se puede afilar, la desperdiciaste! y son caras!**siempre elegir la herramienta mas corta posible**
* Siempre tratar de cortar con **todo el largo de la herramienta** para permitir un desgaste parejo
* Mas corto es mas barato



EL largo **utilizable** de una herramienta de fresado va desde la  punta hasta el final del angulo de la flute
![](https://i.imgur.com/tRfjT1I.png)
_Largo de corte utilizable de una herramienta_

![](https://i.imgur.com/rUPIbsE.png)
_Usar  el menor largo de herramienta posible_

**Ancho**
* Cuanto mas ancho **mas rigidez** y  por ende menor posibilidad de **chatter**
* Cuanto mas ancho **mas precio**
* Cuanto mas ancho **mas rapido come material**
* **Elegir la herramienta mas ancha posible**

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
	* Mas filos sigifica que podemos tener **mas velocidad de avance con el mismo chip load** y entonces **cortar mas rapido** que con menos flutes
	*  Peor chip clearing
		* Si el material es duro, tenes chips mas chiquitos
		* En materiales blandos esto implica mas friccion entre chips, eso puede **derretir plastico** o **fundir aluminio** en lugar de cortarlo
* **Menos flutes** 
	*  Mejor chip clearing, tienen mas espacio y tiempo para salir
		* Bueno si el chip es grande, largo y no se romppe  por que el material es blando!
	*  Peor terminado

En terminos generales usamos

* **1 - 2   flutes**
	* Plastico
	* Madera
	* Metales blandos (aluminio)
* **3 - 4 -5 flutes**
	* Terminados en metales blandoDetalles
	* Metales duros
* **>6**
	* Fibra de carbono
	* Acero de herramientas
	* Terminados

### Angulos 
**Geometria de la punta**
La punta tiene un angulo llamado **rake angle**, este angulo puede estar 
* **Hacia el material (Positivo +)**
* **perpendicular al material (0 o neutral)**
* **Alejandose del material (negativo -)**

![](https://i.imgur.com/YrqE8Gb.png)

**Geometria del largo**
De la misma manera, los filos del largo tambien tienen **rake angles** que pueden ser


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


### Center/non-center cutting
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
	* Solo corta cosas mas blandas que acero o haceros blandos
 	* se parte menos facilmente por no ser tan rigido
 	* Tiene una velocidad de corte mas lenta y un chip load mas bajo
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
	*	Puede cortar a mas velocidad, mas rapido, mayor chip load, mayor cutting speed
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

[Fuente](https://www.youtube.com/watch?v=nY6o04ODJ3U)

Las herramientas pueden estar recubiertas de diferentes materiales para extender su vida util y su filo.

* **Sin recubrimiento**
	* Permite afilar la herramienta, si afilas una herramienta con recubrimiento entonces le sacas el recubrimiento!
* **Titanium nitride** $TiN$
	* De color Dorado
	* Muy comun - Uso general
	* Heat resistant and hard
* **Titanium carbo nitride** $TiCN$
	* Color plateado
	* Mas duro que $TiN$ y genera menos friccion
	* Bueno para cortar aluminio
* **Chromium nitride** $CrN$
	* Color plateado intenso
	* Similar a $TiCN$
	* Puede cortar a mayores temperaturas sin perder sus propiedades
	* Bueno para cortar aluminio
* **aluminum titanium nitride** $AlTiN$
	* Plateado obscuro
	* Mas duro que $TiN$
	* Mantiene sus propiedades a altas tempreaturas
	* Bueno para cortes de acero
* **titanium aluminum carbonitride** $TiAlCN$
	* Color rosado
	* Extremadamente duro
	* se puede usar a altas temperaturas
	* Baja friccion
	* Bueno para aluminio acero, hierro forjado y otros materiales superduros
* **Iron Oxide** $FeO$
	* Se usa cuando hay dificultad en mantener la lubricacion y hay mucha  friccion
	* Color plateado muy obscuro
	* Muy comun para herramientas de roscado, donde hay mucha friccion
*  **Combinados**
	* Tienen dos coatings de los mencionados anteriormente, combinando sus propiedades.
	* Caros y poco comunes




## Face mills

[fuente 1](https://www.youtube.com/watch?v=jwORPpWJ73Y&list=PLpl7LvSkK4IGUEZZ4fh5m5uv94LC73654&index=5)
Un face mill sirve para cortar superficies de manera plana. Todas las consideraciones anteriores para los endmills siguen siendo validas.

* no tienen flutes ni helicoidales
* Mismas consideraciones de material de la herramienta
* Mismas consideraciones de rake angle en el inserto

Los face mills funcionan con herramientas llamadas insertos, que se cambian y son los que hacen el corte.

![](https://i.imgur.com/OFbrATO.png)

## Geometria



### Diametro
El diametro efectivo de un endmill va desde una punto de un filo hasta la punta opuesta.

Siempre **hay que elegir un diametro  1.5 (o mas ) veces mas grande que  el corte que se va a hacer**, eso permite que se forme una viruta de un tamaño razonable que pueda ser evacuada sin generar exceso de calor

![](https://i.imgur.com/hF9kwhz.png)
_Diametro efectivo_


![](https://i.imgur.com/ownymYr.png)
_Formacion de chips con un diametro de herramienta muy pequeño_


### Angulos


Un facemill tiene **dos rake angles**

* **Radial rake angle**
El angulo que forma el cortador con el eje $x$ de la herramienta, puede ser 
* **positivo** (Hacia el material)
*  **neutro** (perpendicular al material)
*  **negativo** (Hacia el lado contrario al material) como se muestra en la imagen
![](https://i.imgur.com/TSOCpEt.png)
_Ejemplo de un radial rake angle negativo_
* **Axial rake angle**
El angulo que forma el cortador con el eje $Z$ de la herramienta, puede ser 
* **positivo** (Hacia el material)
*  **neutro** (perpendicular al material)
*  **negativo** (Hacia el lado contrario al material) como se muestra en la imagen
![](https://i.imgur.com/f4JZAmK.png)


.
**La seleccion del angulo es igual que en los endmills:**
 * Un **rake angle positivo en ambas caras** 
	 * sirve para elementos blandos, ya que  los cortara con el filo.
	 * Toma menos potencia usarla (por que corta con el filo)
	 * El filo va a ser mas fino y por ende mas endeble
 * Un **rake angle negativo en ambas caras** surve para elementos mas duros
     * el filo no corta, sino que **raspa** el material
	 * El filo es mas grueso, y por ende mas fuerte
	 * Se usa en materiales mas duros
	 * toma mas fuerza



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MDg3MzQ3MzQsLTU5MzYzMjU5OCwtOT
U4NDQzNjQ2LDEzMDU0NjE5NTQsLTkzNTk2MzMyLC0xNjU1NDU3
MTUzLDEwNTQ5MTYyNjEsMTc5NTkwMTMxOCwxMjMyNzg1MjIwLC
01NTk4MTg2ODgsMTg0MjI5OTMyMSwxNjE3Mjc4MjEsMTczOTY1
MzIwNSwtNTg2MjEwNjY0LDEyMzkyMTcxNDgsLTE1MTM3OTcxNj
csLTY2NTU0ODYzMCwtMTYwMjAyNTEwNyw5MzExNDk2MzYsMTMw
OTkyNTU0N119
-->