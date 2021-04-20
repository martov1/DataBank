
**Design patterns**
https://www.youtube.com/watch?v=vNHpsC5ng_E&list=PLF206E906175C7E07




## OOP

### Criterios generales
* Los objetos son instanciados desde clases y tienen constructores
* **las propiedades de los objetos son privadas**
	* No se puede cambiar las variables de los objetos sino mediante **getters** and **setters**

### Herencia
* Las clases **heredan** **propiedades** y **metodos** de otras clases
* Regla **"is a"** sirve para determinar si una clase hereda de otra
	* **cat is an animal**, cat hereda de animal



### Polymorfismo

Polimorfismo es **proveer de una interfaz unica  a  objetos de diferente tipo**, se da generalmente cuando una clase **sobreescribe un metodo que heredó**

Esto implica tambien que **perro** y **gato** no solo son sus propias clases sino que tambien son de tipo **animal**, ya que heredan una interfaz aunque su implementacion sea diferente.

**Ejemplo:**
* **animal.moverse()** puede tener una implmentacion x
	* **Perro.moverse()** puede usar la misma implementacion que animal (la hereda)
	* **pajaro.moverse()** heredara el metodo pero lo sobreescribira para poder volar en vez de caminar

### Clases abstractas y interfaces

**Abstract class:**
Una clase abstracta es una clase que no puede ser instanciada por si misma, sino que esta hecha para ser un blueprint de otras clases que la extenderan.

Las clases abstractas pueden tener metodos , metodos estaticos y etodos abstractos (metodos sin una implementacion)

El compiler demandara que todos los metodos de la clase abstracta sea implementados en la clase que hereda

**Interface:**
* Es un **abstract class** en la que todos los metodos son **abstract methods**
* Una clase puede implementar infinitas interfaces.



## Strategy pattern (ej passport.js)
El strategy pattern se trata de **separar una familia de  algoritmos (strategies)** de **la clase que los va a utilizar(client)** para que el algoritmo sea **intercambiable** en runtime.

Por ejemplo en la clase **Encriptador**, los algoritmos (estrategias) de encriptacion tendrian cada uno una clase separada (**AES**, **RSA**, **DES**).


 ```C#
 //Declaras la estrategia (RSA,AES,etc) del encriptador,
 // cuya logica esta en su propia clase
 Encriptador.estrategiaDeEncriptacion = new AES();
 //Ahora el metodo encriptar internamente usa
 // esa nueva estrategia
 Encriptador.encriptar()
 ``` 
**Fijate:**  podes modificar los algoritmos (denominados **strategies**)  sin que esto afecte a las clases que los usan (denominadas **clients**)

**EJEMPLO PRACTICO:**
Passport.js usa este patron para separar los algoritmos que te loguearn a cada provider.

## Observer pattern (ej rxjs)

El observer pattern se usa cuando **tenes varios objetos que tienen que ser notificados cuando ocurre uno o varios sucesos**, para eso separas el problema en dos partes

* **Observers:** Aquellos que tienen que enterarse cuando ocurre un suceso
* **Subject:** Aquel que:
	*  genera el suceso
	* Tiene una lista de Observers y se encarga de notificarlos del suceso

La idea principal es que:
*  a medida que escribis codigo,  vas añadiendo **Observers** al ** array de observers que guarda el Subject**
*  cuando ocurre un suceso el **subject corre la funcion update() de cada uno de los observers en su array**

 ```C#
 //El subject/observable
Central centralDeAlarmas = new CentralDeAlarmas()
//Los observers
Cuartel boulogne = new Cuartel()
Cuartel central = new Cuartel()
Cuartel beccar= new Cuartel()
//añado los observers al array interno del observable/subject
centralDeAlarmas.subscribir(central )
centralDeAlarmas.subscribir(boulogne)
centralDeAlarmas.subscribir(beccar)
//Genero un evento que va a correr la funcion update()
//De cada cuartel
centralDeAlarma.alarma()
 ``` 
 Internamente estas clases se ven asi
El **subject/observable** tiene 
* **un metodo para subscribir observers** 
*  un metodo para **triggerear un evento y notificar a los observers**
 ```C#
public class centralDeAlarmas {

private listaDeCuarteles = [];
	//Añado un observer a la lista
	public function subscribir(cuartel){
		listaDeCuarteles.add (cuartel)
	}
	//Alerto a todos mis observers
	public function alerta(){
		foreach (listaDeCuarteles as cuartel){
			cuartel.update()
		}
	}
}
 ``` 
 Cada cuartel (observer) implementa su funcion **update()** para reaccionar al evento.
 ```C#
public class cuartel{
	//Esta funcion es la que el observable correra
	//Cuando haya un evento
	public function update(){
		console.log("alerta alerta")
	}
}
 ``` 


## Factory pattern (angular)

la fabrica actua como **intermediario** que **evita** que el **cliente** (programador que usa tu libreria) **instancie un objeto** de una familia de objetos  **directamente**, sino que **abstrae la creacion de un objeto**

**La fabrica:**
* **Consume** un input simple del programador
* **Devuelve** la instancia de un objeto de una clase acorde al input

**Sirve cuado:**
* Tenes varias clases que heredan de la misma clase
	*  EJ: en angular tenes factories que devuelven siempre clases que heredan de la clase  `Component`
* Queres centralizar:
	* El codigo que elige que objeto instanciar
	* La creacion de objetos
* Cuando no sabes antes de tiempo que clase necesitas instanciar(ej depende de las acciones del usuario o del programador)
* Queres hacerle la vida mas facil al programador para usar una familia de clases parecidas. 
	* evitas que necesite conocerlas todas las clases
	* Podes agregar clases a tu libreria sin que el programador tenga que cambiar su codigo.

**EJ:** un factory de enemigos que puede instanciar diferentes tipos de enemigos, pero todos heredan de una clase en comun
![enter image description here](https://lh3.googleusercontent.com/e1bXR9lbdABCtJuOlEDc66ntnNuabutQZolYUd2BB0Buyi0Gow0kqHC3pIigeFOGPNisONWHkcZI)

## Singleton pattern


**Cuando se usa:**
*   Queres **Evitar que exista mas de una instancia de un objeto**

 ```C#
public class miSingleton{
	// La unica instancia que puede existir es estatica
	private static instancia = null;
	
	//Solo la instancio si aun no existe 
	getInstance(){
		if (!instancia){
			instancia  = new miSingleton()
		}
		return instancia;
	}
}
 ``` 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQyODYyNzc1MV19
-->