  
  
# Contenido:

* Consideraciones
* Comunicacion view -> component
	* Escuchar eventos
	* Eventos predefinidos
* Comunicacion componente -> view
	* Interpolacion 
	* Property binding a estilos, propiedades de DOM
* Comunicacion componente1->view->componente2
	* Property binding a componentes y directivas 
	* Eventos customizados 
* comunicacion view <->component
* Reference variables 
* Pipes


# Consideraciones

**1)** el tag `<script>` esta prohibido para evitar atques de script inyection. **Angular sanitiza los tags de todos lados para sacarla**

**2)** Cada vez que bindeas algo, bindea a un **DOM property y no a un HTML Attribute**, es decir, cambia las cosas en el objeto JS que representa a ese elemento HTML. es importante porque no todas las propiedades tienen el mismo nombre que los atributos.

**Atributo HTML**
`<p style="algo"></p>`

**Propiedad del DOM**
`P.style`

>Los atributos estan en la propiedad **attr** del DOM en caso de que quieras modificarlos.

**3)** En un template solo podes usar aquellos componentes, directivas y pipes que:
* Esten en el **array de declarations** del modulo del componente que tiene el template
* Esten en el **array de exports** de un modulo que estes **importando**



---

# Comunicacion view -> component


## 1) Escuchar eventos

El view puede escuchar eventos que suceden y activar funciones o modificar valores en el componente, esto se hace mediante **Template statements**

* Los **Eventos** pueden ser nativos del DOM o custom events de una directiva
* Los **Template statements** son similares al codigo JS y pueden referenciar a valores del component, asignar valores o llamar funcione
* Con **$event** podes acceder al Evento.

**La sintaxis para escuchar eventos es:**

```` js
(evento)="Template statements" 
````


 **EJ:**
````html
 <button (click)="miFuncion($event)">Delete hero</button>
````
 
 En el componente:
 
````js
 miFuncion(event: MouseEvent) { 	// with type info
    this.values += (<HTMLInputElement>event.target).value + ' | ';
  }
````
 
## 2) Eventos predefinidos

Podes usar **cualquier evento del dom sin el prefijo ON**
lista: https://www.w3schools.com/jsref/dom_obj_event.asp

* **Keyup** -- Disparado cuando el usuario suelta cualquier tecla
* **Keyup.enter.control.alt.N** -- Disparado cuando el usuario suelta la/s teclas definidas
* **click** -- Disparado al hacer click
* **blur** -- Disparado cuando el usuario sale del focus del elemento (click afuera)
* **Keypress** -- Disparado cuando el user apreta una tecla
* **Keypress.enter.q** -- Disparado cuando el user apreta teclas predefinidas

---
# Comunicacion componente -> view

Se hace mediante 
* **Interpolacion**
* **Property binding**
* **Emision de eventos**

## 1) Interpolacion

>Angular reemplaza lo que hay entre {{  }} por variables o el resultado de una expresion


simplemente colocas el nombre de la variable del component en el template entre corchetes
El **template es actualizado cuando los valores cambian**

* Podes modificar **propiedades** (detras de escena es un property binding!)
* Podes llamar **funciones**
* Podes hacer **evaluaciones** basicas
* Solo pueden mostrar cosas dentro del component o el contexto del template
* Podes **evitar mostrar undefined o null** con un guard `{{currentHero?.name}}` usando el operador **?**, podes encadenar paths `{{a?.b?.c?}}`. si la propiedad no existen entonces queda en blanco.

````html
<!--- En texto -->
<p>{{myHero}}</p> 	
<!--- En una propiedad -->
<img src="{{heroImageUrl}}" style="height:30px"> 	
<!--- llamando funciones o haciendo calculos -->
<p> el resultado es: {{1 + 1 + getVal()}}</p> 
````

## 2) Property binding

>Asigna el valor de una variable/funcion del componente a **propiedad del DOM, componente ó directiva**

Detras de escena, si haces una interpolacion tal como  `<img src="{{heroImageUrl}}" >`
Angular genera un property binding.

en forma generalizada, es asi:
````js
[target]="expression"
````

Ej:
````html
//bindeas una propiedad del componente a  la propiedad SRC del DOM
<img [src]="heroImageUrl" style="height:30px">

//Colocas condicionamente una propiedad CSS en particular
<button [style.color]="isSpecial ? 'red': 'green'">Red</button>

//Activas condicionalmente una clase
<div [class.miClase]="activada">Este div tiene la clase "miClase"</div>
````


---
# Comunicacion componente1->view->componente2
 
 
 ## 1) Property binding

>Asigna el valor de una variable/funcion del componente a **propiedad del DOM, componente ó directiva**



>Para asignar valores a componentes o directivas tenes que** configurarles esa 
>variable como @Input()**

en forma generalizada, es asi:
````js
[target]="expression"
````


Ej:
````html
//Bieneas una propiedad del component a una variable
//Para hacer esto necesitas que hero tenga el decorador @input!!!
<app-hero-detail [hero]="currentHero"></app-hero-detail>

//Bindeas una propiedad del componente a una propiedad de una directiva
<div [ngClass]="classes">[ngClass] binding to the classes property</div>
````



 ## 2) Emitir eventos custom
 
> Un component puede emitir eventos custom asi para que despues sean escuchados por los parent components en el view.

>**Para emitir eventos necesitar usar @output**

**Emitis** un evento custom asi: 
````js
//mi componente
@Output() miEvento = new EventEmitter<Hero>();

//cuando llamas a esta funcion emitis el evento!.
decirHola() {
  this.miEvento.emit("hola!");
}
````

Despues **escuchas** en el view a ver cuando sucede el evento y haces algo al respecto,
Esto puede suceder en un **parent component ó directive**.

````html
//un parent component que escucha un evento custom
<app-hero-detail (miEvento)="escucharHola($event)">
	<!-- Cuando haces click en el componente, se emite un evento custom "hola" -->
	<mi-componente (click)="decirHola()" ></mi-Componente>
</app-hero-detail>
````
 
 
 ---

# comunicacion view <->component

Es una mezcla de las dos sintaxis anteriores. es basicamente lo mismo que usar un evento para comunicar view->component y un property binding para comunicar component->view.

>**Para asistirte en la creacion de este binding podes usar NgModel, que hace
>todo mas practico y menos verboso, pero solo sirve para forms y 
>elementos HTML estandar**

En el template se implementa de la siguiente forma
* Al cambiar el **target**, el valor de la variable expresada en la **expresion** cambia.
* Al cambiar el valor de la **expresion** cambia el valor del **target**
````js
[(target)]="expresion"
````

Mas concretamente
```` html
<!-- en el template-->
<miComponente [(miVariable)]="miOtraVariable" >
	{{miOtraVariable}}
	<button (click)="cambiarMiVariable()" >
</miComponente>
````


Para implementarlo en el componente necesitas:
* Un `@Input` con `miVariable`, osea el **target**
* Un `@Output` de tipo `EventEmitter` llamado `miVariableChange` 
* Hacer **manualmente** que `miVariableChange` emita el nuevo valor cuando el **target miVariable** sea modificado, por ejemplo dentro de la funcion `cambiarMiVariable()`

Lo que hace angular entonces con la expresion del template es analogo a hacer un **property binding** para **setear una variable en el view** y un **event listener** para **actualizarla en el componente** cuando cambie en el view.

```` html
<!-- en el template-->
<miComponente 
[miVariable]="miOtraVariable" 				//property binding comun: component->view
(miVariableChange)="miOtraVariable=$event" > //event binding comun: view->component

{{miOtraVariable}}
	<button (click)="cambiarMiVariable()" >
</miComponente>
````


EJ:

En el template
````html
<app-sizer [(size)]="fontSizePx">
</app-sizer>
````

en el component
````js
import { Component, EventEmitter, Input, Output } from '@angular/core';
// En el Template hay botones para cambiar la variable target mediante
//Una funcion que ademas emite un evento para notificarle al view del cambio
@Component({
  selector: 'app-sizer',
  template: `
  <div>
    <button (click)="dec()" title="smaller">-</button>
    <button (click)="inc()" title="bigger">+</button>
    <label [style.font-size.px]="size">FontSize: {{size}}px</label>
  </div>`
})
export class SizerComponent {
  //Size puede ser seteado desde afuera, del view al component
  @Input()  size: number | string;
  @Output() sizeChange = new EventEmitter<number>();

  dec() { this.resize(-1); }
  inc() { this.resize(+1); }
  resize(delta: number) {
    this.size = Math.min(40, Math.max(8, +this.size + delta));
	  //Emito un evento cuando cambio la variable para que el view la actualize
    this.sizeChange.emit(this.size);
  }
}
````


---
# ReferencTemplate variables

Son variables que se pueden colocar en el template y referencian un **DOM element, component o directive**. pueden realizar cambios o lecturas directamente sobre esa variable

Estas variables se pueden usar **en todo el template**

La sintaxis para la variable que queres referenciar es
* **#nombreDeVariable** 
* **ref-nombreDeVariable**

Ej en un elemento del DOM con propiedades estandar
````html
//guardo este DOM element en #phone
<input #phone placeholder="phone number"> 
//accedo a su propiedad  nativa·"value" y la uso.
<button (click)="callPhone(phone.value)">Call</button> 
<p>el numero de telefono es: {{phone.value}}</p>
````

Ej en una directiva, en este caso NgForm

*Nota: recorda que cuando importas FormsModule todos los tags  `<form>` se transforman en directivas NgForm*
````html
//accedi a las variables de esta instancia de NgForm
<form (ngSubmit)="onSubmit(heroForm)" #heroForm="ngForm">
  <div class="form-group">
    <label for="name">Name
      <input class="form-control" name="name" required [(ngModel)]="hero.name">
    </label>
  </div>
  <button type="submit" [disabled]="!heroForm.form.valid">Submit</button>
</form>
<div [hidden]="!heroForm.form.valid">
  {{submitMessage}}
</div>
````


---
# Pipes

Son **funciones simples** que **transofrman un input antes de mostrarlo en el template**, hacen cosas como colocar simbolos, agregar mayusculas, pasar todo a mayusculas/minusculas, etc.

Utilizan el simbolo de pipe **|**
````html
//La sintaxis es:
// {{ variable | nombreDeFuncionPipe }}
// Por ejemlo:
	
<div>Title through uppercase pipe: {{title | uppercase}}</div>
	
//podes encadenar varias funciones pipe
{{title | uppercase | lowercase}}

//Tambien podes pasar parametros
<div>Birthdate: {{variable | nombreDeFuncionPipe:'valorParametro'}}</div>
<div>Birthdate: {{currentHero.birthdate | date:'longDate'}}</div>
````

> el pipe Json es util para debugear cosas!
> `<div>{{currentHero | json}}</div>`





> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAzMzE1MDI4MiwxOTM0NzAwMCwtNDc5MT
M5NjE1LDExNjgzNjA0MDJdfQ==
-->