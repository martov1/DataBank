







me quede en generic classes


### types basicos

* **Number y string**
Podes declarar un number o un string asi
`let mystring :string = 'hola'`
`let myNumber :number = 132`

* **Array**
Podes declarar un array de un tipo en particular asi
`let myArray :number[] = [1,2,3,4]`
* **Any**
Es un tipo que es compatible con cualquier tipo
* **Tuples**
Son array predefinido de cierta forma
`let direccion:[string,number]=['españa',542]`
* **enum**
Asigna un numero a una cierta propiedad a partir de cero
Podes asignar manualmente los numeros de cada propiedad tambien
````ts
enum pais {argentina,uruguay, brazil}
let miPais:pais =pais.argentina
console.log( miPais) // da 0
````
* **mezcla de types**
`let edad: Number | String //numero o string`


## types en objects

Podes indicar que types tendra un objeto
````ts
let juan:{name:string, age:number} = {name:juan,age:25}
````

Podes guardar estas definiciones e un alias
````ts
type Persona ={name:string, age:number}
let juan:Persona = {name:juan,age:25}
````

Tambien podes indicar los types de las keys y/o propiedades, aunque no sepas cuales van a ser

````ts
type Persona ={[key: string]: { prop: number }}
let juan:Persona = {name:juan,age:25}
````

## Type casting

podes indicarle a typescript que un objeto es de cierto type en lugar del que typescript supone, de esta forma

````ts
myObject = <TypeA> otherObject;     // using <>
myObject = otherObject as TypeA;    // using as keyword
````


## Funciones

#### Parametros y retorno
Podemos asignar el type que la funcion consume y devuelve

````ts
//toma numeros y devuelve un string
funcion hola(param1: number, Param2: number) :string 
````

o que **no devuelve nada**
````ts
funcion hola() :void //no devuelve valores
````




#### funciones como types

Podes asignar un esqueleto de funcion como type
Por ejemplo aca decimos que la variable myfunction**solo puede contener funciones que tengan dos parametros numericos y devuelvan un string.**
Si te fijas como esta armado angular esto se usa mucho, Ej: pedir que una funcion devuelva un observable
````ts
ley myfuncion:(param1: number, Param2: number) =>string 
````

#### Default parameters

Podemos colocar parametros default en caso de que no se coloque nada
````ts
ley myfuncion = function (param1: number= 10):string { console.log(param1)}
myfunction() //devuelve 10
````



## Classes

### Definicion
Las variables de las clases son **publicas por default**

````ts
class Person {
	name: string, //public by default
	public name2: string,
	private name2: string, //variable privada
	protected name3: string, // accesible a las clases que heredan esta clase
	public algo: Number = 37 //podes inicializar cosas ahi nomas 
	public opcional?: Number, //podes especificar propiedades opcionales
	
	//si poner public en un parametro del constructor se genera una variable
	//pblica nueva con ese nombre en esa instancia de la clase
	constructor(name: string, public age: Number){
	this.name = name
	}
	
	private hola():void{ 	//los metodos pueden ser privados o protected tambien
	console.log("hola");
	}
}

let person = new person("maxi",23)
````

### Herencia


podes hacer que una clase herede todo lo de otra usando **extends**

Para extender su **constructor** tenes que crear uno nuevo y **llamas al viejo constructor** usando `super()`

````ts
class Empleado extends Person{
salario : number
	consturctor(name:string, age:number, salario: number){
		super(name,age)
		this.salario= salario
	}
}

let jorge = new Empleado ("jorge", 23)
````

### getter y setter

hay getters y setters **nativos** que podes usar

````ts
class Empleado extends Person{
_salario : number
	consturctor(name:string, age:number, salario: number){
		super(name,age)
		this._salario= salario
	}
	
	set salario(valor){
	console.log("algo se ejecuta")
	this.salario = valor
	}
	
	get salario(valor){
	return this.salari
	}
}
let jorge = new Empleado ("jorge", 23, 5500)
jorge.salario = 10  //algo se ejecuta
````

### metodos y variables estaticas

Son metodos y variables que **se pueden acceder sin instanciar la clase**

### Abstract classes y methods

Son clases que **no pueden ser instanciadas**, estan hechas para **ser heredadas y que sus herederos sean instanciados**

los **abstract methods** son como declarar interfaces, indicas como se debe ver el metodo pero **le dejas la implementacion a las clases que hereden esta clase**
````ts
abstract class Proyecto {
	name: string, //public by default
	name2: string,
	
	//los herederos DEBEN implementar un metodo realizarTrabajo 
	//que toma un string y devuelve void
	abstract mostrarBudget(trabajo:string):void
}

class ITProject extends Proyect{
//Si no creas esta funcion entonces hay error
 mostrarBudget= function(trabajo:string){
 hacer cosas
 }
}
````

### Frozar singleton

Podes forzar a una clase a ser un singleton 

````ts
abstract class MySingleton {
	//tenes una variable estatica de clase instance donde vas a guardar tu instancia
	private static instance: miInstancia
	
	//El constructor es privado, osea que no lo podes llamar de afuera
	//osea que nunca vas a poder instanciar esta clase de afuera
	private constructor(){}
	
	//si no hay una instancia en la variable instance, la creas y la devolves
	//si ya existe una entonces la devolves. LISTO!, ya tenes un singleton
	static getInstance(){
	if (!miInstancia.instance){
		miInstancia.instance = new MySingleton()
		}
	else{
		return miInstancia.instance
		}
	}
}
````



## Modules


Un modulo es simplemente **un archivo con exports**

````ts
//modulo donde exportas
let decirAlgo = function (mensaje: string) {
	console.log(mensaje)
}
let darError = function () {
	throw("error")
}

export decirAlgo;
export darError
````

Podes importar las cosas de un modulo en otro

````ts
//importar directamente cosas especificas
import {decirAlgo,darError} from 'modulos/miModulo' 
//importar todo el modulo en un alias
import * as miLindoMoudlo from 'modulos/miModulo'
miLindoMoudlo.decirAlgo("hola")

````

## Interfaces

Definir una interface

````ts
interface NamedPerson {
	firstName: string,	//propiedad requerida
	age?: number, 		//propiedad opcional
	[propName: any]:any //aceptar otras propiedades sin dar error
	
	deciralgo(algo: string): void
}
````


uso basico
`let jorge:NamedPerson ={blablabla};

Uso en clases

````ts
class Empleado implements NamedPerson{
aca implementas las cosas requeridas por la interfaz
}
````

pueden ser heredadas
````ts
interface Empleado extends NamedPerson{
	cosas adicionales
}
````

Interfaz de un objeto complejo con interfaces anidadas
````ts
interface Land {
    id: number,
    direccion: string,
    metrosCuadradosVendibles: string,
    zonificacion: string,
    descripcion: string,
    prioridad: number,
    neighbourhood_id: number,
    fot: string,
    frente: string,
    fondo: string,
    imagenes: LandImage[],
    barrio: Barrio
}

interface LandImage {

    posicion: number,
    url: string,
    descripcion: string
}

interface Barrio {
    barrio: string,
    ciudad: string,
    barrioId: number,
    cityId: number

}
````


## Generics

le indica a typescript que **hay cosas que seran del mismo type** pero que **no sabes que type sera**. typescript va a asegurarse de que cuando uses un type puntual esta restriccion se cumpla.

#### En Funciones
En este ejempo **T** es un **type generico**, ahora typescript puede **rastrear** que tipo de salida va a haber basandose en el type de entrada.
````ts'
//La entrada es de type T, por ende la salida en este caso sera rastreada como
//de type T por que devolvermos el argumento type T
let myFunction = function<T>( data: T){
	return data
}

//Tambien pude ser un array de elementos de type T
let myFunction = function<T>( data: T[]){
	return data
}

//tambien podes especificar el type de retorno, en este caso especificas que es de type T
let myFunction: <T>(daya:T) => T = function( data){
	return data
}
````

#### En Arrays

Array es un type generico por default.
````ts
let myArray : Array<number> = [1,2,3]
````

#### En Clases

Te sirve para indicar que **varias cosas seran del mismo type** pero **no sabes exactamente que type va a ser ese**
Ejemplo de uso de generics en clases:

````ts
class MiClase <T>{
	unaVariable: T;
	otraVariable:T;
	hacercosas():number{
		cosas
	}
}

let miInstancia = new MiClase();
miInstancia.unaVariable =10; 		//ahora "T es number
miInstancia.otraVariable ="jorge"; //ERROR: las variables tienen que ser del mismo type
````

#### Generics con restricciones

Podes restringir a que types se le permite ser al generic type
````ts
//Una clase donde T puede ser un numero o un string.
class MiClase <T extends number | string>{
	unaVariable: T;
	otraVariable:T;
	hacercosas():number{
		cosas
	}
}
````

#### Multiples generics

Podes restringir a que types se le permite ser al generic type
````ts
//Una clase donde T puede ser un numero o un string.
class MiClase <U,T extends number | string,G extends number|boolean>{
	unaVariable: T;
	otraVariable:T;
	otra2Variable:U;
	otra3Variable:U;
	otra4Variable:G;
	otra5Variable:G;
	otra6Variable:G;
	hacercosas():number{
		cosas
	}
}
````

## Decorators

Es una forma de añadir funcionalidad a una instancia de clase mediante una funcion que llama a su constructor

````ts
//es una funcion que toma como unico parametro el contructor de la clase que "decora"
function miFuncionDecoradora(constructor: function){
	//hago cosas 
}

@miFuncionDecoradora			//aca la funcion decoradora se ejecuta
class MiClase{
	//mi clase con mis cosas
	constructor(){
	}
}


````

### Factories

Son funciones que **devuelven decorators**, pero como concecuencia pueden tomar otros parametros que no sean el constructor

````ts
//es una funcion que toma como unico parametro el contructor de la clase que "decora"
function miFuncionDecoradora(constructor: function){
	//hago cosas, por ejemplo hago un logging
}

function miFactory(quieroLogguear: boolean){
	//decido si quiero logguear o no cosas
	if (quieroLogguear){return miFuncionDecoradora}
	else{ return null}
}

@miFactory(true)			//aquiero loguear, el factory devolvera miFuncionDecoradora
class MiClase{				//como decorator
	//mi clase con mis cosas
	constructor(){
	}
}


````
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQxNDI2MDkyNF19
-->