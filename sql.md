





**ME QUEDE EN:**
Hacer ejercicios de SQL que quedan en SQLzoo
https://sqlzoo.net/wiki/More_JOIN_operations EJ 12 en adelante (inclusive)
Reever update incert delete

**VER:**
* CASE - WHERE


	

## Intro

>Es un prerequisito tener los conocimientos de Bases de datos relacionales delineados en _computer science/ bases de datos_

Es un lenguaje implementado en base a la relational agebra y su semantica viene principalmente de ahi.



| DDL          | DML    |
|--------------|--------|
| Create Table | Select |
| Delete Table | Insert |
|              | delete |
|              | Update |


## SELECT Y SU SINTAXIS

**Se lee/escribe como:** 
```
SELECT attr1,attr2 FROM tabla1,tabla2 WHERE condicion1 AND condicion2
```

**Se Procesa internamente como:** 
```
FROM tabla1, tabla2 WHERE condicion1 AND condicion2 SELECT attr1,attr2
```

**En algebra relacional seria:**
>**Con:**
>attr1, attr1 = $a_1, a_2$
tabla1, tabla2 = $R_1, R_2$
condicion1, condicion2 = $c_1, c_2$
>**Quedaria:**
$\Pi_{a_1,a_2}(\sigma_{c_1 \land c_2}(R_1 \quad X \quad R_2))$

Notese como el lenguaje de algebra relacional: 
* **Se lee** en el orden que se lee SQL
* **Se interpreta** en el mismo orden en el que se interpeta SQL




| SQL command         | Relational algebra operator                                    |
|---------------------|---------------------------------------------------------------|
| SELECT attr1,attr2  | $\Pi_{attr1,attr2}R_1$                                       |
| DISTICT             | no existe en set theory, no hay elementos duplicados en un set |
| FROM tabla1, tabla2 | $T_1 \quad X \quad T_2$                                      |
| WHERE sueldo > 10   | $\sigma_{sueldo >10}$                                        |

### Ambiguous  select

Notese que si **en dos relaciones hay columnas con el mismo nombre**, para deshacer la ambiguedad hay que especificar (en algebra relacional, seria renombrar) a que relacion pertenece el atributo al que nos referimos.

**En SQL** lo hacemos colocando el nombre de la tabla seguido de un punto: **escuelas.Escuela**


EJ:
Quiero los nombres de los alumnos, sus colegios y la poblacion del colegio al que van
notese el **uso del punto tanto en SELECT como en WHERE**
```
SELECT DISTINCT Alumno,escuelas.Escuela, Estudiantes 
		FROM Escuelas,Alumnos
		WHERE Alumnos.Escuela = Escuelas.Escuela
```

**Alumnos**

| Alumno  | Escuela    | Promedio |
|---------|------------|----------|
| jorge   | nacional   | 7        |
| juan    | Marin      | 4        |
| lucas   | San juan   | 9        |
| estefan | los olivos | 4        |

**Escuelas**

| Escuela    | Partido       | Estudiantes |
|------------|---------------|-------------|
| nacional   | san isidro    | 210         |
| Marin      | san isidro    | 300         |
| San juan   | san isidro    | 200         |
| los olivos | vicente lopez | 100         |

### Arithmetic en select

Podes usar arithmetica basica en SELECT para calcular cosas en base a los atributos, los operadores permitidos son **+,-,*,/,%**

| Operacion | significado                                                             |
|-----------|-------------------------------------------------------------------------|
| +         | Suma                                                                    |
| -         | Resta                                                                   |
| *         | Multiplicacion                                                          |
| /         | Division                                                                |
| %         | Modulo                                                                  |
| DIV       | Division de integers                                                    |
| -         | Cambio de signo unitario EJ: $-(numero)$ revierte el signo del numero |


Ej:
```
SELECT  (biologia + matematicas + fisica)/3 as promedioGeneral 
		FROM NotasDeMaterias
```

### Distintct

**En relational algebra no hay duplicados**, es decir cuando seleccionar algo que es resultado de un cross product, es muy probable que tengas duplicados.
**En SQL SI hay Ntuples duplicados**, para eliminarlos podes usar el **keyword DISTINCT**

```
SELECT DISTINCT attr1,attr2 FROM tabla1,tabla2 WHERE condicion1 AND condicion2
```




### Like

Hace **string matching con wildcards**.


* **%** - actua un wildcard para cualquier numero de caracteres
	* **'bio%'** - todo string que empieza con "bio" seguido de cualquier string3
	* **'%bio%'** - Todo string que contenga "bio"
* **_** -  actua como wildcard para UN caracter
* **[a-zA-Z0-9]** -  indica grupos de simbolos que pueden ocupar ese caracter
 * **'[a-zA-Z0-9]%'** - Cualquier string que comienze con letras o numeros

**USO:**
```
SELECT alumno FROM alumnos WHERE nombre LIKE 'gus_av%';
```

>**Es imporante notar que:**
* LIKE **no se beneficia del indexado** como los operadores = ó ><
	* Como concecuencia en general es mas lento
* Dependiendo de la implementacion puede ser **case-sensitive**


### As

**Es equivalente al operador $\rho$ de algebra relacional.**

**AS** te permite **renombrar Ntuples y relaciones** para trabajar mas comodamente en una query. 

* **Renombrar atributos**
```
SELECT DISTINCT Promedio AS miPromedio
		FROM Alumnos
```

* **Renombrar tablas**
EJ: Buscar todos los alumnos con el mismo promedio.  
```
--diferencias entre alumnos usando DNI1 < DNI2 para que en el resultado 
--no tengas "alumno1 | alumno2" y despues "alumno2 | alumno1",
--ya que es un cross product con la tabla sobre si misma
SELECT  *
		FROM Alumnos AS A1,Alumnos AS A2
		WHERE A1.DNI < A2.DNI AND A1.Promedio = A2.Promedio 
```



### IN


Se Utiliza dentro de la condicion (**WHERE**) para determinar si un atributo se encuentra (**IN**) ó no se encuentra (**NOT IN**) dentro de un conjunto, que podria ser:

* Otra relacion
	* Tabla
	* Subquery 
``` 
--IN
SELECT continent FROM world 
			WHERE  countryName IN (SELECT name FROM G20Countries)
--NOT IN
SELECT continent FROM world 
  		 WHERE  countryName NOT IN (SELECT name FROM G20Countries)
```
* Un array de valores 
```
--IN
SELECT continent FROM world WHERE name IN ('Argentina', 'Australia')
--NOT IN
SELECT continent FROM world WHERE name NOT IN ('Argentina', 'Australia')
```


### Order by

SQL **no garantiza el orden** y vas a tener diferente orden en diferentes DBMS y tal vez en el mismo DBMS. **Para garantizar orden tener que usar ORDER BY.**

**EJ**: Ordenar los rows:
* Por promedio
* Alfabeticamente si tienen el mismo promedio

```
SELECT DISTINCT Alumno,Promedio 
		FROM Alumnos
		ORDER BY promedio desc, nombre desc 
```


## Set operators entre querys

**Son operacion que:**
* Se hacen **Entre los resultados de dos querys** 
* Se **desprenden directamente de set theory** 
	* Como consecuancia son los mismos operadores usados e algebra relacional
	* bajo el mismo nombre



**Las operaciones son:**
* Union $\Large{\cup }$
* Interseccion $\Large{ \cap}$
* Resta $\Large{  -}$


### Union
**Es el equivalente a $\cup$ en algebra relacional.**

Identico al union de algebra relacional. **Coloca los Ntuples de dos relaciones en una sola relacion**. Naciendo de set theory, este operador **elimina elementos repetidos a menos que uses el operador** `UNION ALL`

| Escuela    | Partido       | Estudiantes |
|------------|---------------|-------------|
| nacional   | san isidro    | 210         |
| Marin      | san isidro    | 300         |
| San juan   | san isidro    | 200         |
| los olivos | vicente lopez | 100         |

| universidad    | Partido       | Estudiantes |
|------------|---------------|-------------|
| UBA	   | CABA    | 200.000           |
| 3 de feb      | CABA    | 1000      |

```
SELECT  Escuela as institucion 
		FROM Escuelas
UNION
SELECT  universidad as institucion 
		FROM universidades
```

| institucion 
|------------|
| nacional   |
| Marin      |
| San juan   |
| los olivos |
| UBA	     |
| 3 de feb   |

### Intersect

**Es equivalente a $\cap$ en algebra relacional.**
Toma la interseccion entre dos relaciones, es decir los Ntuples que estan en ambas relaciones.

**Escuelas mixtas**

| Escuela    | Partido       | Estudiantes |
|------------|---------------|-------------|
| nacional   | San isidro    | 210         |
| Marin      | San isidro    | 300         |
| el huerto  | Vicente lopez    | 200     |
| Media 8    | vicente lopez | 100         |

**Escuelas religiosas**

| Escuela | Partido    | Estudiantes |
|----------|------------|-------------|
| Marin    | San isidro | 300         |
| San juan | San isidro | 500         |
| el huerto   | Vicente lopez    | 200     |

```
SELECT  * FROM EscuelasMixtas
INTERSECT
SELECT  * FROM EscuelasReligiosas
```

| Escuela  | Partido    | Estudiantes |
|----------|------------|-------------|
| Marin    | San isidro | 300         |
| el huerto   | Vicente lopez    | 200|

### Except

**Es el equivalente a la resta $-$ en algebra relacional**

Genera una relacion tomando los Ntuples de la primera relacion y quitandole los Ntuples que tambien existan en la segunda relacion

**Escuelas mixtas**

| Escuela    | Partido       | Estudiantes |
|------------|---------------|-------------|
| nacional   | San isidro    | 210         |
| Marin      | San isidro    | 300         |
| el huerto  | Vicente lopez    | 200     |
| Media 8    | vicente lopez | 100         |

**Escuelas religiosas**

| Escuela | Partido    | Estudiantes |
|----------|------------|-------------|
| Marin    | San isidro | 300         |
| San juan | San isidro | 500         |
| el huerto   | Vicente lopez    | 200     |

```
SELECT  * FROM EscuelasMixtas
EXCEPT
SELECT  * FROM EscuelasReligiosas
```

| Escuela    | Partido       | Estudiantes |
|------------|---------------|-------------|
| nacional   | San isidro    | 210         |
| Media 8    | vicente lopez | 100         |


## Sub querys 


Se trata de utilizar**querys anidadas** . Se pueden usar en:

* **SELECT**
Una sub-query en SELECT tiene que devolver **UN SOLO RESULTADO**, el cual es agregado como atributo al resultado de la query
```
    SELECT column1 = (SELECT column-name FROM table-name WHERE condition),
           column2
      FROM table-name
     WHERE condition
```

* **FROM**
El resultado de una sub-query colocada en el FROM se utiliza como una tabla normal al realizar la query. Es decir, **la query es realizada sobre el resultado de la sub-query.**
```
SELECT promedio, nombre 
FROM (SELECT (mate + bio+lengua)/3 AS promedio, nombre FROM notas) AS promedios
WHERE promedio > 4
```

* **WHERE**
Una sub-query en WHERE se utiliza para traer datos adicionales con los que comparar los atributos de las tablas de la query principal, generalmente con el fin de hacer alguna comparacion.

``` 
SELECT name, continent FROM world 
     WHERE continent IN (
	 SELECT continent FROM world WHERE name in ('Argentina', 'Australia')
	 )
```


Una sub-Query **puede devolver uno o mas valores**, dependiendo del numero de valores que devuelva se pueden usar operadores distintos

* **Un valor**
	* **=, <,>,<>**
	Periten comparar un valor con el valor de la sub--query
	* **EXISTS**
	Permite saber si la query no devolvio ningun resultado
* **Multiples valores**
	* **ALL, ANY**  
	Permiten comparar un valor con multiples valores de la sub-Query
	* **IN** 
	Permite ver si un valor esta dentro de los valores devueltos por la sub-query
	
	

### IN

Podes usar **IN** para ver si un atributo esta dentro del resultado de una sub-query 
Tambien podes usar **NOT IN** para verificar que el atributo NO forma parte de la sub-query

* **IN** 
``` 
SELECT continent FROM world 
   WHERE  countryName IN (SELECT name FROM G20Countries)
```
* **NOT IN**
``` 
SELECT continent FROM world 
   WHERE  countryName NOT IN (SELECT name FROM G20Countries)
```



### ALL, ANY

Permiten comparar un valor con varios valores (por ejemplo aquellos devueltos por una sub-Query. **Evalua a TURE si la sub-query no devuelve ROWS**

* **ALL**
Permite usar los operadores de comparacion (=,<,>) sobre una lista de elementos para encontrar el elemento que cumpla la comparacion para **TODOS los resultados del sub-query**
``` 
--Seleccionar el pais con mayor GDP de cada continente
--Hay que verificar que el GDP no sea null.
SELECT continent, name, gdp  FROM world AS w1
			WHERE gdp >= 
			ALL(
				SELECT gdp FROM world 
				WHERE w1.continent = continent AND gdp IS NOT NULL
			)
```
* **ANY**
Igual a ALL; pero alcanza con que la comparacion sea exitosa con **UN solo resultado de la sub-query**
``` 
--Seleccionar el aquellos alumnos con aplazos y su DNI (que no esta en la tabla de
-- aplazos
SELECT alumno, DNI  FROM alumnos AS w1
			WHERE alumno = ANY(
				SELECT alumno FROM aplazos 
				WHERE w1.DNI = DNI
			)
```


>**Nota:**
>ANY y ALL **NO** añaden poder expresivo, siempre se pueden escribir en terminos de **Exists y NOT Exists**


### EXISTS

Permite condicionar una query con el hecho de que otra no devuelva ningun resultado

EJ: encontrar alumnos con el mismo apellido
```
SELECT nombre, apellido FROM alumnos AS a1
 		WHERE EXISTS (
						SELECT apellido FROM alumnos AS A2
						WHERE a1.apellido = A2.apellido
						AND a1.DNI != A2.DNI
					)
```

## JOINs

Los JOINs en SQL son bastante analogos a sus contrapartes en **algebra relacional**
**Se utilizan en la clausula FROM para combinar tablas**
Los JOINS no añaden poder expresivo, se pueden llegar a los mismos resultados con el cross product y las condiciones del WHERE clause.


| SQL Command                                 | Relational algebra operator  | Aclaraciones                                               |
|---------------------------------------------|------------------------------|------------------------------------------------------------|
| $R_1$ NATURAL JOIN $R_2$                | $R_1 \bowtie R_2$          | natural join comun                                         |
| $R_1$ INNER JOIN $R_2$ USING $attr1$  | $R_1 \bowtie R_2$          | Natural join con lista explicita de columnas/atributos     |
| $R_1$ INNER JOIN $R_2$ ON $\theta$    | $R_1 \bowtie_\theta R_2$   | Theta join comun                                           |
| $R_1$ LEFT\ RIGHT\FULL OUTER JOIN $R_2$ | $R_1 \bowtie_{\theta} R_2$ | Theta join, Non matching elements añadidos c/ NULL padding |

>NOTAS:
> $\theta$ es una condicion. EJ: `Almuno LIKE 'jorge%'`


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/SQL_JOINS.png)




### INNER JOIN ON

**En algebra relacional es el Theta join:**
$R_1 \bowtie_\theta R_2$ 

**En SQL:**
$R_1 \quad \text{INNER  JOIN} \quad R_2 \quad \text{ON} \quad \theta $


![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/inner_join.png)


**EJEMPLO:**
En este caso una relacion tiene el atributo `DNI` y la otra `DNIalumno`, y queremos un Ntuple con los datos de ambas tablas para cada alumno (osea con el mismo DNI). Entonces usamos el DNI como la condicion $\theta$

```
--Usando el where clause
SELECT alumno, promedio FROM alumnos, notas WHERE alumno.DNI=notas.DNIalumno
--Usando INNER JOIN USING
SELECT alumno, promedio FROM alumnos INNER JOIN notas USING dni
```

**TABLAS:**

| DNI        | Alumno       |
|------------|--------------|
| 20.200.200 | Jorge hernan |
| 37.256.654 | Hector hugo  |

| DNI        | biologia          | matematicas | quimica | fisica | promedio |
|------------|--------------|-------------|---------|--------|----------|
| 20.200.200 | 6 | 6           | 6       | 6      | 6        |
| 37.256.654 | 8  | 8           | 8       | 9      | 8.75     |

**RESULTADO:**

| alumno       | promedio |
|--------------|----------|
| Jorge Hernan | 6        |
| Hector Hugo  | 8.75     |

>En general todo lo que podes poner en ON, podes ponerlo en WHERE.
>Colocar las condiciones que son particularmente del JOIN en ON muchas veces asisite
>Al query processor a encontrar la forma optima de realizar el query.


### NATURAL JOIN

NATURAL JOIN **toma las columnas (atributos) con el mismo nombre y las usa como condicion para el JOIN** de la misma manera que lo hace el natural join de algebra lineal.
Ademas, al igual que en algebra lineal, **Elimina los duplicados**

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/inner_join.png)


```
--Usando el where clause
SELECT alumno, beca FROM alumnos, notas WHERE alumno.DNI=becados.DNI
--Usando NATURAL JOIN
SELECT alumno, promedio FROM alumnos NATURAL JOIN becados
```

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/natural_join.jpg)

### INNER JOIN USING 

Es muy similar al NATURAL JOIN y al THETA JOIN, **es mas un short-hand que otra cosa**.
Lo usas cuando queres hacer un natural join pero con atributos puntuales.

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/inner_join.png)


```
--Usando el where clause
SELECT alumno, beca FROM alumnos, notas WHERE alumno.DNI=becados.DNI
--usando NATURAL JOIN
SELECT alumno, promedio FROM alumnos NATURAL JOIN becados
--Usando INNER JOIN USING
SELECT alumno, promedio FROM alumnos INNER JOIN becados USING DNI
```


### LEFT\ RIGHT\FULL OUTER JOIN

#### LEFT y RIGHT OUTER JOIN

Son similares al INNER JOIN, pero ademas de devolver los mismos resultados devuelve los valores de la tabla **izquierda o derecha** que **no cumplen con la condicion**, y **los atributos de la otra tabla para estos valores tendran el valor NULL.**

Usar LEFT o RIGHT es lo mismo que invertir el orden de las tablas
$R_1 \text{ left outer } R_2 \text{ ON } \theta = R_2 \text{ right outer } R_1 \text{ ON } \theta$

No añade poder expresivo, se puede hacer con otros operadores de SQL.

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/left_y_right_outer_join_BlNBTGy.png)

**EJEMPLO:**

* Equivalente sin usar el operador JOIN:
```
SELECT alumno, promedio FROM alumnos, notas WHERE alumno.DNI=notas.DNIalumno
UNION
SELECT alumno, NULL FROM alumnos WHERE dni NOT IN (SELECT dni FROM notas)
```

* Usando JOIN:
```
SELECT alumno, promedio FROM alumnos LEFT OUTER JOIN notas USING dni
```

**TABLAS:**

| DNI        | Alumno       |
|------------|--------------|
| 20.200.200 | Jorge hernan |
| 37.256.654 | Hector hugo  |
| 38.256.654 | Pablo hernan |

| DNI        | biologia          | matematicas | quimica | fisica | promedio |
|------------|--------------|-------------|---------|--------|----------|
| 20.200.200 | 6 | 6           | 6       | 6      | 6        |
| 37.256.654 | 8  | 8           | 8       | 9      | 8.75     |
| 27.256.654 | 8  | 8           | 8       | 9      | 8.75     |

**RESULTADO:**


| alumno       | promedio |
|--------------|----------|
| Jorge Hernan | 6        |
| Hector Hugo  | 8.75     |
| Pablo hernan | NULL     |

#### FULL OUTER JOIN

Es la suma de los resultados del LEFT OUTER JOIN y el RIGHT OUTER JOIN eliminando los duplicados.

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/full_outer_join.png)

**EJEMPLO:**
* Equivalente **sin usar** el operador JOIN:
```
SELECT alumno, promedio FROM alumnos, notas WHERE alumno.DNI=notas.DNIalumno
UNION
SELECT alumno, NULL FROM alumnos WHERE dni NOT IN (SELECT dni FROM notas)
UNION
SELECT NULL,promedio FROM notas WHERE dni NOT IN (SELECT dni FROM alumnos)
```
* Equivalente en LEFT/RIGHT OUTER JOIN
```
SELECT alumno, promedio FROM alumnos LEFT OUTER JOIN notas USING dni
UNION
SELECT alumno, promedio FROM alumnos RIGHT OUTER JOIN notas USING dni
```

* Usando FULL OUTER JOIN :
```
SELECT alumno, promedio FROM alumnos FULL OUTER JOIN notas USING dni
```

**TABLAS:**

| DNI        | Alumno       |
|------------|--------------|
| 20.200.200 | Jorge hernan |
| 37.256.654 | Hector hugo  |
| 38.256.654 | Pablo hernan |

| DNI        | biologia          | matematicas | quimica | fisica | promedio |
|------------|--------------|-------------|---------|--------|----------|
| 20.200.200 | 6 | 6           | 6       | 6      | 6        |
| 37.256.654 | 8  | 8           | 8       | 9      | 8.75     |
| 27.256.654 | 8  | 8           | 8       | 10      | 9     |

**RESULTADO:**


| alumno       | promedio |
|--------------|----------|
| Jorge Hernan | 6        |
| Hector Hugo  | 8.75     |
| Pablo hernan | NULL     |
| NULL  	   | 9        |

## Funciones de agregacion 

Son funciones que, a partir de una serie de resultados, computa un solo resultado (Similar al _reduce_ de lodash.js o underscore.js)

Tablas de ejemplos:

| DNI        | biologia          | matematicas | quimica | fisica | promedio |
|------------|--------------|-------------|---------|--------|----------|
| 20.200.200 | 6 | 6           | 6       | 6      | 6        |
| 37.256.654 | 7  | 8           | 8       | 9      | 8.75     |
| 27.256.654 | 8  | 8           | 8       | 10      | 9     |
| 26.256.654 | 9  | NULL          | 8       | 10      | 9     |
#### AVG
Calcula el promedio de los valores obtenidos de una expresion

```
--El promedio de las notas de matematicas
SELECT AVG(matematicas) --(8+6+6)/3
FROM notas;
```

#### MAX, MIN
Obtiene el valor maximo o minimo de una serie de valores
```
--El promedio mas alto de matematicas
SELECT MAX(matematicas) --8
FROM notas;
```
#### COUNT

Cuenta la cantidad de valores devueltos. 
* Si se refiere a un atributo particular, **ignora valores NULL**
```
--Alunos con notas de matematicas
SELECT COUNT(matematicas) FROM notas; --3 (8,8 y 6)
--Notas diferentes de matematicas
SELECT COUNT(DISTINCT matematicas) FROM notas; --2 (8 y 6)
```
* Si se refiere a rows, **NO IGNORA VALORES CON NULL**
```
--Alunos con notas de matematicas
SELECT COUNT(*) --4
FROM notas;
```

#### SUM
El promedio de las notas de matematicas

```
--El promedio de las notas de matematicas, hecho con SUM y COUNT
SELECT SUM(matematicas)/COUNT(matematicas) --(8+8+6)/3
FROM notas;
```

### Group By

Si usas una funcion de agregacion, GROUP BY te permite dividir los resultados en grupos a partir de un atributo.

**No añade poder expresivo**

```
--La cantidad de alumnos que rindieron quimica, separados por promedio general
SELECT COUNT(quimica) AS AlumnosQueRindieronQuimica, Promedio AS conPromedioGeneral
FROM notas
GROUP BY promedio
```

| AlumnosQueRindieronQuimica | conPromedioGeneral |
|----------------------------|-----------------|
| 1                          | 6               |
| 1                          | 8.75            |
| 2                          | 9               |


**Consideraciones:**
* Si pedis**un atributo que no es una agregacion**, te **devuelve uno aleatorio** dentro de las posibles respuestas
```
--La cantidad de alumnos que rindieron quimica, separados por promedio general
SELECT COUNT(quimica) AS AlumnosQueRindieronQuimica,
		Promedio AS conPromedioGeneral,
		dni
FROM notas
GROUP BY promedio
```
Fijate como tira UNO de los DOS posibles DNIs en la ultima linea.

| AlumnosQueRindieronQuimica | promedioGeneral | DNI        |
|----------------------------|-----------------|------------|
| 1                          | 6               | 20.200.200 |
| 1                          | 8.75            | 37.256.654 |
| 2                          | 9               | **26.256.654** |

* Si haces un GROUP BY de **dos columnas o mas**, se formaran grupos para cada conjunto de columnas que compartan el mismo valor (ninguna es descartada, se consideran los conjuntos de 1 row que no sea igual a ningun otro)

### Having 

Te permite colocar condiciones en los grupos generados con GROUP BY, esas condiciones se aplican a todos los **Ntuples que son condensados en cada grupo**

**No añade poder expresivo.**

```
--El promedio de notas de biologia, agrupado por promedios generales,
--Excluyendo los que se sacaron 7 o menos en matematicas
SELECT AVG(biologia), promedio
FROM notas
GROUP BY promedio
HAVING matematicas  > 7
```
| biologia | Promedio |
|----------|----------|
| 7        | 8.75     |
| 8.5      | 9        |


## Comportamiento de NULL  

NULL implica que un valor **no fue definido**, generalmente los DBMS permiten expresar que **un atributo puede o no tener permitido tener valor NULL**

Entonces NULL **no se comporta como otros valores**, no es mayor o menor a ningun otro valor, no puede ser ordenado, etc

Tabla de ejemplo:

| DNI        | biologia          | matematicas | quimica | fisica | promedio |
|------------|--------------|-------------|---------|--------|----------|
| 20.200.200 | 6 | 6           | 6       | 6      | 6        |
| 37.256.654 | 7  | 8           | 8       | 9      | 8.75     |
| 27.256.654 | 8  | 8           | 8       | 10      | 9     |
| 26.256.654 | 9  | NULL          | 8       | 10      | 9     |

* Null no se compara con los operadores **mayor >** ni **menor <**, solo se compara con **IS NULL** ó  **IS NOT NULL**
```
-- el valor NULL no es ni mayor ni menor ni igual a 5
SELECT count(*) FROM notas WHERE matematicas > 5 OR matematicas =< 5 --3
```
```
-- Aca si se toma en cuenta los rows con valor null
SELECT count(*) FROM notas 
	WHERE matematicas > 5 
	OR matematicas =< 5 
	OR matematicas IS NULL  --4
```
* Los agregadores muchas veces **no toman e cuenta NULL** (DEPENDE DEL DBMS) 
```
-- los agregadores muchas veces no toman en cuenta los valores null
SELECT count( DISTINCT matematicas) FROM notas --3 en vez de 4
```

## INSERT, UPDATE, DELETE

### Delete

Es el comando mas simple de todos, el resultado de la query es borrado de la base de datos
```
-- Borra los rows con notas de matematicas mayores a 5
DELETE FROM notas WHERE matematicas > 5 
```

### Insert

Hay dos formas de incertar Ntuples en una relacion, 
* **Mencionando directamente los valores del Ntuple**
```
-- Borra los rows con notas de matematicas mayores a 5
INSERT INTO notas VALUES("38.156.654",5,8,7,6.66) 
```
* **Obteniendo los Ntuples a incertar como resultado de una query**
```
-- Agregar a los alumnos a la tabla de notas, sin ninguna nota 
INSERT INTO notas 
	SELECT DNI, null, null, null, null 
	FROM alumnos 
	WHERE alumnos.DNI NOT IN (SELECT dni FROM notas)
```


### UPDATE

Permite cambiar los valores de un Ntuple en particular

```
-- Aprobar a los alumnos con promedio mayor a 7
UPDATE  alumnos SET aprobado = true
	WHERE (SELECT promedio FROM notas WHERE alumnos.dni=notas.dni)>7
```


## Funciones utilitarias

Son funciones de conveniencia que suelen estar embebidas en las implementaciones de SQL

* **ABS(flot)** - Devuelve el valor absoluto de un numero 
* **LIMIT num** - Limita la canitdad de resultados de una query
`SELECT column_name(s) FROM table_name WHERE condition LIMIT number `
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMxOTc4NDIzOCw3NDQ5MzM1MTBdfQ==
-->