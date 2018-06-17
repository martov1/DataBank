
Ver structural directives
https://angular.io/guide/structural-directives

me quede en
https://angular.io/guide/attribute-directives#respond-to-user-initiated-events

# Contenido:

* Que es
* Directivas comunes
	* ngFor
	* ngIf
	* ngClass
	* ngStyle
	* ngModel
	* NgSwitch 
* Attribute directives customizadas
	* sintaxis


## Que es

Las directivas son basicamente componentes sin templates que se encargan de mutar el HTML donde se las coloca, hay de dos tipos

* Estructurales
 >Modifican el HTML añadiendo, removiendo o reemplazando elementos del DOM, como
 >*ngFor, *ngIf

*  De atributo
 >Modifican la apariencia o comporamiento de un elemento existente, por ejemplo ngModel, ngStyle o ngClass


---


## Directivas Comunes

### *ngFor


Repite el elemento en ngForel que se encuentra la directiva una vez por cada elemento dentro del array "heroes". podes acceder a cada objeto iterado usando hero

````
 <h1>{{title}}</h1>
  <h2>My favorite hero is: {{myHero}}</h2>
  <p>Heroes:</p>
  <ul>
    <li *ngFor="let hero of heroes">
      {{ hero }}
    </li>
  </ul>
````

Tambien podes obtener el **index**
````
<div *ngFor="let hero of heroes; let i=index">{{i + 1}} - {{hero.name}}</div>
````

Tambien podes indicarle a Angular **cuando tiene que recrear los elementos del DOM y cuando no**, ya que por default **al detectar un cambio destruye y recrea todos los elementos de la lista**

EJ: ejecute trackByHeroes() para cada elemento, si devuelve algo diferente que la vez anterior entonces cambia **ese elemento** del DOM
````
trackByHeroes(index: number, hero: Hero): number { return hero.id; }
````

````
<div *ngFor="let hero of heroes; trackBy: trackByHeroes">
  ({{hero.id}}) {{hero.name}}
</div>
````


>Podes obtener otros valores, tales como **First, last, even y odd**
>ver: https://angular.io/api/common/NgForOf

### *ngIf

Agrega el elemento en el que esta la directiva al DOM si se cumple una condicion (da true)

Ej: mostrar solo si hay mas de 3 heroes
````
<p *ngIf="heroes.length > 3">There are many heroes!</p>
````

### ngClass

Sirve para colocar clases en un elemento


>Con el ultimo ejemplo se pueden controlar las clases desde el component

````

//como lista de strings
<some-element [ngClass]="'first second'">...</some-element>

//como array de strings
<some-element [ngClass]="['first', 'second']">...</some-element>

//como objeto armados con key siendo el nombre de la clase y un valor
//booleano para determinar si la clase debe ser activada.
<some-element [ngClass]="{'first': true, 'second': true, 'third': false}">...</some-element>

//Igual que el anterior, pero el objeto esta declarado en el component.
//Cuando cambie el objeto en el component las clases se actualzan en tiempo real
<some-element [ngClass]="myObjetoDeComponent"></some-element>

````


### ngStyle

Sirve para asignar estilos CSS a un elemento
````
<div [ngStyle]="enItalics ? 'italic' : 'nombal'">
  This div is initially italic, normal weight, and extra large (24px).
</div>
````

Puede responder a un objeto con key-value pairs

````
<div [ngStyle]="{font-style:italic,font-weight:bold}">
  This div is initially italic, normal weight, and extra large (24px).
</div>
````

El objeto puede estar en el component

````
<div [ngStyle]="miObjeto">
  This div is initially italic, normal weight, and extra large (24px).
</div>
````

````
//En el component
setCurrentStyles() {
  // CSS styles: set per current state of component properties
  this.currentStyles = {
    'font-style':  this.canSave      ? 'italic' : 'normal',
    'font-weight': !this.isUnchanged ? 'bold'   : 'normal',
    'font-size':   this.isSpecial    ? '24px'   : '12px'
  };
}
````

### ngModel

Forma parte del **FormsModule** y sirve para **formar un two-way databinding en forms** 


Es similar a lo que vimos en two way data binding, solo que mas comodo para forms


> Es una **abstraccion muy simple** que sabe **que evento escuhar** para cada cada **tipo de input** estandar y lo asigna a la variable que designas
>
>**Esa es la razon por la que no funciona en otra cosa que no sean forms estandar, tendrias que usar el two way binding comun para eso**

esto:

````
<input [(ngModel)]="currentHero.name">
````

Es sinonimo de esto:

````
//Value e Input son propiedades y eventos nativos del DOM object de <input>
<input [value]="currentHero.name"
       (input)="currentHero.name=$event.target.value" >
````

Tambien existe una forma extendida por si necesitaras hacer algo con los datos antes de guardarlos

````
<input
  [ngModel]="currentHero.name"
  (ngModelChange)="hacerAlgoConLosDatos($event)">
````

### NgSwitch 

Basado en una condicion, muestra uno de varios posibles elementos.

**ngSwitchngSwitch** esta vinculado a una variable, si la variable coincide con
algun valor de **ngSwitchCase** entonces se muestra el elemento con esa directiva y
se oculta el resto.

** *ngSwitchDefault ** es el elemento que sera elegido si la variable asignada a
ngSwitch no tiene un valor o el valor no es un ngSwitchCase

````
<div [ngSwitch]="currentHero.emotion">
  <app-happy-hero    *ngSwitchCase="'happy'"    [hero]="currentHero"></app-happy-hero>
  <app-sad-hero      *ngSwitchCase="'sad'"      [hero]="currentHero"></app-sad-hero>
  <app-confused-hero *ngSwitchCase="'confused'" [hero]="currentHero"></app-confused-hero>
  <app-unknown-hero  *ngSwitchDefault           [hero]="currentHero"></app-unknown-hero>
</div>
````
![](http://i.markdownnotes.com/switch-anim.gif)


---
## Attribute directives customizadas

Recordemos que las **Attribute directives** son aquellas que **Modifican la apariencia o comporamiento de un elemento existente**, por ejemplo ngModel, ngStyle o ngClass

Algunas caracteristicas basicas son:

* **Selector entre corchetes** para significar que es un atributo 
* Hay que agregarlas a **declarations** en el modulo que las contendra


### Sintaxis:


````
import {Directive} from '@angular/core'

@Directive({
	selector:[MySelector]
})

export class MiDirectiva{
	//ahora podes acceder al elemento donde esta la directiva y hacer
	//lo que quieras
	constructor(private el: ElementRef){}
}
````

Uso:
````
<p MySelector> contenido!</p>
````



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NjY4OTMxNzhdfQ==
-->