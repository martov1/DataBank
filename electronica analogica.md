

**VER aplicacion en reparacion de notebooks**
https://www.youtube.com/watch?v=1XGun_-06aA&list=PLHk1hZEmw3_zlUPRfVeBHLSUviVNfR4pNvideo 3 minuto 7



# Resistores

### Clasificaciones
Son elementos diseñados para ofrecer una resistencia al paso de la corriente

Consumen energia electrica y la transforman en **Calor** respetando

$$W_{\text{consumida}}=V.I$$
Donde $V$ es la caida de voltaje a lo largo del resistor y $I$ la corriente que lo atraviesa


Se clasifican en 
* **Fijos:** La resistencia esta determinada por un valor fijo de fabricacion
* **Variables:** La resistencia cambia con un desplazamiento mecanico
	* Potenciometros
* **No lineales:** La resistencia es funcion de una propiedad fisica
	* Fotorresistores
	* Termorresistores

Hay diferentes tipos de resistencias fijas dependiendo de la potencia y precision necesarias
![](https://i.imgur.com/3wxr7cX.png =550x)

### Valores
#### Significado de los valores


* **Resistencia nominal:** La resistencia que se espera que tenga el componente
* **Tolerancia:** Margen de error que tiene el resiistor, expresado en % del valor nominal
* 
![](https://i.imgur.com/7x1in7D.png)
#### Valores y precisiones estandar

[fuente](https://www.youtube.com/watch?v=jSPNvJ0XYCQ)
Los resistores se clasifican en "series estandar" llamadas **E-series** clasificadas en el estandar **IEC 60063** para resistores, inductores y diodods zener.

Las **series standard** se calculan de tal manera que se dividen los valores de 0 a 1000 en X cantidad de "pasos"

**E-12** divide en 12 pasos
**E-24** divide en 24 pasos 
**E-6** divide en 6 pasos

Los **pasos no son iguales entre si** sino que **cada paso en un porcentaje mas grande que el anterior** 

**E-12** cada paso es un 20% mas grande que el anterior, esto permite que siempre exista una exactitud de +-10%
![](https://i.imgur.com/DihiZV2.png)
Podemos calcular el step size asi

$step size = 10^{\frac{1}{\text{cantidad de pasos}}}$

![](https://i.imgur.com/1Yi1lpp.png =300x)
Al aumentar la cantidad de pasos, tambien estamos aumentando la exactitud de los componentes

![](https://i.imgur.com/0oUIbdG.png =300x)
Las series mas populares son las siguientes. Podemos conseguir componentes de estas series con multiplos esos valores en ohms.
![](https://i.imgur.com/ZEdxfpS.png)
#### Capacidad de potencia y tamaño fisico
Los resistores cambian su tamaño dependiendo de la potencia que pueden disipar en forma de calor sin quemarse
![](https://i.imgur.com/qIhVTSV.png)

## Resistores Fijos

### Resistencias tubulares
#### Codigo de colores

Las resistencias nos indican mediante un codigo de colores cual es su **valor nominal** y su **tolerancia**, en base a eso ademas podemos definir a que **serie pertenecen**

![](https://i.imgur.com/aLuFpcL.png =500x)
![](https://i.imgur.com/033ZctY.png =500x)
#### Codigo de colores alta precision

Cuando llegas a cierta precision, la **temperatura** comienza a afectarte la medicion de resistencia, **ya que el resistor cambia su resistencia cuando cambia su temperatura.** 
Cuando tenes resistores que estan hechos para tanta presicion, vienen con una banda mas que indica cuanto cambia la resistencia por grado de temperatura fuera del valor ideal.

El coeficiente esta expresado en partes por millon $PPM/C$, es decir, dividis la resistencia $R$ del resistor en un millon de partes, y el coeficiente te dice cuantas de esas partes cambian por grado centigrado, partiendo desde una temperatura de referencia, normalmente de $25C$.
$$\frac{R}{1.000.000}*\text{coef}*\Delta T$$

EJ:
* **Datos:**
* Resistor $10\Omega$
* Coeficiente $50\frac{ppm}{C}$
* **Calculo:**
	* Una millonesima parte de $R$ es $\frac{10\Omega}{1.000.000}=0.00001 \Omega$
	* Como el coeficiente es $50\frac{ppm}{C}$, por grado cambia 
		* $50*0.00001\Omega=0.0005\Omega$
	* Osea que si cambia 5 grados centigrados de la temperatura estandar, es decir, esta a $30C$ la variacion de resistencia es 
		* $5*0.0005\Omega=0.0025\Omega$

![](https://i.imgur.com/c9SjPNv.png =x250)
### Resistencias SMD
a
 
 #### Resistencias mayores a 10$\Omega$
 
Tienen en general una tolerancia del $5\%$ y se indican con dos digitos que indican numeros y un digito que indica la cantidad de ceros que colocarles

![](https://i.imgur.com/1HVgAp8.png)

 #### Resistencias Menores a 10$\Omega$
Se utiliza la letra $R$ para indicar un punto decimal

![](https://i.imgur.com/z0eK60C.png)
 #### Resistencias de precision
 Se miden igual que los demas, pero tienen una tolerancia de $1\%$ y tienen un numero mas, por lo que permiten un numero mas de precision

![](https://i.imgur.com/BRA8QhS.png)
Asimismo, tienen su correlato para resistencias menores de $100\Omega$
![](https://i.imgur.com/pBniQZV.png)
 #### Resistencias de codigo EIA-96

Los primeros dos digitos responden a una tabla, el tercer digito es una letra y representa un multiplicador que se multiplica por el valor de la tabla. tienen una precision con un $1\%$ de tolerancia

![](https://i.imgur.com/Ke95hXh.png =400x)


### Resistencias de potencia
Son las resistencias hechas para soportar una cantidad mayor de potencia que las resistencias comunes. Usan en general un marcado alfanumerico que indica 
* **potencia soportada**
* **Resistencia**
* **Tolerancia**
* 

![](https://i.imgur.com/n20zwqj.png =x200)


## Resistores variables

### Potenciometros
[fuente](https://www.youtube.com/watch?v=jli6YBkRt3U&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=3)
Es una resistencia variable que cambia segun un mecanismo,
 **pueden ser:**
* **Logaritmicos**
	* Para audio, por que el oide escucha en una escala logaritmica
* **Lineales**

![](https://i.imgur.com/gt4CdPd.png =x150)


**Los hay:**
* **Rotativos**
* **Deslizantes**
	* ![](https://i.imgur.com/XYTMk1o.png =100x)
* **Multivuelta**
	* ![](https://i.imgur.com/qztn530.png =100x)
* **Deslizante con tornillo**
* **De ajuste (trimmer)**
	* Hecho para ajustar una vez y no tocarlo mas, generalmente para compensar algo de otro componente.
	* Tienen gran precision
	* ![](https://i.imgur.com/5z2a4c4.png)
* **De control**
	* Facil accionamiento, robusto, para que el usuario lo toque
	* ![](https://i.imgur.com/VKmx6pQ.png =100x)

### Variables no lineales

Varian con determindas magnitudes fisicas. su simbolo es
![](https://i.imgur.com/42E9TQM.png =200x)

#### Termistor

Son resistencias que **varian segun la temperatura**, los hay de dos tipos. Tienen como caracteristica **no tener una curva temperatura-resistencia lineal**

* **Negative temperature coeficient (NTC)** Varias su resistencia inversamente a la temperatura 
	* Mas temperatura, menos resistencia
	* Se usan como termostatos o sensores de temperatura en refrigeracion
* **Positive temperature coeficient (PTC)**
	* Mas temperatura, mas resistencia
	*  Se usan en termostatos y protecciones contra sobretensiones y corto-circuitos

Simbologia:
![](https://i.imgur.com/bE0tNKr.png)
Curva de resistencia-temperatura
![](https://i.imgur.com/Tyjjot5.png =250x)

#### Termoresistencia RTD

Similares a los termistores, pero tienen una curva **temperatura-resistencia lineal**.
Al aumentar la temperatura, aumenta su resistencia
Algunos ejemplos estandares son
* **PT100** - a 0º presenta $100\Omega$
* * **PT1000** - a 0º presenta $1000\Omega$

![](https://i.imgur.com/U0SE0rl.png)
#### Varistor - VDR

Es una resistencia que **varia con la tension**, su **resistencia disminuye con mayor tension**, la variacion **no es lineal**
Se usan para
* Eliminacion de chispas
* Proteccion contra sobretension
* Estabilizacion de tension




![](https://i.imgur.com/Ugb3zas.png =500x)
Generalmente se colocan en paralelo con una entrada de tension para cortocircuitarla en caso de un pico de tension y protejer al aparato, muchas veces quemando un fusible.
![](https://i.imgur.com/CPtxKLb.png)
#### Fotoresistencias LDR

Varian su resistencia con la luz, generalmente **no son lineales**, hay tablas que te dicen de acuerdo a cuantos **lux** que resistencia tendran

![](https://i.imgur.com/035We3a.png)
## Circuitos con resistores

### Divisor de tension


#### Hasta $0V$

[ejemplo](https://tinyurl.com/yfawc4ap)

### Estrella-triangulo 
Se trata de dos circuitos equivalentes de resistencias.
Mas que nada se trata de una "regla" que resume esta situacion, que es muy comun.
![](https://i.imgur.com/2uXZCsz.png)

Se puede llegar a estas formulas 

1. Teniendo los valores de resistencia de uno de los dos circuitos
2. Asumiendo que la corriente que sale por$A,B,C$ es la misma en cada circuito
3. Aplicando ley de kirchoff KCL para cada nodo
4. Asumiendo que el voltaje entre nodos $A,B,C$ es la misma en cada circuito
5. Aplicando KVC para cada nodo 
6. Reemplazando, obtengo una expresion para $V_m$ (el voltaje en el centro de la estrella
7. Tenemos todos los datos para obtener las resistencias 
[Prueba](https://drive.google.com/file/d/130gNaUIwi_HZYXLLy_pG-38Okxu0oMrK/view)

Las equaciones quedan asi
![](https://i.imgur.com/i2PZg5q.png)

### Wheatstone bridge - WIP


# Fuentes

### Generalidades
Las fuentes se dividen de la siguente forma
* Magnitud que proveen
	* Voltaje
	* Tension
* Idealizacion
	* Fuentes ideales
	* Fuentes reales

### Fuentes reales

Las fuentes reales son fuentes ideales a las que se les coloca una resistencia interna $R_g$ para **modelar la caida de tension que tiene una fuente real cuando le exigis demasiada corriente**

![](https://i.imgur.com/9jciDfn.png =250x)
**Cuanto mas corriente exigis, menos voltaje tenes**
![](https://i.imgur.com/hg0oRhV.png =250x)
**Ejemplo intuitivo:**
Tengo una fuente real de $12v$ con una resistencia interna $R_g=0.1\Omega$
Si le pongo una resistencia externa grande ($R=12\Omega$) veo que tengo una caida de tension en $R$ de $11.9V$ y una caida en $R_g$ de $0.1V$. Osea que desde la perspectiva de **afuera de la fuente, el voltaje cayo 0.1v** (esto por ley de ohm)

![](https://i.imgur.com/UjLbxje.png)
En cambio de pongo una **resistencia chica en comparacion con $R_g$**, por ejemplo $R=0.5 \Omega$, vemos que **caen $2V$ en la resistencia interna** y solo quedan $10V$ para la **carga externa**

![](https://i.imgur.com/nbKvsCn.png)
**ENTONCES:**
Cuanto mas chica la resistencia $R$ comparada con $R_g$, menos voltaje tenes en $R$. Como $R_g$ esta diseñada para darte una corriente especifica "estable", Cuando pedis mas corriente, mas voltaje cae en $Rg$ y menos voltaje tenes disponible para usar.


# Transformadores


### Transformadores ideales
Son elementos que transforman 
* variacion de corriente y voltaje en variacion de campo electrico
* La variacion de campo electrico nuevamente en corriente y voltaje
* Y lo hacen con una relacion


Como la potencia en ambos del transformador es igual (leyes de conservacion)
$$P_1=P_2 \\
V_1.I_1=V_2.I_2\\
\frac{v_1}{v_2}=\frac{I_2}{I_1}$$

Y ademas esto es igual a la relacion entre el numero de vueltas

$$n=\frac{vueltas_1}{vueltas_2}=\frac{v_1}{v_2}=\frac{I_2}{I_1}$$

### Transformadores reales

* Tienen en cuenta el nucleo del transformador, que puede tener mejor o peor conductancia magnetica.
* Tienen en cuenta la resistencia de cable del que esta costruido el transformador
* Un transformador real tiene dos limitantes
	* **SU IMPEDANCIA INTERNA** 
		* que genera una caida de tension, la cual crece cuanta mas corriente pedimos.
	* **El ancho de sus cables**
		* Que determina la maxima corriente que puede pasar por el transformador sin recalentarse por efecto joule
* Estas limitaciones el fabricante te las expresa diciendote la maxima potencia aparente para la que el transformador esta diseñado

![](https://i.imgur.com/UUWybFN.png =400x)



### Polaridad

La regla de la mano derecha te indica la polaridad de cada devanado del transformador. tenemos que tener en cuenta como la bobina enrrolla al campo magnetico

![](https://i.imgur.com/6cAVlOy.png)
### Transformadores de varias salidas

Son transformadores que tienen varios cables saliendo de varios puntos del debanado, permitiendo sacar diferentes tensiones de ellos debido a que cambia la relación de conversión

![](https://i.imgur.com/jeGD3PL.png)

Esto funciona debido a que las tensiones salientes tienen un desface de 90º para el caso de transformadores de dos fases o bifasicos. con un neutro en el medio. Entonces
* **fase1-neutro** $12V$
* * **fase2-neutro** $12V$
* * **fase1-fase2** $24V$ por un desfajase de 90º

### Valores

Los valores principales de un transformador son en genera 
* Voltaje de entrada
* voltajes de salida
* maximo amperaje de salida
	* Para evitar efecto joule

Por ejemplo

$$230/12/12 - A$$

![](https://i.imgur.com/cxilMNZ.png =150x)




# Capacitores

Son componentes que pueden guardar energia

## Valores
#### Mas importantes
Los condensadores tienen los siguientes valores
* **Capacitancia**
* **Tension maxima** entre extremos
	* Si se supera, se perfora el dielectrico, generando un arco, calor y finalmente la explosion del capacitor
* **Polaridad** (Con o sin)
* **Tolerancia**
	* La posible variacion de capacidad, por ej $+-10\%$del valor indicado
* **Tension de pico** es la maxima tension que soporta el capacitor en un pico brve de tension

#### Normalizacion y valores marcados

Los **valores de tension maxima** estan normalizados, son $$6.3-10-16-25-40-63-100-160-250-350-358-450$$

#### Leer valores

Para los capacitores con valores que **no estan claramente marcados**, existen estos codigos

* Capacitores $<1 p F$ se expresa en picofaradios, por ejemplo este capacitor tiene $100000pF$, a su vez pueden o no tener **tension y tolerancia**
* ![](https://i.imgur.com/dHgWXw8.png =400x)
* ![](https://i.imgur.com/RdD4wOw.png)
* * Los de **plastico metalizado** a su vez suelen tener la siguiente nomenclatura
* ![](https://i.imgur.com/MdDP5Gr.png)
## Calculos
### Calculo de capacidad
La capacidad es una funcion de la superficie de las placas, su distancia y la permitividad del dielectrico entre ellas

![](https://i.imgur.com/wIG4MKz.png =250x)
A su vez, la carga almacenada depende de la tension y la capacidad
![](https://i.imgur.com/mzMl5uX.png)
### Capacitores reales vs ideales


Un capacitor real se concibe añadiendo en paralelo la resistencia del dielectrico. esta es **inmensa** y entonces el 99% de las veces es despreciable, pero sirve para determinar por ejemplo La cantidad de calor que va a disipar el capacitor

![](https://i.imgur.com/z1KbjXC.png =250x)
### Energia almacenada en un capacitor
[Explicacion piola](https://www.youtube.com/watch?v=9T6HGC-m8zU&t=309s)
![](https://i.imgur.com/dSANpS1.png)
### Capacitores en paralelo

Los capacitores en paralelo suman su capacidad como si se tratara de un solo capacitor mas grande, ya que suman superficie de placas

$$C_t=C_1+C_2+C_3$$

Ademas en paralelo, es obvio que la suma de las corrientes es la corriente total

$$I_t=I_1+I_2+I_3$$

y la corriente en cada capacitor en capacitores en paralelo es proporcional a la capacitancia de ese capacitor comparado con la total

$I_{c1}=V\frac{c_1}{c_1+c_2+c_3}$


### Capacitores en serie

Cada capacitor funciona como una pequeña batería, sumando su diferencia de potencial al siguiente

$$V_t=V_1+V_2+V_3$$

Y su capacitancia, como si fueran resistencias en paralelo
$C_t=\frac{C_1.C_2}{C_1+C_2}$

Es **critico** notar que 
* la cantidad de carga en cada capacitor en serie es la misma ($Q_1=Q_2=Q_3$)
* A su vez es la misma cantidad de carga que  el circuito ve como total $Q_1=Q_2=Q_3=Q_t$. Esto **no es un error**, la cantidad de carga **no es la suma de las cargas**
* Cuanto **mas chico el capacitor**, este esta mas lleno y por ende **tiene mas voltaje**

## En AC sinusoidal (impedancia)
[fuente](https://www.youtube.com/watch?v=17Fk2MN9c_Q&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=39)
Forma una impedancia que se calcula como
$$\Omega impedance = \frac{1}{(w).L}=\frac{1}{(2\pi f)L}$$

* osea que **a menos frecuencia, mas impedancia!**
* Cuanto **mas chico el capacitor, mas impedancia**
	* Si es lo suficientemente grande tal vez ni notes un cambio



## Tipos

### Comparacion 
Aqui podemos ver una comparacion de la **capacitancia** de los diferentes tipos de capacitores

![](https://i.imgur.com/Eva4FMo.png)

### Electroliticos

Generalmente se clasifican por el **tipo de dielectrico con el que son fabricados**

* Electroliticos
	* Son los de mejorratio capacitancia-volumen
	* Son dos placas enrolladas metalicas con un papel impregnado en un electrolito entre ellas
	* Tienen **polaridad**
	* Pueden ser de:
		* **Aluminio**
		* **Tántalo**

#### Aluminio


**Aluminio** Tienen una armadura externa de aluminio
* Capacidad entre  $0.1 \mu F$ y $100 \mu F$
* Tolerancias entre $+-10\% ;+30\%;+50\%$
* Generan explosiones al cortocircuitarse
*	**Fallan en circuito abierto**
 
![](https://i.imgur.com/qMZwaSY.png)

#### Tántalo

*	Tienen mayor capacidad  $0.1 \mu F$ y $1200 \mu F$
*	Tolerancias $+-5\% ;+-20\%$
*	Generan explosiones **violentas** y **arden** al cortocircuitarse
*	**Fallan en circuito cerrado**
![](https://i.imgur.com/HvFEVAJ.png)

![](https://i.imgur.com/2CJc1jl.png =150x)

**APLICACIONES**
Se pueden usar como
* Reservorios de energia
* Retardadores para temporizadores
* Filtrado de señales
* Acoplamiento entre etapas de amplificacion

###  Plastico metalizados

Son capacitores mas robustos y con menos probabilidad de explosion, son placas separadas por plastico.

Tienen como caracteristicas principales
* Grandes **tensiones** de funcionamiento
* Funcionan a gran **variedad de temperaturas**
* **Capacidad autoregenerativa** si el dielectrico se rompe, la temperatura del arco que se genera vaporiza el metal del otro lado y se extingue el arco, la perdida de capacitancia es despreciable, el capacitor sigue operativo




**Los hay:**
* **Tipo K** Armadura de laminas de metal
	* Alta precision, muchas veces para audio y osciladores
	* **KS** Poliestireno como dielectrico
	* **KP** Dielectrico de polipropileno
* **Tipo MK** Armadura de laminas de metal vaporizado
![](https://i.imgur.com/UvilDyl.png)
![](https://i.imgur.com/x7l0HXu.png)
### Ceramicos
Usan como dielectrico una ceramica

**Los hay**
* **Monocapa**
	* Es una lamina de ceramica recubierta de amos lados con metal
	* Capacitancia desde $2.2pF$ (pico) hasta $0.22 \mu F$
	* Maxima tension de aprox $63V$
	* ![](https://i.imgur.com/H8CPSyw.png)
* **Multicapa**
	* $1pF$ (pico) hasta $10 \mu F$
	* ![](https://i.imgur.com/rKBPABS.png)
* * **Mica**
	* Estables, precisos, caros
	* $1pF$ (pico) hasta $0.1 \mu F$
	* ![](https://i.imgur.com/cibP3Jg.png)

### CAEV (Cap alta eficiencia volumetrica)

Tienen como caracteristica tener una superalta capacidad con respecto a su volumen,
* Capacitancias de  **10 a 50 veces mas que los electroliticos**
* Manejan **bajas tensiones (ej $5V$)**
* No utilizan dielectrico
* Capacidades gigantes, por ejemplo $1F$
![](https://i.imgur.com/FycgPL2.png)


### Capacitores variables

Son capacitores que pueden variar su capacitancia, algunos ejemplos son

* **Trimmers con dielectrico**
	* De ajuste, para variar su capacitancia durante el uso del circuito o si hace falta ajustarla durante la fabricacion
	* ![](https://i.imgur.com/2h9LRm9.png)
* **Trimmers de aire**
	* Antiguos y se usan poco, su dielectrico es el mismo aire
	* ![](https://i.imgur.com/JMyoRea.png)

# Inductores


## Calculo
### Que son
Son dispositivos que generan campos **magneticos** mediante una corriente que los atraviesa.
* Cualquier conductor es un inductor que genera un campo a su alrededor según el **maxwell corkscrew law**
* Si enrollas el conductor, entonces los campos se continuan entre si.

![](https://i.imgur.com/lV8XhnG.png)
### El Henrrio

Es la unidad de inductancia, que indica cuantos volts genera el inductor cuando la corriente **cambia** un ampere por segundo

$$L=\frac{V}{\Delta A}=\frac{V}{i(t)dt}$$

>Osea que una bobina de **1 webber** hacer aparecer
 **1 volt** si la corriente que la atraviesa cambia **1 amper** por segundo

Tambien es la relacion entre el flujo magnetico creado ($ø$) y la corriente $i$

$L=\frac{ø}{i}$

La inductancia de un inductor esta definida por algunas características físicas

$$L=\frac{Vueltas^2.Area.M_r.M_o}{largo}$$
Donde
* $Vueltas$ del conductor, al estar **al cuadrado** es el parametro mas importante
* $M_r$ es la permitividad relativa del nucleo
	* Un nucleo mas permeable (hierro) aumenta mucho mas la inductancia que un nucleo poco permeable (aire)
* $M_o$ es la permitividad del free space (una constante)
* $Area$ o seccion del nucleo
* $Largo$ del nucleo

### El inductor real

Un inductor real tiene una cierta resistencia debido a la resistencia del cable, para modelar un **inductor real** entonces usamos un **inductor ideal** en paralelo con una **resistencia**.

![](https://i.imgur.com/twBMtc0.png)
### Energia almacenada por una bobina

$E(t)=\frac{1}{2}L(i(t)^2)$

### Inductores en serie y paralelo

Se calculan como si fueran resistencias

**Serie:**
$$\boxed{L_t=L_1+L_2+L_3}$$

**Paralelo:**

$$\boxed{L_t=\frac{1}{\frac{1}{L_1}+\frac{1}{L_2}+\frac{1}{L_3}}}$$



### Ley de faraday - WIP

El **Voltaje** entre las terminales de un inductor es directamente proporcional a la **cantidad de vueltas** y a la **velocidad de cambio del campo magnetico**

### Ley de Lenz - WIP

## En DC
### Carga a corriente variable

El proceso de **"carga y descarga"** es muy similar al de un capacitor, con la salvedad de que en vez de **acumular carga** estamos **acumulando campo magnético**

Usan las mismas equaciones de carga y descarga que el capacitor.

$$\large{V_l(t)=V_ie^{\frac{-t}{\tau}}}$$
$$\large{i_l(t)=i_f+(i_i-i_f)e^{\frac{-t}{\tau}}}$$

A su vez

$$\tau = \frac{l}{r}$$
>Notamos que a diferencia del capacitor, la bobina se **descarga o carga mas rapido cuanto mayor resistencia** ya que $\tau$ sera menor

Inversamente a un capacitor, un inductor se comporta como un circuito abierto en $t=0$ y como un corto en $t=5\tau$

![](https://i.imgur.com/xBwKf8i.png =250x)
Se puede apreciar aca como inicialmente el inductor opone una reistencia $T=0$ y va cediendo a medida que se genera el campo magnetico $t=5\tau$

![](https://i.imgur.com/ud11as3.png)
### Carga a tension constante
[Fuente](https://www.youtube.com/watch?v=ZcSSSi6go7c&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=37)

Desde la definicion
$$L=\frac{V}{\Delta A}=\frac{V}{i(t)dt}$$

Se desprende que


$$\boxed{\huge{i_l(t)=\frac{1}{L}\int V_l(t)dt}}$$

Si la corriente es constante, esto resuelve a (???)
$$\boxed{\huge{i_l(t)=\frac{1}{L}V_l.t+I_i}}$$
lo cual resulta en un cambio de corriente **lineal** y **NO EXPONENCIAL**


### Descarga

Inversamente, cuando se deshace el campo magnetico este mantiene brevemente la corriente que empuja, **independientemente de la resistencia que tenga conectada**, esto implica que podemos generar **miles de voltios** si hacemos pasar esa corriente de descarga por funa resistencia muy grande [fuente](https://www.youtube.com/watch?v=SB4LfSd_tCI&list=PLdnqjKaksr8qQ9w3XY5zFXQ2H-zXQFMlI&index=81)



## En AC sinusoidal (impedancia)

[fuente](https://www.youtube.com/watch?v=AYQgpRUtLwU&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=38)
En AC la bobina tiene una impedancia igual a

$$\Omega impedance = (w).L=(2\pi f)L$$

Es decir
* Cuanta **mayor frecuencia**, **mayor impedancia**
* Cuanta **mayor inductancia**, **mayor impedancia**

Ademas sabemos que para la bobina
$$\boxed{\large{i_l(t)=\frac{1}{L}\int V_l(t)dt}}$$

Sabemos que en AC 
$V(t)=V_{pico}.sin(w)tdt$

Reemplazano

$$\boxed{\large{i_l(t)=\frac{1}{L}\int (V_{pico}.sin(w)tdt)dt}}$$

Acomodando


$$\boxed{\large{i_l(t)=\frac{V_{pico.sin(wt-90°)}}{Lw}}}$$

Que implica
$$\boxed{\large{i_l(t)=\frac{V_{pico.sin(wt-90°)}}{impedancia}}}$$
Que implca
$$\boxed{\large{i_l(t)=\frac{V(t)}{impedancia}}}$$
Y eso es basicamente la deduccion de la ley de ohm en alterna!


### Aplicaciones

Son elementos de control de corriente, nunca permiten un cambio bruzco de corriente

## Tipos

### Fijas

Son bobinas con una inductancia fija, las hay de varios tipos

* **Nucleo de aire**
	* Baja inductancia por baja permitividad del aire
	* Generalmente trabajan a alta frecuencia y en equipos de comunicacion
	* ![](https://i.imgur.com/gb8EmPr.png =x50)
* **Nucleo de hierro**
	* Mayor inductancia por mejor permitividad del hierro
	* Operan en bajas frecuencias, muchas veces en fuentes de alimentacion
	* ![](https://i.imgur.com/jw7WAvy.png =x70)
* **Nucleo de ferrita**
	* Mayor inductancia y menor tamaño que las de hierro
	* ![](https://i.imgur.com/j9LtS4J.png =x70)

### Variables

Son bobinas a las que se les mueve el nucleo, cambiando la inductancia, generalmente el nucleo es un tornillo que al girarlo se va metiendo en la bobina, aumentando la permitividad.

El ajuste en un circuito encendido se hace con un **destornillador de plastico**, ya que el de metal aumenta la permitividad mientras lo ajustas

![](https://i.imgur.com/dFvq1iq.png =x100)
# Potencia aparente y react

Aca vemos la corriente y la potencia con un **desface**, como 
$P=V.I$, vemos que en los momentos en los que
* **Los dos son positivos:** potencia positiva (activa)
* **los dos son negativos:** Potencia positiva (activa)
* **solo uno es negativo:** Potencia negativa (reactiva)
	* La potencia vuelve al generador 

![](https://i.imgur.com/R3tgN40.png)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5OTYxNDM0MzksLTM4Nzk4ODIwNCwtMT
M4MzEyNTU0NiwtNzAyMTAxMTYwLC01NTU0ODk2NTYsLTE5NjI5
NDI2OTMsLTE4Njk1OTY1ODUsMTA5OTc5MzY4OSwtMjAxNjM4Mz
k3Miw4NTUwMjE2MDEsMTI2MjUyMzQ0MCwtNzQzMTA3ODMxLC0x
MjgzODIzMTEyLC01MzI5OTIzMCwxMjEwODYyMjA5LDkzNzIxMT
Y2MCwtMTAyMDQ2OTcyNSw5ODQ4NTM4OTYsMTY3NTg0NzU2NCwy
NjM5NzQxMzhdfQ==
-->