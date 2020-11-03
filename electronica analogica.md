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

### Potenciometro

Es una resistencia variable
<!--stackedit_data:
eyJoaXN0b3J5IjpbODExMjgyODkzLDE4ODY1MzI4NzhdfQ==
-->