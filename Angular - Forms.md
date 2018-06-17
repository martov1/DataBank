

Me quede en dynamic forms
https://angular.io/guide/dynamic-form#dynamic-forms

# Contenido

* Notas sobre documentacion
* Tipos de forms
	* Template based forms
		* NgForm 
		* NgModel 
	* Reactive forms
		* FormControl
		* FormGroup
		* FormFactory
		* FormGroups anidados
		* FormGroup - setear valores en el form
		* FormArray - para agregar controles dinamicamente
* Validacion



# Notas sobre documentacion

para documentacion de implementacion de angular con:

radio buttons
https://angular.io/api/forms/RadioControlValueAccessor
Selects
https://angular.io/api/forms/SelectControlValueAccessor
Checkboxes
https://angular.io/api/forms/CheckboxControlValueAccessor


---


# Tipos de forms

Existen dos formas de manejar forms en Angular.

* **Template based forms** - 
	* Faciles de crear
	* Menos flexibilidad
	* La mayoria del codigo esta en el template
	* Mas dificiles de testear
* **Reactive forms** 
	* Menos faciles de crear
	* Mas flexibles
	* La mayoria del codigo esta en el componente
	* Mas faciles de testear

---

# Template based forms

Utilizan directivas en el template para generar la mayor parte de la funcionalidad, principalmente **NgForm** y **NgModel**

## 1)NgForm

Se crea una instancia de NgForm cada vez que angular detecta un `<form>`.

* Podes acceder a la instancia mediante **template variables**
* Podes controlar que sucede cuando submiteas con el **evento ngSubmit**


NgForm tiene las siguientes propiedades y metodos:

* **ngForm.valid** te permite sabes si todos los datos son validos.
* **ngForm.valueChanges** - observable que dispara evento cuando cambia algo
* **ngForm.pristine** - True si el user aun no modifico el form
* **ngForm.dirty** -true si el user modifico el form
* **ngForm.touched** - true si el user toco el form
* **ngForm.errors** - contiene errores de validacion
* **ngForm.reset()** - Pone las propiedades en default y elimina los valores

EJ:

````html
<form (ngSubmit)="onSubmit()" #miForm="ngForm">
	
	<!-- submit no habilitado si los datos no son validos -->
	<button type="submit" [disabled]="!miForm.form.valid">
</form>
````

---


## 2) NgModel

Podemos usar ngModel para **Vincular el form con un modelo en el componente** 

cada instancia de la directiva ngModel:

* genera un **two way data binding**
* Tiene las **mismas propiedades que NgForm** pero para ese elemento
	* valid
	* dirty
	* pristine
	* etc
* **Añade clases CSS** al elemento basado en esas propiedades ya mencionadas

#### La sintaxis es

````html
<input type="text"  
	
	[(ngModel)]="variableModelo" // two way data binding
	name="unNombre"  			// requerido por angular forms
	#instanciaDeNgModel="ngModel"> <!-- opcional para acceder a las propiedades-->
	
	<!-- Ahora podes acceder a las propiedades de ngModel-->
	{{instanciaDeNgModel.valid}}
```` 


para esto necesitas:
* Que los elementos tenga un atributo **name**
* Una variable que actue de **modelo** en el componente

````
<form (ngSubmit)="onSubmit()" #heroForm="ngForm">
	<input type="text"  
	[(ngModel)]="model.alterEgo" 
	name="alterEgo"  
	#nameModel="ngModel"> <!--control form-->
	es valido: {{nameModel.valid}}
</form>
````

Adicionalmente en un form podes tener
* ** ngSubmit** como evento para detectar cuando el user hace un submit
* **Una variable de template apuntando a ngForm** para obtener una referencia al form


>NgModel tambien **agrega y remueve clases CSS** a los elementos del form
>
* **ng-touched/ng-untouched** Si se toco al elemento
* **ng-dirty/ng-pristine** si el valor ha cambiado
* **ng-valid/ng-invalid** si el valor es valido

---

## 2) Reactive forms 

Cuando usas Reactive forms, **creas un modelo detallado del form en tu componente** y despues lo aplicas al template.

>El modelo se compone de:
>
>* **FormControl** - Es el **bloque basico de construccion de forms**, permite vincular el component con un elemento del template
* **FormGroup** - Te permite **agrupar FormControls** para organizarlos mejor 



### Critico
>Ambos tienen **propiedades similares a NgForm** y podes accederlos **en el controler** o tambien **en el template**:
* valueChanges - Observable, emite evento si hay cambios
* valid
* invalid
* disabled
* dirty
* reset({nuevo estado}) - Propiedades en default, carga nuevo estado como patchValue()
* value (te da el valor del form como un hermoso Json)
* etc




## 2A)FormControl



El modelo detallado del form se genera con instancias de la clase **FormControl**, el componente luego puede pushear, pullear y reaccionar a cambios en el form.



Al crear un FormControl podes colocar **tres argumentos opcionales**.
* El **valor incial** que tendra ese campo en el form
* un **array de validators** que validaran el campo del form
* un **array de async validators** que validaran el campo en el form

a su vez lo vinculas con el template usando `[formControl]="nombreDeVariable"`

Una vez vinculado actua como un **two way databinding**

sintaxis:
````
  <!-- Esta sintaxis te sirve si no estas en un formGroup-->
  <input  [formControl]="miVariable">

````

````
  miVariable = new FormControl(valorInicial, [validators], [async validators]);
  
  //LEER VALORES
  miVariable.value //el contenido del formControl
````



## 2B)FormGroup

Un formGroup puede contener varios FormControls
La  **clase FormGroup** busca una instancia de la **Clase FormGroup** en el componente y la asocia a ese componente.

Podes acceder a todos los valores del form con **FormGroup.value** en una hermosa estructura JSON

>Cada **FormControl** tiene que tener un atributo **formControlName** que **indique el nombre del FormControl dentro del FormGroup**


Sintaxis:
````
// Genero un FormGroup con todos los FormControl dentro
miFormGroup = new FormGroup ({
    miFormControl1: new FormControl()
	miFormControl2: new FormControl(valorInicial1, [validador1])
  });
 
 //LEER VALORES
miFormGroup.value //Json de todos los valores del formGroup
miFormGroup.get('miFormControl1').value //leer el valor de algo en el formGroup

````

````
<!-- novalidate evita que el browser haga validaciones HTML-->
<form [formGroup]="miFormGroup" novalidate>
	  <!-- hay que aclarar como se llama el FormControl dentro del FormGroup-->
	  <!-- Para eso usamos formControlName -->
      <input  formControlName="miFormControl1">
	  <input  formControlName="miFormControl2">
</form>


mi form es valida?:  {{miFormGroup.valid}}
````

## 2C) FormBuilder

Te permite declarar FormGroups y FormControls de forma mas simple y legible. basicaente te ahorras escribir `new FormControl(valorInicial)`.

Esto:
````
// Genero un FormGroup con todos los FormControl dentro
miFormGroup = new FormGroup ({
    miFormControl1: new FormControl(valorInicial1)
	miFormControl2: new FormControl(valorInicial2, [validador1])
  });
````

Se traduce a esto

````
	this.miFormGroup = this.formBuilder.group({
      miFormControl1: valorInicial1, 
	  miFormControl2: [valorInicial2, Validator1 ], 
    });
````

EJ:
````
this.heroForm = this.fb.group({
      name: ['', Validators.required ],
      street: '',
      city: '',
      state: '',
      zip: '',
      power: '',
      sidekick: ''
    });
````

## 2D) FormGroups anidados

Podes anidar FormGroups, esto te permite facilitar la validacion de a pedazos y juntar los datos en una estructura JSON con mas sentido

````
this.heroForm = this.fb.group({ // <-- the parent FormGroup
      name: ['', Validators.required ],
      address: this.formBuilder.group({ // <-- the child FormGroup
        street: '',
        city: '',
      })
    });
	
//LEER VALORES
this.heroForm.get('address.street').value //obtener el valor de algo anidado
this.heroForm.value 	//Obtener todos los valores como Json
````

Fijate que en el template hay que agrupar los FormControls que corresponden al nuevo FormGroup dentro de un div con la directiva `formGroupName` apuntando al FormGroup anidado
````
<form [formGroup]="heroForm" novalidate>
	<input  formControlName="name">
	<!-- apunta al formgroup "adress" -->
	<div formGroupName="address" class="well well-lg">
	      <input formControlName="street">
	      <input  formControlName="city">
	</div>
</form>	
````

## 2E)FormGroup - setear valores en el form

Una vez que armaste el **form model** con los FormControls y FormGroups, tal vez quieras colocar una serie de datos provenientes del server en el form que creaste, esto se puede hacer con `patchValue` o `setValue`

* **patchValue()** -  Setea los valores de algunas propiedades del modelo, falla silenciosamente 
* **setValue()** - Setea los valores de todas las propiedades del modelo, da error si falta alguna propiedad por setear o si hay propiedades de mas

Sintaxis:
````
setValue({
	formControl1: valor1,
	formControl2: valor2
	formGroup1:{
		formControl3: valor3
	}
})
````

## 2F)FormArray - para agregar controles dinamicamente

A veces queres tener forms que no tienen un tamaño definido. Ej: un form donde queres que el usuario pueda agregar una **cantidad indetermidada de personas**, entonces con un boton **añade mas campos** al form.

Para eso esta el **FormArray**

````
//Sin notacion formBuilder
const arr = new FormArray([formControl1, formGroup1,formGroup2, .. ]);

//Notacion formbuilder
const addressFormArray = this.fb.array([formControl1, formGroup1,formGroup2, .. ]);

//agregar el array a un FromGroup, en este caso heroForm
this.heroForm.setControl('miFormArray', addressFormArray);

//Obtener el array de el FormGroup
this.heroForm.get('miFormArray') as FormArray;

//agregar un formGroup al FormArray
//Creo el FormGroup
miNuevoFormGroup = this.fb.group([formControl1, formGroup1,formGroup2, .. ]);
//Lo añado al array
this.heroForm.get('miFormArray').push(this.fb.group(miNuevoFormGroup));

````

Para mostrarlo en el template usamos la directiva **fromArrayName**

````
<div formArrayName="secretLairs" class="well well-lg">
  <div *ngFor="let address of miFormArray.controls; let i=index" [formGroupName]="i" >
    <!-- The repeated address template -->
  </div>
</div>
````

# Validacion
Podes usar los **medotodos de validacion estandar de HTML**


Tambien podes usar **Validator functions** si fuera necesario, que pueden ser

* **sync validator functions** - inmediatamente devuelven ya sea un error de validacion o null si la validacion es correcta
* **async validator functions** - devuelven un observable que se transformara en un error de validacion o en null. esa bueno si queres mandar algo al server

> hay funciones validator predefinidas con los mismas funciones de validacion que la validacion HTML
<!--stackedit_data:
eyJoaXN0b3J5IjpbODExMDA0NTIwXX0=
-->