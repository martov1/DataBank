
# Contenido:

* Capacidades
* Setup
* Arquitectura
	* Observable
	* Observer
	* vincular observer a un observable
* Operadores
	* Combinar operators con Chaining y piping
	* switchmap/flatmap y mergemap
	* Forkjoin
	* concat 
	* merge
	* Race
	* pairwise
	* zip
	* Retry
	* do / tap
* Subjects
	* Son Observables singletons
	* Emiten valores a demanda




## Arquitectura

La idea principal es que podes tener un **data stream** al cual estas **observando** y multiples **observadores** que hacen cosas cuando ese data stream **recibe nuevos valores**

![enter image description here](https://lh3.googleusercontent.com/zhKBn0oBE0zMZia_FyiFhIbcZ0aumdxTntrAE0Qg7FGLu38OvfyiL27re5PezhwD8OmaMUMaUUhN)

**Un Observable invoca funciones en todos los observers que estan subscriptos cuando entra un dato nuevo.**

Por ejemplo, un **Observable que corresponde a llamadas HTTP** puede estar siendo **observado** por:
* **Ll view** para mostrar datos en una planilla cuando la llamada termine
* **Un loading indicator** mientras hay llamadas en curso
* **Un servicio de sesiones** para ver si la respuesta del servidor indica que las credenciales caducaron, etc


### Observable

Es un **wrapper alrededor de un stream de datos** que sirve para observarlo, puede ser sincronico o asincronico.

**Muchos observables ya vienen armados o con metodos para crearlos rapidamente**, por ejemplo:

* **eventos** de usuario (**click, mouseover, etc**)
* **AJAX**

Podemos crear uno ya predetermiado para **eventos de click** asi:
````js
var observable = Rx.Observable.fromEvent(button, 'click')
````

Lo podemos crear **desde cero** asi.
````js
var observable = Rx.Observable.create(function (observer) {
  observer.next(1); //Devolvemos un dato a los observers usando sus next()
  observer.next(2); //Devolvemos un dato a los observers usando sus next()
  setTimeout(() => {
    observer.complete(); //Devolvemos La señal de terminado a los observers
  }, 1000);
});
````


### Observer

Es un objeto con funciones que **hacen algo con los datos nuevos de un Observable**, tiene tres funciones en las que podemos armar nuestra logica.

* **Next(datoNuevo)** - Cuando aparece un nuevo dato en el observable (Ej: el usuario hizo click)
* **Completed()** - Cuando el observable indica que termino, ya no habra mas datos
* **Error()** - Cuando el observable indica que hubo un error, no habra mas datos

**Algunos observables nunca llamara a la funcion completed** de sus observers porque no siempre tiene sentido (un click event listener nunca deberia terminar).

Un observer se veria asi:
````js
var observer = {
  next: (valor) => console.log('el valor es:  ' + valor),
  error: (err) => console.error(err),
  complete: (valor) => console.log('Observer got a complete notification'),
};
````

### vincular observer a un observable

* **vinculo entre un observable y un observer se llama subscription**
* puede haber **muchos observers subscriptos a un observable**
* Cada vez que te suscribis a un observale estas creando **una instancia aparte**

````js
observable.subscribe(observer)
````

y desvincularte con 
````js
observable.unsubscribe(observer)
````


un ejemplo mas completo:

````js
//configuro el observer
var observer = {
  next: valor => console.log('el valor es:  ' + valor),
  error: err => console.error(err),
  complete: () => console.log('Observer got a complete notification'),
};
//creo el observable
var observable = Rx.Observable.fromEvent(button, 'click')
// subscribo el observable a ese observer
observable.subscribe(observer)
````

Tambien podes declarar el observer de forma directa colocando las **funciones del observer como parametros de la funcion subscribe**. Al hacer esto la linea entre Observer y Observable se torna media dificil de ver.
````js
var observable = Rx.Observable.fromEvent(button, 'click')
observable.subscribe(
(dato)=>{ mi funcion next},    			//el primer parametro es la funcion next      
(dato)=>{mi funcion error},				//el segundo parametro es la funcion error
(dato)=>{mi funcion complete},			//el tercer parametro es la funcion complete
)
````


## Operadores

La principal **motivacion** de **usar observables** es que **podes usar operadores**


Los operadores son metodos de los Observables, **no mutan el observable sino que crean una nueva instancia basada en el observable anterior**

#### **Critico**:

> Los operadores **no mutan el observable** sino que crean un **nuevo observable basado en el observable anterior**

**Alunos operadores comunes:**

* **Observable.map(funcion)** - Devuelve un observable con valores cambiados por la funcion que coloques como parametro
* **Observable.interval(milisegundos)** - Devuelve un observable que se activa cada x milisegundos y devuelve como valor numeros incrementales del 0 a infinito
* **Observable.throttleTime(milisegundos)** - Devuelve un observable que emitira los eventos solo cuando hay por lo menos 2 segundos entre si
* **Observable.debounceTime(Milisegundos)** - Devuelve un observable que aguarda a que haya una pausa de x milisegundos en la emision de valores y emite el ultimo valor
* **Observable.filter(funcion)** - Devuelve un observable que emitira los valores que satisfagan las condiciones de la funcion (cuando la funcion devuelva true)
* **Observable.distinctUntilChanged()** -Devuelve un observable que omite todo valor que sea identico al ultimo valor emitido
* **Observable.reduce(funcion(total, nuevoValor))** - Devuelve un observable que va calculando un valor acumulativo a medida que recibe eventos (como reduce de lodash) y devuelve el resultado cuando el observable envia la señal de complete()
* **Observable.scan()** Igual que reduce pero devuelve el total en cada next() en lugar de esperar a complete()
* **Observable.pluck('prop', 'childDeProp')** parece map  pero extrae **una sola** propiedad del objeto, como parametros toma el path a esa propiedad, es decir en este caso el path es _prop.childDeProp_
* **Observable.take(number)** - Finalizara el observable despues de 10 valores emitidos
* **Observable.takeWhile(funcion())** - Finaliza el observable cuando la funcion devuelva false
* **Observable.of(valor1,valor2, valorN)** - crea un observable que emite los valores que colocas como atributos

### Combinar operators con Chaining y piping

Podes encadenar operators de dos formas

**Chaining**

Como cada operator devuelve otro observable, podes encadenarlos asi
````js
const source = from([1, 2, 3, 4, 5, 6, 7, 8, 9]);

source
  .filter(x => x % 2)
  .map(x => x * 2)
  .scan((acc, next) => acc + next, 0)
  .startWith(0)
.subscribe(console.log)
````


**piping**

Importas los operators como funciones independientes, y los colocas como argumentos de la funcion pipe

````js
import { from, retry } from 'rxjs/operators';

const source = from([1, 2, 3, 4, 5, 6, 7, 8, 9]);
    .pipe(
      retry(3), // retry a failed request up to 3 times
      catchError(this.handleError) // then handle the error
    );
````

### Switchmap/flatmap y mergemap

Cada vez que un observer **emite un valor**, switchmap **crea un observer nuevo**, si ya habia creado uno antes entonces **descarta el anterior**.

````js
const stream1 = Rx.Observable.interval(4000)

const resultado = stream1.switchMap(valor => {
 console.log("valor de stream1 " + valor); //outputea el valor emitido por stream1
 stream2 = Rx.Observable.interval(1000) //inicio una instancia stream 2
 return stream2
});
resultado.subscribe(
  console.log,
  console.error
);
````

por cada valor nuevo de stream1 se crea un observador hijo nuevo y se descarta el anterior
````js
valor de stream1  0			
      0						//instancio un observer stream2
      1
      2
      3						
valor de stream1  1			//Nuevo valor!, descarto la instancia stream2 anterior
     0						//E inicio una nueva desde cero
     1
     2
     3
valor de stream1  2			//Nuevo valor!, descarto la instancia stream2 anterior
     0						//E inicio una nueva desde cero
     1
     2
etc....
````

> Por esto se llama tambien **flatmap**, porque en vez de devolver un array de arrays con el resultado de cada observable, te da un array de resultados.
````js
//flatmap
['a','b','c'].switchmap(function(e) {
    return [e, e+ 'x', e+ 'y',  e+ 'z'  ];
});
//['a', 'ax', 'ay', 'az', 'b', 'bx', 'by', 'bz', 'c', 'cx', 'cy', 'cz']
//map comun	
['a','b','c'].map(function(e) {
    return [e, e+ 'x', e+ 'y',  e+ 'z'  ];
});
//[Array[4], Array[4], Array[4]]
````


**mergemap** es igual, pero no descarta las instancias de stream2 que se van creando.

````js
valor de stream1  0			
      0						//instancio un observer stream2
      1
      2
      3						
valor de stream1  1	4		//Nuevo valor!, descarto la instancia stream2 anterior
     0	5					//E inicio una nueva desde cero
     1  6
     2	7
     3	8
valor de stream1  2 9 4		//Nuevo valor!, descarto la instancia stream2 anterior
     0	10	5				//E inicio una nueva desde cero
     1	11	5
     2	12	7
etc....
````

### Forkjoin

Se usa cuando **tenes multiples observables** y te interesa obtener **el valor final de todos**. por ejemplo **cuando terminan varios http requests**

````js
const example = forkJoin(
  //emit 'Hello' immediately
  of('Hello'),
  //emit 'World' after 1 second
  of('World').pipe(delay(1000)),
  //emit 0 after 1 second
  interval(1000).pipe(take(1)),
  //emit 0...1 in 1 second interval
  interval(1000).pipe(take(2)),
  //promise that resolves to 'Promise Resolved' after 5 seconds
  myPromise('RESULT')
);
//output: ["Hello", "World", 0, 1, "Promise Resolved: RESULT"]
const subscribe = example.subscribe(val => console.log(val));
````

### Concat

Forma un queue de observables. **se hacen uno por uno en orden**
````js
//emits 1,2,3
const sourceOne = of(1, 2, 3);
//emits 4,5,6
const sourceTwo = of(4, 5, 6);

//used as static
const example = concat(sourceOne, sourceTwo);
//output: 1,2,3,4,5,6
````

### merge

**Transforma muchos observables en uno solo**
````js
//emit every 2.5 seconds
const first = interval(2500);
//emit every 2 seconds
const second = interval(2000);
//emit every 1.5 seconds
const third = interval(1500);
//emit every 1 second
const fourth = interval(1000);

//emit outputs from one observable
const example = merge(
  first.pipe(mapTo('FIRST!')),
  second.pipe(mapTo('SECOND!')),
  third.pipe(mapTo('THIRD')),
  fourth.pipe(mapTo('FOURTH'))
);
//output: "FOURTH", "THIRD", "SECOND!", "FOURTH", "FIRST!", "THIRD", "FOURTH"
const subscribe = example.subscribe(val => console.log(val));

````

### Race

agarras el observable que sea el primero que emita un valor
````js
//take the first observable to emit
const example = race(
  //emit every 1.5s
  interval(1500),
  //emit every 1s
  interval(1000).pipe(mapTo('1s won!')),
  //emit every 2s
  interval(2000),
  //emit every 2.5s
  interval(2500)
);
//output: "1s won!"..."1s won!"...etc
const subscribe = example.subscribe(val => console.log(val));

````

### pairwise

Cada vez que se emita, agarras el valor actual y el ultimo valor emitido. ambos son integrantes de un array

````js
//Returns: [0,1], [1,2], [2,3], [3,4], [4,5]
interval(1000)
  .pipe(pairwise(), take(5))
  .subscribe(console.log);

````

### zip

Espera a que **todos** los observables emitan un valor y luego emite los valores como array, repite esto cuando **todos** los observables emitan otro valor

````js
const example = zip(
  sourceOne,
  sourceTwo.pipe(delay(1000)),
  sourceThree.pipe(delay(2000)),
  sourceFour.pipe(delay(3000))
);
//output: ["Hello", "World!", "Goodbye", "World!"]
const subscribe = example.subscribe(val => console.log(val));
````

### Retry

vuelve a crear el observable y vuelve a intentar en caso de error. la cantidad de veces a reintentar esta sujeta al attributo que coloques


````js
const source = interval(1000);
const example = source.pipe(
  mergeMap(val => {
    //throw error for demonstration
    if (val > 5) {
      return _throw('Error!');
    }
    return of(val);
  }),
  //retry 2 times on error
  retry(2)
);

````

### do / tap

Te permite atajar un valor del observable en algun momento de la cadena de operadores y hacer algo arbitrario con ese valor. No te permite modificarlo y enviar la modificacion mas abajo de la cadena.

````js
//transparently log values from source with 'do'
const example = source.pipe(
  tap(val => console.log(`BEFORE MAP: ${val}`)),
  map(val => val + 10),
  tap(val => console.log(`AFTER MAP: ${val}`))
)

//'do / tap' no modifica los valores
//output: 11...12...13...14...15
const subscribe = example.subscribe(val => console.log(val));
````

---

## Subjects

**Caracteristicas**
* son como observables pero **son singletons**
* Pueden **emitir valores a demanda** como si fueran event emitters

### Son Observables singletons
Aca se puede ver como **los observables no son singletons**
````js
//creo un observable
var observable = Rx.Observable.create(function(source) {
  source.next(Math.random());
});
//Añado observers
observable.subscribe(valor => console.log('consumer A: ' + valor));
observable.subscribe(valor => console.log('consumer B: ' + valor));
/* Los observers no comparten la misma instancia */
// consumer A: 0.25707833297857885
// consumer B: 0.8304769607422662
````

Cuando suscribamos un subject a un observable todos **los observers que hagan uso del subject compartiran una misma instancia**
````js
//creo un observable
var observable = Rx.Observable.create(function(source) {
  source.next(Math.random());
});
//creo un subject
var subject = new Rx.Subject();
//Una nueva instancia de observable queda vinculada a un subject
observable.subscribe(subject);
// Configuro un subject con algunos observers
subject.subscribe(valor => console.log('consumer A: ' + valor));
subject.subscribe(valor => console.log('consumer B: ' + valor));
/* Esos observers comparten la misma instancia */
// consumer A: 0.8495447073368834
// consumer B: 0.8495447073368834
````

### Emiten valores a demanda

**Podes emitir valores a demanda usado**
````js
subject.next('valor');
````

# Async pipe en angular

Cuando haces operaciones async con observables en angular vas a usar el **async** pipe, que **se subscribe** a un observable y te devuelve el ultimo valor emitido.

## Trabajar con async objects  en template
EJ:

	// un atributo de un objeto que todavia no llego
    [ngStyle]="{'background-image': 'url(' + rootApiUrl + (landsObservable | async)?.imagenes[0].url + ')'}"


## Evitar multiples requests

Como cada async pipe se **subscribe** y una subscripcion **genera una nueva instancia del observable** cada vez que llames al async pipe generas un nuevo **http ajax call**

Para evitarlo usa **el operador share** que comparte un unico data stream entre todos los que se subscriban al obsevable

	
    this.landsObservable  =  this.route.params
    .pipe(
	    share()
	    )

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYwNjI1MTkyLC0xOTAyNDUyNTEyLC05OT
A5MTUxNjJdfQ==
-->