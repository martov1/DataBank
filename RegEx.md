

**Me quede en grouping**

# Lo basico

Las regular expressions van entre `/`

```
/Mi regular expression / flag
```

## Busqueda de strings

### String exacto
Podes buscar un string simplemente colocandolo en la regular expression, es **CASE SENSITIVE**
```
/jorge/ flag
```

### Characters en  sets

Te permite matchear usando un patron con un caracter que esta dentro de un conjunto.

#### Character en set especifico
Busco todas las instancias de "te" con y sin acento, ya que busco usando el character set $[e,é]$



```
/t[e,é]/ g
```
>Notese que La posicion del conjunto indica la posicion del caracter buscado, osea que "et" no matchea

#### Excluir si tiene character en set especifico
Podes buscar todo lo que no matchee un caracter en un set especifico, lo haces con el operador $\land$ 

EJ: matchea _pato_ y _geto_  pero no _gato_
```
/[^ga]to/ g
```

### Sets predefinidos:
Tenes una serie de sets predefinidos conocidos como **ranges**

* **[a-z]** - Todas las letras minusculas 
	* **[c,z]** - Todas las letras entre c y z 
* **[A-Z]** - Todas las letras en mayusculas
* **[A-Za-Z]** - Todas las letras mayusculas y minusculas
* **[0-9]** - Todos los numeros
	**[5-9]** - Todos los numeros entre 5 y 9

### Caracteres que se repiten (quantifiers)

#### Repeticion una cantidad de veces indefinida:
Si queres buscar caracteres que 
* aparecen una o multiples veces en sets podes indicarlo usando el signo **+**
* Aparecen zero o una vez **?**
* Aparecen cero o multiples veces **\***

**EJ:** Todo substring que se componga de numeros 
```
/[0-9]+/g
```
#### Repeticion una cantidad de veces definida:
**Ej:** Una serie **8 caracteres** numeros entre el 0 y el 9
```
/[0-9]{8}/g
```

**EJ:** todas las palabras en minusculas de **entre 5 y 8 caracteres**
```
/[a-z]{5,8}/g
```

**EJ:** todas las palabras en minusculas de **mas de 8 caracteres**
```
/[a-z]{8,}/g
```

**EJ:** todas las palabras en minusculas de **menos de 8 caracteres**
```
/[a-z]{0,8}/g
```

### Lazy vs greedy search

Podes hacer que un cuantificador sea lazy colocandole un **?**

 * **Lazy** busca el string mas corto
	* Ej: matchel el primer **<** con el primer **>** que encuentra  
	*	**<.+?>** matchea **< h1>** hola **< h1>**
 * **greedy** busca el string mas largo
	 * Ej: Matchea el primer **<** con el ultimo **>** que encuentra 
	*	**<.+>** matchea **< h1>hola< h1>** 

## Flags

Los flags determinan el comportamiento de la busqueda del regular expression

* **sin flag** - Matchea el primer resultado y lo devuelve
* **g** - Global, no detiene la busqueda despues de encontrar el primer resultado. Si no esta activa solamente devuelve el primer resultado
* **i** - Insensitive, hace que la busqueda no sea case sensitive
* **s** - Single line, Trata el string como si fuera una sola linea
* **m** - Trata el string como teniendo varias lineas



**Ejemplo:**
```
/jorge/gi
```

## Escaping characters

El scape character de regEx es `\`, te permite usar meta-characters
buscar un punto
```
/\./
```
 
## Meta-characters



* **\d** - digito, es lo mismo que poner **[0-9]**
* **\w** - Word character, equivalente a **[a-zA-Z0-9_]**
* **\s** - Space, matchea spaces, tabs, ect
* **\t** - Solo tabs
* **\n** - New line
* **\r** - carriage Return
* **\f** - Form feed  

## Special characters

>Podes escapar estos special characters con \\
>EJ: \\?

* **?** - Hace que el caracter que lo precede sea opcional (aparece cero o una vez).
	* **hello?** matchea **hell** y **hello** 
* **.** - Machea con cualquier caracter excepto new line
* **\*** - el caracter que lo precede aparece cero o mas veces
* **+** - El caracter que lo precede aparece una o mas veces
* **|** - Matchea la expresion de la derecha **o** la de la izquierda
	* **p|jancho** matchea "p" o "jancho" 
	* **(p|j)ancho** matchea "pancho" o "jancho"
	* **(juan|jorge|julian) el jefe** matchea 
		* "juan el jefe"
		* "jorge el jefe" 
		* "julian el jefe"


## Boundaries

### Starting and ending patterns

Para indicar que buscas un patron
*  Al **comienzo del string** usas el caracter $\land$ **ANTES** del patron
*  Al **final del string** usas el catacter **$** al **FINAL** del patron

**EJ:** Buscar un string que comienza con 5 letras minusculas
```
/^[a-z]{5}/
```

**EJ:** Buscar un string que termina con 5 letras minusculas
```
/[a-z]{5}$/
```

**EJ:** Buscar un string que comienza y termina con 5 letras minusculas
```
/^[a-z]{5}$/
```

### Word boundaries

Indica el comienzo o final de un word boundary, es decir el lugar donde comienza o termina una palabra.
Esto se detecta cuando se juntan un caracter \w y un caracter [^ \w], es decir , **guiones, espacios, tabs, ete**

**Usando \b :**

ej:  `/   \bPalo\b /`

unPalo **Palo** Palote

**Mientras que si no usaras \b :**
ej:  `/   Palo /`

un**Palo** **Palo** **Palo**te


## Grouping

Agrupas cosas en regex con parentesis

Agrupas "pa"
`/   (Pa)?lo /`

matchea **palo** y  **lo** 

Los grupos quedan **automaticamente numerados de izquierda a derecha**

`/   (\d+)-(\d{4})-(\d{4}) /`
Matchea todo: **011-4544-3233**

**Grupo 1**: 011
**Grupo 2**: 4544
**Grupo 3**: 3233

Si quisieras los matchear los numeros donde los primeros 4 digitos son iguales a los segundos 4 digitos.

`/   (\d+)-(\d{4})-\2 /`
matchea: **011-4545-4545**

## Lookaround

Lookaround te permite buscar elemenstos cuando estan antes o despues de una cierta palabra o patron sin necesidad de matchear esa palabra o patron.

### Positive Look-ahead

Queres buscar algo que **va despues** de una cierta palabra o patron

 **se hace asi:**
 `/   palabra(?=busqueda) /`

**EJ: quiero buscar todos los precios:**
 Busco todos los digitos que son seguidos por un espacio y el signo pesos.
 `/   \d+(?=\s$) /`
 * **100** $
 * el precio es **500** $
   
 ### Negative Look-ahead
Queres buscar algo que **no va despues** de una cierta palabra o patron

 **se hace asi:**
  `/   palabra(?!busqueda) /`
  
**EJ: Quiero buscar todos los numeros que no son precios**
 Busco todos los digitos que NO son seguidos por un espacio y el signo pesos.
 `/   \d+(?!$) /`
 * el **22**/**10** el precio aumenta a 100 $
 * La entrada para ver **300** esta 140 $

## Positive look-behind

Cuando queres matchear un elemento **cuando una cierta palabra o patron viene ANTES**

 **se hace asi:**
  `/   (?<=busqueda)palabra /`

**EJ: Quiero buscar todos los modelos de celular marca samsung**
 Busco aquella palabra precedida por "samsung"
  `/ (?<=samsung\s)\b\w+\b/`
 * samsung **galaxy**
 * samsung **pocket**
 * nokia 1100
 
 ## Negative look-behind

Cuando queres matchear un elemento **cuando una cierta palabra o patron NO viene ANTES**


 **se hace asi:**
  `/   (?<!busqueda)palabra /`

**EJ: Quiero buscar todos los modelos de celular que NO son marca samsung**
 Busco aquella palabra precedida por "samsung"
  `/ (?<!samsung\s)\b\w+\b/`
 * samsung galaxy
 * samsung pocket
 * nokia **1100**
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg2MDQ3Nzg0NSwtOTY1MTM5XX0=
-->