
# Contenido:

* Capacidades
*  Setup
 * Elemento base
 * Configurar rutas
 * Router outlet
 * Child routes
* Links
	* Link activo y css
	* Links Dinamicos
	* Absolute y Relative paths
	* Links con parametros
* Router
	* Consideraciones
	* Estado actual del router y parametros
	* Eventos de Router
	* Navegacion imperativa
	* Rutas Secundarias
* Lazy loading
* pre loading
	* Estrategia PreloadAllMoudels
	* Estrategia custom
* Route guards
	* CanActivate
	* CanDeActivate
	* Resolve
	* canLoad


## Capacidades

El router puede hacer las mismas cosas con las URL que el navegador, tales como 
* volver **atras** e ir **adelante**
* interpretar o enviar **parametros** como `sitio/users:214`
* vincular **html como hipervinculos** 
* navegar **programaticamente** usando funciones
* Tener rutas y componentes **anidados** como  `sitio/users/about`
* Pedir **confirmacion** antes de salir de una ruta
* **Redireccionar** al usuario (ej 404)
* asignar **clases CSS** a elementos dependiendo de la ruta activa
* obtener **informacion de la ruta actual**
* Cuando el navegador cambia de ruta, **el router activa una instancia del componente esppecificado**

---
## Setup

El router **no forma parte del Angular core**, hay que importarlo 
````js
import { RouterModule, Routes } from '@angular/router';
````



Si creaste la aplicacion con --router en AngularCli entonces las rutas se generan en un modulo separado ubicado en el archivo `app-routing.module.ts`, el mismo exporta una instancia del modulo `RouterModule` configurada con las **rutas necesarias** para ser **consumida por el modulo principal de la aplicacion.**

````js
import { NgModule }              from '@angular/core';
import { RouterModule, Routes }  from '@angular/router';
import { CrisisListComponent }   from './crisis-list.component';
const appRoutes: Routes = [
  { path: 'crisis-center', component: CrisisListComponent }
];
@NgModule({
  imports: [
    RouterModule.forRoot(		// configuro RouterModule
      appRoutes
    )
  ],
  exports: [
    RouterModule				//Lo exporto para su uso en otro modulo
  ]
})
export class AppRoutingModule {}
````
**Tambien hay que importar los components que seran cargados en cada ruta**

### Elemento base

Le indica al _router_ cual es la URL de la que nacen las rutas, si la carpeta app esta en la aplication root entonces tenes que colocar `<base href="/">` justo despues de `<head>`.

* `<base href="/">` - Las rutas empiezan con **www.dominio.com/**
* `<base href="/misitio/">` Las rutas comenzaran con **www.dominio.com/misitio/**

### Configurar rutas

Las rutas se pueden definir en un array de objetos que describe como es cada ruta, luego se puede pasar a la funcion `RouterModule.forRoot(MisRutas)` si estas inicializando el router o a `RouterModule.forChild(MisRutas)` si el router ya se inicializo.


* **cada ruta mapea una URL a un componente**
* **No** se usan leading slashes
* Los **parametros** se definen como `/:nombreDeParametro`
* Podes guardar datos **estaticos de solo lectura** como titulos o tags en la propiedad **data**
* La **ruta default** se simpoliza con **' '**, se va ahi cuando no hay un route en la url
*  la **ruta que no corresponde a ninguna otra** se simboliza con ** dos asteriscos **  y se usa para llegar a una pagina 404, tiene que ir al final
* **El orden importa**, la primera ruta en hacer un match gana
* podes **redireccionar** colocando `redirectTo: '/otroPath'`
* enableTracing loguea los eventos del router, permite hacer **debugging**

````js
const misRutas: Routes = [
  { path: 'crisis-center', component: CrisisListComponent },
  { path: 'hero/:id',      component: HeroDetailComponent },     //parametros
  {
    path: 'heroes',
    component: HeroListComponent,
    data: { title: 'Heroes List' }								//datos estaticos
  },
  }
  { path: '',
    redirectTo: '/heroes',        								//redirect
    pathMatch: 'full'						//redireccionamos cuando TODA la URL es ''
  },
  { path: '**', component: PageNotFoundComponent }					//404
];
@NgModule({
  imports: [
    RouterModule.forRoot(
      misRutas,
      { enableTracing: true } // <-- debugging purposes only
    )
    // other imports here
  ],
  ...
})
export class AppModule { }
````


### Router outlet

El tag

````html
<router-outlet></router-outlet>
<--Los componentes se agregan aca-->
```` 

Le indica al router donde tiene que colocar los elementos de la ruta en la que esta, el elemento de esa ruta se colocara **debajo** del router outlet, **no en su interior**


### Child routes

Los child routes son rutas cuyos componentes aparecen en **un router outlet que esta en el parent component.**

Notese que **los path de los child components siempre son relativos al path del parent component**

>En este ejemplo el componente **CrisisCenterComponent** tiene un router outlet donde aparecera **CrisisListComponent**, este a su vez tiene un router outlet donde, dependiendo del path, aparece **CrisisDetailComponent** o **CrisisCenterHomeComponent**
````js
const crisisCenterRoutes: Routes = [
  {
    path: 'crisis-center',
    component: CrisisCenterComponent,
    children: [
      {
        path: '', 				//<---- path relativo al parent component!
        component: CrisisListComponent,
        children: [
          {
            path: ':id',
            component: CrisisDetailComponent
          },
          {
            path: '',
            component: CrisisCenterHomeComponent
          }
        ]
      }
    ]
  }
];
````

---
## Links

Los cambios de URL pueden hacerse normalmente desde el navegador poniendo una URL arbitraria, pero tambien podemos usar botones como se hace convencionalmente usando **routerLink**

````html
 <nav>
    <a routerLink="/crisis-center" >Crisis Center</a>
    <a routerLink="/heroes">Heroes</a>
  </nav>
````

### Link activo y css

Ademas usando **routerLinkActive** el router le asignara **clases CSS** al elemento cuya ruta coincida o sea un padre de la ruta actual en la que esta el navegador.


````html
 <nav>
    <a routerLink="/crisis-center" routerLinkActive="unaClaseCSS otraClaseCSS">Crisis Center</a>
    <a routerLink="/heroes" routerLinkActive="unaClaseCSS">Heroes</a>
  </nav>
````

Si queres que las clases se activen solo si **la ruta coincide exactamente**, es decir, si no queres que se active para `/crisis-center/otracosa`, hay que colocar `[routerLinkActiveOptions] =  { exact: true }`

asi:
````html
 <nav>
    <a routerLink="/crisis-center" routerLinkActive="unaClaseCSS otraClaseCSS" [routerLinkActiveOptions] =  { exact: true }>Crisis Center</a> 
  </nav>
````


### Links Dinamicos

Las **rutas pueden ser dinamicas** y estar conformadas por variables del componente.

`<a routerLink="['/team', teamId, 'user', userName, {details: true}]">link to user component</a>`

Generaria la ruta `/team/11/user/bob;details=true`

### Absolute y Relative paths

Si el path comienza con `/` entonces el router va a **buscar la ruta desde el root de la aplicacion**
`<a routerLink="/about">link to user component</a>`

Si no comienza con nada o comienza con `./` entonces el router **busca la ruta como child de la ruta actual**

### Links con parametros

Podes añadir parametros de las siguientes maneras

**Desde un objeto en el array routerlink**

* `<a routerLink="['/team',{details: true}, hero.id]">link to user component</a>`
Generaria la ruta `/team;details=true`

**Con la directiva queryparams**, tambien podes vincular con un achor tag de la pagina usando **fragment** para scrollear a una parte particular de esa pagina apenas carga
* `<a [routerLink]="['/user/bob']" [queryParams]="{debug: true}" fragment="education">` generaria la ruta `/user/bob#education?debug=true`

---

## Router

### Consideraciones
El router es un ** servicio singleton**, como tal solo hay que crearlo **una vez**, la creacion sucede con la siguiente funcion

`RouterModule.forRoot(MisRutas)`

**Se espera que se llame a esta funcion en tu modulo principal** como su nombre lo indica.

Si queres añadir rutas en modulos que se cargan despues de la inicializacion de la aplicacion (lazy loading) entonces **hay que usar la siguiente funcion en los modulos que se cargan despues de que el router** ya se inicializo

`RouterModule.forChild(MisRutas)`


**cualquiera de las dos funciones devuelve un modulo** conteniendo una instancia del servicio **router** configurado con esas rutas. **Despues del bootstrap de la aplicacion el router realiza la primera navegacion** (generalmente a la ruta vacia ** ' '** )

Al usar `RouterModule.forChild(MisRutas)` para crear un **modulo nuevo con rutas, hay que exportarlo e importarlo en el modulo que contiene los componentes para esas rutas y a su vez importar este al modulo principal**


````
				es importado a						es imporado a
Modulo de rutas --------------->modulo de feature ---------------> main module
````

No olvides importar en el  modulo principal el modulo de rutas principal **despues** de todos los demas modulos con rutas, porque las rutas se matchean en un **first found basis**


 EJ:
````js
 //este es el modulo principal
 imports: [
  BrowserModule,
  FormsModule,			//Este es un modulo de rutas y componentes periferico
  HeroesModule,			//Este es un modulo de rutas  y componentes periferico
  AppRoutingModule     // Este es el main
]
````

para mas detalles: https://angular.io/guide/router#milestone-3-heroes-feature

### Estado actual del router y parametros

Con este proposito se puede leer la **instancia actual** de `ActivatedRoute` y leer sus propiedades.
La instancia actual se encuentra en `router.routerState;` o se puede importar directamente como servicio

**el router guarda un historial de todos los `ActivatedRoute` en los que se estuvo desde que arranco la aplicacion**

````js
import { Router, ActivatedRoute, ParamMap } from '@angular/router';
@Component({...})
class MyComponent {
  constructor(private route: ActivatedRoute) {
  	this.route.paramMap.subscribe(
	parametros => this.variableDondeGuardoAlgo = parametros.get('miParametro'))
  }
}
````

Podes acceder a las siguientes propiedades
![enter image description here](https://lh3.googleusercontent.com/tN03l_wFD9op2J5R0OevXA3L-hHD0wRO5ZypQm0wz1AmGK809sAnu5P6uVn0nrV8_0yVE9VaIUL1)

### Eventos del router

El Router **emite eventos al navegar** a travez de `Router.events` en forma de **observables**

Estos son los eventos emitidos:


![enter image description here](https://lh3.googleusercontent.com/y39hWLvcbfKA93qbSPN7xQMhV_XL6gaG3Px8vODN1awU7sY3Js0qpTlknNNkjEqCadIlfdu9fR6g)

### navegacion imperativa

Podes navegar de forma imperativa, la sintaxis de array es igual que la de links dinamicos.

`this.router.navigate(['/heroes', { id: heroId, foo: 'foo' }]);`

para navegar de forma **relativa** tenes que proveeer el ActivatedRoute
````js
constructor(private route: ActivatedRoute) {}
this.router.navigate(['../'], { relativeTo: this.route });
````

Podes configurar un NavegationExtras para que **mantenga los queryparameters** que ya tenes al navegar a otra pagina
````js
let navigationExtras: NavigationExtras = {
  queryParamsHandling: 'preserve',
  preserveFragment: true
};
this.router.navigate(['/heroes', { id: heroId, foo: 'foo' }], navigationExtras);
````

### Rutas secundarias

Podes tener **mas de un router outlet**, por ejemplo si queres tener popups podes poner un router outlet alternativo en el root.

* Los **router outlets secundarios tienen que tener un nombre**
* Son **independientes** unas de otras
* Funcionan **al apar de las rutas _primarias_**
* Las vistas de las rutas secundarias permanecen aunque cambies de ruta primaria

el outlet se ve asi:

````html
<router-outlet></router-outlet>
<router-outlet name="popup"></router-outlet>
````

la ruta se ve asi:

````js
{
  path: 'compose',
  component: ComposeMessageComponent,
  outlet: 'popup'                // <---- nombre del outlet
},
````

Un vinculo a la ruta secundaria se ve asi
````html
<a [routerLink]="[{ outlets: { popup: ['compose'] } }]">Contact</a>
````

la url se vera asi:

>http://.../elpath/elfeature/loquesea(popup:compose)

Para salir de la ruta secundaria podes llamar:
`  this.router.navigate([{ outlets: { popup: null }}]);`

---


## Lazy loading

Podes cargar modulos _a demanda_

1)Elimina de el modulo principal los imports y referencias al modulo que queres cargar asincronicamente
2)En el modulo de rutas principal tiene que tener esta sintaxis
````js
{
  path: 'miPath',
  loadChildren: 'pathAlModulo/enElFileSystem/archivo.module#NombreDelModuloExportado',
},
````

3)El modulo que esta siendo cargado puede verse como algo asi, el **path inicial tiene que estar vacio**
````js
const adminRoutes: Routes = [
  {
    path: '',
    component: AdminComponent,
    canActivate: [AuthGuard],
    children: [
      {
        path: '',
        canActivateChild: [AuthGuard],
        children: [
          { path: 'crises', component: ManageCrisesComponent },
          { path: 'heroes', component: ManageHeroesComponent },
          { path: '', component: AdminDashboardComponent }
        ]
      }
    ]
  }
];
````

## pre loading

podes cargar modulos asincronicamente inmediatamente despues de que la aplicacion se inicia, acelerando el tiempo de carga de la app.

El router viene con dos **preloading strategies**


**1)** Precargar todos los lazy loaded modules
**2)** no Precargar nada (default)

### Estrategia PreloadAllMoudels

Para hacer un uso eficiente de Preloading hace falta crear **custom strategies**

Para usar la estrategia **1)** lo que se puede hacer es colocar los modulos como si se fuera a hacer lazy loading y luego en el main routing de la aplicacion colocar la estrategia **PreloadAllMoudels**
Obviamente no carga los modulos que tengan un **canLoad** guard.

````js
RouterModule.forRoot(
  appRoutes,			//este objeto es el que tiene las rutas configuradas
  {
    preloadingStrategy: PreloadAllModules		//La estrategia de preloading
  }
)
````

### Estrategia custom

Podes crear una estrategia asi

Imaginemos que queremos precargar las rutas con un flag, por ejemplo si tiene 'precargar' en el objeto "data"

**La ruta es:**

````js
{
  path: 'crisis-center',
  loadChildren: 'app/crisis-center/crisis-center.module#CrisisCenterModule',
  data: { preload: true }
},
````

Podemos crear una estrategia que lea la ruta  y vea si hay que precargar
Para eso creamos una clase que implementa **PreloadingStrategy** e implementamos un metodo llamado **Preload()** que admite la ruta
**selective-preloading-strategy.ts**
````js
import 'rxjs/add/observable/of';
import { Injectable } from '@angular/core';
import { PreloadingStrategy, Route } from '@angular/router';
import { Observable } from 'rxjs/Observable';

@Injectable()
export class SelectivePreloadingStrategy implements PreloadingStrategy {
  preloadedModules: string[] = [];

  preload(route: Route, load: () => Observable<any>): Observable<any> {
  	//aca haces algo con la ruta para ver si la precargas o no
	//por ejemplo si la ruta tuviera un flag "precargar"
    if (route.data && route.data['precargar']) {
      // add the route path to the preloaded module array
      this.preloadedModules.push(route.path);
      return load(); //cargar la ruta
    } else {
      return Observable.of(null); 	//no cargar la ruta
    }
  }
}
````

Esta estrategia debe ser activada de la misma foma que **PreloadAllModules** mas arriba, ademas hay que agregarla al modulo principal en su array de providers

>en runtime podes ademas **importar la estrategia** SelectivePreloadingStrategy y acceder a su propiedad `preloadedModules ` para encontrar una **lista de los modulos precargados hasta el momento**

---

## Route guards

Los guards son **servicios** que **implementan una interfaz** que es **reconocida por el router** en la **configuracion de rutas**

Evitan los cambios de rutas, por ejemplo

* Perhaps the user is not authorized to navigate to the target component.
* Maybe the user must login (authenticate) first.
* Maybe you should fetch some data before you display the target component.
* You might want to save pending changes before leaving a component.
* You might ask the user if it's OK to discard pending changes rather than save them.
* **Si el guard devuelve true permite la navegacion, sino no navega o redirecciona a otra pagina**
* el guard puede hacer operaciones asyncronicas y devolver un `Observable<boolean>`, el router esperara a que se resuelva. **el Observable debe llegar a complete()**

Hay varias interfaces de guards:

* **CanActivate** - Puede activar esta/s ruta/s
* **CanActivateChild** - Puede activar las child routes ?
* **CanDeactivate** - puede salir de esta ruta para navegar a otra ruta?
* **Resolve** to perform route data retrieval before route activation.
* **CanLoad** to mediate navigation to a feature module loaded asynchronously.

**los guards son servicios** veamos:

### CanActivate
el guard:
````js
import { Injectable }     from '@angular/core';
import { CanActivate }    from '@angular/router';
@Injectable()
export class AuthGuard implements CanActivate {
  canActivate() {
    let puedePasar = checkeoLoQueMePinta();
    return puedePasar;			//si devuelvo true lo dejo pasar 			
  }
````
  
Coloco el guard en el path
````js
  import { miGuard }                from '../auth-guard.service';
const adminRoutes: Routes = [
  {
    path: 'admin',
    component: AdminComponent,
    canActivate: [miGuard],
    children: [
      {
        path: '',
        children: [
          { path: 'crises', component: ManageCrisesComponent },
          { path: 'heroes', component: ManageHeroesComponent },
          { path: '', component: AdminDashboardComponent }
        ],
      }
    ]
  }
];
````
  
>Nota como hay una ruta sin componente que tiene varios children, asi podes agrupar varias rutas bajo un solo guard.

podes inyectar  ActivatedRouteSnapshot y RouterStateSnapshot si **queres ver los datos de la navegacion para decidir algo en la logica del guard**, o cualquier servicio que te sea util.
````js
import { Injectable }       from '@angular/core';
import {
  CanActivate, Router,
  ActivatedRouteSnapshot,
  RouterStateSnapshot
}                           from '@angular/router';
import { AuthService }      from './auth.service';

@Injectable()
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}
  canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): boolean {
    let url: string = state.url;
    return this.checkLogin(url);
  }
````

### CanDeactivate

Es probable que CanDeactivate necesite acceder al componente del que se esta saliendo para saber si esta en condiciones de irse (Ej: si el usuario guardo los cambios)

Hay dos formas de hacer esto

1) darle a todos los componentes una funcion que lo verifique y hacer un **guard generico** que ejecute esa funcion y use el resultado para determinar si se puede navegar fuera del componente o no.

````js
//Declaro que existe una funcion canDeactivate que devuelve un observable boolean
export interface CanComponentDeactivate {
 canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
}

@Injectable()
//Normalmente pondriamos como generic de canDeactivate el componente que queremos 
//desactivar para que cuando armamos el guard la IDE nos autocomplete con tipos 
//todo lo que queremos, pero como aca queremos hacer un componente generico
//hacemos una interfaz para la unica funcion que el componente tal vez tenga.
//y se la damos a conocer al guard. es la funcion CanComponentDeactivate()
export class CanDeactivateGuard implements CanDeactivate<CanComponentDeactivate> {
  canDeactivate(component: CanComponentDeactivate) {
    return component.canDeactivate ? component.canDeactivate() : true;
  }
}
````

2)Hacer un **guard especifico** que maneje ese componente en particular

````js
import { CrisisDetailComponent } from './crisis-center/crisis-detail.component';
@Injectable()
//CanDeactivate tiene un generic donde hay que poner el component para que pueda
//proveer soporte de types cuando lo uses en el interior.
export class CanDeactivateGuard implements CanDeactivate<CrisisDetailComponent> {

  canDeactivate(
    component: CrisisDetailComponent,		//indico el componente
    route: ActivatedRouteSnapshot,			//inyecto servicios que puedan servir
    state: RouterStateSnapshot				//inyecto servicios que puedan servir
  ): Observable<boolean> | boolean {	
    // Get the Crisis Center ID
    console.log(route.paramMap.get('id'));

    // Get the current URL
    console.log(state.url);

    // Allow synchronous navigation (`true`) if no crisis or the crisis is unchanged
    if (!component.crisis || component.crisis.name === component.editName) {
      return true;
    }
    // Otherwise ask the user with the dialog service and return its
    // observable which resolves to true or false when the user decides
    return component.dialogService.confirm('Discard changes?');
  }
}
````

### Resolve

Sirve para buscar los datos del servidor que son necesarios para que un componente funcione y hacerlo antes de que el componente se inicialice.


**El guard**

Sale a buscar los datos al server y los devuelve
````js
import { Crisis, CrisisService }  from './crisis.service';
@Injectable()
export class MiResolver implements Resolve<datos> {
  constructor(private BuscoAlServer: BuscoAlServerService, private router: Router) {}

  resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Crisis> {
    let id = route.paramMap.get('id'); //puedo usar algo de info del router!
	//voy a buscar algo al server con algun servicio
	//Usamos take(1) porque asegura que el observable llegara a complete()
	// Si nunca llegara a complete() la navegacion no continuara
    return this.BuscoAlServer.porId(id).take(1).map(datos => {
      if (datos) {
        return datos; 		//Devuelvo los datos que fui a buscar al server
      } else { // id not found
        this.router.navigate(['/crisis-center']); //Si no lo encontre navego para atras
        return null;		
      }
    });
  }
}
````

lo agregamos como **provider** al modulo que deba ser

````js
providers: [
    MiResolver
  ]
````

**Configuramos la ruta** para que use el guard

Tambien se configura el nombre de la propiedad de route.data donde estaran los datos, en este caso sera route.data.misDatos
````js
  {
    path: ':id',
    component: MiComponente,
    canDeactivate: [CanDeactivateGuard],
    resolve: {
      misDatos: MiResolver //Este es el nombre con el que leeremos los datos 
    }
  },
````

Finalmente en el component **leemos los datos obtenidos**

Y hacemos lo que queramos hacer con ellos

````js
ngOnInit() {
//Accedo a los datos que me interesan
//recorda que 
  this.route.data
    .subscribe((respuesta: { misDatos: datos }) => {
      this.miVariable = respuesta.misdatos.loQueMeInteresa
    });
}
````

### CanLoad
Permite o evita que se descarguen los modulos asincronicos correspondientes a cierto path

La logica es igual que la de los otros guards
````js
{
  path: 'admin',
  loadChildren: 'app/admin/admin.module#AdminModule',
  canLoad: [AuthGuard]
},
````
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY2NTA3MTA1MSwtMTA1OTA3MjQ1Ml19
-->