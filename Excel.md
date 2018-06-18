


**mE QUEDE EN**
160 - TERMINAR automate sum function with code

**VER:**
* Power query




# Contenido



* Basico
	* fechas
	* Styles
	* Impresion
		* Preview 
		* Page layout
		* Print area
		* Mantener titulos en todas las pag.
* Listas 
	* Sort 
	* Filter
	* Subtotales
	* Formatear como tabla
	* Funciones para tablas / DBs 
		* DSUM, Davg, Dcount 
		* Subtotal()
	* Validar datos
	* Pivot tables
		* Pivot table grouping
		* Drill down
		* Slicer
	* Powerpivot, modelos relacionales
		* Añadir tablas a un modelo
		* Hacer joins
		* Hacer pivot tables con data model
		* Datos precomputados
* Agrupar y desagrupar datos
* Consolidar datos
* Name ranges
* Funciones condicionales
	* IF
	* AND
	* Anidacion de funciones
	* CountIF
	* SumIf
	* CountIFS, SumIFS..
* Lookup functions
	* Vlookup
	* Hlookup
	* Index() and Match()
		* Combinacionde nidex y match
* Text functions
	* Left, Right, mid
	* Length
	* Concatenate
	* Search
* What if analisys
	* Busqueda de objetivo
* Macros
	* Seleccionar cells hasta el final de los datos
	* UI para macros
* VBA
	* Variables
	* Metodos
	* Loops
 	* Logica
 	* Palabras reservadas
	* Interaccion con el usuario
	* User controlls sin forms
	* User forms
		* Eventos
		* Reserved words
	* Editar macros
 

 








# Basico

* **Copiar formato:**
	* Toma el formato de una cell y lo aplica en otras

* **Quircks de formatos**
	* Los porcentajes deben ir como numeros **entre 1 y 0**

* **Ocultar y mostrar rows y columnas**
	* right click en col o row -> hide
	* right click en las col o rws entre las que hay cosas ocultas ->unhide

* **hacer templates**
	* Podes hacer que un archivo sea un template simplemente guardandolo como un excel template 

* **freezar los headers**
	* Podes hacer que los headers se queden siempre a la vista aunque scrollees **seleccionando un cell por debajo de donde queres freezar** y llendo a **view->freeze panes**

## Fechas

* **10/10/10 +1 =11/10/10** añadir uno es siempre añadir un dia
* **WEEKDAY(fecha, formato)** da el numero del dia de la semana
	* **formato=0** para tener lunes =1 y domingo = 7

## Styles

los estilos son un conjunto de formatos (colores, fonts, backgrounds, etc) que estan definidos en un solo lugar y pueden aplicarseen muchos lugares pero si editas el style, se editan todos los lugares que los usan

* Colocas formato en un cell hasta que este como desees y la seleccionas
* en home,  vas a **"cell styles"->"new cell style"**

Una vez que hiciste eso, podes **editar el style haciendo click derecho en el ->modify**

## Impresion

### Preview

Podes escalar para abajo una impresion para que encaje en la hoja de la siguiente manera.

![enter image description here](https://lh3.googleusercontent.com/jC8JAQNpW-PLPfOyuu4RhBj-yIOTSWBFfuka4F76W0pJ_gA0l2y22qKhdp0Zu_EoaYqkqgXm1hvO)


Si usas **custom scaling options podes escalar aumentando el tamaño**


![enter image description here](https://lh3.googleusercontent.com/q9g11tzwHgLuEVYWZMzp5_UkekBCAzSS5-Z3dJ5OGhKSFPqTaOIozYvbq0wAXcl5mAM8z25QBKMj)


Tambien podes **indicar los margenes y los anchos de cada columna y fila de manera interactiva**
![enter image description here](https://lh3.googleusercontent.com/gu3e0bg9sYCgCsfAD9CA-lY9Wtep5GRaajlYW070R_JX08r76doOoZdetpNy-qhgD6sjikwYsOOy)


### Page layout

Podes acceder al page layout asi:


![enter image description here](https://lh3.googleusercontent.com/Ml5eNMVk7-IDRpRG6Qu2o5dB-wwbfsG7tgKr5hvxo2igsW-RKROR8iQfLmNecOFtwP40N5p4fJVX)

**desde ahi podes arrastrar y resizear los elementos a gusto hasta que entren**

Ademas podes **añadir headers y footers clickenado en esa area** 

![enter image description here](https://lh3.googleusercontent.com/_-J-A2U9DPhoY6_rV4B3WfPrScd_aul24ryWmLbZliri5hF7p8aq5VFKlC5LrX9D-2ghkZRllqlE)

### Print area

Podes imprimir una subseccion de l documento usando **print area**
Para remover el print area apreta en la flechita del icono

![enter image description here](https://lh3.googleusercontent.com/H_8tD6tRhjQe6vKYVd1wotse0cbgX_QQXy7pzt_el4OQeHugltbvmcH12H1hc7oubxXoy0pWJ5Cr)



### Mantener titulos en todas las pag.

Podes mantener titulos en todas las paginas asi:
![enter image description here](https://lh3.googleusercontent.com/7rnvPiZwy-Us-pa-U7g243m2CDGeCD2CUjbndFhz-om9qA5YgFF0rNt0wRamuuMrX9mmkrnXJcML)



# Listas


Las listas son reconocidas por excel por:
* Tener un row con formato distinto, reconocido como **header**.
* un **row vacio** se reconoce como **fin de la lista**.

## Sort

podes ordenar en varios niveles y usando valores o fechas asi:
![enter image description here](https://lh3.googleusercontent.com/QdtnQ075e9INAEAwSzrm4ZjYruVGFgalSD9jeOjTM7d635S5W98lC_kESoGNVP2B515X0WG09QxS)


## Filter

Podes filtrar por los valores de una columna asi


![enter image description here](https://lh3.googleusercontent.com/zsxCjnxiBHDzV9mqBrhQIv0hUI6eRv0WKcbTBP9CdtvJynxQzuFjZIANhtchuMtU7v10ItLFO72p)


## Subtotales

Te permiten sumar subconjuntos de listas, cada subconjunto esta definido por el valor de un cell.
![enter image description here](https://lh3.googleusercontent.com/go1Me9qyQ5P4sc27EmhImNBu9Ui18fvwcH7CelpuPrMPSFLpuf0yZZsvBWCPrVDFWc0W3OdXrSiN)


Resultado final
![enter image description here](https://lh3.googleusercontent.com/ul_jxd9SrjsAeMKa-GK081vJL2keVA1kTBABl9udksNmG6AXIMM1pE7u9rrd2zLPXgeFEhQl6RNs)


## Formatear como tabla

Esto te permite
* Colocr un estilo que se mantiene aunque reordenes o filtres
* Tiene calculos de aquellos valores resultantes de un filter o un order

**PARA EXTENDER LA TABLA, ARRASTRA LA PUNTITA AZUL EN LA ULTIMA CELL DE LA PARTE INFERIOR IZQUIERDA**

![enter image description here](https://lh3.googleusercontent.com/1FiOZuJHvcaW08RUCBsfxO6UbATXxgSX7PhAu3nvhH5sM5H808sVisACAir-hnm8RyMAUQbuJabJ)


Tenes una serie de opciones aca
![enter image description here](https://lh3.googleusercontent.com/1J2wrc0Q4ugOWMs8gGJcoiMlaxLqGukr-PklCnHZWzlf-DWivM6YLL4XhL-b-zJTbMH6DybPjCiW)

## Funciones para tablas / DBs


### DSUM, Davg, Dcount
>Estas funciones no se rompen con records filtrados o reordenados



>**Es analogo a:**
* **Daverage()**  - saca el average de los records que cumplen una condicion
* **Dcount()** - cuenta la cantidad de records que cumplen una condicion
* **DSUM()** suma los valores de una DB(tabla) que cumplan una condicon
* **casi todas las funciones que operan con  D**


* **La condicion:** (en rojo) es indicada por uno o mas pares de headers y valores o operadores logicos
* **Field:** es la columna de la tabla que te interesa sumar/avg/count
* **database:** es la tabla

**sumar todos los expenses con concepto = "supplies"**
![enter image description here](https://lh3.googleusercontent.com/7tpIkRYSANSZdACRB-n7APCpDu3KTigo0CbMy9dhnMc_0-XoIejcBKT5BNRlbzs-eaPF964bLZtD)


Las **condiciones pueden ser operadores logicos**
![enter image description here](https://lh3.googleusercontent.com/QXYrdYMTsJ9L01Z7yxe2uNvGrwDzEHjwcDDd4tyd5CJKpl1SAkvVSllx4N_NqergmBSrpAVGD_Zs)


### Subtotal()


Suma/avg/count/otros los records de una db que cumplan una condicion
**no se rompe usando filtros/sort**

* **toma N parametros:**
	* **function_num** - 1 para suma, 2 para avg, etc. mirar la referencia
	* **columna1** - columna de la que queres calcular un subtotal
	* **columna2**
	* **columna N**

## Validar datos

Podes limitar lo que el usuario puede poner eln la DB a una lista predeterminada.

**EL USUARIO VA A VER UN DROPDOWN CON LAS OPCIONES QUE PUEDE ELEGIR**
![enter image description here](https://lh3.googleusercontent.com/b61I2gelJDXM64JtMjDC7Rwq9e23UmW6y0Pwj9nk-yVIVMsn8BZp-wHM3arBpjDuz9CWoVgKyJ00)






## Pivot tables

son tablas que se alimentan de otras tablas para resumir la informacion de la primera.

Por ejemplo,**a partir de una tabla de ventas, podes armar un pivot table que indique las ventas por vendedor y por mes.**


**Se arman simplemente arrastrado los elementos en el UI**


![enter image description here](https://lh3.googleusercontent.com/sbYW-y7Po9uj3n_TKNhGgSZLpAcaKyXPc7ccMWlLig5g7nJYrAVSJwxgf4HkhdNskFqcvcc1ARdy)

![enter image description here](https://lh3.googleusercontent.com/u6JtuWrkCfAzrUWtQbOZ5QVWY_p3gjMnNQcChWm1HCjrPFqQNL09-cXh5o7mj-H_0N3VhZkd1Tuu)


Podes indicar como queres que se haga el calculo de valores (suma, avg, count, etc)
![enter image description here](https://lh3.googleusercontent.com/ts4m8JAkMphJ6rCrb3yDZClIYuh5t6wpIWUTgC8zNHSwKhtaS9XCL65IegOu9lt5XMPfXeZVlNDs)

Tambien podes indicar **calculos mas complejos**, por ejemplo comparar con la fila anterior.

![enter image description here](https://lh3.googleusercontent.com/sZMVkK9RwJadS5G-hweSLPNQkHEmY_rX8v8GWS2ZTugFhrJr2DkC7wzI6d1_ideA6bxykNLgK1Ui)


### Pivot table grouping

Podes agrupar elementos de un pivot table para lograr un **ordenamiento logico** (EJ: cuatrimestes)

![enter image description here](https://lh3.googleusercontent.com/AMxY28bpfWmmRGndiIgEaoY5X1K8nkt4QjeTaPhmlHwyRFA12MzSV5g-_Uvh5aDfHMsnPEbIlZ4e)


### Drill down

si haces doble click en un campo de un pivot table, **te lleva a una tabla separada** donde ves todos los **datosque se sumarizaron en ese cell**

![enter image description here](https://lh3.googleusercontent.com/rMFU47JVlgNzQmlZxXtRu-VbdsHOygslD5BWtJrSepkddxkvHIUUZ7VA6nIsU5LjYiflL6m-R5b5)

### Slicer
Los slicers te permiten **aplicar filtros en las pivot tables de manera mas comoda para alguien que no entiende nada de excel**, te arma unos botones grandes que aplican un flitro en la tabla en vez de apretar en las columnas y usar el filtro desde ahi

![enter image description here](https://lh3.googleusercontent.com/cgY7CUcVrD0GKMoiouYsR0FqeevEY-lR0CfmD8MAmyozI-IJDRyaSM7mWtgX1vYn-NLXQqac-1xb)



# Powerpivot, modelos relacionales

Power pivot te permite crear un **modelo relacional a partir de listas y JOINS**, una vez que creas el modelo podes hacer 

* un pivot table a partir de esos datos.
* Calculos predefinidos para colocar en pivot tables


## Añadir tablas a un modelo


Para aañadir tabllas a un model, clickeas en la tabla yy haces esto

![enter image description here](https://lh3.googleusercontent.com/v7v7PWG6K_FAM6yZsQK8j9fqZQDO0qRXuxTOj0KLVxSfQPIpNkA8MhLkm6E7K8eN63G6DEesrJbM)


## Hacer joins
Para hacer joins, te paras en el diagram view y arrastras las keys que estan relacionadas entre si.

![enter image description here](https://lh3.googleusercontent.com/VPHKzv-Ic877soqV7becRS9QssLAoHUNq4yBCc1i9JcgS5C9eZh6HTqdnZ18PFeF5x3AVnqMQCur)


## Hacer pivot tables con data model


Una vez que tenes tu modelo, creas la pavot table y elegirs como queres mostrar esos datos como si fuera un pivot table comun
![enter image description here](https://lh3.googleusercontent.com/qjwxX2XuwTqQk4BsmiPBSTjc_SlW9LWb8yQ_cmM6HE5dN-ZXcvzkjkByBkybv_uQniB_8ux_x6HO)

![enter image description here](https://lh3.googleusercontent.com/TiG2YsnfzCT7A5DYSLJFTcaH1i9aOzlBB1fiu3NKb4gfr1heQ_ABSTITPavQWKgUZgv8N5EIOBfy)


## Datos precomputados

Podes calcularcosas en el data model y despues mostrarlas organizadas en un pivot table (por mes, nombre, etc)

EJ: **precomputar la suma de los precios en el modelo y despues en el pivot table mostrar el avg de precio por categoria de producto**
![enter image description here](https://lh3.googleusercontent.com/1nxmHB1s_YqZ5FycOR6Y31POC6hkKQx0Xm81A8Bx9mpZglReymw1bGLaU_IuwPvH0FFec1fnSrC5)


# Agrupar y desagrupar datos

Podes generar un grupo para ocultar/mostrar datos y **generar un UI para colapsar datos facilmente**


![enter image description here](https://lh3.googleusercontent.com/ennvz8ptYn-mjLQOK3eDTjA30l0ttMkVMD7u-eR6-QxVE73Kl0npDOIA4UPR_3Xr_Q5yeqLDaKxf)

# Consolidar datos

Te permite tomar varias tablas y combinarlas en una sola haciendo sumas o contando los campos donde los valores son iguales

![enter image description here](https://lh3.googleusercontent.com/hU7A0bPkHY1qZbvcjpMDQSqEynVXOOzQl-PTnJnwWdg1I0xSFCJRvyBsXwFlKb7wk782hbEi8I4B)

# Name ranges

Te permite nomrar un rango para usar el nombre en tus cuentas

Simplemente selectionas las cells que queres nombrar y escribis el nombre del grupo arriba a la derecha, luego apretas **enter**
![enter image description here](https://lh3.googleusercontent.com/9Ln8eMV6_dt2hB2zZ_aViLl_XRupw0Tf7IKYHAxl5kz34igKPWHLifIYQj_rDnbHJuSzZLLlA6rS)



Luego podes usar ese nombre en otras formulas
![enter image description here](https://lh3.googleusercontent.com/VaqmXlwTIidm-z8ySNLuMx54JgGvKixrBTW9i9lBNPWW5artaBDH5AANCXWdmuI7Fg1IAHaOBrq7)


# Funciones condicionales

## IF

Usa un condicional para determinar el contenido de un cell.

la condicion puede ser una compaacion de dos o mas cells.
Los valores pueden ser un cell o un valor
![enter image description here](https://lh3.googleusercontent.com/ZxZ7O8VHF9B8GWeh_mhmrTUAUoHcGLFNVsHdBhqhB7b8X2gJIpZa3erkUsvx0pob1pO5z-NCYwFd)


## AND

es una funcion que se puede anidar en un IF o cualquier otra funcion logica
**permite corroborar que N condiciones son true con un AND estre ellas**

![enter image description here](https://lh3.googleusercontent.com/fnN6lwUUYGiP7UEAWDceG5FSCKD47PIrMZka_sZQHgnKdFa2jww2SLX04RIMoTAJ7xSCLpqF6YFF)





## Anidacion de funciones

Podes anidar funciones libremente.
![enter image description here](https://lh3.googleusercontent.com/ocMx9k01QJaNd2A5OhGCqr5WsttRGTgg6v00hGyJPMXwqULkKSzPdbFc7NkPFDNOYCxP4x6DTOGa)


## CountIF

Te permite contar/sumar los records que cumplen con una condicion

Acepta el rango de records y una condicion o un valor que buscar para ver si es true

![enter image description here](https://lh3.googleusercontent.com/w_mcZnAt4yYJwQMECqYgjv-NMOUZVwoeYkl3B5VwPepxS2B2JQVCG3YwfR0p0-c-hy7wEdqj3GNa)



## SumIf

Te permite sumar una cantidad de records que cumplan con una condicion 

**Acepta:**
* **Range:** Los valores donde se van a chequear los criterios
* **Criteria:** El criterio que se va a usar para determiar si se suma o no
* **sum_range:** El valor que se va a sumar (cada elemento en range es un criterio para sumar cada elemento de sum_range)

![enter image description here](https://lh3.googleusercontent.com/87ILFsUgdaYkK-683nswe998iuzexWMLMdtH6VOYDVXaJYmhtUD37J17JRdyys8bdEDvMgm8xmze)


## CountIFS, SumIFS..

te opermite contar o sumar una serie de capos que cumplan con N condiciones


# Lookup functions

## Vlookup

Busca por la prmera columna de una tabla un varlor y devuelve unel valor de una columna de esa tabla

* **lookup_value** El valor que vas a buscar en otra tabla
* **table_array:** La tabla donde buscas ese valor
* **col_index_num** el N de la columna de la tabla Table_array cuyo cell queres devolver cuando encuentres el valor en lookup_value
* **range_lookup:** dejar en false!

![enter image description here](https://lh3.googleusercontent.com/3IAAF294V07x4DmrMildsRMHMwC0eSNB62xlEZHWMZAP5YZ4e-8hr8EvsFOubK18D1loNaagy3RN)
 
 ## Hlookup
 
 Identico, pero compara los valores del primer row del table array y devuelve un row N
 
 ![enter image description here](https://lh3.googleusercontent.com/F7eo6-vIVoVo3Gd-AAyINR6zKlVT4qHFd9FCsDkqZ-kGVg7uj1AUMTZ6nOmdGkjI3DvTRqIst-pI)
 
 ## Index() and Match()
 
 
 * **Index** en una tabla, devuelve el valor de la columna N, row M
![enter image description here](https://lh3.googleusercontent.com/WOoIi0lBCDktZK_acvQEOqUONfxxZR1KkvlPRmaw5VKZDczRHoAzXbsQ8G3yhqzDVrogHXKDZyAL)


* **Match()** 
	* En una columna, devuelve el numero de row donde este un valor. 
	* En una row devuelve enl numero de columna donde esta el valor
 ![](http://i.markdownnotes.com/5656556.jpg)

### Combinacionde nidex y match

Podes anidar match dentro de index, es decir 

* Queres encontrar un valor relacionado a un valor $V$ que conoces
* **con match buscas el indice de un valor $V$ en una tabla**
* **con index buscar en la tabla ese valor y devolves la colmna o row M o N asociada a ese alor**

 ![enter image description here](https://lh3.googleusercontent.com/kkb6ME2icApWIMlapBHZIit0uAnuC7pV3uM8uJIYK9GVxYqedsvkA57YTDavlJppBLJZPtlgCJUb)
 
 # Text functions
 
 
 ## Left, Right, mid
 
* **Left** desde la izquierda del string, toma N caracteres del string
* **Right** desde la derecha del string, toma N caracteres del string
* **Mid** desde la izquierda, saltea N caracteres y luego toma M caracteres

## Length

Indica la cantidad de caracteres en un string

## Concatenate

Te permite concatenar textos 

## Search

Te idica la **posicion de un substring** en un string (ej un espacio, una coma, etc) , lo podes usar combinado con **left, right, mid** para conseguir un substring que vos quieras


# What if analisys

## Busqueda de objetivo

Te permite encontrar valores tal que una funcion devuelva un resultado.

Por ejemplo, encontrar el valor de un cell tal que un calculo con ese cell de un resultado $X$

Toma tres argumentos
* **set cell** - El cell que contiene la formula
* **to value** - el valor a que queres que llegue esa formula
* **bu changing cell** - la celda que toma la funcion como imput, y cuyo valor excel debe encontrar para que la formula de el valor deseado

![enter image description here](https://lh3.googleusercontent.com/ROPV-HpNv7heEKRT-RABN1I-u9pVA-rP6pN2qnzPtFJiKjiwlObbeJuJ3WVelsTuq-TEnxTyGZ6k)



# Macros

Podes grabar una serie de acciones y guardarlas como un macro

## Seleccionar cells hasta el final de los datos

podes seleccionar **y dejar grabado** que seleccionas cells **hasta que haya un cell vacio** haciendo 

* **Ctrl + Shift + $\rightarrow$** 
* **Ctrl + Shift + $\downarrow$**

## UI para macros

Podes crear botones que corran macros (cosas simples como filtrar o esconder cosas pueden hacerse A prueba de boludos con esto)
![enter image description here](https://lh3.googleusercontent.com/pzeGikA5TIYFh7uj8xZaGRQAkPtPj7MRJmdGD5q5a8Rp9_3ucRV0QLHsNQrU1ewqd-ZIPx8LcDNX)


![enter image description here](https://lh3.googleusercontent.com/ypYk7DmWUNsTYIXfjECs_2wrkvSTJsa7it3TzRmtXkdsof6Lc1viTbuDdQoTkdzbvRCHI5nSggBk)



# VBA

Para entrar en el editor apreta **Alt + F11**
## Variables

	Dim MiVariable As Tipo


## Metodos

podes armar una funcion asi

	Public Sub nombreDeMetodo()
	//haces cosas
	
	End Sub

## Loops

* **do while loop**
		Do While ActiveCell <> "algo"
		//hacer cosas
		Loop
* **For loop**
for i=0 to 5


	
## Logica

	If CONDICION Then
	//cosas
	
	End If

## Palabras reservadas

Navegacion, seleccion y leer valores

* **activecell** - La celda seleccionada por el usuario al momento que corre el script
	* **.value** - El valor de esa celda
	* **.Offset(x,y)** -  cambia la celda activa a otra en las coordenadas **relativas** x,y 
	* **.Adress** - La ubicacion de la celda (EJ: A5)
* **worksheets** - Es la coleccion de todos los sheets
	* **.count** - Indica cuantos worksheets hay 
	* **worksheets(N).Select** - devuelve el worksheet numero $N$
* **ActiveSheet** - La sheet en la que estas parado 
* **Range("A15")** - Representa una celda o rango de celdas
	* **.select** - Selecciona esa celda o rango
* **Selection** * Representa la seleccion actual
	* **end(atr)**  - Indica donde termina la seleccion
		* **end(xldown)** - Indica que termine donde haya un cell vacio hacia abajo
		* **end(xlRight)** - Indica que termine donde haya un cell vacio hacia la derecha
	* **copy** - copia lo que esta seleccionado al portapapeles 


## Interaccion con el usuario

* **InputBox("mensaje al usuario")** - Pide al usuario un valor y lo devuelve
		dim variable = InputBox("mensaje)
* **msgbox("mensaje", tipoDeMsgBox)** - abre una ventana al usuario con un mensaje, el tipo de messagebox determina que botones tiene (si/no, aceptar/cancelar, aceptar/reintentar/abortar, etc)
		dim acepta As Int	
		acepta = msgbox("acepta", VbYesNo)	


## User controlls sin forms

Podes poner user controlls y referenciar funciones ("macros") de vba
![enter image description here](https://lh3.googleusercontent.com/Pu8mvrEXv-PiyD-_54FhePpyY_ZB8EsMxwMS7ELOowWpnil0yxvdFxzXDItnNBU-_ALw5ynFNTA-)

## User forms

Podes crear un form haciendo **instert->user form**.
Podes editar sus propiedades (texto, color, etc) haciendo click sobre el elemento **creado y editando sus propiedades**

![enter image description here](https://lh3.googleusercontent.com/6q__qSbWdKO4JPfJ4sd1Yxx3qa8BPBmrdrzU4XltGPyMvhcwbwUbSp0qYnTEyaMU0T_BaoVpcpW4)


**Podes agregar controlls usando el controll toolbox:**
![enter image description here](https://lh3.googleusercontent.com/1LvNw97EGPIByx2PKhrh3E6_BHNxeBJKtqA-SNLUCUQNEWo5DaGoWs2uYWp_iX6XHlhforHE2Xlg)



**Podes ver el codigo del form aca**
![enter image description here](https://lh3.googleusercontent.com/crLm_45c2RfGiIYsOerKZQyGHkjEuMN_aDEIMsbQS-oQd2REf7TMZNxWVd9ZepQPJypMgEhMwbST)


**y agregar codigo para distintas partes del form asi:**

![enter image description here](https://lh3.googleusercontent.com/8B91H_zJ7bD3O7wNXAmEN5V0J8zCy3zJHo98PjS9Je5YBp11pLWISte0l2i4VMj2KlZ4NZlTl_P5)


**Los forms funcionan con EVENTOS, cada evento busca un metodo con un nombre especifico que tiene que ejecutar, elegir el elemento y el evento desde la interfaz de la imagen de arriba TE ESCRIBE EL METODO DE CALLBACK PARA ESE ELEMENTO Y ESE METODO**

### Eventos

Si queres mostrar datos en la form, tenes que usar el evento **INITIALIZE**

		Private sub miForm_initialize()
			//cosas
		End Sub
		
**Otros eventos:**

* **cosa_change()** - Corre cuando cambia el valor del controller (ej un dropdown)

## Reserved words

* **me** - contiene el form en al que estas programando
	***.MiBoton** - Referencia el controller con ese nombre (boton, drop down, etc) 

## Editar macros

Los macros aparecen como **metodos** en Vba
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk2NzE1Mzg5OSwxMjIxOTUwNjQ2XX0=
-->