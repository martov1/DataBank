

# Contenido:

* lo basico
	* Estructura
	* Metadata
	* importar y exportar
	* Providers
* Bootstraping
* Organizacion en Feature modules


# Lo basico

## Estructura

Un modulo es un contenedor de componentes y servicios, a su vez puede requerir de otros modulos para funcionar

el modulo tiene un **decorator @NgModule** con un objeto que contiene **metadata** y una **clase** 

````js
// decorador
 
@NgModule({
  declarations: [SomeComponent, SomeDirective, SomePipe],
  providers: [SomeService],
  imports:[ OtroModulo]
})
 
// clase
export class SomeModule {}
````

## Metadata


* **declarations** - Declara los componentes/directivas/pipes que el modulo contiene.
* **providers** - Declara los servicios que el modulo contiene.
* **imports** - Declara los modulos que se deben cargar para que este modulo funcione
* **exports** - Declara los componentes/directivas/pipes que pueden ser usados por aquellos modulos que importen este modulo.
* **bootstrap** - Declara El componente inicial dentro del cual estaran todos los componentes. este campo debe estar presente unicamente en el **root module**, es decir el modulo que importa todos los modulos
* **entryComponents** - Lista de componentes que pueden ser creados de forma imperativa, por ejemplo con `ViewComponentRef.createComponent()`, para mas datos ver Angular - Components - Crear componentes dinamicamente


````js
@NgModule({ 
  providers?: Provider[]
  declarations?: Array<Type<any> | any[]>
  imports?: Array<Type<any> | ModuleWithProviders | any[]>
  exports?: Array<Type<any> | any[]>
  entryComponents?: Array<Type<any> | any[]>
  bootstrap?: Array<Type<any> | any[]>
  schemas?: Array<SchemaMetadata | any[]>
  id?: string
})
    
````

## importar y exportar

### Critico
> los imports de Typescript no son equivalentes a los imports de NgModule

## Lo basico

 * **Exportas** de un modulo los componentes, servicios, etc que queres que otros modululos puedan usar
 * **Importas** lo que otro modulo tiene para exportar, y lo usas como si estuviera en tu array de declarations o providers

>**Regla general:**
>Importa los **modulos con providers** solo **una vez** para evitar que una instancia pise a la otra, o usa el patron **forRoot()**. no hay problema con importar varias veces modulos con componentes repetidos
> ver mas en: _Angular - services - Lazy loading y service shadowing_


**Una vez importado, se pueden usar todos los componentes, servicios, etc del modulo en los templates, componentes, etc del modulo que lo importo a lo largo de toda la aplicacion**

## Ejemplos 

**Importar** algo de un modulo
````js
//Import de typescript, no tiene nada que ver con angular
import { BrowserModule } from '@angular/platform-browser';
	
//Import de NgModule, ahora el modulo BrowserModule esta disponible para
//ser usado en este modulo llamado appModule. ahora podes usar los componentes,
//servicios, etc de BrowserModule
@NgModule({
  imports:[ BrowserModule]
})
	
export class appModule {}
````

**exportar** un modulo.
````js
// Si importas este Modulo entonces podes usar SomeComponent y SomePipe en tus
// templates
 
@NgModule({
  declarations: [SomeComponent, SomeComponent, SomePipe], //cosas importables
  providers: [SomeService],									//cosas importables
  imports:[ OtroModulo],
  exports: [SomeComponent,SomePipe]
})
 
// Exportacion del modulo
export class SomeModule {}
````

---

## Providers

El array de providers:
* **En un modulo eagerly loaded** - instancia los servicios globalmente como singletons
* **En un modulo lazy loaded** - Instancia los servicios localmente para ese modulo
* **En dos modulos con servicios repetidos** - sobreescribe el servicio, el ultimo servicio cargado "gana"

---
# Bootstraping

Es la accion de activar el **root module**, se hace asi
`platformBrowserDynamic().bootstrapModule(AppModule);`



# Organizacion en Feature modules

Los feature modules son una forma de organizar el codigo de una aplicacion, contienen todo lo necesario para hacer andar un feature, esto puede ser **forms, componentes, servicios, routes, etc**

* Son modulos con todo lo necesario para hacer andar un feature
* **pueden o no** tener su porpio modulo de rutas, esto se obtiene con **lazyloading**


![enter image description here](https://lh3.googleusercontent.com/3eaFQEv8sR6uWqn0w-BO3ustLWXrINw7YMwiRaFfHBsXCosooefeB4DFdHWryFqGeiC1KlyLtr30)


Mas detalles en **Angular router - lazy loading**
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgxOTY4MTM3NCwxNTg5OTgwNDE2XX0=
-->