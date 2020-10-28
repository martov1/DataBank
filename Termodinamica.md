[fuente](https://www.youtube.com/watch?v=TwKQ3MDrLlM&list=PLkiO5Q9dOKIJtJSu7f8f7dfSIPSPM4aVU&index=6) 
Quede en el video 14

[Fuente mejor](https://www.youtube.com/watch?v=MGA2uGck3iQ&list=PLX2gX-ftPVXXMDW2aoPCk7nM-58n7nW5M&index=112)

entropia segun otro profesor
https://www.youtube.com/watch?v=OmNG8woYHTY&list=PLr1GRpwvVUHQPCf9nVhmS-whdsS7OWPxs&index=21




---


Para Máquinas térmicas, resolver problemas de 
* ciclos de vapor mediante el uso de diagrama
para la parte teórica tener presente
*  Ciclo diessel
*  Otto
*  Rankine
*  Turbina de gas
*  definiciones de Primer y segundo principio, evoluciones con gases ideales. 

---

**CRITICO:** CORREGIR energia interna $u$ vs energia $E$, por que $u$ incluye $p.v$ y la enrgia que entregas con calor cuando entregas calor pero la temperatura no sube (en temp de saturacion)
![](https://i.imgur.com/sfLPDsD.png)
Simplificar con esto
https://www.youtube.com/watch?v=fSEFfWf2au0&list=PLH2l6uzC4UEVUmJdTMStYXad_sI73_T0x&index=10

# Sistemas
## Definiciones

* **Energia:** capacidad para realizar cambios o realizar un trabajo
* **Sistema termodinamico:** una parte del universo que se aisla para su estudio
	* Los sistemas termodinamicos tienen **fronteras** que los definen en el espacio
	* **Tipos de sistemas**
		* **Abierto/Volumen de control:**  Con una cantidad de materia no definida (ej un volumen en el espacio) que puede cambiar, osea que puede cruzar la **frontera**.
		* **Cerrado/Masa de control:** Con una cantidad de materia definida que **no cambia**, osea no cruza la **frontera**
			* **Aislado:** Con una cantidad de energia definida que no cambia 
 
 ![](https://i.imgur.com/1JCi5fx.png =350x)
 _Ejemplos de sistema cerrado y abierto_

## Propiedades de sistemas

### Propiedades intensivas/extensivas

Las **propiedades** de un **sistema termodinamico** son sus caracteristicas, por ejemplo

* **Propiedades intensivas** (indep. de la masa)
	* Presión
	* Temperatura
	* Densidad 
* **Propiedades Extensivas** (dependen de la masa)
	* Volumen
	* Energia interna 
		*  Chem. bonds
		*  Temperatura
		*  Trabajo mecanico
		* Agitacion de las moleculas que no resulta en temperatura
	* Masa
* **Propiedades especificas** (intensivas pero independizadas de la cantidad de masa)
	* Volumen especifico ($v=\frac{volumen}{masa}$)
	* energia interna especifica ($u=\frac{energ. interna}{masa}$)

### Presion

#### Unidades y calculo
La presion es la fuerza **normal** por unidad de area que ejerce un fluido sobre una superficie y se mide en **Pascal**

$$Pascal=\frac{Fuerza}{Area}=\frac{Newton}{M^2}$$

La presion para una columna de liquido a una cierta profundiad esta dada por
$$P=dgh$$
donde 
* $d$ es densidad
* $h$ es altura/profundiad
* $g$ es gravedad	

La forma del recipiente no altera este calculo

![](https://i.imgur.com/o4m30vV.png)

Otras unidades son

$Bar=100000P$
$atm=101325P \approx 1Bar$
$1Psi=6894.76P$

#### Medicion absoluta, manometrica, de vacio

La manera de medir la presion siempre es con respecto a otra cosa, las 3 comparaciones que siempre  hacemos son

* **Presion absoluta $P_a$:** Presion comparada con el vacio absoluto
	* Marcada como $P_a$ o **Absolute pressure**
* **Presion manometrica $P_g$:** Presion comparada con la presion atmosferica (0=1 atm)
	* $P_{g}=P_{abs}-P_{atm}$
	* Medida con un **Manometro**
* **Presion de vacio:** es la presion comparada con  la presion atmosferica (1 atm), pero los valores positivos estan entre 1 atm y 0atm
	* $P_{vac}=P_{atm}-P_{abs}$
	* Medida con un **Vacuometro**

![](https://i.imgur.com/L5jf3yZ.png)

### Temperatura y calor

Llamamos:

* **Temperatura** - Es una magnitud escalar que determina la cantidad de **energia termica**, osea las vibraciones de los atomos de la materia
	* Medido en **grados celsius**
	* El **Zero absoluto** es la ausencia total de energia termmica
* **Calor** - El **flujo de energia termica** de un lugar a otro
	*	Cuando se alcanza el equilibrio termico (una taza de cafe tiene la misma temperatura que el ambiente), no hay mas flujo de temperatura, osea no hay mas **calor**

![](https://i.imgur.com/PSc8M1S.png =500x)


## Estados y equilibrio de sistemas

**ESTADO:** El conjunto de propiedades de un sistema en un momento determinado en el tiempo se le dice **estado**

**EQUILIBRIO:** Un sistema esta en equilibrio si el estado no cambia por si solo salvo que existan interacciones externas


![](https://i.imgur.com/kv0zL08.png)
### Sistemas compresibles simples
#### Que son
| | |
|-|-|
|CRITICO:exclamation::exclamation: | Aunque parezca super limitado, **La mayoria de los sistemas usados en la termodinamica aplicada son de este tipo**|



Llamamos **Sistemas compresibles simples** a aquellos que carecen de efectos
*	Electricos
*	magneticos
*	Gravitacionales
*	De movimiento
*	De tension superficial

#### Postulado de estado

Para estos Sistemas el **estado se encuentra totalmente definido si CONOZCO:**
* Dos propiedades 
	* extensivas ó especificas 
	*  independientes entre si

## Procesos

#### Definicion
Los procesos son los cambios de un estado de equilibrio a otro, en el caso de los **sistemas compresibles simples** es el cambio de **dos de sus propiedades**

![](https://i.imgur.com/60OSpKp.png =500x)
#### Procesos cuasiestaticos

Son procesos en los que el **cambio es tan lento** que el sistema esta en **equilibrio todo el tiempo**. osea **las propiedades cambian en todo el sistema mas o menos al mismo tiempo de forma uniforme**.

Algunos ejemplos son
*	**Isobarico**: Proceso a presion constante
*	**Isotermico**: Proceso a temperatura constante
*	**Isocorico**: proceso a volumen constante


#### Procesos flujo-estacionario

Es un sistema **abierto** en el que **entra y sale masa** pero **Las propiedades del sistema no cambian**

![](https://i.imgur.com/iISRrlF.png)


# Fases y cambios de fase

## Las fases y sus energias

Las fases de una substancia son su estado de la materia. nos referimos generalmente a 3 fases

* **Solido**
	* Moleculas con baja energia, no vencen las fuerzas intermoleculares
* **Liquido**
	* Moleculas con mediana energia, vencen un poco las fuerzas intermoleculares
* **Gaseoso**
	* Moleculas con mucha energia, vencen casi por completo a las fuerzas intermmoleculares

**CRITICO: :exclamation:** La **fase** depende de la cantidad de energia que tiene esa materia  que **vencera a las fuerzas intermoleculares**.

![](https://i.imgur.com/MvXQN9s.png)

Entonces  para cambiar de fase hace falta que la substancia **Absorba o libere  energia de sus moleculas** para que cambie en relacion con las fuerzas intermoleculares.

![](https://i.imgur.com/9cI9iqH.png)

## Calor latente

El **Calor latente** es **la cantidad de energia absorbida o liberada durante un proceso de cambio de fase** , se dividen en

* **Calor latente de fusion:** Cantidad de energia 
	* Absorbida durante la fusion
	* Liberada durante el congelamiento.
* **Calor latente de evaporacion**: Cantidad de energia
	*  Absorbida durante la evaoperacion 
	* Liberada durante la consensacion

## Temperatura de saturacion

Es la temperatura a la que puede comenzar a producirse un cambio de fase. la **temperatura de saturacion dependera de la presion**

>Generalmente nos importa la temperatura de saturacion para un sistema que **tendra una presion constante a lo largo del cambio de fase** y lo que varia es la temperatura

## Presion de saturacion

Es la Presion a la que puede comenzar a producirse un cambio de fase. la **Presion  de saturacion dependera de la temperatura**

>Generalmente nos importa la Presion  de saturacion para un sistema que **tendra una Temperatura constante a lo largo del cambio de fase** y lo que varia es la presion


## Fases en substancias puras

### Diagrama 3D presion-volumen-temperatura

**CRITICO:** Una fase esta determinada por 3 valores
*  **volumen especifico**
*  **temperatura** 
*  **presion** 

Podemos visualizar toda esa información en un grafico tridimensional que es **especifico para cada substancia pura**.

**Cambiar de fase** es entonces moverse desde una superficie de un color del grafico a otra.

![](https://i.imgur.com/VnSXYHH.png)

### Etapas de cambio a presion constante

Para explicar el proceso de cambio de fase vamos a usar una variacion de temperatura y volumen, dejando la presion constande. Asi tomamos nada mas que una **lonja del grafico 3d**

>**CRITICO:** Estas mismas etapas se pueden explicar con
>*  **Presion constante y variando la temperatura** (como se hace en estos ejemplos)
>*  **Temperatura constante y variando la presion.**
>* Cualquier otra variacion

El proceso de Cambio de fase en substancias puras consta de estas etapas, imaginemos una **Temperatura de saturacion T de 100** para **una presion fija dada**



* **liquido comprimido 100<T**
	*  Liquido a una temperatura menor a la de ebullicion y aumentando
	* Volumen en aumento
* **Liquido saturado T=100**
	* Liquido a la temperatura de ebullicion, absorviendo calor para arrancar con el cambio de estado
	* Volumen en aumento, aun cuando no hay gas
* **Mezcla saturada liquido vapor T=100**
	* Liquido y gas a temperatura de ebullicion, sigue absorbiendo el calor para romper mas fuerzas intermoleculares
	* Volumen en aumento
* **Vapor saturado T=100**
	* gas, todavia no a comenzado a subir su temperatura
	* Voolumen en aumento
* **Vapor sobrecalentado T>100**
	* El vapor comienza a elevar su temperatura
	* Volumen en aumento

![](https://i.imgur.com/q4MNE0E.png =400x)

Vemos como **la temperatura se ameseta** entre la fase 2 y 3, pero **el volumen nunca deja de aumentar**
![](https://i.imgur.com/wDpYvcg.png =400x)

### Cambio de fase a presión constante

Si repetimos esto para **diferentes presiones constantes** vemos que como **cambian las temperaturas de saturación** obtenemos las diferentes **curvas de temperatura-volumen** para cada fase.

![](https://i.imgur.com/kBBW3Fl.png =400x)
_Las curvas de mas arriba corresponden a mayores presiones, en realidad este grafico deberia ser 3d, o son varios graficos en uno_

Vemos que en las curvas de temperatura-volumen con presiones mayores **las etapas de liquido saturado y vapor saturado** se van achicando hasta transformarse en la misma etapa, llamada **punto critico**

>A las **propiedades del punto critico las llamamos**
>* Temperatura critica
>* Presion critica
>* Volumen especifico critico
> **CRITICO: Estos valores ya estan tabulados en tablas y graficos para su uso**

Si dibujamos una linea entre todos los estados de liquido saturado y los estados de vapor saturado, obtenemos el famoso **Diagrama temperatura-volumen especifico** que es **unico para cada substancia pura**

![](https://i.imgur.com/62TCNcr.png):rotating_light:_No es mas que una perspectiva mas acotada del mismo grafico 3d de volumen-presion-temperatura_


**CRITICO:** Este grafico nos permite, sabiendo una temperatura y un volumen, determinar la **fase** de la substancia y la **etapa del cambio de fase**, **independientemente de la temperatura**. 
si quiero saber datos para una **presion especifica** entonces **sigo el camino punteado que corresponda**

### Cambios de fase a temperatura constante

Asi como podemos añadir energia calorica a una substancia para elevar la energia de las molecular y **luchar con las fuerzas intermoleculares** tambien **podemos añadir energia en forma de presion para lograr lo mismo** y generar un cambio de fase

Haciendo lo mismo que con la temperatura, llegamos a un grafico **presion-volumen** donde estan representados los **graficos de cambio de fase para diferentes presiones** y **dibujando una linea entre los estados de liquido saturado y vapor saturado**

![](https://i.imgur.com/fTmQxGD.png =400x)
:rotating_light:_No es mas que una perspectiva diferente del mismo grafico 3d de volumen-presion-temperatura_


### Determinar la fase


**SISTEMA DE PRESION CONSTANTE**
Como la Temperatura de un sistema se mantiene igual a la **Temparatura de saturacion** durante las fases intermpedias, podemos concluir que 

* En un sistema de **temperatura constante**, si
	* $P<P_{sat}$ estas en la fase de vapor sobrecalentado
	* $P=P_{sat}$ estas en alguna de las fases intermedias
	* $P>P_{sat}$ estas en la fase de liquido comprimido* En un 

**SISTEMA DE TEMPERATURA CONSTANTE**
De igual manera  Como la presion de un sistema se mantiene igual a la **presion de saturacion** durante las fases intermpedias, podemos concluir que 

* En un sistema de **presion constante**, si
	* $T>T_{sat}$ estas en la fase de vapor sobrecalentado
	* $T=T_{sat}$ estas en alguna de las fases intermedias
	* $T<T_{sat}$ estas en la fase de liquido comprimido


### Diagramas de tres fases

Son diagramas como los anterores pero extendidos para tener todas las fases de esa substancia.

Se pueden hacer tiendiendo en cuenta **presion constante** o **temperatura constante**

![](https://i.imgur.com/qdJD9jn.png =350x)
:rotating_light:_No es mas que una perspectiva diferente del mismo grafico 3d de volumen-presion-temperatura_



# Entalpia

### En general

Entalpía $E$ la suma de la  energia de un sistema, que se compone de su energia interna $E$ y su presion $P$ por volumen $V$ 

$H=E+PV$

Como es imposible determinar la energia interna de un sistema $E$, generalmente lidiamos con los **cambios de entalpia**

$\Delta H =\Delta E + \Delta PV$


La **energia** puede ser cambiada forma de **trabajo mecanico** $W$ o de **calor** $q$, osea que $\Delta E=w+q$

$\Delta H =w+q + \Delta (PV)$

### En presión constante sin trabajo mecánico

Para **reacciones quimicas** generalmente asumimos algunas cosas.


Si asumimos que la presion fuera constante
$\Delta H =w+q + P \Delta V$

A su vez podemos asumir que el unico trabajo involucrado es el trabajo de expansion del volumen en esa presion fija, osea
 $w=-P\Delta V$

$$\Delta H =-P \Delta V +q + P \Delta V$$


Pero entonces, asumiendo todo eso, notamos que el cambio de energia en el sistema es meramente **el calor**
$$\Delta H =\sout{-P \Delta V} +q + \sout{P \Delta V}$$

$$\Delta H =q $$


# Analisis en cambio de defases 

### Volumen, entalpia y energia en una fase

Durante el cambio de fases, podemos obtener la entalpia, el volumen especifico y la energia interna. para eso:

* Dada una situacion donde esta sucediendo un cambio de fase, existen las dos fases a la vez. obtengo primero los valores para cada fase desde una tabla
	* Fase **liquido saturado**
		* $V_f$ vol. especifico de liq saturado
		* $u_f$ energia interna especifica de liquido saturado
		* $h_f$ entalpia especifica de liquido saturado
	* Fase **vapor saturado**
		* $V_g$ vol especifico gas saturado
		* $u_g$ energia interna especifica de vapor saturado
		* $h_g$ entalpia especifica de vapor saturado

Ejemplo de una tabla
![](https://i.imgur.com/3iySNJf.png)
>Si nuestro valor esta entre dos elementos de la tabla entonces finjimos que hay una relacion lineal entre los elementos para aproximar el valor deseado.

### Titulo o ley de sistema de varias fases

Un sistema que se encuentra dentro de la campana de vapor, es decir es una mezcla de liquido saturado y vapor saturado, tambien llamado **vapor humedo**,  entonces 


* :warning: **DEFINICION:** La **ley de un sistema** es la proporcion de vapor saturado y liquido saturado
	* $ley=\frac{M_{vapor}}{M_{total}}=\frac{M_{vapor}}{M_{vapor}+M_{liquido}}$
		* Notamos que $ley=1$ cuando la fase es vapor saturado
		* Notamos que $ley=0$ cuando la fase es liquido saturado

![](https://i.imgur.com/hhcqmi6.png)

---

### Volumen, entalpia y energia en cambio de fase

Si se evapora una cantidad de liquido y se transforma e gas, entonces el cambio de volumen es: 

$$\Delta V=V_{gas} - V_{ \text{liquido que se evaporo}}$$

y a eso llamamos $\Delta V_{fg}$

$$\fbox{  $\Delta V_{fg}=V_{g}-V_{f}$ }$$

**El mismo razonamiento ocurre con la energia interna $u$ y con la entalpia $h$**

$$\fbox{  $\Delta V_{fg}=V_{g}-V_{f}$ } \\
\fbox{  $\Delta h_{fg}=h_{g}-h_{f}$ }\\
\fbox{  $\Delta u_{fg}=u_{g}-u_{f}$ }$$

:arrow_right:**ENTONCES:**

Puedo calcular el **volumen especifico**, **entalpia especifica** y **energia interna especifica** de una substancia pura que esta en dos fases al mismo tiempo.

>:radioactive:**ATENCION:** Todos los volumenes/entalpias/energias aca siempre son **especificos**, osea divididos por la masa.

obviamente sabemos que por cada kilo de masa con fases mezcladas, el volumen sera:
$V_{total}=V_{\text{liquido}}+V_{gas}$

Notamos que si no tenemos $V_{gas}$ pero tenemos la $ley$ entonces podemos hallar $V_{gas}$

$V_{gas}=(V_{fg})(ley)$
>**NOTA:** Usamos $V_{fg}$ y no $V_g$ para tener en cuenta el volumen de liquido que ya no esta por que se evaporo!

Quedando entonces

$V_{total}=V_{\text{liquido}}+(V_{fg})(ley)$

O en notación normalmente usada

$$\fbox{  $V=V_f+x(V_{fg})$ }$$

:arrow_right:**ENTONCES:**

usamos el mismo razonamiento  para la **entalpia especifica** y la **energia interna especifica**
$$\fbox{  $V=V_f+x(V_{fg})$ }\\
\fbox{  $h=h_f+x(h_{fg})$ }\\
\fbox{  $u=u_f+x(u_{fg})$ }$$

# Calor
###  El calor
Conocemos entonces la relacion entre temperatura, presion, volumen especifico y las fases, pero **cuanto calor es necesario para subir la temperatura de la materia?**

>:warning: **RECORDAMOS:** Calor es el **flujo de energia termica** de un lugar a otro

Lo medimos en $joules$ o $Kj$ (kilojoules) y lo simbolizamos con $Q$

Un sistema que no transfiere calor se lo denomina **ADIABATICO**

###  Transferencia de calor

Podemos indicar la taza de transferencia de calor asi

transferencia de Calor por unidad de masa
$q=\frac{Q}{m}$

transferencia de Calor por unidad de tiempo

$Q=\int^{t_2}_{t_1}Qdt$
 o con tiempo constante $Q=Q\Delta t$

### Calor especifico

Se trata de la cantidad de calor necesaria ara **elevar un grado centigrado** a una **unidad de masa**, depende de cada substancia

Naturalmente sera
$$C_{esp}=\frac{Kj}{kg}$$

El calor especifico **no es fijo** sino que **varia con la presion y el volumen especifico**, podemos simplificarlo asi
* $C_v$ calor especifico a volumen constante
* $C_p$ calor especifico a presion constante

Generalmente 

$$C_p>C_v$$

Es decir hace falta mas energía si la presión es constante que si el volumen es constante.

### Cambio de Energia para cambio de temperatura - WIP

Por la ley de conservacion de la energia sabemos que para todo sistema

$$E_{total}= E_{inicial}+E_{entrante}-E_{saliente}$$
osea
$$\Delta E=E_{entrante}-E_{saliente}$$
De forma diferencial

$$dE= \delta  E_{entrante}-  \delta E_{saliente}$$

Sabiendo que  el cambio de  energia es el calor mas el trabajo$\Delta E=w+q$, si asumimos que no hay trabajo siendo generado $w=0$

$$dE= \delta  q_{entrante}-  \delta q_{saliente}$$

Si asumimos que
*  no estamos en una **temperatura de saturacion**
* Estamos a **volumen constante** 
* Conocemos el calor especifico a presion cte $C_p$

Entonces si hay un cambio de temperatura, la energia para producir ese cambio es **el calor especifico multiplicado por el cambio en la temperatura**
$$C_vdT= \delta  E_{entrante}-  \delta E_{saliente}$$

Osea
$$dE=C_pdT$$
Despejando

$$\fbox{$\frac{dE}{dT}=C_p$}$$

>Es decir: el **calor especifico a volumen constante** es el cambio de energia interna por unidad de temperatura (que tiene sentido)

Bajo un razonamiento que no entiendo, "siguiendo los mismos pasos" me queda que 
$$\fbox{$\frac{d(entalpia)}{dT}=C_v$}$$



# Gases ideales

## Distincion gas-vapor

Hacemos la siguiente distincion

* **gas** substancia por encima de su temperatura critica
* **vapor** substancia por debajo de su temperatura critica

![](https://i.imgur.com/iIwFID1.png)
## Ley de gases ideales


### Ley general 
Los gases ideales son aquellos en los que su comportamiento se aproxima a uno en el que **sus particulas no se atraen ni se repelen**

En ese caso, respetan la siguiente ley

$$\fbox{$Pv=RT$}$$

Donde
* $P$ Presion absoluta
* $v$ volumen especifico
* $R$ constante de ese gas en particular
	* $R=\frac{R_u}{M}$ donde
		* $R_u$ constante unversal de los gases
		* $M$ masa molar del gas en cuestin
* $T$ temperatura absoluta (kelvin)

Para una masa particular de gas, podemos multiplicar por la masa de cada lado, entonces.

$$\fbox{$PV=mRT$}$$

Donde
* $P$ Presion absoluta
* $V$ volumen de la masa de gas
* $m$ masa de gas
* $R$ constante de ese gas en particular
	* $R=\frac{R_u}{M}$ donde
		* $R_u$ constante unversal de los gases
		* $M$ masa molar del gas en cuestin
* $T$ temperatura absoluta (kelvin)

### Valor constante entre estados

Cuando un gas pasa de un estado a otro, siempre respeta el mismo valor, es decir.

![](https://i.imgur.com/ILWT0zv.png)
## Calor especifico en gases ideales


###  Cambio de energia, derivacion
:arrow_right:**1) RECORDAMOS:** que los calores especificos estan definidos como
$$\fbox{$\frac{dE}{dT}=C_p$}$$
$$\fbox{$\frac{d(entalpia)}{dT}=C_v$}$$

:arrow_right:**2) RECORDAMOS:** A su vez, recordamos que el **cambio de  entalpia ó energia interna** de un gas que solo genera trabajo por la expansion de su volumen a presion constante  $w=-P\Delta V$ es

_revisar?¿?¿_
$$\Delta H =q $$

:arrow_right:**ENTONCES:** los calores especificos para gases ideales son solo **funcion de la temperatura**

$$\fbox{$\frac{dU(T)}{dT}=C_p(T)$}$$
$$\fbox{$\frac{dH(T)}{dT}=C_v(T)$}$$
Implicando ademas que si conozco la variacion de temperatura, conozco la variacion de energia interna o entalpia
$$\fbox{$\Delta U(T)=\int^{T_1}_{T_2} C_p(T)$}$$
$$\fbox{$\Delta H(T)=\int^{T_1}_{T_2} C_v(T)$}$$

:warning: **Estas funciones existen como aproximaciones de taylor a las que se llega de forma experimental para cada compuesto**

![](https://i.imgur.com/DukxxBq.png)
###  Cambio de energia, Por tablas

La misma informacion se puede obtener por tablas (Calor especifico a temperatura A, calor especifico a temperatura B) o  hacer interpolacion lineal para los valores intermedios.
Cuando los tenes, calculas la entalpia/energia con ellos

Tambien hay tablas que indican una "entalpia/energia" para cada valor de temperatura, y restando el valor de de entalpia para $T_1$ con el de $T_2$ obtenes el cambio en entalpia $\Delta H$ o de energia interna $\Delta u$

![](https://i.imgur.com/DmJZ471.png)
###  Ley de gases ideales con variacion de temp

:arrow_right:**RECORDAMOS:** los calores especificos para gases ideales son solo **funcion de la temperatura**

$$\fbox{$\frac{dE(T)}{dT}=C_p(T)$}$$
$$\fbox{$\frac{dH(T)}{dT}=C_v(T)$}$$

:arrow_right:**RECORDAMOS:** La entalpia se define como

$$h=u+Pv$$
:arrow_right:**RECORDAMOS:** La ley de gases ideales es

$$\fbox{$Pv=RT$}$$

:arrow_right:**Entonces:**

$$h=u+RT$$

En forma diferencial

$$\frac{dh}{dt}=\frac{du}{dt}+RT$$

entonces, por definicion de $C_p$ y $C_v$ 
$$\fbox{$C_p=C_v+RT$}$$

## Trabajo de gases ideales

:arrow_right:**RECORDAMOS:** Que el trabajo es fuerza por distancia 
$$W=F.D$$

:arrow_right:**RECORDAMOS:** Que la presion es Fuerza por area

$P_\text{resion}=\frac{F_{\text{uerza}}}{A_{\text{rea}}}$
osea que 
$F=P.A$

:arrow_right:**ENTONCES:** Veamos el trabajo de un gas entonces cuando se expande o contrae

![](https://i.imgur.com/onWnFRf.png)

reemplazando $F$ Entonces el trabajo de un gas a presion es

$$W_{\text{ork}}=P_{\text{resion}}.A_{\text{rea}}.D_{\text{istancia}}$$

:arrow_right:**NOTAMOS:** que 
$$Area.Distancia=\text{volumen expandido}$$ entonces
$$W=P.V_\text{olumen expandido}$$

Que en forma diferencial a presion constante  es


$$\fbox{$dW=\int^{v_1}_{v_2}P.dV_\text{olumen expandido}$}$$

Entonces el trabajo es el area debajo de la curva del grafico **presion-volumen**

![](https://i.imgur.com/49NWbs2.png)

# Flujo masico y volumetrico

### Velocidad promedio
Es el flujo de masa por un "tubo"
Debido a la friccion, la masa va a velocidades diferentes dentro de cada parte del tubo.

![](https://i.imgur.com/2V7zqa9.png)

Para simplificar esot usamos una **velocidad promedio**

### Flujo Volumétrico

Es el volumen por unidad de tiempo, normalmente simbolizado como $\dot{\forall}$, que no es mas que la **velocidad promedio del fluido** $V$ multiplicada por la **seccion del tubo** o area transversal $A_t$

$$ \dot{\forall}=\text{Velocidad}.\text{Seccion del tubo}$$
ó
$$ \dot{\forall}=V.A_{t}$$

### Flujo másico

Es el flujo de masa por un "tubo" en un periodo de tiempo determinado. Es facil ver que

$$\fbox{$\text{flujo de masa}= \text{Densidad}.\text{Velocidad}.\text{Seccion de tubo}$}$$

y su unidad sera  $\frac{kg}{s}$



Ya que $seccion$ ($A_t$) por $velocidad$ ($V$) dara el volumen circulando, y eso multiplicado por la $densidad$ ($\rho$) dará el flujo de $masa/seg$ ó  ($\dot{m}$)

$$\fbox{$\dot{m}=\rho VA_t$}$$

A su vez tambien podemos indicarlo usando el **flujo volumentrico** ya que $\dot{\forall}=V.A_{t}$

$$\fbox{$\dot{m}=\rho\dot{\forall}$}$$

Es **obvio** que si entra masa a un sistema ($\dot{m}_{\text{entrante}}$) y a su vez sale masa de un sistema ($\dot{m}_{\text{saliente}}$), entonces la velocidad a la que el sistema gana o pierde masa ($\frac{dm}{dt}$) sera 

$$\dot{m}_{\text{entrante}}-\dot{m}_{\text{saliente}}=\frac{dm}{dt}$$
### Flujo másico - Proceso flujo-estacionario

Si el profeso fuera **flujo-estacionario** entonces entra y sale la misma cantidad de masa
$$\sum \dot{m}_{\text{entrante}}= \sum \dot{m}_{\text{saliente}}$$

osea
$$\frac{dm}{dt}=0$$

### Flujo volumetrico en fluidos Incompresible
Si fluyen liquidos, estos no se comprimen, entonces siempre sucedera que el flujo volumtrico entrante y saliente seran identicos


$$\sum \dot{\forall}_\text{entrante}= \sum \dot{\forall}_\text{entrante}$$
![](https://i.imgur.com/F9I7OwG.png =200x)
# Entropia

#### Definicion
Es una manera de medir la cantidad de energia que no esta disponible para realizar trabajo. 

Para $T$ constente:
$$\Delta s = \frac{\Delta Q_{rev}}{T}$$ 

Para $T$ no constante
$$\Delta s = \int \frac{Q_{rev}}{T}$$

El **cambio de entalpia** es:
* **el calor** aplicado sobre un sistema **reversible** sobre **la temperatura a la que fue aplicado** ese calor 
* Si sucedió varias veces entonces es la **suma de todas**
* Su unidad es $\frac{Joule}{Kelvin}/kg$
* Es una **propiedad extensiva**


#### Ejemplo

Se derrite un cubo de hielo de 1kg, añadiendo calor $Q=334880j$  y manteniendose a temperatura $T=273K$.

$$\Delta s =\frac{Q}{T} = \frac{334880j}{273K}=1277\frac{j}{K}$$ 

#### Definicion como desorden

La entropia mide el desorden molecular, por eso un gas tendra mayor entropia que un liquido
#### Graficos T-S
Hay graficos  temperatura entropia y sus relaciones definen tambien la fase de la substancia

![](https://i.imgur.com/EzDhAko.png =x250)
#### Cambios en la entropia, proc isentropicos

* Para todo proceso **no reversible** se **crea entropia nueva** $S_{gen}$
* Para los procesos adiabaticos y reversibles no se genera entropia y se los llama **procesos isentropicos**

![](https://i.imgur.com/l86GTdW.png =x130)

# Leyes de la termodinámica 

## Primera ley
_La energia no se crea ni se destruye, solo se transforma_

La primera ley, enterminos matematicos, nos va a decir que 

>**CRITICO:**:warning:**La suma de la energia que se transforma, entrante y saliente del sistema siempre sera 0**:warning:

En terminos simples

$$E_{inicial} + E_{entra}-E_{sale}=E_{final}$$
ó en terminos de cambio de energia
$$ E_{entra}-E_{sale}=\Delta E$$

### En sistemas cerrados


Es decir que **en un sistema cerrado** el cambio en energia interna de un sistema es el calor absorbido ($q$ entrante) en ese instante menos el trabajo realizado ($w$ saliente) en ese instante

En un **Sistema cerrado**

$$\Delta U = q - w$$

### En sistemas abiertos
Si el sistema **es abierto** entonces hay que tener en cuenta la **energia de la masa que entra o sale**

$$\Delta U = q - w + E_{\text{masa que entra}}-E_{\text{masa que sale}}$$

alternativamente

$$\Delta U = \Delta q -  \Delta w + \Delta E_m$$

#### Energia de la masa en movimiento
Podemos definir la energia que tiene la masa como

$$E_m= w +U+E_c+E_p$$

Donde 
* $w$ Trabajo que hace el fluido
* $u$ energia interna de la masa
* $E_c$ energia cinetica de la masa
* $E_p$ Energia potencial gravitatoria de la masa

:arrow_right:**Recordamos** que el trabajo que genera un fluido es $w=PV$ entonces
$$E_m= PV+U+E_c+E_p$$

:arrow_right:**Recordamos** que la entalpia es $H=U+PV$, reemplazando

$$E_m= H+E_c+E_p$$

:arrow_right:**Recordamos** que $E_c=\frac{mv^2}{2}$ y $E_p=mgz$, reemplazando 
$$\fbox{$E_m= m(h+\frac{V^2}{2}+gz)$}$$
>(notemos que la entalpia absoluta $H$ pasa a ser entalpia especifica $h$)

:arrow_right:**Podemos** verlo sobre unidad de tiempo
$$\dot{E_m}= \dot{m}(h+\frac{V^2}{2}+gz)$$

#### En sistemas flujo-estacionarios

En un sistema de flujo estacionario entra la misma cantidad de masa que sale. 

$$\sum \dot{m}_{\text{entrante}}= \sum \dot{m}_{\text{saliente}}$$


En estos sistemas las variables $V,m,T$ etc permanecen constantes, como asi tambien la energia en el volumen de control $E_{vc}$.


![](https://i.imgur.com/2KRHAVC.png)
Por la primera ley de la termodinamica tendremos que **la suma de las energias de entrada sera igual a las energias de salida**.

Lo que cambia es la materia que entra y sale, y la energía que esta disipa dentro del sistema (calor y trabajo)

$$\fbox{$\dot{Q}_{\text{entr}}+\dot{w}_{\text{entr}}+\sum{\dot{E}_{\text{masa entr}}}=\dot{Q}_{\text{salid}}+\dot{w}_{\text{salid}}+\sum{\dot{E}_{\text{masa salid}}}$}$$

:arrow_right:**RECORDAMOS** 

La energia de la masa es el flujo de masa $\dot{m}$ multiplicada por la suma de las energias especificas (Entalpia especifica$h$,energia Potencial graviatoria $E_p$, energia cinetico $E_c$)
 
$$\dot{E}_{\text{masa entr}}=\dot{m}.(h+E_c+E_p)$$
osea
$$\dot{E_m}= \dot{m}(h+\frac{V^2}{2}+gz)$$

:arrow_right:**ENTONCES** 
Reemplazamos la energia y calculamos la energia de la materia de entrada y de salida usando los valores 
* Velocidad de entrada$V_e$  y salida$V_s$
* Altura de entrada $z_e$ y salida$z_s$
* Entalpia de entrada $h_e$ y salida $h_s$
$$\fbox{$\dot{Q}_{e}+\dot{w}_{e}+\sum{ \dot{m}(h_e+\frac{V_e^2}{2}+gz_e)}=\dot{Q}_{s}+\dot{w}_{s}+\sum{ \dot{m}(h_s+\frac{V_s^2}{2}+gz_s)}$}$$

#### Casos con $E_p$ despreciable (bombas, toberas)

En muchos dispositivos que modelamos como sistemas flujo-estacionarios **no hay una variacion importante de altura**,
Entonces podemos eliminar el termino $+gz_s$ siempre que nuestro dispositivo no tenga grandes diferencias de altura de entrada o salida
 $$\fbox{$\dot{Q}_{e}+\dot{w}_{e}+\sum{ \dot{m}(h_e+\frac{V_e^2}{2})}=\dot{Q}_{s}+\dot{w}_{s}+\sum{ \dot{m}(h_s+\frac{V_s^2}{2})}$}$$

#### En sistemas de flujo-no-estacionarios

La principal diferencia con estos sistemas es que **la masa que entra no es igual a la masa que sale**

Las diferencias son
* $m$ ya no es igual en los dos lados, ahora hay $m_1$ y $m_2$
* Hay un termino adicional $m_2.e_2-m_1.e_1$ que indica la **energia de la masa que no salio del sistema**

$$\fbox{$\dot{Q}_{e}+\dot{w}_{e}+\sum{ \dot{m_1}(h_e+\frac{V_e^2}{2}+gz_e)}=\dot{Q}_{s}+\dot{w}_{s}+(m_2.e_2-m_1.e_1)+\sum{ \dot{m_2}(h_s+\frac{V_s^2}{2}+gz_s)}$}$$

#### Eficiencia

En un motor o una serie de procesos, llam

## Segunda ley
_de forma natural La entropia solo puede aumentar_

$$\Delta S  \geq 0$$


En terminos sencillos _El calor fluye de cosas a alta temperatura a cosas de baja temperatura_

# Ciclos -WIP

Un ciclo es una **serie de procesos** en el que, al final del ultimo proceso,  el **estado final es igual al inicial antes de empezar**.

Esto implica que para todo ciclo el cambio de energia interna $U$ entre el principio y el final del ciclo es cerp $\Delta U = 0$


![](https://i.imgur.com/i5rgNXC.png =400x)


## Ciclo de carnot 

Es el ciclo de motor de calor mas eficiente, pero **aun siendo ideal, no tiene una eficiencia del 100%**
* Requiere de una pequeña cantidad de **trabajo negativo en forma de compresion**  para producir **trabajo positivo en forma de expansion** 



**Pasos del ciclo**
1. Añado calor $Q_1$ de forma **isotermica**, osea que la temperatura $T_1$ no cambia, ese calor cambia el volumen $V_1$ del fluido, generando trabajo $w_1$ que empuja el piston (intercambio perfecto de  $Q_1$ por $w_2$, osea que $\Delta U = Q_1 - w = 0$)
2. Mantengo el sistema **adiabatico** (sin transferencia de claor al exterior) la energia termica interna $U$ se va disipando hasta que pasamos de $T_1$ a $T_2$ transformándose adiabaticamente en volumen $V_2$ transformando $\Delta U=w$ **sin perdida de energia por calor**
3. El piston ejerce **trabajo negativo** $-w_3$ comprimiendo el gas, ese trabajo se disipa en forma **isotermica** $Q_2=-w_3$, esto hace que $w_3$ sea lo mas chiquito posible
4. El piston ejerce **trabajo negativo**  $-w_4$ en forma **adiabatica** transformando el trabajo en temperatura, elevando la energia interna $w=\Delta U$ hasta alcanzar la temperatura $T_1$




**Algunas observaciones importantes**

* :warning: Es el mas eficiente por que **todo el calor POSITIVO se transforma en trabajo (expansion isotermica y luego adiabatica)**
* :warning: no tiene eficiencia del 100% por que **para volver al estado inicial hace falta comprimir el gas (hacer trabajo negativo $-w$), pero para hacerlo con el menor trabajo posible**
	*  **Para retornar $PV$ al punto de origen de la forma mas eficiente** Se lo comprime de forma **isotermica** (aumenta $PV$)
	* **Pare retornar $T$ al punto de origen de la forma mas eficiente** Se lo comprime de forma **adiabatica** (aumenta $T$)
* Notamos que entra un $Q_1$ en el paso 1 y sale un $Q_2$ en el paso 3, entonces **no todo el calor se esta transformando en trabajo** $w$.
	* En los procesos $adiabaticos$ no se pierde calor
	* En los procesos isotermicos se gana $Q_1$ o se desecha $Q_2$
	* Entonces el cambio de energia interna al final del ciclo es cero, por que vuelvo a donde empece  $\Delta U=0= Q_1-Q_2-w$
	* Entonces el trabajo sera igual a $w=Q_1-Q_2$

![](https://i.imgur.com/MaGMtE9.png)



![](https://i.imgur.com/eSdA52A.png)
## Ciclo rankine (turbina de vapor)

Nuevamente, como concencuencia de la primera ley

$W_{out}-W_{in}=Q_{in}-Q_{out}$

![](https://i.imgur.com/xySYJ8H.png)





## Ciclo refrigeracion por gas

![](https://i.imgur.com/kKIGpn4.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NzY0NzgxNDMsLTk4NTA4Nzk1OCw3Mj
U5MjcwMjgsMjM5MDAzNjAsLTE5ODA0OTI4MTgsLTE0ODIzNzcw
ODcsLTE0ODEzNjU5NTUsLTgzMjI0MjI3LC01MjM5Nzk0ODcsLT
EwNjI3NDYzMzEsMTgwODcxNDgzNSwxODk0NDgyNTIzLDE5MjU3
MDAyMTUsLTIzOTc5MTQ3MCwtMTUxMDg1MDc3OSwtMTU2NjU3Mj
UzOCwtMTY4MDc2Njg1LC04MzUxNDEyMTMsLTY1ODU5OTc0MCwt
MTY4OTczMDY5NV19
-->