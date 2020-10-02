

# Coordennadas

El torno CNC es en general una maquina de dos ejes, $X Z$


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/hEaCU8S.png)


## Comandos basicos

### Giro

Existen dos maneras de determinar la velocidad de giro

**Determinando directamente las $RPM$**
* `G97 S300 M3`
	* `G97` Modo de giro en $RPM$ en vez de $\text{avance}$ 
	* `S300` Giro de la pieza seteado a 300 rev/min
	* `M3` Iniciar giro en sentido orario

**Determinando la surfice speed y dejar que la maquina calcule las $RPM$ sola**
Esto implica que dependiendo de que tan cerca o lejos este la herramienta de la pieza, el giro sera **mas rapido o mas lento**
* `G96 S180` Modo de giro en **Surfice speed**, las $RPM$ son calculadas automaticamente
	* El giro sera calculado para obtener una **surfice speed** de $180mm/min$


* `G50 S500` 
	* La velocidad maxima de giro, que la maquina no debe superar
	* Es modal
	* Si en algun momento usas avance  $G96$ basado en **Surfice speed**, esto evita que la maquina vaya a maximas revoluciones cuando esta llegando al centro de la pieza

### Avance

El avance puede tener dos modos
* `G98` Avance por minuto
* `G99` Avance por revolucion
## Linea de seguridad
```
G18; Usar el plano XZ
(avance en Unidades por revolucion, no)
( por min)
G99;  
G50 S500; Configurar una velocidad maxima, no usar la del programa anterior!
```
## Canned cycles

### G72 -Rougth   Facing



Se usa para hacer un frentado grueso

![](https://i.imgur.com/HaEzuja.png)

* Primero nos colocamos a una **altura segura** usando $G0$
 * luego procedemos a llamar a $G72$ configurando todos los **parametros para el ciclo**
 * Luego procedemos a indicar
	 * Linea de **inicio**
	 * Lineas **intermedias** para determinar la forma de la pieza
	 * Linea de **finalizacion**

**G72 se usa con dos lineas**

* Parametros de la primera linea:
	* `W` Profundidad del corte en **cada passada**
	* `R` cantidad de mm a la que retraerse antes de volver a arrancar el corte
* **Parametros de la segunda linea**
	* `U` Cantidad que dejar para una finishing pass despues, en eje  $X$ (para facing sera $0$)
	* `W` cantidad que dejar para finishing pass en eje  $Z$
	* `P`  linea $N$ donde empezar la operacion
	* `Q`linea $N$ donde terminar la operacion
	* `F` feed rate


```
(configuacion inicial)
G72 W0.8 R2.0; profundidad cada corte 0.8
G72 P200 Q300 U1.0 W0.5 F0.2;

(Linea de inicio)
N200 G0 X19.0 Z0;

(lineas intermedias)
G01 Z0.0; cortar hasta Z0
G01 X20 Z-5; cortar hasta X20 Z-5

(Linea de finalizacion, alejo mi herram.)
N300 G0 X70.0 Z5.0 F200;
```


### G71 - Rougth turning cycle

#### Rougthing cycle diametro externo

![](https://i.imgur.com/ovFbqMn.png)

 
Igual que G72 pero en vez de facing (desde afuera hacia adentro) es  turning
* **Primera linea**
	* `U` profundidad de cada pasada
	* `R` Cuanto alejarse de la pieza despues de la pasada
* **Segunda linea**
	* `P` y `Q` lineas de inicio y fin de ciclo
	* `U` y `W` cuanto dejar en $X$ y $Z$ respectivamente para un finishing pass
	* `F` feed rate

```
G0 X3 Z.1;Distancia segura a la que volver
G71 U1 R1; Prof x pass. y retract.
G71 P100 Q110 U0.2 W0.05 F0.2
N100 G0 X0 Z1
G1 Z-1 
G1 X1 
G1 Z-1
G1 X1.5
G1 Z-1.5
G1 X2
G1 Z-2.3
N110 X3
```

#### Rougthing cycle interno

![](https://i.imgur.com/MmznR15.png)

* I**gual al externo, pero**
	*  programamos con path ($G1$) desde un agujero central y hacia afuera
	* La posicion inicial sera **dentro del agujero inicial**
	* `U` y `w` van a usar el signo opuesto (por que "dejar material" en coordenadas desde adentro va a llevar el signo opuesto)

### G70 - Finishing cycle

Sirve para hacer la terminacion del rougthing hecho con $G71$ o $G72$
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMzkzMDExNTksLTM1OTUyMjQ5OSwxNj
Y3MTA0ODg2LDE0NDEwMjM2OTIsMTk1NjIzMDQxMiwtMTY0NjM1
NDQ3NCwtMjcyMzc2ODE1LC0yMDc3NjkwMTQwLC00NTAzODIxNT
ddfQ==
-->