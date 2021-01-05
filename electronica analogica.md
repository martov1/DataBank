

**Nivel técnico electrónico**
https://www.youtube.com/watch?v=sekdEc5wU6k&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=70

 Como calcular el valor promedio de señales DC mas utilizadas en electronica

**transistores**
https://www.youtube.com/watch?v=dIV5l9cx_ck&list=PLuzS0jdNRVvpVTO-2va0jHcAyt5q8HV-O

https://www.youtube.com/watch?v=4rfMe_QVbDs&list=PLChMFns-GJssNBAo1xbJHSduZ0FXLer4T&index=2

https://www.youtube.com/watch?v=-LPALAwcYkg&list=PL4651816D92AB6B2B&index=7



**VER aplicacion en reparacion de notebooks**
https://www.youtube.com/watch?v=1XGun_-06aA&list=PLHk1hZEmw3_zlUPRfVeBHLSUviVNfR4pNvideo 3 minuto 7

# Componentes


## Resistores

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

## En AC
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



## En AC

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

# Circuitos comunes


## Estrella-triangulo 
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

## Wheatstone bridge - WIP

## Circuito Resistor-Capacitor (RC) en CC

[fuente](https://www.youtube.com/watch?v=IAD3OK7i-pM&list=PLdnqjKaksr8qQ9w3XY5zFXQ2H-zXQFMlI&index=72)

Se trata de un circuito con un capacitor y un resistor
![](https://i.imgur.com/xR2LR4r.png =200x)
Se analiza usando una tecnica denominado **Transient analisis**, que estudia el circuito a lo largo del **tiempo**

### Carga
Las magnitudes en el capacitor **durante su carga** se modelan con

* $\large{I_{cap}(t)=Ie^{\frac{-t}{\tau}}}$ general decay function
* $\large{V_{cap}(t)=V_f+(V_i-V_f)e^{\frac{-t}{\tau}}}$ exponential growth function
* Donde $\tau=R.C$ es aprox un quinto $\frac{1}{5}$ del tiempo que tardara el capacitor en llenarse, es decir se llenara el cap en $5\tau$

[Derivacion de esas equaciones](https://www.youtube.com/watch?v=gd7caHXKtp8)

A su vez, podemos analizar lo que sucede en el resistor $R$
* Notamos que $I_R=I_{cap}(t)$ por que esta en serie con el capacitor y entonces pasara la misma corriente.
*  Por ley de ohm $\large{\frac{v_{R}(t)}{R}=I_{cap}(t)}$
	* Entonces en el resistor $V_{R}(t)=I_{cap}(t)R$
* Tambien podes usar **KVL** o/y **KCL**

![](https://i.imgur.com/FUy3unc.png =600x)
### Aplicación
Esto se usa para circuitos que necesitan cambios de tension lentos y no abruptos, cambiando la combinacion de $R$ y $C$ cambio $\tau$ y eso cambia la cantidad de tiempo que tarda el circuito en elevar su tension hasta la tension maxima.

**los capacitores amortiguan rapidos cambios en voltaje**

### Carga a corriente constante

Si la carga del capacitor es a **corriente constante** (por que hay una **fuente de corriente**) entonces la carga obedece a

$$\boxed{\huge{v_c(t)=\frac{1}{c}\int i_c(t)dt}}$$
Que tiene todo el sentido del mundo, por que es la suma de las cargas que se van depositando en el capacitor, osea la carga total en el capacitor, sobre la capacitancia. Osea obedece a 

$Q=C.V$
osea
$V=\frac{1}{C}Q$
que es lo mismo que
$V=\frac{1}{C}\int i_c(t)dt$
ya que la carga total $Q$ es la suma de la corriente a lo largo del tiempo



Si la corriente es constante, esto resuelve a (???)
$$\boxed{\huge{v_c(t)=\frac{1}{c}i.t.V_i}}$$


### Descarga

Similarmente
* $\large{I_{cap}(t)=-Ie^{\frac{-t}{\tau}}}$ general decay function
* $\large{V_{cap}(t)=V_i.e^{\frac{-t}{\tau}}}$ exponential growth function
* Donde $\tau=R.C$ es aprox un quinto $\frac{1}{5}$ del tiempo que tardara el capacitor en llenarse, es decir se llenara el cap en $5\tau$

A su vez ahora el resistor (en serie, no el de carga) disipa esa potencia acumulada en el capacitor usando ese mismo voltaje $I_{cap}(t)$ y amperaje $V_{cap}(t)$
![](https://i.imgur.com/3Yy3x0V.png)

### Potencia disipada

Durante la descarga
* El **resistor disipa potencia**
* El **Capacitor absorbe energia**, que desde la perspectiva de la fuente es como si disipara potencia

Durante la descarga
* Un resistor disipa potencia
* El capacitor provee potencia (o disipa potencia negativa, depende de como lo veas)

![](https://i.imgur.com/5iRtEh4.png)
Vemos que la potencia total consumida en la carga va a ser la suma de la potencia absorbida por el capacitor y la disipada por el resistor.
La linea roja es la potencia total, y es igual a la suma de las dos lineas moradas que son la potencia disipada por el resistor y la potencia absorbida por el capacitor.

![](https://i.imgur.com/CyfeQps.png)

### Analisis con thevenin

Cuando tenes varios resistores, podes pensar el equivalente de thevenin y tratar el circuito como un RC

![](https://i.imgur.com/0OMngol.png)

## Filtros pasivos

### Filtro alto-bajo
Es un filtro que filtra las **frecuencias altas** o las **frecuencias bajas**, esto se hace aprovechando que
* la impedancia del capacitor es **mayor a mas frecuencia**
	* Elimina las frecuencias altas
* La impedancia del inductor es **mayor a menor frecuencia**
	* Elimina las frecuencias bajas


![](https://i.imgur.com/vim2R55.png =x300)
#### Frecuencia de corte

[fuente](https://www.youtube.com/watch?v=KQvxdAlBj04&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=47)

**Bobina:**
Es la frecuencia a partir de la cual el filtro empieza a actuar  y el filtro comienza a no dejar pasar la tension.
Se calcula como:
* $Z=w.L=R_{th}$ cuando la bobina no esta cargada, solo tiene como resistencia la $R_{thevenin}$, es decir, la bobina no presenta ninguna resistencia
* como $w=2\pi f$, reemplazando y despejando $f$
$\huge{\boxed{f_c =\frac{R_{th}}{\pi L}}}$
A este $f_c$ lo llamamos frecuencia de corte, y es cuando a este circuito en particular le va a empezar a actuar el filtro de manera significativa
![](https://i.imgur.com/ohxpW8r.png =300x)

**Capacitor:**

Es súper similar, pero usando la formula de impedancia del capacitor en vez de el del inductor

 * $Z=\frac{1}{w.L}=R_{th}$ con el capacitor descargado, la unica resistencia que hay es la de thevenin
 * $Z=\frac{1}{2\pi f C}=R_{th}$ reemplazando $w=2\pi f$
 * $f_c=\frac{2}{\pi R_{th}C}$ y esa es la frecuencia de corte

Podemos ver como los voltajes que estan por debajo de cierta frecuencia quedan reducidos de manera lineal, mientras que los que estan por encima pasan de forma plena

![](https://i.imgur.com/wqqWBsx.png =300x)

Puede ser en serie o en paralelo, lo que cambia es $R_{th}$
![](https://i.imgur.com/QCCi3E4.png =300x)
![](https://i.imgur.com/8U0fXHI.png =300x)

### Filtro Paso y rechaza banda
[Fuente](https://www.youtube.com/watch?v=4LhDcDaefzo&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=48)


#### Pasa banda
**Filtro paso banda**
Es muy similar al filtro alto-bajo, pero se compone de dos filtros, de tal manera que deja pasar **solo un rango de frecuencias** y elimina las demas.

Se calcula como dos filtros alto-bajo separados 

![](https://i.imgur.com/tcByJuD.png)

#### Rechaza banda

Es un filtro que deja pasar todas las frecuencias salvo las que estan en un rango, a la que llamamos la **frecuencia de resonancia**.


![](https://i.imgur.com/tIXxpWz.png)




$$\large{\boxed{f_r=\frac{1}{2\pi \sqrt{LC}}}}$$

### Aplicaciones
En un parlante de 3 speakers que reproducen los sonidos graves, medios y agudos, se usan 3 filtros. 
* **paso bajo** para los bajos
* **paso alto** para los altos
* **paso banda** para los medios

Todos se pueden hacer con capacitores y/o inductores en serie y/o paralelo.

![](https://i.imgur.com/d7MkbVD.png)![](https://i.imgur.com/gQrZG5G.png =200x)
### Filtro de  Resonancia

Es un filtro que solo deja parar una **frecuencia especifica** (no una banda, una frecuencia puntual).

#### Frecuencia de resonancia serie
[fuente](https://www.youtube.com/watch?v=KxDOmMMo6so&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=49)
Llamamos resonancia a cuando le impedancia de un inductor se **cancela perfectamente** con la de un capacitor para una frecuencia de resonancia $f_r$ 

En **RESONANCA** todo el **voltaje** pasa por $R$

>Se usa mucho para **sintonizadores de radio** por ejemplo, para poder filtrar una sola frecuencia especifica

![](https://i.imgur.com/D64Zk9D.png)

Podemos calcular la resonancia en este circuito IRL en paralelo viendo cuando la impedancia del inductor es igual a la del capacitor.

$\text{Inductor } \Omega  =\text{Capacitor } \Omega$
osea
$wL=\frac{1}{wc}$

Despejando $w$
$w=\sqrt{\frac{1}{LC}}$
Reemplazando $w$ por su definicion $w=2\pi f$ y despejando $f$ obtengo $f_r$

$$\boxed{f_r=\frac{1}{2\pi \sqrt{LC}}}$$

#### Frecuencia de corte
[fuente](https://www.youtube.com/watch?v=KxDOmMMo6so&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=49)
A su vez observamos que a los costados de esa curva existe un lugar donde la potencia es la **mitad de la maxima**, esos puntos los vamos a considerar como "frecuencias de corte".

La corriente en las frecuencias de corte $f_1$ y $f_2$ es $\frac{I_{resonancia}}{\sqrt{2}}$ ([deduccion](https://www.youtube.com/watch?v=KxDOmMMo6so&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=49))

Al rango de **frecuencias entre las frecuencias de corte** le decimos **ancho de banda** o **band-width**

![](https://i.imgur.com/62XQBG4.png)
#### Factor de calidad

El factor de calidad del circuito $Q$ es que tan grande es el ancho de banda que deja pasar mas alla de la frecuencia de resonancia $F_r$.

En un circuito de un sintonizador de radio por ejemplo, cuanta mas calidad, menos de otras frecuencias escuchamos y mas de la frecuencia $f_r$.

$\boxed{Q \to \inf \Rightarrow |f_1-f_2| \to 0}$ 

Esto se determina, logicamente, como
$\boxed{|f_1-f_2|=\frac{f_r}{Q}}$ 
ó
$\boxed{Q =\frac{f_r}{|f_1-f_2|}}$ 


**Como lo calculamos:**
[fuente, no se entiende exactamente de donde sale](https://www.youtube.com/watch?v=KxDOmMMo6so&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=49)

$Q=\frac{V_l}{V_r}=\frac{V_c}{V_r}$

Esto implica como efecto secundario, si tengo un alto factor de calidad, tal vez tenga una muy alta tension en la bobina
$V_l=QV_r$
Y asi mismo para el condensador
$V_c=QV_r$
Por eso cuando pones un condensador tiene que estar pensado para la potencia que ese factor de calidad te puede generar!

#### Frecuencia de resonancia paralelo
[fuente](https://www.youtube.com/watch?v=vHFVBn3E3l4&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=50)

A diferencia del circuito en serie, este tiene impedancia maxima cuando llegas a la frecuencia de resonancia $f_r$, eso significa que toda la corriente pasa por $R$.

>En **resonancia** toda la **corriente** pasa por $R$

Lo que sucede en resonancia es que **el capacitor y el inductor INTERCAMBIAN CORRIENTE** entre si, pero no con el circuito


![](https://i.imgur.com/L7sg0WE.png)
Si ponemos un capacitor y una bobina en paralelo, sabemos que


$$Z_{paralelo}=\frac{(Z_l)(-Z_c)}{Z_l+(-Z_c)}$$

Cuando nos aproximamos a la frecuencia de resonancia, sucede que
$$Z_l=Z_c$$

Entonces nos damos cuenta que
 $Z_l+(-Z_c) \to 0$ 
 
y por ende
 $Z_{paralelo} \to \inf$

Es decir, en $f_r$ninguna corriente pasara por el capacitor o por el inductor, toda lacorriente pasara por el resistor.

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


# Diodos

## Diodo P-N

### Descripcion y valores
Es un **semiconductor** que transmite la corriente en un solo sentido.


* **Transmite** la corriente en un sentido a partir de un cierto voltaje $V$
	* Para diodos de **silicio** suele ser mas o menos $0.7V$
	* Para otros la tension varia
* **Detiene** la corriente en el otro sentido
	*  hasta cierta tension llamada tension de ruptura $V_{rupt}$ y el diodo se destruye
* **Soporta** hasta cierta corriente maxima


   ![](https://i.imgur.com/7xDded4.png)
### Circuito equivalente

al ser un elemento **no-lineal** no lo puedo calcular con mis herramientas de analisis de circuitos normal. Tengo que hacer algunas simplificaciones.

Como el diodo genera
* **En la polaridad normal**
	* Una caida de potencial de $0.7V$
		* **MODELO:** Una fuente de tension con la polaridad al revez, tal que elimine $0.7v$
	* Una relacion casi lineal de $V$ y $I$ luego de los $0.7v$
		* **MODELO:** Un resistor que genere una relacion lineal entre $V$ e $I$
		* **MODELO:** En general es tan chico que ni se coloca
* **En la polaridad inversa**
	* Una interrupcion de la corriente en polaridad normal
		* **MODELO:** Interuptor abierto




![](https://i.imgur.com/6MOtKeJ.png)
### Analisis de circuito

* Haces el reemplazo del diodo por la fuente (su equivalente)
* Usas las herramientas normales (mallas, etc)
* **caso 1:** Si te da una tension $<0.7$ o negativa del catodo al anodo del diodo, es que no pasa corriente por el diodo 
* **caso 2:** Lo volves a modelar el circuito como un circuito abierto t resolves


### Tipos

![](https://i.imgur.com/fW6B1eR.png) 
### Prueba y medicion 
 
Con un tester en modo diodo, que es similar al de conductividad pero con mas voltaje se mide **con polaridad**, si la invertis da **resistencia infinita**

El tester mostrara la **tension de codo**, es decir **a partir de que tension el diodo es conductor**

Posibles fallos:
* **corto** sin resistencia en ambos sentidos
* **abierto** resistencia infinita en ambos sentidos
* **fugas** Baja tension de codo, resistencia en polaridad inversa $<0.018M\Omega$ (mega omnios)

## Circuitos cpmunes

### Protector de polaridad inversa

Hay varias formas de protejer un circuito DC contra una fuente con la polaridad invertida (por ejemplo, por que le colocan la pila al reves)

Esto se puede hacer 
* con un diodo simple
	* Con la polaridad inversa, el circuito**no funciona pero no se quemara**
*  con un Full bridge rectifier
	* El circuito **funcionara aun con polaridad inversa**

![](https://i.imgur.com/1gqUItH.png)


### Clipper de onda

[fuente](https://www.youtube.com/watch?v=S76CnEJMl5E)

[Ejemplo falstad](https://tinyurl.com/yxocj8ru)
Es un circuito que recorta una onda o señal sinosoidal a una tension maxima o minima.

Se usa un diodo con una fuente en oposcion al paso de la tension.
Cuando $V_{sinusoidal}>V_{oposicion}+0.7v$ el diodo deja pasar el exceso de tension que este por encima de  $V_{oposicion}$.

Siempre que la fuente de oposicion sea mas fuerte, o la onda este invertida, el diodo se comporta como un circuito abierto

Esto mantiene como maximo $5V$ a la salida


![](https://i.imgur.com/Q5uQYvi.png)
Se puede usar el mismo circuito al revés para la otra mitad de la onda

![](https://i.imgur.com/Vkx7M23.png)
### Diodo anti-chispa protector de bobina

Son diodos usados para cortocircuitar una bobina cargada cuando a esta se le interrumpeel circuito.

[fuente](https://www.youtube.com/watch?v=Euj7xa4WoVE&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=55)
[ejemplo](https://tinyurl.com/y6ox6u3j)

**El problema:**
* La bobina cargada actua como fuente de corriente
* Cuando se interrumpe su paso de corriente, esta lo toma como una resistencia infinita, generando tensiones gigantescas
* esto genera un chispazo en el interruptor

**Para evitarlo**
* Coloco un diodo paralelo a la bobina
* Al tocar el interruptor, el diodo permite a la corriente recircular por la misma bobina (ya que esta misma esta generando una tension entre sus bornes)
* La energia se disipa en forma de calor en 
	* la resistencia del bobinado 
	* El diodo

![](https://i.imgur.com/Q2HhM9d.png)

### Rectificador

#### De media onda y como control de potencia

**Rectificador de media onda:** 
* Elimina la mitad de una onda sinusoidal con un diodo
* [ejemplo](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3AWAnC1b0DYQGYBM0B2AViIA4i4jdIEKSQikGQFsAoAExCSzA0hzZe-ELhAcApgDMAhgFcANgBc2AN27CBPUUSwCICAUSgmYRNgCdBm6zr3h4bAO63cujXahsA9qJAYEE0MUZhhINxMxMXYgA)
* Se trata de un diodo en serie con una fuente alterna, de tal manera que **no deja pasar la parte negativa de la onda**

![](https://i.imgur.com/Nkcqxw1.png)
**EJEMPLO PRACTICO:**
Se puede limitar a la mitad la potencia de una resistencia calefactora decidiendo si hacer pasar o no la potencia por un diodo
[Ver circuito](https://tinyurl.com/y5zvdfjj)

![](https://i.imgur.com/QI0ElUH.png)

#### De onda completa 2 diodos

[ejemplo](https://tinyurl.com/yxr7kslh)


Es un rectificador que transforma los dos lados de la onda en voltajes positivos. usa (por ejemplo) un transformador a $24V$ y obtiene una tension rectificada de $12V$

Es mas **CARO** que el **full bridge rectifier** por que:
*  necesita un **transformador del doble del voltaje objetivo** 
* y con **salida intermedia**

![](https://i.imgur.com/QjIhfMq.png)


#### Rectificador en puente (full bridge rectifier)

Es un rectificador de onda completa que usa 4 diodos. Usa (por ejemplo) un transformador de $220V-24V$ y obtiene una tension rectificada de $24V$
[ejemplo](https://tinyurl.com/y5t5kot8)
![](https://i.imgur.com/1WOyQzj.png)

Vienen en diferentes formas
![](https://i.imgur.com/IbXFOUC.png =500x)
La codificacion suele ser la siguiente

* $B80$ valor de tension eficaz soportada en Voltios (en esta caso $80 volts$)
* $C2300-1500$ Cantidad de corriente soportada con y sin disipador de tension expresada en miliamperes
	* $2300ma$ con disipador
	* $1500ma$ sin disipador

![](https://i.imgur.com/cfhTzFg.png)

### Duplicador de voltaje

[fuente](https://www.youtube.com/watch?v=k2w1bMIf7mw&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=60)

Este es un circuito que 
* Rectifica media onda
* Duplica su pico cargando un capacitor
[Ejemplo](https://tinyurl.com/y4uhcvvr)

Se trata de un circuito que 
* con una mitad de la onda mantiene un capacitor cargado, mediante un diodo que se salta la resistencia, cargando el capacitor. 
	* osea que desde la perspectiva de la resistencia no hay onda negativa
* En la media onda positiva, el voltaje de la fuente se suma al del capacitor, y al no poder pasar por el diodo, se disipa sobre la resistencia.
	* Como el capacitor cargado tendra el voltaje de la fuente, y estan en serie, se suman, generando el doble de voltaje.
	* Osea que la resistencia ve un pico del doble de voltaje que la fuente



![](https://i.imgur.com/NfbrKBU.png)
### Multiplicador de voltaje

Funciona con varios capacitores en serie con una fuente $AC$
[ejemplo](https://tinyurl.com/y8gvnexs)

La gracia de este circuito es que los capacitores solo pueden descargarse en una direccion, como estan en serie primero se cargan unos y estos **bloquean el paso de la corriente de los otros dos** por lo que **ahora estos tampoco se pueden descargar**
![](https://i.imgur.com/qiOLtLi.png)



### Duplicador y sostenedor de voltaje

Es un circuito similar al anterior, la idea es que carga dos capacitores en serie pero mediante el uso de diodos no permite que se descarguen.

La suma de sus tensiones entonces es el doble de tension maxima de la onda original, y si los capacitores son lo suficientemente grandes  o la resistencia es muy grande, entonces mantienen la tension duplicada aun cuando la onda esta en lugares intermedios.

[Ejemplo](https://tinyurl.com/y55npkhp)
![](https://i.imgur.com/BX6Fneu.png)

## Diodo Zenner

### Descripcion y valores

Se trata de un diodo

* Tiene una curva de funcionamiento similar  a un diodo normal
* En polaridad inversa, despues de cierto voltaje $V_{zener}$, **conduce**
	* Se consiguen diodos con diferentes valores de $V_z$
* **Soporta** una corriente maxima de $I_{zt}$
* Tiene una **resistencia interna** $Z_{Zt}$ que en general es despreciable

![](https://i.imgur.com/znAmbFr.png)

## Diodo LED
[fuente](https://www.youtube.com/watch?v=13rcRufDGGQ&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=69)

### Generalidades
Es un diodo que **en vez de disipar la potencia en calor, la disipa en luz**, generalmente
*  Tienen una **tension de codo de** $1.5V-3.5V$
* Tienen una **corriente maxima**
	*  por lo que **a diferencia del diodo comun** no los podemos alimentar con **cualquier tension**
* Soporta bajas **tensiones inversas**

Hay tres metodos para distinguir el **anodo y catodo**, se aprecian en esta figura
![](https://i.imgur.com/c50sk6Y.png)

### Calculo de Resistencia

Si el diodo LED tiene 
* Resistencia interna de $R_{LED}=50\Omega$
* Corriente maxima de $I_{max}=30ma$
* Voltaje de codo de $V_{codo}=3V$

Y tengo una fuente de $V_{fuente}=5V$ entonces

* **Conexion directa**
	* pasaran $2V$ a traves del diodo 
		* $V_{fuente}-V_{codo}=2V$
	* por ley de ohm $2V/50=0.04A=40ma$
	* **El diodo se quema** $40>I_{max}$

Entonces calcularemos una resistencia para este led usando la **ley de ohm**

* **Calculo resistencia**
	* Deseo que pasen $25ma$ por la fuente 
	* $2/(R_{adicional}+R_{led})=0.025A$
	* $R_{adicional}=30\Omega$

### LED en serie

* Se suman los voltajes codo de cada led $V_{codoTotal}$
* **La fuente de alimentacion debe ser** $V_{fuente}>V_{codoTotal}$
* El voltaje que sobra de la fuente debe, por ley de ohm usando la **resistencia interna** de los led en serie,  **generar una corriente soportada por los led**
	* Caso contrario, **Calcular una resistencia** que lo baje a la corriente soportada usando ley de ohm
	* calcular la **potencia disipada por el resistor** para saber que comprar

### Display numerico LED

Son en realidad varios LEDs
![](https://i.imgur.com/diciLOp.png)
### LED en AC  220v

[Fuente](https://www.youtube.com/watch?v=13rcRufDGGQ&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=69)
#### Metodo ineficiente (Resistencia)
Como los LED tienen **baja tolerancia a tencion inversa** hace falta protejerlos de esta. Se puede hacer **permitiendo el paso de la corriente con otro diodo**

Para evitar que se queme el LED ademas,  usaremos una **resistencia** que reduzca el voltaje a una cantidad adecuada
[ejemplo](https://tinyurl.com/y8tq7pj6)

* La tension  **promedio** es de $\frac{220\sqrt{2}}{\pi}=104V$ (ya que la onda esta rectificada y es media onda)
* La resistencia sera de $10k\Omega$ ya que $1200\Omega=\frac{104V-2V}{0.010A}$
* Como los picos de **tension inversa** son breves por que estamos a $50Hz$ al led no le pasara nada

**Esto es muy ineficiente, por que:**
* **El led disipara** en promedio $2V*0.010= 0.02W$ 
* **La resistencia** un promedio de $102V*0.010= 1W$

![](https://i.imgur.com/NkHf08B.png)
#### Metodo eficiente (Capacitive dropper)
[fuente](https://www.youtube.com/watch?v=13rcRufDGGQ&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=69)
![](https://i.imgur.com/90im7sS.png =250x)

**EL CAPACITOR**
Para hacer uso mas eficiente de la electricidad podemos usar **la impedancia de un capacitor** para limitar la corriente en lugar de hacerlo con una **resistencia**, ya que **los capacitores no disipan potencia pero si tienen una impedancia que limita la corriente**



**LA RESISTENCIA**
Igualmente es necesario colocar una resistencia para limitar el **pico de corriente** que se puede generar si al conectar el circuito estamos en el **pico de la onda**.
Esta **resistencia** la calculamos con la ley de ohm para no sobrepasar la **corriente de pico maxima** del LED segun el datasheet

>**CALCULO DE LA RESISTENCIA**
>**Aplico ley de ohm** 
>Considero que el capacitor esta vacio y me conecto a la red en el momento de maxima tension para calcular la resistencia necesaria para limitar el pico de corriente por el capacitor
$$R=\frac{V_{eficax}\sqrt{2}-V_{caidaDeLed}-V_{capacitor}}{V_{picoDeLed}} \\[10pt]
R=\frac{220v\sqrt{2}-2V-0}{1}\\[10pt]
R=323\Omega$$ Necesitaremos por lo menos una resistencia igual o mayor a este valor.

>**CALCULO DE CAPACITOR**
>**Aplico ley de ohm** 
>Si el led necesita $0.020A$, osea que la impedancia necesaria sera
>$$Z=\frac{230V}{0.02}=11500\Omega$$
>Como tengo el valor de la resistencia, solo tengo que despejar la impedancia del capacitor que hace falta
>$$Z=\sqrt{R^2+X_{cap}^2}\\[10pt]
>11500=\sqrt{323^2+X_{cap}^2}\\[10pt]
>X_{cap}=11490\Omega$$
>Que por la equacion de resistencia del capacitor, a $50hz$, sera
>$$X_{cap}=\frac{1}{2\pi f C}\\[10pt]
11490=\frac{1}{2\pi 50 C}\\[10pt]
>C=2.77E-7 = 0.277\mu F$$

#### Ejemplo practico
[fuente](https://www.youtube.com/watch?v=13rcRufDGGQ&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=69)
Un boton luminoso que se enciende cuando la lampara principal esta apagada
![](https://i.imgur.com/XyElslP.png =250x)
# Transistores - WIP

## Bipolares PNP/NPN - WIP

### Intro
[fuente](https://www.youtube.com/watch?v=dIV5l9cx_ck&list=PLuzS0jdNRVvpVTO-2va0jHcAyt5q8HV-O)

La **utilidad del transistor BJT** radica en que **permite controlar una corriente de forma proporcional a otra corriente mas chica**.

 El factor de proporcion se llama $Hfe$  o tambien $\beta$


Es uno de los tipos de transistores mas comunes y mas basicos, **tienen 3 patas:**
* **COLECTOR:**
	* Por aqui entra la corriente al transistor
* **EMISOR**
	* Por aca **sale la corriente del transistor**, de forma **proporcional** a la corriente de la base
* **BASE:**
	* Determina la corriente **Colector-Emisor** proporcionalmente a  la corriente **Base-Emisor**
	* el vinculo **Base-Emisor** es un **DIODO** y entonces tiene una **caida de tension de** $0.7V$ 



![](https://i.imgur.com/f0ZDUAS.png =250x)

### PNP vs NPN

Los dos tipos de transistores son super similares, la diferencia principal es
* **NPN:** 
	* La corriente va desde **colector a emisor** (conventional current)
	* $I_{ce}$ esta definida por la corriente que **ENTRA** por la base $I_b$ y que va hacia el emisor, osea 
		* $\boxed{I_e=I_b+I_c}$ 
	* Hay una **CAIDA DE POTENCIAL** entre **base y emisor** de $0.7V$, 
		* **critico:** asi que si **colector y base comparten el positivo** de la misma fuente, **CIRCULA CORRIENTE**
	* ![](https://i.imgur.com/HblVeUG.png =130x)
* **PNP** 
	* La corriente va desde **emisor a colector** (conventional current)
	* $I_{ce}$ esta definida por la corriente que **SALE** por la base $I_b$ y que viene desde el emisor, osea 
		* $\boxed{I_c=I_b-I_e}$ 
		* Hay una **CAIDA DE POTENCIAL** entre **emisor y base** de $0.7V$.
			 * **critico:** asi que si **colector y base comparten el negativo** de la fuente, **CIRCULA CORRIENTE**
		* ![](https://i.imgur.com/V3vu9km.png )

### Zonas de trabajo

[ejemplo](https://tinyurl.com/y3ypu423)
[fuente](https://www.youtube.com/watch?v=7Q79fhvoRSs&list=PLuzS0jdNRVvpVTO-2va0jHcAyt5q8HV-O&index=2)
![](https://i.imgur.com/CYzJxHv.png =300x)

Los transistores BJT tienen 3 zonas de trabajo
* **ZONA DE CORTE:** 
	* Las corrientes de $I_{base}$ donde **no pasa corriente** por $I_{emisor}$ 
	* $\boxed{I_{emisor}=0}$ 
	* $\boxed{V_{emisor-colector}<0.7}$ 
* **ZONA ACTIVA:**
	* Las corrientes de $I_{base}$ donde $I_{emisor}$ es **poroporcional** a $I_{base}$
	*  $\boxed{I_{emisor}=hfe.I_{base}}$
* **ZONA DE SATURACION:**
	* Las corrientes de $I_{base}$ donde $I_{emisor}$ es **maxima y no puede aumentar mas**
	*  $\boxed{I_{emisor}=I_{\text{saturacion}}}$



| Zona Corte       | Zona Activa          | Zona saturacion        |
|------------------|----------------------|------------------------|
| $I_{b}=0$        | $I_c=\beta.I_b$      | $I_b = I_{saturacion}$ |
| $I_{c}=0$        | $0<V_{ce}<V_{src}$   | $V_{ce}\approx 0$     |
| $0<V_{be}<0.7$   | $V_{be}\approx 0.7V$ |   $V_{be}>0.7V$                     |
| circuito ABIERTO | Amplificacion        | circuito CERRADO       |



### Circuitos comunes y aplicaciones
#### Interruptor digital - Baja potencia
[fuente](https://www.youtube.com/watch?v=kVBHdR5V7MU&list=PLuzS0jdNRVvpVTO-2va0jHcAyt5q8HV-O&index=3) 

[Ejemplo](https://tinyurl.com/y49wqczv)

El transistor BJT se usa comunmente como **interruptor**, para que una **corriente de control** chiquita (de un arduino por ejemplo) active una **corriente de trabajo** (grande, para un motor o una lamapara).

Para esta utilidad nos interesan la **ZONA DE CORTE** y la **ZONA DE SATURACION**. 

**Por ejemplo:**
*  Un microcontrolador manda una tension de $5v$ pero solo puede emitir una **corriente max** de $1ma$
	* Con un **transistor** enviamos $5v$ de la fuente para prender un LED con $100ma$
* Añadimos una **resistencia** adecuada para **limitar la corriente** que sale del microcontrolador.
* Cuando el microcontrolador deje de enviar esa señal booleana, el **LED se apaga**.

[Ejemplo](https://tinyurl.com/y49wqczv)
![](https://i.imgur.com/gCvDjV3.png)
#### Interruptor digital - Alta potencia
[fuente](https://www.youtube.com/watch?v=TE_pQ8pyL80&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=83)
[Ejemplo](https://tinyurl.com/yy9qzgty)
El concepto es similar, pero en lugar de usar un integrado para accionar un  transistor para alimentar algo, usamos el transistor para accionar un rele.
![](https://i.imgur.com/EH3Ahxy.png =700x)
#### Interruptor digital octoacoplado - Alta potencia 
[fuente](https://www.youtube.com/watch?v=slNPfrQaVlo&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=84)
Similar al anterior, pero con las siguientes mejoras.
* **Octoacoplacion:**  aisla fisicamene el circuito de control del circuito de corriente, esto evita que el circuito de control se dañe si algo sale mal con el circuito de corriente.
* **led indicador** de funcionamiento (facil, simplemente un led y una resistencia)

[Ejemplo](https://tinyurl.com/y3fnbdq9)
![](https://i.imgur.com/KxE9tEc.png)
#### Interruptor digital inversible - puente H 
[fuente](https://www.youtube.com/watch?v=eWkXawMjDxQ&list=PLuzS0jdNRVvpVTO-2va0jHcAyt5q8HV-O&index=7)
[ejemplo](https://tinyurl.com/yxms2tg3)
Se trata de una configuracion de transitores que permite **revertir el paso de la corriente**, por ejemplo para revertir el giro de un motor DC.

Usa dos transistores NPN y dos PNP
![](https://i.imgur.com/QOMLzxP.png)
#### Par Darlington - WIP
[fuente 1](https://www.youtube.com/watch?v=AO4faM1yhLw&list=PLuzS0jdNRVvpVTO-2va0jHcAyt5q8HV-O&index=10)


Se trata de dos transistores BJT en serie

![](https://i.imgur.com/OTt5rMV.png =200x)

* **Super sensibles** con poca corriente los saturas
	* Con **MUY poca corriente** podes hacer pasar un monton de corriente
* Suelen **disipar mucha potencia**
* **Caida de tension de saturacion** Tenes una caida de tension que es el doble a un solo transistor, osea en vez de $V_{ec}\approx 0.2v$ se ve mas como $V_{ec}\approx 0.6v$
* **Muchas veces se vende hecho**
	* Con resistencias para rapidez de conmutacion
	* Con diodo de proteccion para control de motores DC
	* ![](https://i.imgur.com/m74hL9Q.png =150x)




#### Voltage-divider biasing - WIP
https://tinyurl.com/yyccztsx
[ACAAAAA](https://www.youtube.com/watch?v=4kOVYORP1uo)
[ACA TMB](https://www.youtube.com/watch?v=YQlbPGNB-ys)
https://www.youtube.com/watch?v=t0UOSIUve9E&t=475s
https://www.youtube.com/watch?v=IkabRft5Sdk

#### Amplificador Clase A - WIP
#### Amplificador  Clase B - WIP
#### Amplificador  Clase AB - WIP
#### Amplificador  Clase C - WIP
#### fuente entabilizada de tension con transistor - WIP
[Fuente de tension  estabilizada con transistor](https://tinyurl.com/y7z3hu3a)

[Fuente de corriente estabilizada con transistor](https://tinyurl.com/y7c6umte)
## MOSFET - WIP



## JFET - WIP

[ver, explicacion y circuitos comunes aca](https://www.youtube.com/watch?v=PAsQYiWP7sg&list=PLveP8oiH14b5FbY_Aho6lfsi37AU-L7cS)
[Ver, explicacion y circuitos comunes 2](https://www.youtube.com/watch?v=dJx0VZfW6J8&list=PLC7117B136C379C6E&index=3)

[ejemplo JFET](https://tinyurl.com/ybj3947f)


# Amplificadores - WIP

[ver](https://www.youtube.com/watch?v=vE_bQivEVuE&list=PLuzS0jdNRVvocxP2rQjT0EL0mqcoB1JLV)

# Fuentes de alimentación

## Simple estabilizada con zener


[ejemplo](https://tinyurl.com/y958utw7)
[Ejemplo con detalles](https://tinyurl.com/ycp7f64j)
Se trata de una fuente sencilla, tiene
* **Un rectificador** que transforma la onda AC en una onda DC
* **Un filtro** que aplana la onda DC, que consta de
* **Un estabilizados** que evita que la tension en DC sobrepase un valor determinado

Como la **estabilizacion** se hace mediante **diodo zener**, nunca podra **proveer mas potencia que la que el diodo puede disipar**


![](https://i.imgur.com/0xgLqpQ.png)

### El filtro


La fuente sin el filtro tendria una onda de salida asi

[Ejemplo](https://tinyurl.com/y7lv255h)
![](https://i.imgur.com/U8EIh2W.png)
Añadiendo un capacitor que pueda **cargarse cuando la onda sube** y **descargarse cuando la onda baja** permite mantener un voltaje mas constante

Como el **capacitor se puede cargar casi instantáneamente** eso significa que puede absorber mucha corriente junta. Para que no pase tanta corriente tan de golpe colocamos una resistencia que limite la corriente.


![](https://i.imgur.com/9aEcqeV.png)

![](https://i.imgur.com/kYkS0KB.png)
**Notamos** como la resistencia limita la cantidad de corriente
[Ejemplo](https://tinyurl.com/ybhp4hqk).
Por ley de ohm, **si no hay un resistor, el capacitor se cargara muy rapido, es decir corriente altisima  por un momento.**
Ademas, la primera vez que lo carguemos, sera **casi infinita** (varios miles de amperios)
![](https://i.imgur.com/3gCkVdW.png)
Si colocamos un resistor, el capacitor tardara un poco mas en cargar, osea que la corriente sera menor.
>Recordamos que la carga de un capacitor esta definida por 
>* $\large{I_{cap}(t)=Ie^{\frac{-t}{\tau}}}$ general decay function
>* $\large{V_{cap}(t)=V_f+(V_i-V_f)e^{\frac{-t}{\tau}}}$ exponential growth function
>* Donde $\tau=R.C$ 
>Osea que si $R\to 0$ entonces $I\to \infty$ y $V \to V_f$

![](https://i.imgur.com/oU0Re4h.png)

### El estabilizador

Se mantiene la **tension constante en la salida** de la fuente independientemente de si la **tension de entrada sube**



Para eso usamos
* un **Diodo zener** que tenga su $V_z$ igual al voltaje que deseamos en la fuente
* un **resistor limitador de corriente** para que el zener nunca sobrepase su maxima corriente

![](https://i.imgur.com/2lYSQ7d.png)


**La estabilizacion funciona asi**
* El zener **deja pasar la tension en exceso** (la que es mayor que $V_z$), disipandola
* La tension que no deja pasar ($V_z$) es la **tension estabilizada**
* Si **no hay nada conectado a la fuente**, la resistencia limitadora se encarga de que la corriente **no exceda la corriente maxima del zener**

[ejemplo](https://tinyurl.com/y958utw7)

### Calculos

A continuacion estan los  calculos que nos permitiran **elegir los componentes** par auna fuente de
* $15V$
* $100ma$
* Estabiliza de $16V$ a $20V$


#### Transformador

Necesitamos un transformador que entregue un **pico** de $15V$
Un transformador de $12V$ **eficaces** tiene un pico de

$$12v * \sqrt{2} = 17v$$

Si pensamos que los **diodos rectificadores** tienen una caida de $0.7v$ cada uno, entonces si pasa por los dos, el pico es de
$$17-2(0.7)=15.6v$$







#### Filtro - capacitor

Pongamos como punto de partida que queremos que **el capacitor en su peor momento llegue a los** $14.4v$
![](https://i.imgur.com/0hI8K4H.png)
se que la impedancia de un capacitor es

$$\Omega = \frac{1}{2\pi f c}$$

y la ley de ohm es
$$\frac{V}{R}=I$$

despejando y reemplazando
$$V= \frac{I}{2\pi f c}$$

Si deseo que la diferencia de voltaje sea de $15.6V-14.4V$ es decir $1.2V$, reemplazo y despejo la **capacitancia** sabiendo que 
* la **frecuencia** es el doble que la de la red (por el rectificador)
* la **corriente** es la **maxima para la que diseño** la fuente
* el **voltaje** es la diferencia de voltaje que requiero


$$1.2= \frac{0.1A}{2\pi 120 c}$$

>**CRITICO:** Puedo usar un capacitor mas grande y la brecha sera menor
>Es decir, **cuanto mas capacitancia, mejor**

#### Filtro - resistencia

Sin una resistencia, el capacitor nos genera algunos problemas

![](https://i.imgur.com/pRQvdzy.png)

* **CARGA INICIAL:** el capacitor, al no tener una resistencia que limite la corriente,  se cargara por **primera vez** con un **pico gigantesco de corriente casi instantaneo** de **MILES DE AMPERIOS**.  [ejemplo](https://tinyurl.com/yd5t4s54)
 ![](https://i.imgur.com/3gCkVdW.png)
* **EN REGIMEN PERMANENTE:** se cargara muy rapido, generando picos de varios amperios.




Para evitar esto, elegirmos una **resistencia pequeña** en funcion a un **pico maximo de carga deseado** usando la **ley de ohm** y asumiendo que el capacitor esta descargado.

$$R_s=\frac{V_{transfo}-2V_{caidaDiodo}-V_{capacitor}}{I_{deseada}}$$
$$R_s=\frac{15.6-2(0.7)-0}{5}$$
$$R_s=3$$


#### Rectificador

[fuente min 26](https://www.youtube.com/watch?v=eATKEOlqjkw&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo&index=68)
Tenemos que colocar diodos que soporten las corrientes para las especificaciones de la fuente.

Como solo una pareja de diodos esta activa a la vez, cada pareja llevara la mitad de la corriente promedio del diseño.

$I_{prom}=\frac{I_{diseño}}{2}p_{eriodo}$

$I_{prom}=\frac{100ma}{2}20ms$
$I_{prom}=\frac{100ma}{2}20ms$
$I_{prom}=1000ma=1A/s$

Pero la corriente no fluye continuamente, lo hace en forma de **picos** debido a **al tiempo de carga del capacitor** $T_{carga}$

Despejando el **tiempo de carga del capacitor** de su ecuacion, puedo saber en cuanto tiempo esa energia promedio de $1A/s$ de carga cantidad de carga se metera en el capacitor.

Consideramos el **pico como un triangulo**, su area **sera** igual a la **corriente promedio**

$1A/S=\frac{I_{pico}.T_{carga}}{2}$

Despejando $I_{pico}$ obtengo que el pico es de $0.77A$

Los diodos deben soportar mínimamente
* **Corriente promedio** de $50ma$
	* Por valor de diseño de la fuente
* **Corriente de pico repetitiva** $0.77A$
	* por el capacitor elegido y su tiempo de carga
* **Corriente de pico maxima** de $5A$
	* Por la resistnecia elegida en el filtro para el pico inicial


#### Estabilizador

![](https://i.imgur.com/dqPrJdb.png)

Comenzamos eligiendo un **diodo zener** con
*  un $V_z=15V$ para estabilizar la tension deseada.
* Con $I_{max}>100ma$, ya que diseñamos la fuente para hasta $100ma$ y **cuando la carga este desconectada el zener absorbera esa potencia**

**Resistencia minima:**
*La que garantice que con $20V$ no se exceda la corriente maxima del zener, por ejemplo  $0.1A$, siendo $V_z=15$

$$R=\frac{V_i-V_z}{I_z}$$
$$R=\frac{20V-15V}{0.1A}$$

$$R=50\Omega$$


## Con capacitive dropper

[fuente](https://www.youtube.com/watch?v=-n22cqZkxNQ)
Es la misma fuente, pero al tener que alimentarse de $220V$ para dispensar $5V$ es necesario bajar un monton el voltaje.

Para eso podemos usar un **Capacitive dropper** es decir **usar la impedancia de un capacitor como resistencia**. De esta forma **es como usar una resistencia para bajar el voltaje, pero no lo perdemos en forma de calor, ya que los capacitores no disipan potencia**

Notamos que:
* **PELIGRO:** El capacitive dropper puede tener $5V$ entre sus terminales pero $215V$ entre una terminal y tierra (dependiendo de la polaridad con la que lo conectes a $220v$)
* Con el capacitor bajamos la tension a algo cercano a la tension de salida, entonces **el zener tiene que disipar poquita potencia**
* **BARATA:** no necesita transfo, es mas barata!
[Ejemplo](https://tinyurl.com/y86k2r4l)

![](https://i.imgur.com/7y5VSPw.png)
## Con transformador

Identica a las anteriores, pero baja la tension con un transformador.
* **Mas caro:** los transfos salen dineros
* **Mas seguro:** te queda una tension siempre con respecto a tierra (no como en el capacitive dropper que marca $5V$ pero puede matarte igual)
[Ejemplo](https://tinyurl.com/ybv49rv7)
![](https://i.imgur.com/N9o6kBE.png)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1MzA5NzYxMiwxNDEyMjk3MjUsMTk3Mz
M2OTMwMCwzNDc0NzAzMTUsMTQ0MzE3MjU4NywtMTE4NDM5MjAy
LC0zMzM3MzEwNDQsMTExOTc1NjAxOSwtMTU3ODQzNzQ1MSwtMT
c3MjE5MTk1MywtMzEyODI2NTQwLC0xMTI0MTUzOTQsLTE1MzUy
ODk3NTEsLTE5MjU4MzMyNSwtMTYwMDM4MzE1Myw3Mzg3ODkzOD
MsLTY2OTE0MzI3NywtMTY1MDU1MDkzMCwtNTI1NjM1ODQ0LDIw
MzE2NDc3NTVdfQ==
-->