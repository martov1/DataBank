

# Contenido


* Setup
* Estructura de animaciones en angular
	* Definiendo las animaciones
	 * Triggers
	 * Estados
	 * Transiciones
	 * Transiciones con cambios de estilo
	 * :enter y :leave
	 * Lectura de propiedades en runtime
	 * Animaciones con varios pasos
	 * Animaciones paralelas
	 * Animar inner elements usando query
	 * Animation callbacks
* ejemplo completo
* Aplicando las animaciones a elementos HTML


## Setup

Primero hay que instalar la libreria de animaciones que viene separada
````
npm install @angular/animations@latest
````

hay que añadirlo al app.module.ts (o al modulo que desees)
````js
import{BrowserAnimationsModule} from '@angular/platform-browser/animations'
 
@NgModule({
	imports:[
	BrowserAnimationsModule
	]
})
````

Finalmente se carga en un component de ese modulo como metadata
````js
import{ { trigger, stylesate, style, animate, transition,state} from  '@angular/animations'';
@Component({ 
  animations:[animacion1, animacion2]
})
````

## Estructura de animaciones en angular

Las animaciones en angular consisten en **una lista de estados** y **transiciones entre esos estados**



## Definiendo las animaciones

Las animaciones `animacion1` y `animacion2` deben definirse, por ejemplo asi:

### Triggers

Un trigger es **el nombre de un conjunto de animaciones que se le puede asignar a un elemento**, por ejemplo un trigger puede contener las animaciones de click, mouseover, etc de un boton
````js
trigger('nombreDelTrigger',[estado1,estado2,transicion1,transicion2])
````

### Estados
Los estados son estilos que estan asignados a un nombre ej **botonClickeado**

````js
state('botonClickeado', style({
      backgroundColor: '#eee',
      transform: 'scale(1)'
    }))
````

### Transiciones
las transiciones son **animaciones entre dos estados**
se indica con una **=>** de que estado a que estado estas cambiando, podes usar **<=>** para indicar que se usa la misma animacion hacia ambos lados
Se indica la animacion que usas con **animate('duracion retraso nombreDeAnimacion')**

En lugar de usar el nombre del estado, podes usar ** * ** para indicar _cualquier estado_
````js
 transition('botonClickeado => botonNoClickeado', animate('200ms 100ms ease-in')),
````

### Transiciones con cambios de estilo

Tambien podes usar un array con style para decir como se ve el elemento inicialmente y animate para cambiarlo

````js
transition('inactive => active', [
  style({transform: 'scale(3)'}),     //al principio es grande
  animate('80ms ease-in', style({transform: 'scale(1)'})) //se anima y ahora es chico
]),
````

Podes separar varios estilos con comas

`style({opacity: 1, transform: 'translateX(0)',     offset: 0})`

### :enter y :leave

Algunos cambios de estado tienen un alias, por ejemplo
````js
transition(':enter', [ ... ]); // El elemento se crea
transition(':leave', [ ... ]); // el elemento se va
````

Estos son aliases para
 `void => *` y `* => void`, donde ** * ** es cualquier estado y **void** es un estado especial que todo componente tiene cuando no esta siendo renderizado

### Lectura de propiedades en runtime

Si necesitas usar una propiedad de un objeto que aparece en el momento (ej el alto de un div que esta puesto con %) podes usar el valor `'*'`

````js
transition(':leave', [			   	   // al desaparecer
      style({height: '*'}),            //La altura que tenga el objeto ahora
      animate(250, style({height: 0})) // animarla hasta cero
    ])
````

### Animaciones con varios pasos

Se utilizan **keyframes**  para indicar **varios estilos que se deben atravezar** en una animacion.
Cada keyframe tiene una propiedad **offset** que indica en que momento de la animacion se activan esos estilos, **donde 0 es el comienzo de la animacion y 1 el final**

Se usa mucho para hacer efecto _rebote_ de botones o para sacudirlos
````js
transition('void => *', [
      animate(300, keyframes([
        style({transform: 'translateX(-100%)', offset: 0}), //estilo inicial
        style({transform: 'translateX(15px)',  offset: 0.3}), //al 30% de la animacion
        style({transform: 'translateX(0)',     offset: 1.0}) //al final
      ]))
    ])
````

### Animaciones paralelas

Si queres hacer varias animaciones en paralelo, por ejemplo si tienen tiempos distintos, podes hacer **grupos** de animaciones

````js
transition(':enter', [
      group([
        animate('0.3s 0.1s ease', style({          //animacion 1
          transform: 'translateX(0)',
          width: 120
        })),
        animate('0.3s ease', style({               //animacion 2
          opacity: 1
        }))
      ])
    ])
])
````


### Animar inner elements usando query

Podes usar la funcion `query()` para buscar inner elements de tu componente

````js
query('.some-element-that-may-not-be-there, .otro-elemento, div, :self', [
  animate(...),
  animate(...)
], { optional: true })
````

si colocas **optional:true** entonces la funcion no tira error si intentas seleccionar un selector que no existe.

Podes usar estos selectores especiales

* ** :enter :leave **Querying for newly inserted/removed elements
* **:animating** Querying all currently animating elements
* **@triggerName** Querying elements that contain an animation trigger
* **@*** Querying all elements that contain an animation triggers
* **:self** Including the current element into the animation sequence using query("")



### Animaciones en cascada con stagger

Stagger te permite hacer animaciones en cascada, por ejemplo si tenes una lista de 10 elementos y queres que aparezcan uno despues de otro con un leve retraso (queda re lindo)

**Stagger** se usa dentro de **un query que define que elementos participan de la cascada**, dentro de la funcion se especifica la cantidad de milisegundos de retraso entre la animacion de los elementos y 

````js
transition('* => *', [ // each time the binding value changes
    query(':leave', [
      stagger(100, [
        animate('0.5s', style({ opacity: 0 }))
      ])
    ])
````


![enter image description here](https://lh3.googleusercontent.com/xOCSyCqDVB2WoCaXGi1MNYkLEGuaEcTk9XO7cTOdPY8fJxHzx7-sNs7qr1ij7TsnaQkaPa5X4V8Y)

### Animation callbacks

Podes llamar a una funcion cuando la animacion comienza o termina, la funcion recibe un 
`animationEvent` con los datos de la animacion.

````js
<li *ngFor="let hero of heroes"
        (@flyInOut.start)="miCallbackDeInicio($event)"
        (@flyInOut.done)="miCallbackDeFin($event)"
        [@flyInOut]="componente.miEstado">
    </li>
````

### Animaciones paralelas de parent y child

Si queres animar un elemento que ademas tiene animaciones en elementos child en interior, tenes que usar la funcion `animateChild()`. Si no lo haces **solo vas a ver las animaciones del parent y las del child son bloqueadas.**
````js
//defino la animacion child
trigger('animacio-hijo', [
	//States, transitions,etc
]),
//Defino la animacion padre y ejecuto las animaciones hijo
trigger('animacion-Padre', [
	//States, transitions, etc
	transition('true => false', [
	//Selecciono el trigger child y lo animo
		query('@animacio-hijo', [
			animateChild()
		]),
	])
]),
````

```html
<div [@animacion-Padre]="unaVariable" >
	<div [@animacio-hijo]="unaVariable">
	</div>
</div>
```
## ejemplo completo:
````js
animations: [
  trigger('heroState', [                         //animacion con estados
    state('inactive', style({
      backgroundColor: '#eee',
      transform: 'scale(1)'
    })),
    state('active',   style({
      backgroundColor: '#cfd8dc',
      transform: 'scale(1.1)'
    })),
    transition('inactive => active', animate('100ms ease-in')),
    transition('active => inactive', animate('100ms ease-out'))
  ]),
  trigger('queryAnimation', [                   //animacion con querys
     transition('* => goAnimate', [
       // hide the inner elements
       query('h1', style({ opacity: 0 })),
       query('.content', style({ opacity: 0 })),
       // animate the inner elements in, one by one
       query('h1', animate(1000, style({ opacity: 1 })),
       query('.content', animate(1000, style({ opacity: 1 })),
     ])
   ])
]
````



## Aplicando las animaciones a elementos HTML

Se coloca el nombre del **trigger** entre corchetes con una @, luego se coloca el nombre de la **variable que contiene el nombre del estado** que se desea representar.

**Cuando esa variable cambie a otro estado, el elemento se anima**

````js
<div [@nombreDelTrigger]="componente.unaVariable"
          (click)="hero.toggleState()">
        {{hero.name}}
      </div>
````

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ5MTk3NzkwMSwtNTQ2NTQzODYxLDEwMz
U1Mjg1MTZdfQ==
-->