


**Volver a ver videos y documentar**
* Forms
* Event emitters


# Contenido

* Tipos de testing y nomenclatura
	* Principio tripple A
	* Tipos de tests simples 
		* Numeros
		* strings
		* arrays
* Testing en angular 
	* Generalidades 
	* Unit tests en components
		

# Tipos de testing y nomenclatura

* **Unit testing**
Prueba un componente aislado de los servicios, routers, backend y view. basicamente solo como una typescript class

* **Integration tests**
Probar un component con angular y con su view, pero con fake services

* **end-to-end tests**
Prueba toda la aplicacion

## principio Tripple A
* **A**rrange
Inicializar el sistema que vamos a testear, inicializar variables y declarar el mockup
* **A**ct
Realizar la accion a testear, correr la funcion o lo que haga falta
* **A**ssert
Verificar que los valores obtenidos son los que se esperan




# Testing en angular

## Generalidades

Los archivos de tests deben tener esta convencion para que **karma** los reconozca y los ejecute.

```js
nombreDeFuncion.spec.ts
```

## Unit tests en components

Tenemos un componente que se llama **VoteComponent** el cual puede llamar a su metodo **upVote** para aumentar su variable interna **totalVotes** en **1**

```js
describe ("VoteComponent",()=>{
	//Inicializacion de la clase para cada test.
	beforeEach(()=>{
		let component = new VoteComponent(); 
	})
	
	it("should increment totalVotes when upvoted",()=>{
		component.upVote();
		expect(component.totalVotes).toBe(1)
	})
	it("should increment totalVotes when upvoted",()=>{
		component.downVote();
		expect(component.totalVotes).toBe(1)
	})

})
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM5ODk4MDQ1OSwtMjE4NDQyMDQ4XX0=
-->