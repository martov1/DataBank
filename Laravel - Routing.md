


# Contenido



* Intro
	* API style
	* View style
	* Controller style
* Redireccion 
* Parametros 
	* Patametros de URL
	* Parametros opcionales
	* Parametros con defaults
	* Limitar parametros con RegEx 
* Rutas nombradas
	* Redireccion programatica 
	* obtener URL programaticamente 
	* Rutas firmadas de alta entropia 
* Obtener informacion de la ruta actual
* Route groups
	* Compartir multiples middlewares
	* Compartir un namespace
	* Compartir un subdominio
	* Asignar prefixes
	* Rate Limiting
		* Rate limiting dinamico 
* Route Model Binding
	*  Implicit Binding
		* Implicit binding con otra key  
	* Explicit Binding
* CSRF **WIP** 





# Intro

Los archivos de rutas se cargan automaticamente y estan ubicados en la carpeta **/routes**

*  **RUTAS EN `routes/api.php`** 
	* utilizan el **middleware API**
		* No tienen **sesiones**
		* Estan bajo el prefijo **URI "misitio.com/api"**
*  **RUTAS EN `routes/web.php`** 
	* utilizan el **middleware WEB**
		* tienen **sesiones automaticas** usando cookies
		* Usan y esperan recibir **CSRF tokens**



**La forma mas basica de configurar una ruta es con un closure:**
```php	
	//determino la RUTA, el VERBO y establezco un CALLBACK que devuelve algo al cliente
	Route::MIVERBO('/MIRUTA', MIFUNCTION(){});
	
	// EJEMPLO
	Route::get('/miRuta', function () {
		// Devolver algo, por ej un view
		return view('welcome')
	});
```
podes realizar querys o cualquier proceso dentro de la ruta.
	
	

## API style
**Si devolves un query como resultado de una route, laravel expone el resultado como JSON**
```php	
	Route::get('MIRUTA', function(){
		// ORM query builder
		$users = DB::table('usuarios')->get();
		//Eloquent
		$resultado = App/miModelo::miFuncion() 
		
		return $users
	})
```
### View style

* Usando compact podes enviar variables al view desde el route
* Podes especificar el nombre del view, si esta en una subcarpeta de la carpeta views podes usar la sintaxis **/ruta/al/view**

```php	
	Route::get('MIRUTA', function(){
		$users = DB::table('usuarios')->get();
		//Enviar datos como parametros para el view
		return view('usuarios/usuario/perfil', compact('tasks'))
	})
```
**Una forma mas compacta permite directamente dirigir a un view puntual:**	
```php	
	//Redirigir a un view estatico
	Route::view('/miRuta', 'miView');
	//Redirigir a un view y enviarle algun dato
	Route::view('/welcome', 'welcome', ['name' => 'Taylor']);
```

### Controller style

Si queres que la ruta sea controlada por un controller, podes poner el nombre del controller en lugar de la funcion (el controller no es mas que una clase con un metodo que reemplaza a las funciones anteriores).  

**Un controler es simplemente colocar el callback de la ruta en otro archivo**

Para definirlo se usa la nomenclatura **controller@metodo**

sin parametros:
```php	
	Route::get('MIRUTA', 'MiRutaController@Metodo')
```
Con parametros:
```php	
	Route::get('usuarios/{id}', 'UserController@mostrar')
```


# Redireccion

Podes redirigir un request asi
```php	
	//Especificas desde donde, a donde redirigir y con que codigo de redirecion
	Route::redirect('/DESDEAQUI', '/HASTAAQUI', CODIGO 3XX);
	//ej
	Route::redirect('/here', '/there', 301);
```

# Parametros



## Patametros de URL

Podes conseguir parametros de la url colocando el parametro entre **{}** y colocandolo en el callback/controller
	
```php	
	//Un parametro
	Route::get('user/{id}', function ($id) {
	    // Hacer cosas
	});
	//Multiples parametros
	Route::get('posts/{post}/comments/{comment}', function ($postId, $commentId) {
    	// Hacer cosas 
	});
```

* los parametros 
	* **No pueden** contener **Guiones -** 
	* **pueden** contener **guiones bajos _** y caracteres **alfanumericos**
* Los parametros son **inyectados en los callbacks o funciones en el orden en el que son escritos**

## Parametros opcionales

Podes determinar parametros opcionales, pero en ausencia de ellos debe haber un **default** preconfigurado
```php	
	//Colocas 'John' como default si no hay nada configurado
	Route::get('user/{name?}', function ($name = 'John') {
	    return $name;
	});
```
## Parametros con defaults

Podes definir parametros que al estar ausentes tengan un valor default. podes asignar estos defaults **en un middleware** para no tener que hacerlo en cada ruta.

Los defaults se setean con **URL::defaults**
```php	
	namespace App\Http\Middleware;
	use Closure;
	use Illuminate\Support\Facades\URL;
	
	class SetDefaultLocaleForUrls
	{
	    public function handle($request, Closure $next)
	    {
	        URL::defaults(['locale' => $request->user()->locale]);
	
	        return $next($request);
	    }
	}
```



## Limitar parametros con RegEx

Podes limitar los parametros utilizables mediante una RegEx, si la RegEx devuelve **true** entonces el parametro se utiliza. 
```php	
	Route::get('user/{name}', function ($name) {
	    //hacer cosas
	})->where('name', '[A-Za-z]+');
```
Podes hacer que esta limitacion sea **global** usando **Route::pattern()** en un **service provider**
```php	
	//Hacer que todas las rutas sean numericas.
	public function boot()
	{
	    Route::pattern('id', '[0-9]+');
	
	    parent::boot();
	}
```

# Rutas nombradas

## Redireccion programatica


Podes darle nombres a las rutas y cuando vos quieras podes redireccionar a esa ruta con un HTTP 3xx de forma programatica

Por ejemplo, queremos redirigir a una ruta que llamaremos "home"
**En las rutas:**
```php	
	// Hago una ruta con el nombre de home
	Route::get('MIRUTA', 'MIRUTACONTROLLER@mostrar')->name('home')
```
**En otro lado:**
```php	
	//Indico en algun lugar de mi codigo que quiero redirigir 
	//a esa ruta en ese momento
	redirect()->home()
```
## obtener URL programaticamente

**Obtener URL de una ruta con nombre:**
```php	
	$url = route('home');
```
**Podes obteneer la URL con parametros asi:**
```php	
	//Ruta que acepta parametro id
	Route::get('user/{id}/profile', function ($id) {
	    //
	})->name('profile');
	
	//Colocas los parametros en un array para obtener la URL
	$url = route('profile', ['id' => 1]);
	
	//Obtener una URL de un modelo (usando un id)
	echo route('post.show', ['post' => $post]);
```


## Determinar nombre de la ruta de un request

Si tenes acceso a un request (mediante un middleware por ejemplo), podes determinar si fue ruteado a travez de una ruta con un nombre determinado mediante **named()**.

```php	
	public function handle($request, Closure $next)
	{
		//Determinar si el request viene de un route con nombre "profile"
	    if ($request->route()->named('profile')) {
	        //
	    }
	
	    return $next($request);
	}
```
## Rutas firmadas de alta entropia


Podes crear **rutas firmadas por laravel**, esto te permite **evitar que la ruta sea modificada**. Un ejemplo es un boton de unsubscribe de un mail donde no queres que la URL pueda modificarse para desuscribir a otros usuarios.

* **Hacer una ruta firmada a partir de una ruta nombrada**
	```php	
		use Illuminate\Support\Facades\URL;
		return URL::signedRoute('NombreDeRuta', ['user' => 1]);
	```
* **Hacer una ruta  firmada con expiracion**
	```php	
		use Illuminate\Support\Facades\URL;
		
		return URL::temporarySignedRoute(
		    'NombreDeRuta', now()->addMinutes(30), ['user' => 1]
		);
	```
* **Verificar firma de una ruta firmada**
	```php	
	    if (! $request->hasValidSignature()) {
        abort(401);
    	}
	```
	* **Verificar automaticamente la firma con un middleware**
	```php	
			//En el kernel
			protected $routeMiddleware = [
			    'signed' => \Illuminate\Routing\Middleware\ValidateSignature::class,
			];
			//En la ruta
			Route::post(blablabla)->name('unsubscribe')->middleware('signed');
	```
		


# Obtener informacion de la ruta actual


Podes obtener la ruta actual, el nombre o la accion de la siguiente manera

```php	
	$route = Route::current();
	
	$name = Route::currentRouteName();
	
	$action = Route::currentRouteAction();
```


# Route groups

Los grupos te permiten compartir atributos, middleware o namespaces en un grupo de rutas

## Compartir multiples middlewares
```php	
	//Comparitr una serie de rutas
	Route::middleware(['first', 'second'])->group(function () {
	    Route::get('/', function () {
	        // Uses first & second Middleware
	    });
	
	    Route::get('user/profile', function () {
	        // Uses first & second Middleware
	    });
	});
```

## Compartir un namespace
```php	
	Route::namespace('Admin')->group(function () {
	    // Controllers Within The "App\Http\Controllers\Admin" Namespace
	});
```
## Compartir un subdominio

Por ahi queres agrupar varias rutas dentro de lo que sera un subdominio
```php	
	Route::domain('misub.dominio.myapp.com')->group(function () {
		//ruta1
	    Route::get('user/{id}', function ($account, $id) {
	        //
	    });
		//ruta2
		 Route::get('user/{id}', function ($account, $id) {
	        //
	    });
	});
```

## Asignar prefixes


Por ahi queres tener un grupo de rutas **detras de un prefix**.
```php	
	Route::prefix('admin')->group(function () {
	
		// Matches The "/admin/users" URL
	    Route::get('users', function () {
	        
	    });
		
		// Matches The "/admin/users2" URL
		Route::get('users2', function () {
	        
	    });
	});
```
## Rate Limiting

Podes limitar la cantidad de llamadas que hace un usuario por minuto a la API usando el **throttle middleware**, este acepta dos parametros: **cantidad de llamadas, cantidad de minutos** es decir que si pones 60,1 entonces un usuario autenticado podra hacer 60 llamadas por minuto.
```php	
	Route::middleware('auth:api', 'throttle:60,1')->group(function () {
	    Route::get('/user', function () {
	        //
	    });
	});
```
### Rate limiting dinamico

Podes condicionar el Rate limiting, por ejemplo, puede depender de un parametro del modelo llamado "miParameto"
```php	
	Route::middleware('auth:api', 'throttle:miParametro,1')->group(function () {
	    Route::get('/user', function () {
	        //
	    });
	});
```
# Route Model Binding

Te permite a travez de un primary key (el id del modelo por default) inyectar el modelo correspondiente dentro de la ruta o controller

## Implicit Binding

La uri termina en  **/users/**, y la variable es de tipo **App/user** y se llama **$user**, entonces laravel sabe que debe inyectar el usuario con el id reflejado en **{id}**

Si no lo encuentra entonces devuelve **HTTP code 404 not found**
```php	
	Route::get('api/users/{id}', function (App\User $user) {
	    return $user->email;
	});
```

### Implicit binding con otra key

Si queres usar implicit binding con **otra key que no sea id** podes cambiarlo en el **modelo** con la funcion **getRouteKeyName**

```php	
	public function getRouteKeyName()
	{
	    return 'miColumna';
	}
```	
## Explicit Binding

Podes determinar explicitamente que un modelo debe ser inyectado en una ruta cuando aparezca una variable de ruta con un nombre detemrinado. esto debe hacerse en el **RouteServiceProvider**

**En el RouteServiceProvider:**
```php	
	public function boot()
	{
	    parent::boot();
		// Las rutas con {user} apuntaran siempre al model USER
	    Route::model('user', App\User::class);
	}
```
**En la ruta:**
```php	
	Route::get('profile/{user}', function (App\User $user) {
    //
	});
```
# Method spoofing

Los browsers solo envian **Get y POST**, podes **simular PUT, PATCH, DELETE, etc** en un form mediante el campo **_Method**
```html
	<form action="/foo/bar" method="POST">
	    <input type="hidden" name="_method" value="PUT">
	    <input type="hidden" name="_token" value="{{ csrf_token() }}">
	</form>
```
En blade tambien podrias usar este shorthand
```html
	<form action="/foo/bar" method="POST">
	    @method('PUT')
	    @csrf
	</form>
```


	
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI4ODA5MjQzNCwtNTY2MTgwNzYyXX0=
-->