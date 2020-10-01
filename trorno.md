**VER**
https://www.youtube.com/watch?v=H6Dnmd3lDzA&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN

**Ver**

https://www.youtube.com/watch?v=DQ4yKKXdvng&list=PL2935W76vRNGZaLzcqvAjcIblmrIVQIzj


**Parting tool**
https://www.youtube.com/watch?v=5LtYzjR1JuM


**Tools**
https://www.youtube.com/watch?v=__A2xtLF0AU

**Tools**
https://www.youtube.com/watch?v=bvJhRtRR7rk


# Herramientas - WIP


## Herramientas de corte - WIP

#### Parting tools

Son herramientas para dividir la pieza en pedazos, 
* **NO** son herramientas de corte de un solo punto, sino que son herramientas de forma
* Pueden ser de acero rapido o de inserto de carbide

![](https://i.imgur.com/sxnfOPP.png)
Hay de varios tipos
* Herramienta de torno norma con forma
	* Podes usar un holder normal
	* tiene mucha rigidez por que es mas ancho
* Blade
	* Necesita un holder separado
* Carbide Insert
	* Menos filoso y mas duro
	* Pide **AUN MAS** de la maquina

#### Debarbing tool - WIP

Es una herramienta para sacar la rebaba de los agujeros

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/j976nxh.png)

#### Tapering tools - WIP

#### Rimmer - WIP

Son herramientas diseñadas para hacer el **termiado de precision de un agujero**, se hace el grueso del agujero con un **drill bit** hasta una precision de aproximadamente $0.5mm$ y se usa un rimmer para llegar al diametro final.

Un rimmer
* **es un instrumento de alta precision**
* Tiene gran **dureza**
* **NUNCA debe ser usado en direccion inversa**

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/2El0lwx.png)



#### Inside corner turning bit - WIP

Se trata de una herramienta con un angulo de 85 grados en vez de 90 para poder hacer cortes llegando a una pared de 90 grados sin rozar la pared (por que la herramienta tiene 85grados y no 90)
![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/djr0l63.png)

#### Boring bars - WIP

Para agrandar agujeros internos

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/7GrpJat.png)
## Herramientas de tapping y dies  - WIP


### Taps - WIP

* **Ridiculamente** duras

## Material - WIP
Tienen las mismas caracteristicas en cuanto al material que las herramientas de fresa.

* Carbide 
	* Caro
	* No afilable
	* usa Inserts
	* Requiere feeds and speeds minimos para funcionar correctamente
* Acero rapido
	* Barato
	* Afilable y se puede cambiar su forma
	* forgiving


## Angulos  - WIP

# Consideraciones-WIP

### Tool holder -WIP

Se trata de una parte que sostiene la herramienta y permite ajustar su altura

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/7CncxqX.png)

Se suele reemplazar el tool holder entero, se saca y se pone y con una palanca se asegura por presion.

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/HlqwqJ7.png)
Ademas suelen tener un ajuste para cambiar el angulo de la herramienta con respecto a la pieza  

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/pyArBwM.png)


### Hand weels
#### Backlash

Los engranajes que mueven el carro porta herramientas tienen un juego cuando te moves atras y adelante o en cualquier direccion, si vas a hacer movimientos de presicion tenes que retroceder y volver a avanzar para asegurarte de no estan en el punto donde hace juego.

**Sino no podes confiar en el indicador de milimetros**

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/SYzoi0V.png)
#### Direct e indirect hand weels

Las **hand weels** vienen en dos variedad

* **Direct read** indican la reduccion de **diametro** que estas haciendo
* **indirect read** indican la reduccion de **radio** que estas haciendo

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/8Ycy5Ge.png)

### Chatter

Igual que en la fresa, el chatter es causado por la ausencia de rigidez en la maquina o por la flexibilidad del material. Para evitarlo

* usar tail support
* Intentar meter la pieza mas adentro del plato
* apretar todas las palancas y partes de la maquina
* Cambiar los spindle barrels
* Reducir el tool preassure haciendo cortes menos profundos

### Platos

Hay platos de diferentes propiedades

#### Self centering 3 jaw chucks

Son platos de 3 mordazas donde las 3 apretan al mismo tiempo cuando las apretamos 

* Autocentrantes
* Centran con cierta precision
* **El centrado no es repetible**, osea que si centras dos veces una pieza no necesariamente es concentrica las dos veces con la posicion anterior
* Toma poco tiempo poner la pieza

#### 4 jaw independent chucks - uso en piezas circulares

[como usar](https://www.youtube.com/watch?v=CKqEuSvO86I&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=9)
Son platos de 4 mordazas donde cada una tiene que ser apretada individualmente

* **El centrado es repetible**
* Toma mucho tiempo poner la pieza (hay que medir la concentricidad)
* Centran con alta precision
* **Solo se puede hacer con superficies ya maquinadas o de precision!**

Para utilizarla, colocamos un medidor de distacia y vamos girand y ajustando, teniendo en cuenta que **siempre comparamos y ajustamos los jaws opuestos entre si**

Para las ultimas milesimas directamente ajustas mas la mordaza a la que le faltan las milesimas

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/ILwNBLE.png)

#### 4 jaw independent chucks - uso en caras no circulares

El plata de 4 mordazas independientes tambien te permite agarrar objetos no cilindricos para hacer caras planas!

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/IpKQf07.png)


# Preparacion de la pieza
## Concentricity

[fuente](https://www.youtube.com/watch?v=MofsvIIKx3k&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=8)


Si bien cuando hacer **turning** logras **siempre** un circulo concentrico con el plato, **SI SACAS Y PONER LA PIEZA DEL PLATO, LA CONCENTRICIDAD CON EL PLATO SE PIERDE POR ALGUNAS MILESIMAS** ya que hay variaciones en el mecanismo del plato.


**Solucion:** Si tenemos que reganar la concentricidad que teniamos si sacamos la pieza del plato, tenemos que usar un plato de **cuatro mordazas de ajuste independiente** y **DOLOROSAMENTE** ajusatar cada mordaza mientras usamos un medidor de distancia para asegurar que al girar el plato, el medidor no cambia.

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/mgg5Q5q.png)


## Agarre torcido en platos

antes de empezar tenes que verificar que la pieza no este torcida con respecto al plato.

Con un medidor de distancia  verificas que al girar la pieza siempre tenes la misma distancia.  Caso contrario pueden ser dos cosas
* La pieza esta agarrada de manera torcida
	* **Solucion:**  dar un golecito con un martillo a la pieza para moverla las milesimas necesarias y medir de nuevo, repetir.
* La pieza en si misma no esta derecha
	* **Solucion:** Turning

## Tail support - WIP

#### Criterio y colocacion

Si la pieza es **dos o tres veces mas larga que su radio, necesitas un tail support**. Por supuesto depende de la rigidez o flexibilidad de la pieza en si misma.

Para colocarlo, acercamos el centro hasta que haga presion moderada y lo trabamos con la palanca
![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/xQB1aKG.png)


#### Preparar la pieza para un tail support - WIP

Para preparar una pieza para usar un tail support, le hacemos una pequeña perforacion con una herramienta llamada **Center drill**  que es super rigida y agujerea exactamente en el punto en el que esta apoyada.

Al ser tan **Dura** tiende a partirse, asi que vienen con puntas de ambos lados a modo de repuesto

>El **angulo** de todos los **center drills** es el mismo que el de todos los **tail supports**, estan **estandarizados** para que encajen a la perfeccion y que en todas las paredes de la perforacion esten en contacto



![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/BeVMBlv.png)
Pasos
* Colocar el center drill
* Usar $RPM$ rapidas, por que la **surfice speed** en el centro es casi $0$
* Usar cutting oil para lubricar
* Perforar hasta donde termina la parte angulada de la herramienta
* ![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/bHJpdrV.png)


#### Tipos de tail support - WIP


hay 
* **Dead centers:**  
	* no giran con la pieza
	* generan friccion y calor, que puede deformar la pieza o expandir el metal generalndo problemas de exactitud
	* requieren alguna lubricacion 
* **Live center:**
	* Giran con la pieza con rodamientos
	* Son mas grandes
	* Mas caros


# Operaciones


## Facing

[fuente](https://www.youtube.com/watch?v=r9AqbENiLOQ&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=3)

Es trabajar una cara de la pieza para hacerla plana y a 90º, cosa que en general en bruto NO es.

* Ajustar la pieza al plato
* Alinear la herramienta con el eje del torno
	* Se suele hacer con la punta de la cabeza movil, a ojo
	* ![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/sbWsrKL.png)
* Determinar $RPM$
	* Si el torno es de **velocidad variable**, vas a tener que aumentar la velocidad a medida que la herramienta avanza
	* Si es de **velocidad fija**, usas un promedio
* Encendes el torno y acercas la herramienta hasta que toque apenas la pieza hasta tocarla
* Alejas la herramienta en el eje $X$
* Avanzas en $Z$ un poquito ej: $0.5mm$
* Tira de la palanca que asegura el carro porta herramientas para que no se mueva en el eje $Z$
* Avanza en el eje $X$ cortando hasta llegar al centro de la pieza
	* ![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/E2LYis6.png)
	* Repetir hasta que la cara este pareja
	* ![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/iObQMXs.png)
## Turning

Es reducir el diametro de la pieza a lo largo.
Siempre compramos algo mas grande que nuestro objetivo y hacemos turning en una pieza que compramos para ajustarla a lo que queremos por que
* La materia prima puede (y suele) tener twists
* Puede (y suele) no ser recta
* Asegurar concentricidad perfecta (el plato puede no centrar correctamente)

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/NTlYsJl.png)_Ejemplo de como hacer turning obliga a la concentricidad, aun con un agarre de plato exageradamente no concentrico_

**Pasos**
[fuente](https://www.youtube.com/watch?v=1IsG8vIXA8k&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=5)

* Te acercas a la pieza hasta que la tocas, ahi estas en $X=0$
* Te alejas en $Z$ hasta estar frente a la pieza
* Te acercas en $X$ a la profundidad que queres cortar **ojo con backlash**
* Te acercas en $Z$ en feed speed, comiendo la profundidad $X$ a la que te acercaste
* Medis la pieza, repetis hasta lo que sea necesario, con pasadas **cada vez mas finas mientras te acercas a la dimension que queres**

## Turning a shoulder
[fuente](https://www.youtube.com/watch?v=aQwWRW-PdTE&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=7)
Es una combinacion de **facing** y **turning**, el objetivo es **hacer una parte de menor diametro separada por una pared de 90 grados perfecta por otra parte de diferente diametro**

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/WMlVTbb.png)
_usamos un sensor de comparacion de distancia_

Pasos
* Medimos el lugar donde debe estar la pared
* Colocamos la herramienta ahi
* Colocamos un medidor **comparador de distancia** de tal forma que este en $0$ cuando el carro porta herramientas esta en en el eje $Z$ de tal manera que la herramienta toca el lugar donde debe estar la pared
* Hacemos **turning** quedandonos cortos unas decimas de milimetro (usando el comparador)
* Cuando llegamos al diametro deseado, nos movemos al cero del comparador y hacemos un **facing** desde adentro de la pieza hacia afuera
* **Observese** que siempre va a quedar un pequeño chanfer microscopico por la forma de la herramienta, aun cuando este super afilada, enntonces si otra pieza tiene que encastrar, vas a tener una luz
	* **Solucion 1** durate el facing, cuando estas contra el cilindro interno, hacer una edidura de unas decimas de milimetro para eliminar el chanfer
	* **Solucion 2** Usar un parting tool
![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/aAnYpv5.png)
_Encastre inperfecto debido al chanfer_

## Drilling

[fuente](https://www.youtube.com/watch?v=IHquZSsM_k0&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=10)

> Solo **taladramos** en un torno cuando nos importa mucho que
> * El diametro sea **muy preciso**
> * El agujero sea **muy concentrico con la pueza y muy centrado**
>  * El agujero este a 90 grados de la cara de la pieza
> 
> cosas como esta son importantes en **motores y maquinas de precision**


El taladrado se hace con un jacobs chuck en el tail support

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/D8gvO6u.png)

Pasos:
* **Agujero guia:** Usar un **center drill** (el mismo que usamos para poner un tail support) para asegurarnos un agujero guia bien centrado. aplicando cutting oil
*  **Pilot drill:** taladramos con un drill bit mas chico
	*  **sacando los chips** salienndo del agujero cada tanto si el agujero no es superificial (sentiras la resistencia) 
	* **usando  cutting oil** periodicamente
	* **midiendo profundidad** si hace falta, recordando que no tenemos gran precision
	* ![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/Pgb9o67.png)
* **Drill** usamos un drill bit un poquito mas pequeño que el agujero final que deseamos ($0.5mm$  mas chico que el diametro final)
* **Rimming** usamos un rimmer, para hacer los ultimos $0.5mm$
	* **NUNCA** girar un rimmer en la direccion opuesta a sus filos (ni siquiera  con la mano), arruina totalmente su precision
	* **Usar velcidad lente**
	* **sacar chips** muy frecuentemente, por que no tienen flutes para  hacerlo
	* **cutting oil** usar bastante
	* **tener paciencia**
* **Debarbing:** Sacamos la rebaba con un rebarbing tool
	* Se puede hacer a mano (Toma dos vueltas)
	* ![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/j976nxh.png)

## Boreing - WIP

## Surfice finishing

### Terminado con herramienta de torno
[fuente](https://www.youtube.com/watch?v=1Fgj7m4MTbw&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=12)

Un buen surfice finishing es importante por que

* **Precision** despues de cirto punto, la terminacion afecta las dimensiones de la pieza
* **Durabilidad** una pieza sin rugosidad no **acumula humedad en sus imperfecciones** y se oxida muchisimo menos


**como lograr un buen finishing:**
* hay material que es simplemente mas facil de maquinar
* Usar una herramienta con mas superficie (menos punteaguda, mas redondeada )
* ![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/DbbLukr.png)
* Usar un buen **speed and feed**
	* High surfice speed
	* low feed
* tener una herramienta con **buen filo** y **buenos angulos**
* usar **cutting oil o  WD40**


### Terminado con lija

Podes hacer la terminacion fina con lijas, arrancando con _400_ y cada vez mas, usando oil y con cuidado de no pasarse de la medida


**CRITICO:** 
* **cubrir todas las puperficies de precision** del torno, los trocitos de lija son mas duros que el metal del torno y va a destruir la superficie de precision del torno
* **Sostener la lija con mucha ligereza** si la atrapa el torno, que te las saque de las manos.

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/4WkqNMG.png)

## Deburring

### Operacion

Deburring es **remover la rebaba filosa que queda como resultado del proceso de maquinado en los bordes de la pieza**, no

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/image.png)

Se puede hacer
* Con una **lima**
	* Limamos solo en la direccion de los dientes de la lima
	* nunca acercamos la punta de la lima al chuck para que no la agarre, limamos con el centro de la  lima
	* ![](https://i.imgur.com/g5WQ9ZH.png)
* Tapered cutter, para deburrear agujeros
	* ![](https://i.imgur.com/eFkxaTa.png)
* Deburring tool
	* ![](https://i.imgur.com/YfPhMcE.png)
* Papel de lija

### Importancia para la precision

Muchos elementos de medicion pueden agarrar el burr y darte una medicion inflada. Hay que tener cuidado

![](https://i.imgur.com/JuFR5aC.png)


Ademas si estas trabajando en una fresa, el burr puede modificarte la posicion de la pieza y que quede toricida

![](https://i.imgur.com/RKP8Tkj.png)

## Parting

[fuente](https://www.youtube.com/watch?v=PeHmee4tvYc&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=15)
Es la operacion que consiste en **dividir la pieza en dos partes**, es una **OPERACION PELOGROSA** ya que **la herramienta tiende a partirse**.
Es 

* **USAR** proteccion facial
* **SABER** usar la parada de emergencia
* **Es demandante con la herramienta y la maquina**
* **No acercar la cara**


>Usamos el torno para dividir la pieza **en vez de una sierra** por que
>* Es preciso
>* Es rapido
>* Es comodo

Tener en cuenta
* La herramienta tiene que estar bien **afilada**
* Remover chips frecuentemente
* Los **speeds and feeds** tienen que estar bien
	* Usar velocidades lentas
* La **rigidez** tiene que ser excelente!
	* Bloquear el carro porta herramientas
	* Estar lo mas cerca posible del plato
![](https://i.imgur.com/jdicmQC.png)
	* Usar el menor largo posible de herramienta ![](https://i.imgur.com/2tGwmCO.png)
	* **Altura** del filo alineada perfectamente con el eje del torno, **NUNCA  jamas debe estar debajo del centro**
![](https://i.imgur.com/ADQPa6P.png)
* **Perpendicularidad perfecta** a lapieza 
	* Podes apoyar el carro porta herramientas contra la pieza o contra un cuadrado de maquinista![](https://i.imgur.com/TyTyy7K.png)
* Usar **MUCHO Cuttring fluid**
* Colocar un carton abajo para que cuando la pieza caiga no golpee los rieles de precision del torno 
* Sacar la puntita que queda, podrias hacer
	* Un **facing operation**
	* usar **una lija**




## Tapping -WIP

[fuente](https://www.youtube.com/watch?v=WRuJ3k0V-fA&list=PLY67-4BrEae9Ad91LPRIhcLJM9fO-HJyN&index=17)

### Taps

La ventaja de usar un torno para usar un tap (que podriamos usar manualmente) es que la rosca nos queda perfectamente perpendicular a la pieza.

Pasos:
*	Agujerear el agujero con el diametro correcto segun la tabla de roscas
*	asegurar la pieza y el tap
*	Girar la pieza manualmente mientras se presiona ligeramiente con el tap, evitando que el tap se mueva de alguna manera

![](https://i.imgur.com/WejRYkb.png)


### Dies

Identico a taps pero con un holder 

![](https://i.imgur.com/eAf5FFa.png)
La principal preocupacion sera que el die "muerda" la pieza por primera vez. Para facilitarlo 
* hacemos un taper en la punta
* reducimos el diametro 


### Single point threading
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MTgzNDg2MiwxNDgyOTA4ODQwLDMyNj
Y1MTEyNSwtMjE0Mzg3MTg2NCw0NDM1OTc1NzYsLTEzMDkwMjEw
OTMsNjU1MjM5NjY0LDE0MDEyMDEzNzQsLTIzMDA0MzgzOCwtMT
I2OTkxOTgyNywtMjA2NDg5MzUxNiwtMTcyNzIyMzE4OCw5Njc4
ODU4NDIsLTE4NjExMDU4MjksMTQzOTc0NjUzMSwtNzg1NjYwNz
MzLDE4NjYyNjAzMjgsLTE2MTExNjIzMTYsMTA2NDUxMjI0LDg5
NjgzMjM5MF19
-->