


**Cursos en orden:**

- [ ] [Intro databases standford](https://www.youtube.com/watch?v=D-k-h0GuFmE&list=PL6hGtHedy2Z4EkgY76QOcueU8lAC4o6c3)
- [ ] [Introduction to Database Management Systems](https://www.youtube.com/watch?v=zQuFCsTLLSU&list=PLstRzn3gXZMdXqAiVJ1NN2CoyXHqma7pQ)
- [ ] [Database design](https://www.youtube.com/watch?v=e7Pr1VgPK4w&list=PL_c9BZzLwBRK0Pc28IdvPQizD2mJlgoID)
- [ ] [data modeling](https://www.edx.org/course/introduction-to-data-modeling)
- [ ] [Database Systems internals](https://www.youtube.com/watch?v=xjhQ0e9Hlds&list=PLSE8ODhjZXjYutVzTeAds8xUt1rcmyT7x)
- [ ] [MySQL intro](https://www.youtube.com/watch?v=UGu9unCW4PA&list=PL_c9BZzLwBRKn20DFbNeLAAbw4ZMTlZPH)
- [ ] [Advanced database systems](https://www.youtube.com/watch?v=poEfLYH9W2M&list=PLSE8ODhjZXjYplQRUlrgQKwIAV3es0U6t)
- [ ] [Bases de datos, intro tecnica](https://www.youtube.com/watch?v=lYOVKEMKGWg&list=PL5n1zsTDauPtCTzaowE0Bl8mVoKebL0u8)
- [ ] [MongoDB schema design](https://www.youtube.com/watch?v=LEwehYpTxCg)
- [ ] [MongoDB data wrangling](https://www.youtube.com/watch?v=UJyJm79RS88&list=PLAwxTw4SYaPnq2iMkfPxmXwBFjwc_AXK_)


**Me quede en:**
* Volver a ver **Fourth normal form** para entender bien el video
https://www.youtube.com/watch?v=698GsCsmXIk&list=PLroEs25KGvwzmvIxYHRhoGTz9w8LeXek0&index=22





**Conceptos a profundizar:**
* **Closure**: que es?? Figura brevemente [aca, min 4](https://www.youtube.com/watch?v=nf1-h2GpEGc)
* **Relational agebra**: se ve en el segundo curso "Introduction to Database Management Systems"

**VER:**
* Reorganizar key, indexacion y relaciones, son conceptos cortitos, introducirlos de forma mas reducida
* Definir bien "closure"
* **Organizar bien relational algebra, refactorizar, imagenes, texto claro**
* En abstract algebra, union y intersection necesitan que los nombres de los schemas sean identicos, para eso podemos usar el rename operator. explicar eso, esta [aca, min 8:30](https://www.youtube.com/watch?v=GkBf2dZAES0)
* De-Normalizacion


# Contenido


* Intro
	* Caracteristicas de las bases de datos
	* Glosario
* Modelo relacional
	* Key 
		* Indexacion  - **POBRE**
		* Relaciones - **POBRE**
	* Querys  - **WIP**
		* Closure y Compositionality  - **WIP**
	* Relational agebra **- RE WIP**
	* SQL
* Diseño de bases de datos relacionales **- WIP**
	* Anomalias
	* Functional Dependencies (FD) 
		* Dependencia singular
		* Dependencia multiple 
		* Identificar functional dependencies
		* Formalizacion como clase de equivalencia 
		* Closure y FDs como keys
	* Multi-Valued Dependencies (MVD) 
	* Normalizado 
		* Boyce–Codd normal form
		* Fourth normal form 
	* De-Normalizacion **WIP**









# Intro

## Caracteristicas de las bases de datos

Los sistemas de bases de datos estan diseñados para:

* **Masivo:** Guardar y manejar cantidades masivas de informacion
* **Persistente:** Guarda datos de forma persistente (en disco)
* **seguro:** Estan preparados para **sistemas criticos**, tienen grandes garantias. incluso contra cortes de luz.
* **Concurrentes:** Muchos usuarios y aplicaciones pueden acceder de forma paralela
* **Gran Abstraccion:** Las instrucciones para extraer los datos (sql o otra abstraccion) son independientes de la eleccion de algoritmo que la base de datos use para sacar esos datos ó para almacenarlos.
* **Eficiente:** Es Increiblemente eficiente y optimizado.

## Glosario

Las siguientes definiciones son muy necesarias para hablar sobre bases de datos

**Partes de un sistema de base de datos:**
* **database:** Una coleccion de datos organizada de una cierta forma para representar algo. Generalmente esta armada para ser interpretada por un DBMS puntual.
* **Database model:** Es la estructura logica abstracta como estan organizados los datos en la base de datos. Ejemplos son: 
	* **Relacional** - sql, tablas,rows, etc
	* **Grafo**
	* **Documento** - JSON en mongoDB
* **database-management system (DBMS)** - Es un programa que interactua con una o varias bases de datos para capturar, analizar y modificar datos en una base de datos. En general lo hace a pedido de usuarios o otras aplicaciones.
	* MySql
	* Oracle
	* MongoDB
	* Reddis 
* **Schema:** Estructura predefinida que deberan tener los datos en la base de datos 
* **Data Definition Language (DDL):** Es un lenguaje que permite describir Schemas en el DBMS.
* **Data Manipulation Language (DML):** Es un lenguaje que permite expresar modificaciones y manipulaciones en los datos para que el DBMS los lleve a cabo.

**Personas involucradas en un sistema de base de datos:**

* **DBMS Implementer** - La persona que desarrolla DBMS, trabaja en oracle, mysql, etc.
* **Database designer** - La persona que usa un DBMS para diseñar los schemas de una base de datos para un uso particular (EJ: una empresa, un comercio).
* **Aplication developer** - La persona que crea aplicaciones que realizan operaciones sobre la base de datos (web developer, android developer, etc)
* **Database administrator** - La persona que mantiene y optimiza la base de datos.



# Modelo relacional

El modelo relacional es un modelo en el cual:

* los datos son organizados como **Ntuples** predefinidos por el **schema**
	* Es decir **"Atributo1,Atributo2,Atributo3"**
		* **"Nombre, apellido, DNI, telefono"** siempre en ese orden
	* Esto hace que **parezcan filas en una tabla.**
* Los **Ntuples** estan **agrupados en relaciones**
	* Todos los **Ntuples** que son "estudiantes" (tabla)
	* Todos los **Ntuples** que son "empleados" con "sueldo" > 1000 (tabla y valor)

En este sistema:
* los **Ntuples** son **un conjunto ordenado de attrobute values.**
* Las **Relaciones** agrupan **Ntuples** de acuerdo a sus caracteristicas, 
	* Una query es una relacion que agrupa ciertos **Ntuples** y los devuelve como resultado
	* Una tabla es una relacion que agrupa **Ntuples** con los mismos tipos de atributos.
* **Consistencia** de la base de datos esta formada por un **schema predefinido y rigido** que indica como deben estar conformados los **tuples** y son enforceadas por el DBMS
* Basado en algebra relacional

## Key

**Un atributo que es unico para ese Ntuple**, generalmente un 
* UserID
* DNI
* Telefono
* Index

**Te sirve para:**
* Identificar **Ntuples** especificos.
* **Indexar Ntuples**
* Vincular **Ntuples** entre si


Un **Ntouple1** puede referirse a un **Ntuple2** que tiene informacion adicional teniendo en uno de sus **atributos** una **key de Ntuple2**


![enter image description here](https://lh3.googleusercontent.com/MI43KpSDlqzz4jA6qMGIkFLCF2aXYllDGvsxMlu_oGpLIYzvc-nQL1RInMK62K0wE3agY7kU9HiL)
### Indexacion

Los DBMS usan keys para ordenar (indexar) los **Ntuples** de tal forma que buscarlos usando ese key sea extremadamente rapido



## Querys y SQL

Las **querys** en una base de datos relacional se hacen usando un **high level language** que generalmente es SQL, de esta forma **no necesitamos saber el algornitmo elegido por el DBMS, solo debemos expresar que es lo que deseamos y el sistema lo hace por nosotros**

En este caso **SQL** cumple la funcion de **DDL y DML**.


### Closure y Compositionality

**Compositionality:** La capacidad de realizar una query sobre el resultado de otra query

**Closure:**


## Relational agebra

Es un **lenguaje formal matematico** que forma la base de los lenguajes implementados para describir querys en una base de datos.

**Operadores del algebra relacional**

* . $\sigma_{condition}R_i = R_f$ - **Select operator**, selecciona **Ntuples** de una **Relacion inicial** $R_i$ usando una condicion, dando como resultado una **Relacion final** $R_f$ que **es un subconjunto de la relacion inicial**
	* EJ: $\sigma_{sueldo > 1000} \text{Empleados}$ Devuelve una relacion compuesta por todos los **Ntuples** que cumplen esa condicion.
* . $\land, \lor $ - And y OR, añaden mas condiciones al operador $\sigma$
	* $\sigma_{sueldo > 1000 \quad \land \quad horario = tarde}\quad \text{Empleados}= R_f$


* . $\Pi_{\text{atributo1,atributo2}}R_i=R_f$ - **Proyect operator**, Selecciona de una relacion,**ciertos atributos** de los **Ntuples** y los devuelve como una relacion.
	* EJ: Quiero ver solo el nombre y sueldo de la tabla empleados 
	$\Pi_{\text{"nombre","sueldo"}}Empleados$
* . $R_1XR_2=R_3$ - **Cross-product**, A partir de dos relaciones, Genera una relacion que consiste en todas las combinaciones posibles de Ntuples de esas dos relaciones 
	* EJ: $\text{Empresas } X \text{ Empleados}= R_3$ 
	 Haces un query con el resultad, buscas los Ntuples de los empleados con un sueldo minimo (que esta en la tabla de empleados) y que sea una empresa estatal (tabla empresas):$\sigma_{Empresa.cuit = empleados.cuitEmpleador \land sueldo > 1000\land dueño = "estatal"} R_3$ 
	 * Notese que $R_3$ tiene dos atributos duplicados, ya que une  "cuitEmpleador" de la relacion "empleados"  y "cuit" de la relacion "empresas", usando ese atributo repetido es que podemos identificar aquellos Ntuples de $R_3$ con ambos valores iguales, implicando que son empleados de esa empresa, el resto de los Ntuples son de poca utilidad.
![enter image description here](https://lh3.googleusercontent.com/qmPMqfqx0lIIV1uKeC9AnWhJohW1eLMdIJIqkKMN24tzu4uOObxoWr3coMKDwkoInEKDa-3I4gKc)

* .$R_1\bowtie R_2 = R_3$ **Natural Join** -La combinacion de Ntuples de dos relaciones** cuyos Ntuples tienen uno o mas valores en comun, considerando los atributos repetidos como uno solo**. es un subconjunto del cross product.
	*  Es identico a decir
	$\sigma_{R_1.atr1=R_2.atr1} (R_1 X R_2)$
	Con un ejemplo practico
	$\sigma_{Empresa.cuit = empleados.cuitEmpleador} (\text{Empresas } X \text{ Empleados})$
	* Es una operacion de conveniencia, no añade poder expresivo ya que podriamos decir lo mismo usando el cross product y el selection operator
		![enter image description here](https://lh3.googleusercontent.com/pZ2bMJYJgFRfwAYg-fZqCAEpx2kKjGav97TVFhJz8RUYzcA8PpSwln7HmMHJBkWix-YbmcB2yvV9)
	
* .$R_1\bowtie_{\theta} R_2 = R_3$ **Theta Join** - Implica el cross product de dos relaciones a las cuales luego se le seleccionan los Ntuples que **cumplen una condicion** $\theta$. 
	* Es como el natural join pero en lugar de usar nombres iguales como condicion de unir Ntuples, usa una condicion arbitraria $\theta$
	* Sinonimo de $\sigma_\theta(R_1 X R_2)$ 
	* En este ejemplo, $\theta= \text{CarPrice} \geq \text{BoatPrice}$ 
	![enter image description here](https://lh3.googleusercontent.com/KUJbTHUbKwH-Z6IR_wtjEaa0N0VQzMnGOCqkX2bibRUCW3dZS3VaWVtHIqbapXmLJxiRDY2Z40vX)
	
* .$\cup$  **Union** - Es la relacion producto de unir dos relaciones con la misma cantidad y tipo de atributos, es decir, se genera una relacion con los Ntuples de ambas relaciones,los Ntuples repetidos se eliminan.
	* Se puede usar para combinar resultados de forma vertical, Ej: los Ntuples de dos Proyect operator 
* .$-$ **Difference** - Es la resta o diferencia entre dos relaciones
	* EJ: Todos los residentes que no estan en el consorcio $Residentes - Consorcio$
	* Los nombres de los empleados que no estan inscriptos como beneficiarios en la obra social
	$\Pi_{nombre}Empleados - \Pi_{nombre}Beneficiarios$

* .$\cap$ **Interseccion** - Dadas dos relaciones con la misma cantidad de atributos, entoncontrar aquellas donde los Ntuples son totalmente iguales.
	* Podes combinarlo con proyection operator para encontrar coincidencias en dos relaciones con atributos diferentes.
	* Encontrar los nombres de aquellos empleados que tambien son operarios
	$\Pi_{nombre} \text{Empleados} \quad  \cap \quad  \Pi_{nombre} Operarios$ 
	* ** No añade poder expresivo, es equivalente a**
	$\Pi_{nombre} \text{Empl} - (\Pi_{nombre} \text{Empl} -  \Pi_{nombre} Operarios)$

* .$\rho_{R_2(att1,att2,att3)}R_1$ **Rename operator** - Toma una relacion $R_1$ y la renombra a $R_2$, tambien renombra el nombre de sus atributos (su schema) a $att1,att2,att3$. Tiene estos shorthands:
	*  .$\rho_{R_2}R_1$ - Solo cambia el nombre de la relacion (de la tabla) y deja los nombres de los atributos (columnas) iguales
	*  .$\rho_{R_2(att1,att2,att3)}R_1$ - Deja el nombre de la relacion igual y cambia los nombres de los atributos (columnas)
	*  EJ: Queres unir una tabla con si misma ($X$ cross-product), si las dos tienen los mismos nombres, como sabe el DBMS a cual de las dos columnas te referis cuando haces un query?, no lo sabe ya que es ambiguo, entonces tenes que renombrar los atributos de una de las dos relaciones para arreglarlo! 
	![](http://i.markdownnotes.com/self_join_BUAxmJa.jpg)



**CORE y NO-CORE operations**

Los operadores **CORE** son aquellos que no se pueden definir con otros operadores, los **NO CORE** son los que no aportan expresividad (son sinonimos de una combinacion de operadores CORE) pero son convenientes


| CORE        			  		         | NO CORE     				|
| -------------    		 		          | -----		 			|
| Relacion $R$  				         |     $\bowtie$  	 |
| $\sigma$      				         |   $\bowtie_\theta$  |
| $\Pi_{a_1,a_2..a_n} R$ 		         |    $\cap$ 			 |
| $R_1 X R_2$ 				         |    					   |
| $R_1 \cup R_2$		  		         |    					   |
| $\rho_{R(a_1,a_2...a_n)}$	         |    					   |


## SQL

Es un lenguaje implementado en base a la relational agebra y su semantica viene principalmente de ahi. Para mas informacion ver _lenguajes/sql_

Sus instrucciones se dividen en:

| DDL          | DML    |
|--------------|--------|
| Create Table | Select |
| Delete Table | Insert |
|              | delete |
|              | Update |



# Diseño de bases de datos relacionales

En general, se refiere al **_diseño de base de datos relacionales_** a la **seleccion de schemas que se va a usar**.

Existen formas de diseñar las bases de datos que minimizan los problemas a la hora de buscar y modificar informacion.


## Anomalias

Las anomalias en una base de datos relacional son fenomenos que dificultan el trabajo del administrador de base de datos y que pueden ser evitados usando un schema diferente.

Base de datos ejemplo:
**Anotados al CBC:**

| DNI        | Nombre | materia a la que se anoto |
|------------|--------|---------------------------|
| 37.222.222 | Juan   | Quimica                   |
| 37.222.222 | Juan   | Fisica                    |


Un buen diseño evita **anomalias** como las siguientes

* **Rebundancia**
Una misma informacion es capturada en la base de datos en mas de un Ntuple.
Por ejemplo en la siguiente tabla El DNI y El nombre son rebundantes para dos datos, podrian estar en una sola tabla y ser vinculados con un foreign key.


* **Actualizacion inconsistente**
Hace falta cambiar el valor de mas de un Ntuple para cambiar Un solo valor representado. EJ: para cambiarle el nombre a JUAN habria que modificar dos rows (y quien sabe que otras partes de la base de datos que tengan su nombre)
* **Borrado Inadvertido**
Es cuando borrar una representacion genera el borrado de otra. por ejemplo, si borramos todos los alumnos que se anotaron a quimica y existe un alumno que solo se anoto a quimica, entonces **ese alumno sera totalmente borrado de la base de datos**, para evitarlo separamos en una tabla los alumnos y en otra las materias para las que los alumnos se anotan.



## Functional Dependencies

Functional dependency es un concepto general que se aplica en varios campos de la computacion, entre ellos la compresion de datos, optimizacion de querys, etc.

Basicamente una dependencia funcional es la implicacion de que **si existe** un dato $A$ entonces debe necesariamente existir **un unico **dato $B$ **para ese** $A$. (Funcion Inyectiva $\Bbb{A} \rightarrow \Bbb{B}$)

**Por ejemplo:**
* Para un **DNI** siempre debe **existir un unico nombre y apellido**, 
* **No necesariamente** para un **unico nombre y apellido existe un solo DNI** (puede haber varios juan perez) 


### Dependencia singular
>Es el concepto de que un elemento $B$ aparece siempre con un elemento $A$. Osea que:
$A \Rightarrow B$

**Ejemplo:**
Aca, **DNI** seria $A$ y **nombre** seria $B$, ya que 
* El alumno con un cierto **DNI** $A$ siempre tendra el mismo **nombre** $B$
. $A \Rightarrow B$
* Un alumno con un **nombre** $B$ no necesariamente esta asociado a un DNI $A$ (puede haber dos que se llamen igual)
 $B \not\Rightarrow A$


| DNI $(A)$       | Nombre $(B)$  | materia a la que se anoto $(C)$ |
|------------|--------|---------------------------|
| 37.222.222 | Juan   | Quimica                   |
| 37.222.222 | Juan   | Fisica                    |

### Dependencia multiple

>Es el concepto de que una serie de elementos $B_{attr_1},B_{attr_2},B_{attr_3}$ aparece **siempre** que aparece una serie de elementos $A_{attr_1},A_{attr_2},A_{attr_3}$. Simbolizamos esto como una clase de equivalencia:
$\bar{A} \Rightarrow \bar{B}$

**Ejemplo:**
* **DNI** seria $\{A_{1}\}$ y forma el conjunto $\bar{A}$ 
* **nombre, apellido, domicilio** serian $\{B_{1},B_{_2},B_{_3}\}$ y forman el conjunto $\bar{B}$ 
* **carrera** y **materia** serian $\{C_1, C_2\}$ forman el conjunto $\bar{C}$

Para un **DNI** $\bar{A}$ siempre habran los **mismos nombre, apellido y domicilio** $\bar{B}$.
No asi para **carrera** y **materia** $\bar{C}$, ya que un alumno puede estar anotado en mas de una.

| DNI         | Nombre | apellido | Domicilio     | Carrera     | Materia    |   |
|-------------|--------|----------|---------------|-------------|------------|---|
| 37.222.222  | Juan   | Ignacio  | España 255    | matematicas | Analisis 1 |   |
| 37.222.222  | Juan   | Ignacio  | España 255    | matematicas | Algebra 1  |   |
|  38.222.222 |  lucas | Muñoz    | honduras 333  | Fisica      | Analisis 1 |   |


>**Entonces podemos simbolizar esto como:**
>La relacion: $R(\bar{A},\bar{B},\bar{C})$ donde:
>$\bar{A}=\{ \text{DNI} \}$
>$\bar{B}=\{ \text{nombre, apellido, domicilio} \}$
>$\bar{C}=\{ \text{carrera, materia} \}$
>Y existe la siguiente **dependencia funcional:**
>$\bar{A} \Rightarrow \bar{B}$


### Identificar functional dependencies

Las **Functional dependencies** dependen del contexto de los datos y que se asume de ellos, por ejemplo as arriba asumimos que un **DNI** esta siempre **asociado** a un **nombre, apellido y domicilio** y por ende hay una **Relacion funcional**, esto es porque **conocemos la naturaleza del DNI**.

De esta forma, **identificamos relaciones funcionales  cuando los datos y el contexto lo permite.**


### Formalizacion como clase de equivalencia

Podemos identificar formalmente las **functional dependencies** como clases de equivlencia, ya que.

Para todo par de atributos $A$ y $B$ de los **Ntuples** de una relacion, existe una dependencia funcional si en todo lugar donde $A$ tenga un valor $a_1$, el atributo $B$ necesariamente deba tener un valor $b_1$

$\forall a,b :$
$a_1=a_2=a_3 \Rightarrow b_1=b_2=b_3$
$\bar{A} \Rightarrow \bar{B}$


## Closure y FDs como keys

Dada una o mas **Funcional relations** $\bar{A} \Rightarrow \bar{B}$ se denomina **Closure** a la suma de $\bar{A}$ y toda la informacion $\bar{B}$ que puede ser obtenida solo con $\bar{A}$

A su vez, Si existe una **Functional relation** $\bar{B} \Rightarrow \bar{C}$, el **closure de $\bar{A}$** sera $\bar{A} \cup \bar{B} \cup \bar{C}$

>Si el **Closure** de $\bar{A}$ resulta ser toda la relacion $R$ entonces podemos decir que **$\bar{A}$ es un key de $R$**

## Multi-Valued Dependencies (MVD) 

Multi-Valued Dependencies es cuando cada valor $a \in A$ esta asociado a multiples valores $\quad b_1,b_2.. \in B \quad$ y $\quad c_1,c_2.. \in C\quad$
Pero $B$ y $C$ no estan asociados entre si.

**Lo simbolizamos:**
$A \twoheadrightarrow B$
$A \twoheadrightarrow C$

**EJEMPLO:**
Por ejemplo, cada **DNI** $A$ puede estar asociado a multiples **materias** $B$ y **carreras** $C$.


| DNI  $A$  | Carrera  $B$ | Materia  $C$ |
|-------------|----------------|----------------|
| **37.222.222**  | matematicas    | **Analisis 1**     |
| 37.222.222  | matematicas    | Algebra 1      |
|  **37.222.222** | Fisica         | **Analisis 1**     |
| 39.555.444  | Fisica         | Fisica 1       |

>**Notese como aparecen duplicados para poder colocar todas las combinaciones de $B$ y $C$**


## Normalizado

 Es el proceso de organizar los schemas de tal forma que queden:
 * **Sin anomalias**
 * **Sin perdida de informacion**


### Boyce–Codd normal form

Es un metodo de normalizacion **cuyo objetivo es remover la rebundancia causada por las Functional dependencies**, no genera una normalizacion perfecta ya que **otros tipos de rebundancia pueden persistir** en una base de datos que esta en **BCNF**

**BASICAMENTE:** Si tenes un dato que depende de otro, deberias ponerlos en una tabla separada.

>**Una relacion esta en Boyce–Codd normal form si:** 
>Dada toda Functional dependency $\bar{A} \Rightarrow \bar{B}$
>*  .$\bar{A}$ es **siempre unique primary key** de $\bar{B}$ en una tabla separada.

>**Esto genera las siguientes concecuencias:**
*  En lugar de hacer referencia a $\bar{B}$ directamente se usa $\bar{A}$ como **Foreign Key**
>* .$\bar{B}$ no aparece en ningun otro lugar de la DB, salvo que
>	* .$B_1 \Rightarrow \bar{C}$, en cuyo caso se crea una nueva tabla con $B_1$ como  **Primary key** , y se usara como **Foreign Key** para referirse a $\bar{C}$.
>	* A su vez, tambien puede usarse $\bar{A}$ para referirse a $\bar{B} $ y a $ \bar{C}$




>Es importante notar que **BCNF no necesariamente elimina todas las anomalias.**


De esta manera, si tenes una gren relacion $R(\bar{A},\bar{B},\bar{C},\bar{D})$ y definis que $\bar{A} \Rightarrow \bar{B}$ y $\{B_1,B_2\} \Rightarrow \bar{C}$

Separas la relacion $R$ en tres relaciones $R_1,R_2, R_3$ que contengan las dos **Functional Dependencies** con sus respectivas keys. Notese que el **Natural Join** de $R_1$ , $R_2$ y $R_3$ devuelve nuevamente la relacion original $R$

$R= R_1(\bar{A},\bar{B})\bowtie R_2(B_1,B_2, \bar{C})\bowtie R_3(\bar{A}, \bar{D})$


**EJEMPLO:**

Nuestra relacion $R$ es la siguiente:

| DNI  $A$  | Nombre $B$ | apellido $B$ | Domicilio $B$ | Carrera  $C$ | Materia  $C$ | Profesor $D$ |
|-------------|--------------|----------------|-----------------|----------------|----------------|----------------|
| 37.222.222  | Juan         | Ignacio        | España 255      | matematicas    | Analisis 1     | Ursino         |
| 37.222.222  | Juan         | Ignacio        | España 255      | matematicas    | Algebra 1      | Mateo          |
|  38.222.222 |  lucas       | Muñoz          | honduras 333    | Fisica         | Analisis 1     | Mateo          |
| 39.555.444  | Lucas        | Edoz           | Peru 555        | Fisica         | Fisica 1       | Araoz          |

**Identificamos las siguientes Functional Dependencies:**
* Un  **DNI** ($A$)siempre esta asociado al mismo **nombre, apellido y domicilio** ($\bar{B}$)
	* .$A \Rightarrow \bar{B}$ 
* Una **materia y carrera** siempre esta asociada al mismo profesor
	* .$\bar{C} \Rightarrow D$ 


**Vemos que las siguientes relaciones NO SON functional dependencies:**
* Un **DNI** puede estar asociado a **mas de una carrera, materia ó profesor**
	* .$A \not\Rightarrow \bar{C}$ 
	* .$A \not\Rightarrow \bar{D}$ 
* Un **Profesor** puede dictar **mas de una materia**
	* .$D \not\Rightarrow \bar{C}$
 
**Entonces separamos $R$ en:**

* .$R_1(\bar{A}, \bar{B})$ 


| DNI  $A$  | Nombre $B$ | apellido $B$ | Domicilio $B$ |
|-------------|--------------|----------------|-----------------|
| 37.222.222  | Juan         | Ignacio        | España 255      |
| 37.222.222  | Juan         | Ignacio        | España 255      |
|  38.222.222 |  lucas       | Muñoz          | honduras 333    |
| 39.555.444  | Lucas        | Edoz           | Peru 555        |

Donde $A$ es nuestra key, ya que $A \Rightarrow \bar{B}$

* .$R_2(\bar{C}, D)$ 

| Carrera  $C$ | Materia  $C$ | Profesor $D$ |
|----------------|----------------|----------------|
| matematicas    | Analisis 1     | Ursino         |
| matematicas    | Algebra 1      | Mateo          |
| Fisica         | Analisis 1     | Mateo          |
| Fisica         | Fisica 1       | Araoz          |

Donde $\bar{C}$ es key, ya que $\bar{C} \Rightarrow D$ 

* $R_3(A, \bar{C})$

Donde asocias las keys de $R_1$ y $R_2$, ya que no existe una **Functional dependency** entre ambos

| DNI  $A$  | Carrera  $C$ | Materia  $C$ |
|-------------|----------------|----------------|
| 37.222.222  | matematicas    | Analisis 1     |
| 37.222.222  | matematicas    | Algebra 1      |
|  38.222.222 | Fisica         | Analisis 1     |
| 39.555.444  | Fisica         | Fisica 1       |


### Fourth normal form

Es un metodo de normalizacion cuyo objetivo es remover la rebundancia causada por las **Multi-Valued dependencies**. Una DB que esta en **Fourth normal form ya se encuentra siempre en BCNF**

**BASICAMENTE:** si tenes datos que son independientes entre si, entonces deberias separarlos en tablas distintas

>**Una relacion esta en Fourth Normal Form si:**
> Para toda **MVD** $A \twoheadrightarrow B$
> * .$A$ siempre es key de $B$ en una tabla separada
> 
> **Esto genera Las siguientes concencuentas:**
> * No hace falta hacer todas las posibles combinaciones de $B$ y otros atributos

**Ejemplo:**

| DNI  $A$  | Carrera  $B$ | Materia  $C$ |
|-------------|----------------|----------------|
| 37.222.222  | matematicas    | Analisis 1     |
| 37.222.222  | matematicas    | Algebra 1      |
|  37.222.222 | Fisica         | Analisis 1     |
| 39.555.444  | Fisica         | Fisica 1       |

**Notese:**
* Rebundancia causada por los **MVDs**, **un solo DNI tiene muchas veces la misma carrera y materia.**
* El Ntuple extra **(37.222.222 , Fisica, Algebra 1)** esta implicito, ya que aunque **Fisica** no tenga la materia **Algebra 1**, ese alumno igual esta anotado en fisica y cursando esa materia.

Vemos que existen dos **MVDs**:
$A \twoheadrightarrow B$
$A \twoheadrightarrow C$

Para que esten en **4NF** tenemos que **separar las dos MVDs en dos tablas separadas.**
De esta manera **eliminamos la redundancia**

* $A \twoheadrightarrow B$

| DNI  $A$  | Carrera  $B$ |
|-------------|----------------|
| 37.222.222  | matematicas    |
|  37.222.222 | Fisica         |
| 39.555.444  | Fisica         |


* $A \twoheadrightarrow C$

| DNI  $A$  | Materia  $C$ |
|-------------|----------------|
| 37.222.222  | Analisis 1     |
| 37.222.222  | Algebra 1      |
| 39.555.444  | Fisica 1       |

## De-Normalizacion

No siempre conviene que la base de datos este **totalmente normalizada**, muchas veces es aceptable tener **anomalias** si **encaja mejor con el diseño o el uso que se le va a dar a los datos.**

Por ejemplo:
* Necesitas **acceso rapido** a un conjunto de datos (muchos JOINs hacen que la base sea lenta)
* Tiene mas sentido logico tener un conjunto de datos en la misma tabla que normalizarlo en varias.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEzNTkzMzQwNV19
-->