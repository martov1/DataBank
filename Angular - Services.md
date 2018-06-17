
**Provider token alternatives**
https://angular.io/guide/dependency-injection-in-action#provider-token-alternatives-the-class-interface-and-injectiontoken


# Contenido:

* Que es
* Dependency Inyection, uso
* Service instances
	* Modulos sin lazy loading
	* modulos con lazy loading
	* Mencion en providers de dos modulos diferentes
	* Mencion en providers de un componente
* Lazy loading y service shadowing
* Dependecy inyection
	* Inyeccion de servicios
	* Inyeccion de valores
	* Inyector chain, @host y @optional
* Providers 
	* Custom providers 




## Que es

Un servicio es una clase con una funcion bien definida, engloba valores, funciones o cualquier funcionalidad que requieras a lo largo de la aplicacion, **son principalmente consumidos por los components**.

Algunos ejemplos:
*    logging service
*    data service
*    message bus
*    tax calculator
*    application configuration

Un ejemplo de un servicio
````js
@inyectable()
export class HeroService {
  private heroes: Hero[] = [];

  constructor(
    private backend: BackendService,
    private logger: Logger) { }

  getHeroes() {
    this.backend.getAll(Hero).then( (heroes: Hero[]) => {
      this.logger.log(`Fetched ${heroes.length} heroes.`);
      this.heroes.push(...heroes); // fill cache
    });
    return this.heroes;
  }
}
````

---

## Dependency injection

Es la forma que tiene angular de proveerle a las instancias de las clases con las dependencias que necesitan, **principalmente servicios**.

Se realiza generalmente en el **constructor** de los componentes o de otros servicios
````js
constructor(private service: HeroService) { } //inyectas HeroService
````


![enter image description here](https://lh3.googleusercontent.com/SAr2AIFg_9OIurd7NQ6AXEiVyebalpGuRTpcpTgYGLbzuxkJJ9s_Z-ByutZkSeToqS4fdJtZKxXA)

Para que el inyector sepa que HeroService existe, hay que decirselo. El inyector busca las cosas que puede inyectar en el array **providers** de cada modulo o componente.

> ** hay que colocar los servicios en el array providers de un modulo o un componente 
> para que pueda ser inyectado.**

### Crucial

> Si registras un service en el **array providers del componente** entonces **creas una
> nueva instancia del service para cada instancia de esecomponente**, si lo haces a nivel **root  component** entonces tenes **la misma instancia del service para todos
>  los  components**


---

## Service instances

Dependiendo de donde se instancie el servicio, es decir **donde sea mencionado en un providers array**, la instancia tendra un comportamiento diferente

### Modulos **sin lazy loading**

>* Los serivios de los modulos que no son cargados usando **lazy loading** estan  disponibles en toda la aplicacion, son **singletons**

### modulos  **con lazy loading**
>* Los servicios en el array de prividers de los modulos **eagerly loaded** aun son singletons y podemos accederlos
* Los servicios en el array de providers de un modulo cargado con **lazy loading** generan **sus propias instancias de servicios**
* Los componentes creados en el modulo tienen instancias locales de estos servicios

### Mencion en providers de dos modulos diferentes

Si dos modulos instancian el mismo servicio en providers, **el segundo sobreescribe al primero**

Podes evitar esto haciendo un chequeo para ver si ya fue importado
````js
constructor (@Optional() @SkipSelf() parentModule: CoreModule) {
  if (parentModule) {
    throw new Error(
      'CoreModule is already loaded. Import it in the AppModule only');
  }
}
````

### Mencion en providers de un componente

Podes instanciar un servicio en un componente, este servicio sera una **instancia aislada solamente accesible para esa instancia de ese componente y sus hijos**

si hay varias instancias de un componente, es decir, aparece varias veces en el template, cada **instancia diferente de ese componente** tendra su **propia instancia de ese servicio**

---

## Lazy loading y service shadowing

Si un modulo cargado con **lazy loading** necesita de un servicio, puede ser que lo nombre en su array de providers. Esto tiene concecuencias:

* **El servicio no existe en la app** - El modulo crea su propia instancia del servicio y la usa.

* **El servicio existe en la app, la idea es que sea singleton** - El modulo crea su propia **instancia paralela al servicio singleton**, esto se conoce como shadowing.

Este problema tiene una solcion **por convencion** que ya se ha visto, la creacion de un metodo **forRoot()** que contenga los providers, para ser llamado solo en el caso que se deseen crear los servicios en el array de providers.

Ejemplo:

````js
@NgModule({
  imports:      [ CommonModule ],
  declarations: [ TitleComponent ],
  exports:      [ TitleComponent ],
  providers:    [ UserService ]
})
export class CoreModule {
	
// Devuelve el modulo pero con MAS SERVICIOS
  static forRoot(config: UserServiceConfig): ModuleWithProviders {
    return {
      ngModule: CoreModule,
      providers:    [ UserService ]
    };
  }
}
````

---
## Dependecy inyection


### Inyeccion de servicios
En un servicio, cuando **decoras** la clase con el decorator **@inyectable()**, estas indicandole al inyector que esta clase puede ser inyectada como dependencia en otras clases.

Luego podes hacer que esa dependencia sea accesible en el codigo colocandola en un **array de providers**, dependiendo de donde este el array, el **inyector** tendra un comportamiento distinto, descripto en service instances, mas arriba.

### Inyeccion de valores

Podes crear valores/variables/objetos inyectables tambien. para eso agregas un elemento al **array providers** con un objeto que detalle:
* un **token** que se usa tanto como nombre para ese valor y como type para ese valor
* un **Valor** 

El token tiene que funcionar como interfaz del valor, pero **typescript borra las interfaces del codigo fuente al compilar** asique no podemos usar interfaces.

para esto podes usar la clase  `InjectionToken` que usa un generic con la interfaz.
EJ:

````js
// EN algun archivo
interface ValorInterface { blablabla}
valor:ValorInterface = {blablabla}
//Generas un token que permita al IDE saber el type de lo que inyectas
token = InjectionToken<ValorInterface>('una descripcion opcional')

//en el modulo, habiendo importado el archivo con un import de typescript
providers: [
  { provide: token, useValue: valor }
],

//Cuando queres inyectarlo
//Fijate como token funciona como interfaz del valor

constructor(private miValor: token){ }
````

### Inyector chain, @host y @optional

Cuando inyectas un servicio en un componente, sucede lo siguiente:

* angular lo busca en el providers **del componente**
* angular lo busca recursivamente en los providers de **los componentes padre**
* angular lo busca en el provider del **modulo principal**
* angular no encuentra el servicio, entonces **devuelve un error**

Podes detener este proceso en cualquier punto de la cadena de componentes usando `@host` en el constructor del componente para que angular no siga su busqueda de un servicio en particular.

Podes indicar a angular que si la dependencia no existe, no lance un error, esto se hace usando `@Optional` cuando pedis el servicio en un componente
````js
constructor(
      @Host() // limit to the host component's instance of the HeroCacheService
      private heroCache: HeroCacheService,

      @Host()     // limit search for logger; hides the application-wide logger
      @Optional() // ok if the logger doesn't exist
      private loggerService: LoggerService
  )
````

---
## Providers

Los providers son una _receta_ que te permite **proveer un servicio a partir de un determinado token**

>**Cuando inyectas un servicio en un componente, lo estas buscando por su token:**
````js
//Aca estamos inyectando un servicio en el constructor de un componente
//El inyector busca un servicio con UN TOKEN igual a BackendService
 constructor(private backend: BackendService)
````


### Custom providers

Generalmente registras tus providers coloclandolos en el providers array. Eso implica que angular crea providers automaticamente a partir de servicios. con **token igual al nombre de la clase del servicio**
````js
providers: [ LoggerService, UserContextService, UserService ]
````

**pero podria ser mas especifico:**
````js
 providers: [
	{ provide: Hero,          useValue:    someHero },
	    { provide: TITLE,         useValue:   'Hero of the Month' },
	    { provide: HeroService,   useClass:    HeroService },
	    { provide: LoggerService, useClass:    DateLoggerService },
	    { provide: MinimalLogger, useExisting: LoggerService },
	    { provide: RUNNERS_UP,    useFactory:  runnersUpFactory(2),
		deps: [Hero, HeroService]}
]
````

**Los tipos de providers son: **

* **Provide object literal** - se coloca el token y el valor/clase/cosa que se desea inyectar usando ese token
	* **Clase** - Provee una clase, no requere estar definida, sobreescribe al usuario anterior del token si existe
		* `{ provide: HeroService,   useClass:    HeroService }`
	* **valor** - Provee un valor que **ya fue definido**
		* `{ provide: Hero,          useValue:    someHero  }`
		* `{ provide: saludo,          useValue:    'hola'  }`
	* **otro token** - Permite que dos o mas tokens mapeen al mismo servicio
		*  
		````
		{ provide: token1,   useClass:    miServicio }
		{ provide: token1, useExisting: token2 }
		````
	* **useFactory** - el token llama una funcion que usa ciertas dependencias y devuelve otra fuencion que devuelva el valor/clase/servicio
		* `{ provide: RUNNERS_UP,    useFactory:  devuelvoFactory(algunValor), deps: [Hero, HeroService] }`
		
		
	 



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzg4OTM4MTY1LC0xODQzNjQ0MzUxLC0xMT
I4MDk3OTg1XX0=
-->