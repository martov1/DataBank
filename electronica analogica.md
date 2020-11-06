**Nivel técnico electrónico**
https://www.youtube.com/watch?v=KkoudrHOpGE&list=PLb_ph_WdlLDny2cGloFSxyRgO8B733jeo

Quede en video 3 minuto 7

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
### Valores en resistencias SMD
 

### Capacidad de potencia y tamaño fisico
Los resistores cambian su tamaño dependiendo de la potencia que pueden disipar en forma de calor sin quemarse
![](https://i.imgur.com/qIhVTSV.png)

### Potenciometro

Es una resistencia variable
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI3MjA1MjA0NiwtMTMxOTc2MDA3MSwtOD
cwMDk1NDE1LDEyNTkxNzIwMjIsODExMjgyODkzLDE4ODY1MzI4
NzhdfQ==
-->