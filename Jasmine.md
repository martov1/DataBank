**docs (no son muy grandes)**
https://jasmine.github.io/api/edge/global

**Namespaces:**

- [ ] [jasmine](https://jasmine.github.io/api/edge/jasmine.html)
- [ ] [clock](https://jasmine.github.io/api/edge/Clock.html)
- [x] [Matchers](https://jasmine.github.io/api/edge/matchers.html)
- [x] [spy calls](https://jasmine.github.io/api/edge/Spy_calls.html)
- [x] [spy strategy](https://jasmine.github.io/api/edge/SpyStrategy.html)

**Global:**

 - [x] afterAll 
 - [x] afterEach
 - [x] beforeAll
 - [x] beforeEach
 - [x] describe
 - [x] expect
 - [x] fail
 - [x] it
 - [x] pending
 - [x] spyOn
 - [ ] spyOnProperty
 - [x] xdescribe
 - [x] xit

**Otros:**

 - [x] [async](https://jasmine.github.io/tutorials/async)



# Contenido

* Conceptoa basicoa
	* Tests y suites
	* Assertions con expect() y sus matchers - **wip**
	* Hooks 
	* Fail manual
	* Tests en estado de Pending
* Function call tests usando Spies 
	* Expects
	* Spy Strategy
	* Otros datos
* Async tests y timeouts
	*  Timeouts
	*  Probar procesos asincronicos
		* Done() 
		* Promises
* Ejemplos 
	* Tests simples
	* Tests de browser





# Concepto basico

## Tests y suites

Jasmine agrupa los **tests** en conjuntos denominados **suites**, la idea es que una funcion ó pieza de codigo probablemente tenga varios tests asociados para probar diferentes cosas, entonces los agrupas en una suite

* **describe()** - Un conjunto de tests, denominado "test suite"
	* Como parametro toma un **string** que **describe la suite**
* **it()** - un test, es importante notar la semantica
	* Como parametro 1 toma un **string** que **describe el comportamiento esperado del codigo testeado** 


```js
describe ("miSuite",()=>{
	it("deberia hacer blabla 1 ",()=>{
		// mi test 1
	})
	it("deberia hacer blabla 2 ",()=>{
		//mi test 2
	})
	it("deberia hacer blabla 3 ",()=>{
		//mi test 1
	})
})
```


Tambien pueden haber **describes anidados**

```js
describe ("miSuite",()=>{
	it("deberia hacer blabla 1 ",()=>{
		// mi test 1
	})
	it("deberia hacer blabla 2 ",()=>{
		//mi test 2
	})
	describe ("miSuite-subSuite",()=>{
		it("deberia hacer blabla 3 ",()=>{
			//mi test 1
		})
	}
})
```

## Assertions con expect() y sus matchers

La funcion **expect()** toma como parametro una funcion u objeto, lo evalua y lo devuelve como un objeto con multiples metodos (Llamados matchers) para comparar el resultado de esa evaluacion con el resultado esperado.
```js
describe ("saludo",()=>{
	it('should say Hola',()=>{
		expect (saludo()).toBe("hola")	//Comparacion con el resultado esperado
	})
})
```


* **Expect()**
	* **.toBe(param)** - Que el valor sea igual (===) a **param**
	* **toEqual({OBJ})** - Compara el resultado con el objeto dado. hace **deep comparison**
	* **.toBeCloseTo(float, precis)** - Que el valor este cerca de un numero, con cierto margen de precision expresado en cantidad de decimales
		```js
		expect(number).toBeCloseTo(42.2, 3);
		```
	* **.toBeDefined()** - Que el valor no sea indefnido
	* **.toBeUndefined()**
	* **.toBeFalsy()** - Que el type casting a bool no de false
	* **.toBeTruthy()**
	* **.toBeGreaterThan(int)** - Que sea mayor que cierto numero
	* **.toBeGreaterThanOrEqual(int)** 
	* **.toBeLessThan(int)**
	* **toBeLessThanOrEqual(int)**
	* **toBeNaN()**
	* **toBeNegativeInfinity()**
	* **toBePositiveInfinity()**
	* **toBeNull()**
	* **toContain(elem o substring)** - Busca en el resultado:
		* Un substring, si el resultado es un string
		* Un elemento, si el resultado es un array 
	* **toMatch('regex')** - Que el resultado haga match con una regular expression
	* **toThrow({objeto})** - Que el resultado sea una excepcion con valor igual a objeto. Si  no se especifica ningun objeto entonces solamente expera que arroje una excepcion.
	* **toThrowError(clase, mensaje ó regex)** - 
		* Que arroje una instancia de la clase error o de la clase privista como primer argumento si lo hubiere. 
		* Que el error tenga el mensaje indicado en el segundo argumento, o haga match con una regex del segundo argumento
	* **toThrowMatching(funcionEvaluadora)** - Que el resultado sea una excepcion, la cual se pasa como parametro a la funcionEvaluadora que devuelve un bool, si devuelve false entonces el test falla.


## Hooks


Los hooks disponibles son:
* **beforeEach()**
* **afterEach()**
* **beforeAll()**
* **afterAll()**

**Ejemplo:**
Cada vez que haces un test, jasmine NO reinicia el estado del objeto siendo testeado

```js
describe ("miSuite",()=>{
	it("aumentar el sueldo en 500",()=>{
		expect(empleado.aumentar(500)).toBe(1500)
	})
	it("aumentar el sueldo en 700",()=>{
		expect(empleado.aumentar(700)).toBe(1700) //ERROR, el valor es 2200
	})
})
```

Podemos usar un hook **beforeEach** para reiniciar el valor cada vez que hacemos un nuevo test

```js
describe ("miSuite",()=>{
	beforeEach(()=>{
		empleado.sueldo = 0;
	})
	it("aumentar el sueldo en 500",()=>{
		expect(empleado.aumentar(500)).toBe(1500)
	})
	it("aumentar el sueldo en 700",()=>{
		expect(empleado.aumentar(700)).toBe(1700) //ERROR, el valor es 2200
	})
})
```




## Fail manual

Podes hacer fallar un test en cualquier momento usando **fail()**
```
it("should not call the callBack", function() {
    foo(false, function() {
      fail("Callback has been called");
    });
```



## Tests en estado de Pending

Podes declarar tests pero no escribirlos, y que figuren en el report como pendiente, es similar a escribir un //TODO:
Podes suits enteras en estado pending con **xdescribe** y tests individuales con **xit ó pending("mensaje")**
**Pending describe con xdescribe**
```js
//Esta suite no se ejecuta, pero aparece en el report como "pending"
xdescribe("describe pendiente", function() {
  it("test", function() {
  	//blabla
  });
});
```

**Pending test con xit ó pending**
```js

describe("A spec", function() {
    xit("Spec pendiente", function() {
    	expect(true).toBe(false);
 	});
	
	it("spec que si correra", function() {
    });
	it("spec que no correra", function() {
		pending("Test no terminado")
    });
});
```


# Function call tests usando Spies

Dado un objeto con una funcion:
SpyOn agrega a ese objeto una serie de metodos para anlizar cuando y como es llamada esa funcion. El spy es destruido cuando sale del bloque **it() ó describe** del que fue llamado.

**IMPORTANTE:**
* SpyOn **muta** al objeto que se coloca como parametro
* Cuando el test llame a la funcion, esta no correra hasta que el **spy lo indique**, esto debe **hacerse manualmente**

```
spyOn(obj, 'miFunc') // assumes obj.miFunc is a function
obj.miFunc()
expect(obj.miFunc).toHaveBeenCalled() // true!
```

### Expects
* Expect(spy.miFunc)
	* **.toHaveBeenCalled()** - True si la funcion ya fue llamado
	* **.toHaveBeenCalledBefore(otro spy)** - true si fue llamado antes que otra funcion
	* **.toHaveBeenCalledTimes(int)** - True si fue llamdo esa cantidad de veces
	* **.toHaveBeenCalledWith(arg1,arg2)** - True si fue llamado con esos argumentos


```js
spyOn(obj, 'miFunc') // assumes obj.miFunc is a function
expect(obj.miFunc).toHaveBeenCalled() // Verificar que se llamo al metodo
expect(obj.miFunc).toHaveBeenCalledWith('foo', 'bar') //Verificar si fue llamado con
```


### Spy Strategy

Lo que puede hacer el spy con la funcion. como interceptar el llamado e insertar un mock, o devlver un valor fijo.

* **tenes parametros:** Especificar con que parametros con los que se llama a la funcion usando `.withArgs(ARGUMENTOS).and.`
* **No tenes parametros** Llamas directamente a los metodos despues de usar `.and.`

**donde el spy es:**
```js
spyOn(obj, 'miFunc') // assumes obj.miFunc is a function
```

**Se pueden usar:**
* **obj.withArgs(1, 2, 3).and.**
	* **.callFake(Function)**
	LLama a otra funcion que remeplaza la
	original cuando se llame a a obj.miFunc()
	* **.callThrough()**
	Llama a la funcion original cuando se llame a obj.miFunc()
	* **.exec()** - Ejecuta la spy strategy
	* **.returnValue(valor)** 
	Le indica al obj.miFunc() que no debe ejecutarse y 
	en su lugar debe devolver un valor
	* **.returnValues[a,b,c]** 
	indica a obj.miFunc() que en lugar de ejecutarse
	debe devolver estos valores (uno por cada vez que se la 
	llame
	* **.stub()** - Indica no hacer nada cuando se llame a obj.miFunc	
	* **.throwError(something)** - Indica que obj.miFunc() debe devolver esta excepcion

```js
spyOn(obj, 'miFunc') 
obj.callFake(Function) 
obj.callThrough() 
obj.returnValue(valor) 
obj.returnValues[a,b,c]			
obj.stub()		
obj.exec() 
obj.throwError(something) 
```

### Otros datos


Podes obtener los datos de llamadas especificas. ej: parametros, que numero de invocacion es, etc.
* **spy**
	* **.all()** Obtenes los datos de las veces que se llamo al spyen forma de array
	* **.allArgs()** Obtenes todos los argumentos de cada vez que se llamo al spy (array)
	* **.any()** True si se invoco al spy
	* **.argsFor(int)** Argumentos para la invocacion numero int
	* **.count()** Cantidad de veces que se invoco el spy
	* **.first()** Obtenes los datos de la primera vez que se llamo al spy
	* **.mostRecent()**  Obtenes los datos de la ultima vez que se llamo al spy
	* **.reset()** Resetea el spy, como si nunca hiubiera sido llamado




#Async tests y timeouts

##Timeouts

Podes especificar timeouts en **it** o en los **hooks** usando su tercer parametro.
Si el test no termina y se llega al timeout, se considera que el test fallo
```
// timeout de 10000 segundos en hook
beforeEach(function(done) {}, 10000);

// timeout de 10000 segundos en it
  it('should call fetchData from apiService', function() {}, 1000000);
});
```


##Probar procesos asincronicos
###Done()

Cuando llamas a **it()** o a cualquier **hook**, la funcion que corresponde al segundo argumento acepta como parametro la funcion inyectada **done()**, al agregar este argumento jasmine sabe que no debe terminar el test hasta que llames a **done()**
```
//Ejemplo usando beforeEach
beforeEach(function(done) {
	//async thingy
  setTimeout(function() {
    done(); // end test
  }, 100);
});

//Ejempo usando it
  it('should call fetchData from apiService', function(done) {
    playlistsService.fetchPlaylistsData()
      .then((result) => {
        expect(apiService.fetchData).toHaveBeenCalledWith(video);
        expect(result).toEqual(promisedData);
        done();
      });
});
```

###Promises

Si el spec devuelve una promesa, entonces se considera que si la promesa se cumple el spec funciona, si la promesa no se cumple el spec falla.
```
it("should complete the promise", function() {
  return asyncCall()
});

```


#Ejemplos


##Tests simples

* **Numeros**
```
describe (miFuncion,()=>{
	it('should return 0 if input is negative',()=>{
		let result = compute(-1)
		expect (result).toBe(0)
	})
})
```

* **strings**
```
		let result = obtenerMensaje(jorge)
		expect (result).toContain("jorge") // devuelve "hola jorge, buenos dias"
```

* **arrays**
```
	let result = getCurrencies()// devuelve ["USD", "CAD", "ARG"]
	expect (result).toContain("USD") 
	expect (result).toContain("CAD") 
	expect (result).toContain("ARG") 
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNzU4MTM1NzUsMzg5MDA0MjRdfQ==
-->