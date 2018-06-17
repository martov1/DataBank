
# Contenido:

* Creacion de proyecto
* Estructura de carpetas
* Patron de aplicaciones angunlar
* Crear Feature Modules
	* Hacer el modulo principal y el de routing
	*  Hacer componentes
	*  Hacer las rutas

## Crear proyecto

**Al crear** un nuevo proyecto con angular CLI, verificar lo siguiente:

1) Colocar todas las rutas en un solo archivo usando [--routing](https://github.com/angular/angular-cli/wiki/stories-routing)  y [--style=scss](https://github.com/angular/angular-cli/wiki/stories-global-styles)
````
 ng new testbed --routing --style=scss
```` 

2) usar [npm shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap) luego de instalar dependencias para controlarlas con exactitud

````
npm shrinkwrap
````

3) usar ng g para generar nuevos componentes, directivas, etc. son creados en nuevas carpetas <3 

## Estructura de carpetas

* **/src** : El codigo fuente de la app
 * **index.html** Lo primero que se carga, contiene el root component
 * **styles.scss** La hoja de estilos global, todos estos estilos se usan en toda la app
 *	**/assets** todo lo que se copiara tal y como esta (ej imagenes)
 *	**/environments** las variables de entorno de la aplicacion
 *	**main.ts** Entry point the la aplicacion
 * **/app** : toda la logica de la aplicacion
 	* **app-routing.ts** las rutas de la aplicacion
 	* **app.component.ts ** la logica del root component
 	* **app.component.scss ** los estilos del root component
 	* **app.component.html ** el html del root component
 	* **app.module.ts** el modulo del root, **carga los modulos de features**
 	* **/feature1**	
 		* **feature1-routing.ts** las rutas de la feature 1
 		* **feature1-guards.service.ts** los guards del feature
 		* **feature1.module.ts** el modulo de la feature 1. aca se carga **TODO** lo del feature
 		* **/comp1**
 			* **feature1.comp1.ts ** la logica del componente 1 de esta feature
 			* **feature1.comp1.scss ** los estilos  del componente 1 de esta feature
 			* **feature1.comp1.html ** el html  del componente 1 de esta feature
 		* **/comp2**
 			* **feature1.comp2.ts ** la logica del componente 1 de esta feature
 			* **feature1.comp2.scss ** los estilos  del componente 1 de esta feature
 			* **feature1.comp2.html ** el html  del componente 1 de esta feature
 	* **/shared** - aca van los modulos compartidos, ej: autenticacion etc
 		* **/auth**


## patron de aplicaciones angular


   * Cada feature tiene **su propia carpeta**
   * Cada feature tiene **su propio modulo**
   * cada feature tiene un **root component al que se llega con el router** con poco
   contenido y child routes, una de las cuales es la default con path ''
````js
     {
    path: '',							//root component
    component: CrisisCenterComponent,
    children: [							// child components con todos los components
      {									//para el feature.
        path: '',						//main component del feature
        component: CrisisListComponent
      },
	  {									
        path: 'blabla',
        component: CrisisblablaComponent
      }
    ]
  }
];
````
   * El feature root component tiene su **propio router outlet y child routes**


## Crear Feature Modules

### Hacer el modulo principal y el de routing

Para crear un Feature module, podes usar este comando de CLI

>ng generate module customers --routing

Esto te genera
* **/customers**  - Una carpeta para el feature
	* **CustomersModule**. - Un modulo para el feature
	* **CustomersRoutingModule** - Un routing module para el feature

### Hacer componentes

Para crear un componente en la carpeta del modulo hacemos:

>ng generate component customers/customer-list

### Hacer las rutas

En tu modulo de **routing pricipal**

````js
const routes: Routes = [
  {
    path: 'customers',
    loadChildren: 'app/customers/customers.module#CustomersModule'
  },
  {
    path: '',
    redirectTo: '',
    pathMatch: 'full'
  }
];
````
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcwMjgxODQ4NF19
-->