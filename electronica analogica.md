**Nivel técnico electrónico**
https://www.youtube.com/watch?v=KkoudrHOpGE&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo

Quede en clase 6
**VER BIEN FUENTES REALES Y CAIDA DE TENSION!**
https://www.youtube.com/watch?v=JSnm1vGaWBE

**VER aplicacion en reparacion de notebooks**
https://www.youtube.com/watch?v=1XGun_-06aA&list=PLHk1hZEmw3_zlUPRfVeBHLSUviVNfR4pN


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
Cuando estamos en el punto de diseño de la fuente, por ejemplo $12V$, esta nos va a entregar una corriente maxima $I_{max}=6A$

Vemos por ley de ohm
$\frac{V}{R_g}=I$

$\frac{12v}{R_g}=6A$
osea que la resistencia interna es $R_g=\frac{12}{6}=2\Omega$
Imaginemos ahora que nosotros le exigimos mas corriente
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDM4MzE4NTEwLDE3NjgyMjY4NjcsNDA4Nj
I4NTk1LC00NjI4NTM2MzksODAyMzU1MTUsMjA4NzQ2NDkzMiw2
NDA5NTcwODcsMTk3ODg4NDM2OCw1MzY1MTkxODYsLTY2MzYzMT
M5OCwtMjMwMTIzNDE0LDIwNjM0MDc4ODQsLTEzOTIxMDEzNzcs
LTEzMTk3NjAwNzEsLTg3MDA5NTQxNSwxMjU5MTcyMDIyLDgxMT
I4Mjg5MywxODg2NTMyODc4XX0=
-->