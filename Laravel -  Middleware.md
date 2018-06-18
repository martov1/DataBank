


# Contenido


* Intro
* Crear un middleware
	* Antes del procesamiento
	* Despues del procesamiento 
* Registrar middleware
	* Middleware global
	* Middleware por ruta
* Middleware groups





# Intro

Los middlewares van en `app/Http/Middleware`

**Los middleware ste sirven para filtrar los HTTP requests y manipularlos:**

*	**Antes que el router** de que lleguen a tu router y controller
*	**Despues del router** de que lleguen al router pero antes de llegar al callback o controller
*	**Despues del router y controller**

**Algunos middlewares por default son:**

* **Auth**
	* Determina si el usuario esta autenticado, si no lo esta lo redirge a la pagina de login
* **CSRF**
	* Determina si el token existe y es valido, si no lo es rechaza el request   


# Crear un middleware


Podes crear un middleware con el siguiente comando de artisan

	php artisan make:middleware MiMiddleware
	
**Se ve asi:**
```php
	namespace App\Http\Middleware;
	use Closure;
	
	class MiMiddleware
	{
		//La funcion handle tiene como parametros el request y la funcion $next
	    public function handle($request, Closure $next)
	    {
			//Darle el request al proximo middleware del stack
	        return $next($request);
	    }
	}
```
Los middleware tienen minimamente los parametros
* **$request** que contiene el request hecho por el browser
* **$next** que le entrega un $request al proximo middleware del stack

## Antes del procesamiento

Es un middleware que corre antes de que el request sea procesado
```php
	namespace App\Http\Middleware;
	use Closure;
	
	class BeforeMiddleware
	{
	    public function handle($request, Closure $next)
	    {
	        // Perform action
	
	        return $next($request);
	    }
	}
```
## Despues del procesamiento

Es un middleware que corre DESPUES de que el request es procesado
```php
	namespace App\Http\Middleware;
	use Closure;
	
	class AfterMiddleware
	{
	    public function handle($request, Closure $next)
	    {
	        $response = $next($request);
	        // Perform action
	
	        return $response;
	    }
	}
```
## Antes y despues del procesamiento

Podes crear un middleware que haga cosas tanto antes del procesamiento como despues configurando un metodo **terminate()** que correra cuando **el response este listo para ser envido**
	
>**Notese que**:
>* **terminate() recibe tanto el request como el response como argumentos**
>* Laravel instancia un **nuevo middleware** para correr **terminate()**
>	* Si queres que sea la misma instancia, tenes que hacer un singleton usando el **service container** 
	
	
```php
	namespace Illuminate\Session\Middleware;
	use Closure;
	
	class StartSession
	{
		//Lo que sucede antes del procesamiento
	    public function handle($request, Closure $next)
	    {
	        return $next($request);
	    }
		//lo que sucede despues del procesamiento
		//Tenes acceso al request y al response
	    public function terminate($request, $response)
	    {
	        // Hacer cosas cuando el response este listo
	    }
	}
```
	
#Registrar middleware


Los Middlewares deben estar registrados en el **Http kernel** situado en **app/http/kernel.php**.

**Dependiendo de en que variable estan ubicados, tendran scopes distintos.**
##Middleware global

Es middleware que corre en todas las HTTP requests. 
Se registra en la variable **$middleware** del HTTP KERNEL

	class Kernel extends HttpKernel
	{
	    //los global middleware
	    protected $middleware = [
	        \Illuminate\Foundation\Http\Middleware\CheckForMaintenanceMode::class,
	        \Illuminate\Foundation\Http\Middleware\ValidatePostSize::class,...
	    ];
	
##Middleware por ruta

Podes asignar middlewares por ruta, Para que sean elegibles deben estar registrados en la vartiable **$routeMiddleware** del **HTTP kernel**

    protected $routeMiddleware = [
        'auth' => \Illuminate\Auth\Middleware\Authenticate::class,
        'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
		...


**Luego podes usarlo en las rutas asi:**

	Route::get('/', function () {
	    //
	})->middleware('middleware1', 'middleware2');
	
Podes asignar el nombre completo del middleware con el namespace tambien

	use App\Http\Middleware\CheckAge;
	Route::get('admin/profile', function () {
	    //
	})->middleware(CheckAge::class);
	
	
#Middleware groups

Podes agrupar middleware en un grupo para **correrlos a todos como si llamaras a un solo** middleware, ejemplos de estos grupos son **web** y **api**, que ya vienen con laravel.

para creat un grupo tenes que reguistrarlo en el **http kernel** en la variable **$middlewareGroups** junto con todos los middlewares que utiliza


	protected $middlewareGroups = [
	    'web' => [
	        \App\Http\Middleware\EncryptCookies::class,
	        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class
	    ],
		
		// Mi grupo customizado con los middlewares que yo quiero
	    'miGrupo' => [
	        \App\Http\Middleware\MiMiddleware1::class,
	        \App\Http\Middleware\MiMiddleware2::class,
	    ],
	..


**Los podes asignar a una ruta como si fueran un sulo middleware:**

	Route::get('/', function () {
    //
	})->middleware('miGrupo');


<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAwMDEzMTIxM119
-->