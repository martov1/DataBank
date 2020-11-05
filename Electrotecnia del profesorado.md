



**VER:**
* Densidad de la corriente de un conductor pag 31,32
* Alta tension en transporte de energia pag 33
* **NODOS**: https://www.youtube.com/watch?v=tRWDr-yGy50


# Contenido

* Conceptos basicos de electricidad
	* Coulombs y Amps
	* Voltage
	* Resistencia
	* Ley de Ohm 
	* Conductividad y resistividad
		* En general
		* En caliente 
		* Rigidez dielectrica
	* Watt y potencia
		* Energia electrica consumida
		* Potencia y energia consumida de una resistencia 
	* Efecto termico Joule (Joule a caloria)
	* Calor especifico (caloria a temperatura)
	* Corto Circuto
* Instalaciones electricas
	* Calentamiento de cables **WIP pag 29,30,31** 
	* Caida de tension causada por cableado **WIP pag 32,33**
	* Seleccion de cable considerando calentamiento y caida de tension **WIP pag 33**
	* Llaves termicas **WIP pag 41,42**
	* Consumo de dispositivos segun su resistencia
* Circuitos 
	* Ley de tensiones de kirchoff
	* Ley de corrientes de kirchoff
	* En serie 
		* Deduccion del calculo de caidas de tension (KVL,KTS)
		* Deduccion del calculo de la resistencia total
		* Deduccion del calculo de la potencia y energia total
	* En paralelo **WIP pagina 49** 
		* Deduccion de las corrientes **wip**
		*  Deduccion de la resistencia equivalente **wip**

---




## Coulombs y Amps

* El **Coulomb** es una **medida de carga** definida co2mo **la carga generada por** **$6.242\text{x}10^{18}$ Electrones**.


* El **Ampere** es **el movimiento de carga a lo largo del tiempo**. Mas propiamente dicho
	* El movimiento de columbs por segundo, si la**corriente es constante a lo largo del tiempo** 
$\LARGE{A=\frac{C}{s}}$
	* La derivada de la carga con respecto al tiempo, si la **corriente es variable a lo largo del tiempo**
	$\LARGE{A(t) = \frac{C}{T}}dt$

---

## Voltage

Los electrones **no se mueven solos**, sino que **es necesario proporcionar energia que empuje a los electrones lo largo del circuito, generando como concecuencia una corriente.**

A la cantidad de **energia suministrada(Joule $J$)** por **cada unidad de carga(Columb$C$)** le decimos **voltaje ($V$)**

$\LARGE{V = \frac{J}{C}}$

Esta es la energia suministrada para **bombear los electrones a lo largo del circuito, generando una corriente determinada.**

>**El _bombeo_ de electrones se produce generando y sosteniendo una diferencia de carga $C$ entre dos puntos que estan conectados por un conductor**, para mantener esta diferencia de carga a lo largo del tiempo es necesario realizar un **trabajo ($J$)** (hacer girar un iman, hacer una reaccion quimica, etc)
>
>Mientras se sostenga la diferencia de carga, los electrones querran ir del lugar con mas carga al lugar de menos carga, siendo _bombeados_
>
>A la fuerza necesaria para **mantener la diferencia de carga a lo largo del tiemp** le llamamos **Fuerza electro-motriz**

**EJEMPLOS:**
* Un generador produce **voltaje proporcionalmente a su velocidad a la que hace girar un iman, empujando electrones** 
* Una bateria produce voltaje mediante la **diferencia de electronegatividad de dos substancias** que hace que los electrones **se junten en un lugar y se alejen de otro** generando **dos polos con cargas diferentes**

---

## Resistencia

La resistencia **dificulta el paso de los electrones**. Para atravezar una resistencia es necesario **gastar energia**, lo cual implica que despues de atravezarla se reduce el voltaje (**caida de voltaje**).

**La resistencia entonces consume energia** ($J$), esta se disipa generalmente en **forma de calor, movimiento, luz, etc**. Al consumir energia para atravezar el obstaculo queda menos energia disponible para desplazar los electrones, por lo que la corriente disminuye.

---

## Ley de Ohm


La ley de Ohm indica que **El voltaje y la resistencia determinaran el flujo de electrones.**
Es decir, **La corriente es CONCECUENCIA de un voltaje y  resistencia**

$\Huge{\frac{V}{\Omega} = A}$

---

## Conductividad y resistividad


### En general
La **Conductividad** es la propiedad de un material de permitir el paso de electrones.
Un material conductor es aquel con **baja resistencia.**

**La resistencia representada por un material depende de:**
* La **resistividad del  material** ($p$)
* La **distancia** que deben atravezar los electrones($L$) 
* El espacio que tienen los electrones para fluir indicado por el **diametro** del material ($A$)


Siendo su relacion la siguiente:
$\LARGE{\Omega = \rho \frac{  L}{A}}$

### En caliente

En general los materiales metalicos aumentan su resistencia al aumentar su temperatura
Esta propiedad puede ser problematica o puede ser usada con fines practicos (termometros electronicos por ejemplo)

$R_c = R_f(1+\alpha \Delta t)$

Donde
* .$R_c$ Resistencia en caliente
* .$R_f$ Resistencia a cero grados
* .$\alpha$ Coeficiente de temperatura de ese material
* . $\Delta t$ Elevacion de temperatura.

---

### Rigidez dielectrica

Aun en materiales con **muy alta resistividad** que normalmente se los llama aislantes, existe un punto en el cual**una cantidad muy alta de energia lo torna conductor**, es decir que **despues de determinado voltaje el material cambia sus propiedades y se torna conductor**

---

## Watt y potencia

Sabemos que la **potencia($P$)** es la **rapidez($S$) con la que se realiza un trabajo($J$).**



$\LARGE{P= \frac{J}{T}}$


>**INTUICION**:
> Tiene sentido que la **energia de cada carga** multiplicado por la cantidad de **cargas por segundo** de la **rapidez con la que se entrega energia/realiza un trabajo**

Sabiendo la definicion de potencia y las definiciones de Volt y Ampere, podemos relacionarlos y deducir que estan vinculados matematicamente, mas allá de que intuitivamente vemos el vinculo.

**Sabemos que:**
El volt es la **energia entregada a cada carga**
$\large{V = \frac{J}{C}}$
El Ampere es la cantidad de **cargas por segundo**
$\large{A=\frac{C}{S}}$

**Entonces:**

Si hicieramos
$V*A = \frac{J}{C}* \frac{C}{S}$
simplificamos:
$V*A = \frac{J}{\not{C}}* \frac{\not{C}}{S}$
nos queda:
$V*A = \frac{J}{S}=P$
Reacomodamos:
$\LARGE{\boxed{P = V*A}}$

---

### Energia consumida

**Sabiendo que:**

El volt es la **energia entregada a cada carga**
$\large{V = \frac{J}{C}}$
El Ampere es la cantidad de **cargas por segundo**
$\large{A=\frac{C}{S}}$

>**Podemos calcular la cantidad de energia total utilizada por unidad de tiempo**
>
$\text{Energia por carga}*\text{cargas por segundo}= \text{energia por segundo}$
>
$\text{energia por segundo}* \text{Tiempo } T = \text{energia consumida en T}$

En terminos matematicos

$\large{\frac{J}{C} * \frac{C}{T} = \frac{J}{S}}$

$\frac{J}{S} * T = \text{Jouls totales}$

**Notese que esto es matematicamente equivalente a las siguientes expresiones:**

$P*T = \text{Jouls totales}$


$V*A*T=\text{Jouls totales}$


 $RI^2*T=\text{Jouls totales}$

### Potencia y energia consumida de una resistencia

De la misma forma, si tenemos la caida de tension de una resistencia $R$ y queremos calcular cuanto consume$P$, sabemos por ley de ohm que el **voltaje y la resistencia determinaran el amperaje**, que es lo que necesitamos para calcular el consumo. Con lo cual resolver el **consumo de la resistencia es trivial.**

$V*A=P$ y$A=V/R$

Entonces el consumo de la resistencia $R$ a un voltaje$V$ esta dado por

$V*(V/R)=P \Rightarrow V^2/R=P$

$\boxed{\large{V^2/R=P}}$

La conclusion es que **a MENOR RESISTENCIA, mayor amperaje y por ende MAYOR CONSUMO**

Ya sabiendo la potencia consumida, es trivial cacular el consumo usando los metodos ya vistos.

$J = P*T$

---

## Efecto termico Joule

El efecto Joule es el que describe la transformacion de la energia electrica a energia termica al atravezar una resistencia.

Cada **Joule de energia se tranforma en 0.24 calorias**

$\boxed{J = 0.24C}$

**De esta manera, si queremos calcular las calorias que genera una resistencia $R$ durante un tiempo $t$ cuando es atravezada por una corriente y volataje$A,V$:**

* Calculamos la energia consumida **como se vio en el apartado _Energia consumida_**, tomando la caida de tension de la resistencia como $V$ :

 $$J=V*A*T \\
 \text{ ó equivalentemente } \\
 J=P*T \\
 \text{ó equivalentemente}\\
 J=RI^2*T
$$
* Sabiendo que **cada Joule es 0.24 Calorias**, sabemos la cantidad de calorias disipadas por la resistencia durante el tiempo $T$

 $\large{\frac{J}{0.24}=C}$
 
 
 ---
 
 ## Calor especifico
 
 El calor especifico es **la cantidad de calorias necesarias para elevar $1Cº$ a$1gr$ de un material especifico**.
 
 Por ejemplo:
 * **Agua** $Ca=1$ - hace falta **una caloria** para aumentar en $1C$ a$1gr$ de agua
 * **Cobre** $Ca=0,093$- hace falta **0.093 calorias** para aumentar en $1C$ a$1gr$ de agua

**Otros materiales:**

| Material | Calor especifico |
|----------|------------------|
| Agua     | 1                |
| Cobre    | 0.093            |
|  Acero   |  0.110           |
| PVC      | 0.210            |
| Aluminio | 0.220            |


De esta forma, podemos calcular la cantidad de **calorias** $Q$ necesarias para aumentar la **temperatura** $\Delta T$ de un material de cierta **masa** $M$ y cierto **calor especifico**$c$. 
**Sin tener en cuenta la disipacion de temperatura a lo largo del tiempo.**


$\LARGE{\boxed{Q=m*c*\Delta T }}$

---

## Corto circuito

Se da cuando la unica resistencia que encuentra el voltaje es la de los conductores (cables), generando **corrientes muy grandes** ya que **no hay resistencia que la limite**. 

$\frac{220v}{0.5\Omega}=440A$

Estas grandes corrientes **mediante efecto joule** pueden derretir los conductores y aislantes muy rapidamente.

---

# Instalaciones electricas

## Consumo de dispositivos segun su resistencia

Los dispositivos accionan usando la energia electrica para generar diversos efectos que resulten utiles, como concecuencia de la natrualeza del efecto que se desea generar estos tienen una **Resistencia**.

**Cuanto menor sea la resistencia necesaria para generar ese efecto, mayor consumo tendra el aparato, ya que poca resistencia permite el paso de muchos electrones**

Algunos dispositivos funcionan con muy alta resistencia, permitiendo pasar muy pocos amperios (LED) mientras que otros tienen en comparacion una resistencia mas baja, (caloventores, motores)


---
# Circuitos



## Ley de tensiones de kirchoff


La ley de tensiones de kirchoff es a grandes razgos una aplicacion el principio e conservacion de la energia. 



>**Recordemos que:**
>* .$V$olt es $\frac{energia}{unidad \quad de >\quad carga}$ o tambien $\frac{j}c$
>* El voltaje es resultado de una **diferencia de potencial**
	* El voltaje a lo largo de un cable ideal es **siempre el mismo**


_La energia no se crea ni se destruye, solo se transforma_
Poniendo el **principio de conservacion de la energia** en numeros, podemos ver que:
$\text{Energia aportada en cada carga}= \text{energia consumida en cada carga para hacer trabajo/s}$

**Matematicamente, podemos verlo asi:**
$V_t = V_{consumo1} + V_{consumo2} + V_{consumo3}...$

* Sabemos que el voltaje es **igual a lo largo de los cables ideales**
	* Entonces un  nodo tiene la misma cantidad de energia por carga en todos los cables que salen de el

**CONCLUSION:**

En cualquier **camino cerrado** (aunque tenga nodos) podemos determinar que**la suma de la energia por unidad de carga consumida($V$)** en ese camino es**igual a la energia por unidad de carga aportada a ese camino($V$)**.

>Si hay nodos, eso implica que algunos electrones se van por otros caminos, pero todos los electrones que salen del nodo salen con la **misma cantidad de energia**, incluidos aquellos que van por el camino que elegiste.
>Ademas, aquellos electrones que **terminan de viajar por el camino cerrado** necesariamente van a tener que tener **la misma cantidad de energia porunidad de carga que tenian al comenzar el camino**

La **energia por segundo** o **energia total** consumida debera tener en cuenta la c**antidad de cargas ($A$)**, es decir las diferentes corrientes que atraviesan ese camino cerrado. pero eso escapa de esta ley.

## Ley de corrientes de kirchoff

Esta basada en el **principio de conservacion de la materia**

_Los electrones no se crean ni se destruyen_

Cuando los electrones tienen **varios caminos para seguir**, el amperaje total$A$ tiene que ser igual a la suma de los amperajes$A_1,A_2,A_3$ que pasan por cada resistencia para que se cumpla la **conservacion de la materia**

**CONCLUSION:**
Para todo nodo, las corrientes entrantes son iguales a las salientes.
$A_{ab} = A_1+A_2+A_3$

## En serie

>Recordatorio 
Una **resistencia consume energia** $J/s$ **generando un trabajo** (calor movimiento, luz etc)

Los circuitos en serie son aquellos circuitos donde las resistencias estan una despues de otra.


**Sabemos que:**
* **PRINCIPIO DE CONSERVACION DE LA ENERGIA:** _La energia no se crea ni se destruye, solo se transforma, en este caso en trabajo (calor, luz, movimiento)_
	*  La **energia/seg ($\frac{j}{s}=P$) aportada** tiene que ser igual a la **suma de los consumos/seg**


* **PRINCIPIO DE CONSERVACION DE LA MATERIA:** _los electrones no se crean ni se destruyen_
	* El **amperaje** $A$ es**igual a lo largo de todo el circuito**  ya que en un circuito en serie hay un solo conductor. 

**Entonces el unico lugar de donde puede salir la energia aportada es del Voltaje**, Es decir: **mismo flujo de electrones $A$ llevara una energia menor$V$ despues de pasar por cada resistencia, donde se realiza un trabajo, a esa reduccion de energia le decimos "caida de tenson"**

Recordamos que Volt es energia por cada carga $V=\frac{J}{C}$

![](https://i.imgur.com/LoPnVzC.png)

Se puede apreciar las caidas de tension $V_{AB}, V_{BC}, V_{CD}$ sobre la tension total$V$.


---
### Deduccion del calculo de caidas de tension


* **PRINCIPIO DE CONSERVACION DE LA ENERGIA:**
$\text{Energia aportada/s}= \text{suma de energia consumida para hacer trabajo/s}$
$V_t*A_t = (A_1*V_{1})+(A_2*V_{2})+(A_3*V_{3})...$


* **PRINCIPIO DE CONSERVACION DE LA MATERIA:**
Sabiendo que el amperaje es siempre el mismo, hacemos factor comun
$V_t*A = A*(V_{1}+ V_{2}+ V_{3})$

Simplificando nos damos cuenta que **el vontaje total es la suma de las caidas de tension**

$\LARGE(1)\boxed{V_t = (V_{1}+ V_{2}+ V_{3})}$

**Esto puede usarse para calcular cada una de las caidas de tension**
Conocemos el valor de cada resistencia y del amperaje total del circuito, por lo que podemos predecir cual sera la caida de tension de esta resistencia.

$(2) \quad {\large  \frac{V_1}{R_1}= A \quad \quad \Rightarrow V_1 =A*R_1}$

$(3) \quad {\large \frac{V_2}{R_2}= A \quad \quad \Rightarrow V_1 = A*R_2}$

$(4) \quad {\large \frac{V_3}{R_3}= A \quad \quad \Rightarrow V_1 = A*R_3}$

---
### Deduccion del calculo de la resistencia total 
**Reemplazando en $(1)$ usando$(2),(3),(4)$ notamos que podemos tratar a las resistencias como una sola sumandolas:**
Reemplazamos $V_1,V_2,V_3$

$\large{(A*R_1) + (A*R_2) + (A*R_3)=V_T}$

Factor comun
$\large{A(R_1 +R_2 + R_3)=V_T}$

Nos queda:
$\boxed{\huge{ \frac{V_T}{R_1 +R_2 + R_3}=A}}$

---
### Deduccion del calculo de la potencia y energia total

Habiendo visto todo esto, **es trivial deducir que la potencia total sera la suma de las potencias.**

Sabemos que la **potencia es la caida de tension total por el amperaje**

$P_T=V_t*A$

El **amperaje es constante** en todo el circuito, y la **caida de tension total es la suma de las caidas de tensiones**
$P_T = (V_1+V_2+V_3)*A$


$P_T= (V_1*A)+(V_2*A)+(V_3*A)$

Notamos ahora, que **cada caida de tension multiplicada por el voltaje es la potencia de cada resistencia (ya que esa es la definicion de potencia), y que sumados dan la potencia total**
$\LARGE \boxed{P_T= P_1+P_2+P_3}$


A su vez sabemos que la **potencia total** por **el tiempo** determinara la energia consumida (esto ya lo sabemos hace rato)

$\boxed{\large{P_T * T = J}}$

---

## En paralelo



Es un circuito donde la terminales de las resistencias estan conectadas entre si.

**Sabemos que:**

* **PRINCIPIO DE CONSERVACION DE LA ENERGIA:**
	*   La **energia/seg ($\frac{j}{s}=P$) aportada** tiene que ser igual a la **suma de los consumos/seg**
	* **Entonces:** $\text{Energia aportada/s}= \text{suma de energia consumida para hacer trabajo/s}$
$V_t*A_t = (A_1*V_{1})+(A_2*V_{2})+(A_3*V_{3})...$


* **PRINCIPIO DE CONSERVACION DE LA MATERIA:**
Los electrones tienen **varios caminos para seguir**, el amperaje total$A$ tiene que ser igual a la suma de los amperajes$A_1,A_2,A_3$ que pasan por cada resistencia para que se cumpla la **conservacion de la materia**
$A_{ab} = A_1+A_2+A_3$

* **DEFINICION DE VOLT:**
El volt es **energia/unidad de carga $\frac{j}{A}$**. en el caso de un circuito paralelo, todas las cargas vienen de un mismo cable y llevan la misma energia,luego los electrones se dividen por varios caminos, pero todos llevan la misma cantidad de energia por unidad de carga.

![](https://i.imgur.com/ZDqUoS8.png)


### Deduccion de las corrientes

* Tengo la **energia/unidad de carga** entre los puntos $V_{ab}$

La **energia por unidad de carga** impulsa los electrones a travez de las resistencias, generando **una corriente proporcional a cada resistencia**.
$V_{ab}/R_1=A_{1}$
$V_{ab}/R_2=A_{2}$
$V_{ab}/R_3=A_{3}$

### Deduccion de la resistencia equivalente

* Se por ley de conservacion de la materia que:
$A_{ab} = A_1+A_2+A_3$


**Entonces:**

* Puedo reemplazar cada corriente por su equivalente en voltaje sobre resistencia
$A_{ab}=V_{ab}/R_1 + V_{ab}/R_2 + V_{ab}/R_3$
* Puedo reemplazar la corriente total por el voltaje sobre una resistencia imaginaria que funcionaria como resistencia total
$V_{ab}/R_{ab}=V_{ab}/R_1 + V_{ab}/R_2 + V_{ab}/R_3$
* Despejo la resistencia total.



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM5ODAwMTc4MF19
-->