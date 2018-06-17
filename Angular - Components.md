

     
# Contenido:

* Que es
* Estructura
* Metadata
* Propiedades y metodos
* CSS y estilos
* Proyeccion de contenido
* lyfeCycle hooks
* Data binding
* API del componente con @Input and @output
	* Alias para la API
	* Getters y setters
* Comunicacion entre componentes
	* Mediante los templates
	* Inyectar child components/Elements/Directives
		* @ViewChild / @ViewChildren
		* @ContentChildren / @ContentChil
* Crear componentes dinamicamente


## Que es

Un modulo es un pedazo de logica (**directive**) que tiene a cargo un pedazo de HTML llamado **view**. Los componentes se implementan mediante una **clase** que **interactua con el view** mediante una **API de propiedades y metodos** 

---
## Estructura

Un componente debe pertenecer a un modulo para ser usado por otro componente o aplicacion

el componente tiene un **decorator @component** con un objeto que contiene **metadata** y una **clase** 

````js
//decorador con metadata
@Component({selector: 'greet', template: 'Hello {{name}}!'})
class Greet {
  name: string = 'World';
}
````

## Metadata

Los componentes son clases comunes de typescript hasta el momento en el que le agregas el **decorator @component** y su **metadata** que le **indica a angular como actuar** 

* **animations** - list of animations of this component
* changeDetection - change detection strategy used by this component
* encapsulation - style encapsulation strategy used by this component
* entryComponents - list of components that are dynamically inserted into the view of this component
* exportAs - name under which the component instance is exported in a template
* host - map of class property to host element bindings for events, properties and attributes
* inputs - list of class property names to data-bind as component inputs
* interpolation - custom interpolation markers used in this component's template
* moduleId - ES/CommonJS module id of the file in which this component is defined
* outputs - list of class property names that expose output events that others can subscribe to
* **providers** - Servicios instanciados exclusivamente para este componente y sus childs
* queries - configure queries that can be injected into the component
* **selector** - le indica a angular que instancie un component cuando encuentre este tag
* **styleUrls** - list of urls to stylesheets to be applied to this component's view
* styles - inline-defined styles to be applied to this component's view
* template - inline-defined template for the view
* **templateUrl** - url to an external file containing a template for the view
* viewProviders - list of providers available to this component and its view children



````
@Component({ 
  changeDetection?: ChangeDetectionStrategy
  viewProviders?: Provider[]
  moduleId?: string
  templateUrl?: string
  template?: string
  styleUrls?: string[] ******
  styles?: string[]
  animations?: any[]
  encapsulation?: ViewEncapsulation
  interpolation?: [string, string]
  entryComponents?: Array<Type<any> | any[]>
  preserveWhitespaces?: boolean
  // inherited from core/Directive
  selector?: string
  inputs?: string[]
  outputs?: string[]
  host?: {...}
  providers?: Provider[]
  exportAs?: string
  queries?: {...}
})
````

---
## Propiedades y metodos

Podes crear propiedades y metodos desde la clase o dentro del constructor asi

````
export class AppCtorComponent {
  //Propiedades directamente en la clase
  title: string;
  myHero: string;
  //podes crear metodos
  myFunction = function(){cosas}	
  constructor() {
    //Propiedades en el constructor
    this.title = 'Tour of Heroes';
    this.myHero = 'Windstorm';
  }
}
````

---
## CSS y estilos

Los estilos de cada componente estan aislados del resto, asique no se pisan.

Podes poner los estilos **inline** directamente en el campo de metadata **styles** o podes colocar la URL de un archivo de estilos en el campo de metadata **styleUrls**

Existen algunos selectores que no son estandares

* **:host ** - Permite agregar estilos al elemento padre que contiene al componente. puede activarse condicionalmente si el parent tiene una clase en particular
````
:host {
  display: block;
  border: 1px solid black;
}
/** Activar estos estilos solo si el parent tiene la clase CSS "active"*/
:host(.active) {
  border-width: 3px;
}
````

* **:host-context()** - es como :host pero se activa si existe una clase en algun parent, no solo en el parent inmediato, esta bueno si queres implmenetar themes
````
:host-context(.theme-light) h2 {
  background-color: #eef;
}
````

---
## Proyeccion de contenido


### Single slot
Podes **meter contenido entre los tags de un componente** y decirle a ese componente como manejar ese contenido.

````
<!-- quiero que mi componente haga algo con el contenido que le pasess en
el template -->
<mi-componente>
	<p>mi contenido</p>
</mi-componente>
````

Para eso usamos la directiva `<ng-content>` en el template del componente para **decirle donde colocar lo que le pasamos**
````
<div>
	<p>Este es mi componente!</p>
	<ng-content></ng-content>
	<!-- Esto se va a poblar con <p>mi contenido</p> -->
</div>
````

### Multi slot

Podes identificar distintos bloques de contenido con clases de CSS o con slectores customizados.

en el parent component
````
 <div class="app">
      <my-component>
	  <!-- identificado con clase CSS-->
        <div class="titulo">
          Mi titulo!!!
        </div>
		<!-- identificado con selector customizado -->
        <my-component-content>
          Mi contenido!!!
        </my-component-content>
      </my-component>
    </div>
````

en el template de my-component
````
<div class="my-component">
      <div>
	  <!-- Esto se va a poblar con "mi titulo!!!"-->
        <ng-content select=".titulo"></ng-content>
      </div>
      <div>
	  <!-- Esto se va a poblar con "mi contenido!!!"-->
        <ng-content select="my-component-content"></ng-content>
      </div>
    </div>
````

---
## lyfeCycle hooks
  
  Los componentes tienen un life Cycle
  
  1)  **creacion** el component
  2) **renderizacion** del componente en el dom
  3) Crea y renderiza los **componentes hijos**
  4) **Actualizacion** cuando cambian sus propiedades
  5)  **Destruccion**  antes de sacarlo del DOM
  
  Los lyfecycle Hooks son interfaces que podes implmenetar y te permiten hacer cosas cuando suceden estos pasos. Si un hook no esta implementado entonces Angular no lo llama
  
  
### Oninit

Corre codigo en el momento que se instancia el Componente por primera vez y sus propiedades ya fueron seteadas. Es llamado una unica vez.

Aca colocarias la logica incial, **no en el constructor porque evitaria que el component se renderice rapido**
````
@Component({selector: 'my-cmp', template: `...`})
class MyComponent implements OnInit {
  ngOnInit() {
    // ...
  }
}
````

### OnDestroy

Corre el codigo justo antes de que se destruya el componente.

Aca colocarias logica de limpieza, dessubscripcion a observables, remocion de timers, notificar la eliminacion a otra parte de la aplicacion, etc.
 ````
   ngOnDestroy() {
    // prevent memory leak when component destroyed
    this.mySubscription.unsubscribe();
  }
 ````
 
 ### OnChanges
 
 Corre el codigo cuando **detecta cambios en las _input_ properties.**
 Esta funcion recibe un array con los valores anteriores y los nuevos.
 
### DoCheck

Sirve para buscar cambios que Angular no llega a detectar.
Este hook se activa mucho y es caro de implementar. Preferentemente no usar o mantener una implementacion super liviana.

### AfterViewInit

Se dispara una sola vez cuando el componente y todos sus child components fueron renderizados.

---
 
## Data Binding

Ver Angular - Templates y template syntax

---

## API del componente con @Input and #output


La API de un componente debe ser **especificada expresamente** y consiste en lo siguiente:

>* **Variables** que son expuestas al mundo exterior y pueden ser modificadas desde afuera del componente, generalmente por otro componente en el template. Se marcan con **@Input()**

>* **eventEmitters** que pueden ser expuestos al mundo exterior y otros componentes pueden escuchar los eventos que emita. Se marcan con **@Output()**

**esto hace las veces de una API para limitar que es lo que se puede insertar o sustraer de un component y que se pueda comunicar con otros**

>**EN LUGAR DE ESTO TAMBIEN PODRIAS USAR TEMPLATE VATIABLES PARA MUCHAS DE ESTAS COSAS**

Declaracion de la API
````
//Esto se puede cambiar desde afuera
@Input()  hero: Hero;	
//esto se emite hacia afuera
@Output() deleteRequest = new EventEmitter<Hero>();	
````

Tambien hay una sintaxis de arrays si hay una API extensa
````
@Component({
  inputs: ['hero'],
  outputs: ['deleteRequest'],
})
````

**@input posibilita el data binding desde otro component o el consumir eventos
de otro component**
````
//Bieneas una propiedad del component a una variable del componente padre
//en este caso "currentHero"
<app-hero-detail [hero]="currentHero"></app-hero-detail>
````

**@Output posibilita que otro componente lea los eventos emitidos por el componente**
````
<app-hero-detail (miEvento)="escucharHola($event)">
	<!-- mi-componente tiene un @Output que emite un evento llamado miEvento -->
	<mi-componente (click)="decirHola()" ></mi-Componente>
</app-hero-detail>
````


**Otro ejemplo**
>En este ejemplo hero-detail **recibe informacion de su parent**, seteando hero-detail.**hero** en la variable del parent llamada **currentHero**.
>
Ademas esta **a la escucha de un evento llamado deleteRequest de un component hijo** y al escucharlo activa una funcion **deleteHero()**
>
![](http://i.markdownnotes.com/input-output.png)


### Alias para la API

El **nombre interno** de los elementos de la API puede ser diferente del **nombre expuesto al exterior**. Esto se hace mediante un **Alias**
````
@Output('nombreExterno') nombreInterno = new EventEmitter<string>(); 
@Input('nombreExterno') nombreInterno;
	
//Tambien se puede usar la notacion de array
@Directive({
  outputs: ['nombreInterno:nombreExterno']  
})
````

### Getters y setters

Podes usar los getters y setters de typescript para hacer cosas antes de aceptar la nueva variable que ingresa por al api

````
@Component({
  selector: 'app-name-child',
  template: '<h3>"{{name}}"</h3>'
})
export class NameChildComponent {
  private _name = '';
//setter
  @Input()
  set name(name: string) {
    this._name = (name && name.trim()) || '<no name set>';
  }
//getter
  get name(): string { return this._name; }
}

````
---
## Comunicacion entre componentes


### Mediante los templates

Ver **Angular - Templates y template syntax** secciones
* **Comunicacion componente1->view->componente2**
* **Reference variables #**



### Inyectar child components/Elements/Directives

Existen decoradores que te permiten inyectar child elements dentro de un componente y manipularlos. 

* Los decoradores **en singular** toman el primer elemento que encaje en el parametro de busqueda
* Los decoradores **en plural** devuelven todos los elementos que encajen.
* Los decoradores **En plural** devuelven un ** QueryList ** que te da la posibilidad de **subscribirte al observable changes y recibir eventos cada vez que algo cambie**
* Las **querys se actualizan en tiempo real**, osea que si elmininas el elemento referenciado entonces **la seleccion puede cambiar o ser indefinida**.
* Podes seleccionar **el compoenente, el elementRef, una directiva o ViewContainerRef ** especificandolo con un parametro read

### 1) @ViewChild / @ViewChildren

Podes usar ViewChild para inyectar un component/Elemento/Directiva hijo dentro de un component padre y asi tener acceso y control total.

@ViewChild() **selecciona el primer componente hijo que pueda ser identificado** con el parametro que se le pasa. ademas si queres podes **elegir que seleccionar: ViewContainerRef, ElementRef o alguna directiva**

**La sintaxis es asi:**

````
//Sintaxis simple
  @ViewChild(MiQuery) nombreDeVariable: TypeDeVariable;
  
//con parametro read, en este caso quiero seleccionar el ElementRef
//osea el elemento del DOM directamente
  @ViewChild(MiQuery, {read: ElementRef}) nombreDeVariable: ElementRef;

````

**Donde: **

* **query** - se usa para determinar que elemento hijo se seleccionara. puede ser:
	* Template variable
	* Selector
	* Clase
* **nombreDeVariable** - nombre de la variable que sera poblado con el componente seleccionado
* **TypeDeVariable** - la clase del componente/elemento


>**Es importante notar que para acceder a un child component, este tiene que existir**, para asegurarte que el child component ya fue creado tenes que accederlo  **dentro del lifecycle hook AfterViewInit, que te garantiza que los child components ya estan instanciados.**


Ejemplo:

````
import {AfterViewInit, Component, Directive, ViewChild} from '@angular/core';

@Component({selector: 'someCmp', templateUrl: 'someCmp.html'})
class SomeCmp implements AfterViewInit {
  @ViewChild(ChildDirective) child: ChildDirective;

  ngAfterViewInit() {
    // Aca manipulas child
  }
}

````



Parametros que se pueden usar como querys son:
*  **Template variable**
````
<!-- Podes usar como query la variable de template miVariableDeTemplate-->
<mycomponent #miVariableDeTemplate></mycomponent>
<!-- Otro ejemplo, pero con un elemento HTML-->
<div #miVariableDeTemplate2></div>
````
````
// EN EL COMPONENTE
import { ViewChild,ElementRef} from '@angular/core';
//Presta atencion a los types.
 @ViewChild('miVariableDeTemplate') nombreDeVariable: mycomponent; 
@ViewChild('miVariableDeTemplate2') nombreDeVariable: ElementRef;
````

*  **Selector**
````
<!-- Podes usar como query la variable de template miVariableDeTemplate-->
<mycomponent></mycomponent>
````
````
// EN EL COMPONENTE
 @ViewChild('mycomponent') nombreDeVariable: mycomponentClass;
````

*  **Class** (si pasas la clase de un componente se selecciona la primera instancia) 
````
// EN EL COMPONENTE
 @ViewChild(mycomponentClass) nombreDeVariable: mycomponentClass;
````

### 2) @ContentChildren / @ContentChild

Identico a @ViewChild, pero sirve para seleccionar elementos que se insertaron en un componente mediante **proyeccion de contenido**

EJ:
````
<tab>
	<!-- quiero inyectar este contenido a mi componente tab -->
	<p>My contenido proyectado</p>
</tab>
````

````
@Component({
  selector: 'tab',
  template: `
   <ng-content></ng-content>
  `
})

// Lo que quiero inyectar va a ser proyectado en <ng-content> asique necesito usar 
//@ContentChild en vez de @ViewChild
@ContentChild('p') miContenido: ElementRef
````

---

## Crear componentes dinamicamente

Podes instanciar componentes en run-time si hiciera falta, por ejemplo si queres ir renovando componentes cada tanto (por ej publicidades que tiene estructuras distintas pero sabes donde las queres inyectar)


Podes usar **componentFactoryResolver** para instanciar un componente a partir de una clase. **Hay que instanciar los componentes en un ViewContainerRef**


````
// busco el contenedor donde quiero instanciar mi componente, necesito
// un ViewContainerRef
  @ViewChild('myDiv', { read: ViewContainerRef }) divContainerRef: ViewContainerRef;
  //La variable donde voy a almacenar mi componente es de tipo ComponentFactory
  myCompFactory : ComponentFactory<componenteAInstanciar>;
  
  //Inyecto el ComponentFactoryResolver
  constructor(private componentFactoryResolver: ComponentFactoryResolver) { }
	
  ngAfterViewInit() {
  //Creo la fabrica de componentes, que requiere como unico parametro
  //La clase de componente que queremos instanciar
    this.myCompFactory = this.componentFactoryResolver.resolveComponentFactory(componenteAInstanciar);
    //instanciamos el componente
    this.divContainerRef.createComponent(this.myCompFactory)
	
	//Si queres eliminar los componentes instanciados usas
	//this.divContainerRef.clear()
  }

````

>Si el componente que queres instanciar **no fue instanciado antes en el template entonces hay que agregarlo al array entryComponents del modulo al cual pertenece**

````
@NgModule({
  declarations: [ ....... ],
  imports: [.......],
  entryComponents: [ componenteAInstanciar ],
  providers: [......]
})
````
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTA2MzIzMjU5LC0xOTIwMjcwMjAzXX0=
-->