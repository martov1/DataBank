




**Falta ver:**

**Alta prioridad**
- [x] [Eloquent relationships](https://laravel.com/docs/5.6/eloquent-relationships)
- [ ] [File system](https://laravel.com/docs/5.6/filesystem)
- [ ] [Mail](https://laravel.com/docs/5.6/mail)



**Baja prioidad:**

- [ ] [Service container](https://laravel.com/docs/5.6/container)
- [ ] [Service providers](https://laravel.com/docs/5.6/providers)
- [ ] [Sessions](https://laravel.com/docs/5.6/session)
- [x] [Routing](https://laravel.com/docs/5.6/routing)
- [x] [Middleware](https://laravel.com/docs/5.6/middleware)
- [x] [CSRF](https://laravel.com/docs/5.6/csrf)
- [x] [Controllers](https://laravel.com/docs/5.6/controllers)
- [x] [Requests](https://laravel.com/docs/5.6/requests)
- [x]  [Responses](https://laravel.com/docs/5.6/responses)
- [x] [URL generation](https://laravel.com/docs/5.6/urls)
- [x] [Validation](https://laravel.com/docs/5.6/validation)
- [x] [Error handling](https://laravel.com/docs/5.6/errors)
- [x] [Logging](https://laravel.com/docs/5.6/logging)
- [x] [Authentication](https://laravel.com/docs/5.6/authentication)
- [x] [API Authentication](https://laravel.com/docs/5.6/passport)
- [x] [Authorization]()
- [x] [Eloquent](https://laravel.com/docs/5.6/eloquent)
	- [x] [Eloquent query scopes](https://laravel.com/docs/5.6/eloquent#query-scopes)
	- [ ] [Eloquent events](https://laravel.com/docs/5.6/eloquent#events)

**Herramientas adicionales**
- [x ] [Encriptacion](https://laravel.com/docs/5.6/encryption)
- [x ] [Hashing](https://laravel.com/docs/5.6/hashing)
- [ ] [Password Reset](https://laravel.com/docs/5.6/passwords)
- [ ] [Artisan Console](https://laravel.com/docs/5.6/artisan)
- [ ] [Broadcasting/websockets](https://laravel.com/docs/5.6/broadcasting)
- [ ] [cache](https://laravel.com/docs/5.6/cache)
- [ ] [collections (como lodash)](https://laravel.com/docs/5.6/collections)
- [ ] [events](https://laravel.com/docs/5.6/events)
- [ ] [Notifications](https://laravel.com/docs/5.6/notifications)
- [x ] [Queues](https://laravel.com/docs/5.6/queues)
- [ ] [task scheduler](https://laravel.com/docs/5.6/scheduling)






# Contenido


* Intro
	* Seguridad
		* CSRF tokens 
		* disable CSRF token
		* OS permissions 
		* Aplication key
	* Capacidades
		* Capacidades de artisan cli
		* Capacidades de eloquent ORM
		* Capacidades de blade engine
		* Capacidades de composer
	* Requerimientos
* Instalacion 
* Bootstrap de un proyecto 
* Arquitectura
	* Estructura de carpetas
	* Request lifecycle
	* Dependency inyection 
	* Service providers
		* Registrar nuevos servicios
		* bootear servicios
		* Instanciar servicios
		* Deferir servicios 
* Partes
	* views
		* Variables de template
		* bloques logicos
		* extends e includes
	* Configuracion y credenciales
	* Database
		* Migrations 
			* Crear migraciones 
		* ORM query builder
		* Eloquent
			* Crear models
			* Extender models
			* Referenciar modelos
			* guardar datos en DB
			* Route Model Binding
			* Joins con IDs
	*  Repositories
* Webpack
* Authentication
	* Con sesiones **wip**
* Uso de sesiones
	* Flash 
* Enviar emails 
* Events y listeners **wip**
 



  

# Intro

* Usa **PHP**
* Usa **MVC**
* Usa **carbon** para el formateo de fechas (como MOMENT.JS)

## Seguridad

Es necesario
* Crear una key
* **hacer que apache solo exponga la carpeta public**
* .env **no se guarde en version control**

Podes hashear asi:
```php
	bcrype('cosa para hashear')
```
### CSRF tokens

**Hay tres formas de obtener el token:**

* hidden field para forms 
	```html

	//Esto en blade:
	{{crsf_field()}}
	//Genera
	//<input type="hidden" name="_token" value="7YC0Sxth7AYe4RFSjzaPf2ygLCecJhblahblah">
	```
* outputear CSRF token directamente
	
	```html
	{{ csrf_token() }}
	```
* En un cookie
Laravel envia automaticamente una cookie llamada X-XSRF-TOKEN con el token, podes obtenerlo de JS en la pagina

**Hay dos formas de enviar el token**

* Form field en un post
Si usas el hidden field o lo colocas manualmente, ya esta
* Header
Laravel busca el header **X-CSRF-TOKEN** en el request


### Disable CSRF

Se hace editando el middleware **VerifyCsrfToken**

Si tenes una **API que no usa SESIONES** entonces no lo necesitas.
```php
	<?php
		
	namespace App\Http\Middleware;
	
	use Illuminate\Foundation\Http\Middleware\VerifyCsrfToken as Middleware;
	
	class VerifyCsrfToken extends Middleware
	{
	    /**
	     * The URIs that should be excluded from CSRF verification.
	     *
	     * @var array
	     */
	    protected $except = [
	        'stripe/*',
	        'http://example.com/foo/bar',
	        'http://example.com/foo/*',
	    ];
	}
```
### OS permissions

El web server debe tener permiso de escritura para las carpetas **storage** y **bootstrap/cache**. El resto de las carpetas pueden tener permiso de lectura unicamente (esto seria mas seguro)

### Aplication key

Si instalas laravel usando artisan o composer entonces se genera automaticamente una key de 32 chars en el archivo **.env**, esta key se usa para encriptar sesiones y otros datos.


## Capacidades

* Capacidad de **authentication** y **access control**
* Usa **composer** como CLI interface y deployer
* **Security** layer
* **Ruteo**
* **Sesiones**
* **Views y templates** usando **Blade**
* **Storage y file management**
* **Email config**
* **Cache handling**
* **Crea migraciones** de bases de datos
*  **Asset configutaction**
*  **Eloquent ORM**

### Capacidades artisan cli

* **crear**
	* Controllers
	* models
	* database migration files
	* Providers
	* events
	* jobs
	* form requests
	* **custom commands**
* **Run**
	* Database migrations 
	* _tinker_ (database interaction)  
* **Show**
	* Routes
	
**Ejemplos:**


	php artisan list
	php artisan help migrate
	php artisan make:controller MiController
	php artisan migrate

### Capacidades de eloquent

Es un orm que facilita el trabajo realizando querys con una DB

Utiliza modelos para representar tablas como objetos
```php
	use App/Todo
	$todo = new Todo;
	$todo->title = "Some Todo"
	$todo-> save(); //Guardar en DB con titulo "some todo"
```
	
### Capacidades de Blade temprate engine


* Estructuras logicas (IF, loops, etc) en templates
* Template inheritance
* Create custom components


### Capacidades de composer

* **Podes instalar paquetes globalmente:**

		composer global require "laravel/installer"
	
	* Hace falta colocar el exe del paquete instalado en el path directory si es una aplicacion de CLI		
	**Control Panel->All Control Panel Items->System->Advanced System Setttings->Environment Variables**

* **Podes instalar paquetes localmente:**
	
	composer require "nombre/nombre"

* **Podes buscar paquetes para instalar en packagist:**
https://packagist.org/



## Requerimientos

* **XAMP stack** 
* **Composer** para su instalacion
* Crear un virtual host con apache a la carpeta publica




# Instalacion

* instalar git
* Instalar composer
* Colocar composer en el PATH
* instalar laravel globalmente
		composer global require "laravel/installer" 

https://laravel.com/docs/5.6#installation

# Bootstrap de un proyecto

**Para crear un nuevo proyecto:**

		CD CARPETA
		laravel new NOMBREDEAPP


**Servir el proyect:**

		php artisan serve
		
---

		
# Arquitectura

## Estructura de carpetas

* **MIAPP**
	* **app**
		* **http** -- contiene controllers, middleware y form requests
			* **kernel.php** -- Determina todos los middlewares 
			* **Controllers** --Contiene los controllers  
		* **Mail** --contiene los email templates 
		* **Events** --contiene los eventos que configures
		* **Listeners** -- Contiene los listeners que se triggerean ante un event
		* **console** --contiene los comandos de artisan que crees para tu aplicacion
		* **Broadcasting** --Contiene los broadcast channels de tu aplicacion
		* **exceptions** -- contiene todas las excepciones de la aplicacion
		* **jobs** -- Contiene quable jobs
		* **notifications** -- Se usa para crear y enviar notificaciones via sms, slack, mail etc
		* **Policies** --Guarda las politicas que determinan si un usuario puede acceder a un recurso
		* **providers** --Contiene los service providers
		* **Rules** --Encapstulan logica de validacion complicada en una clase
	* **bootstrap**
	* **config**
	* **database**
		* **factories**
		* **migrations** -- contiene las migraciones que se transformaran en tablas 
	* **public**		-- recursos estaticos compilados por webpack
		* **index.php** -- El entry point de la aplicacion 
	* **resources**
		* **assets**	--recursos estaticos precompilados por webpack
			* JS
			* SASS 
		* lang
		* **views**		--Contiene templates de blade 
	* **routes**
		* **api.php**	--Rutas que usan el middleware API, son para REST APIS
		* **channels.php**  --Contiene event broadcasting channels
		* **console.php**	--Permite configurar callbacks para comandos custom de consola
		* **web.php**	--Rutas que usan el middleware WEB, tienen CSRF tokens y sesiones
	* **storage**
		* **app** -- Guarda a quellos archivos que generes en tu aplicacion 
			* **public** -- Puede usarse para guardar archivos generados por los usuarios  
		* **framework** --Guarda archivos y caches generados por laravel
		* **logs**   --Guarda los logs que generes en tu aplicacion
	* **tests**		--Contiene los tests automaticos 
	* **vendor**	--contiene composer dependencies que elijas usar
	* **.env**  --Almacenamiento de configuracion (claves, users de DB, config DB, etc)
	* .env.example
	* .gitattributes
	* .gitignore  



## Request lifecycle

Todos los requests (comandos de artisan y requests HTTP) entran por el **enrty point public/index.php**

Desde ahi:
* Se envia el request al **kernel HTTP** (app/http/kernel.php) o **kernel consola** (app/console/kernel.php) segun corresponda
	* La instancia del kernel **hereda de la calse kernel** el siguiente comportamiento:
		* Cargar **.env variables**
		* **Bootstrap los service providers** que estan en el array **config/app.php**
* El kernel que corresponda hace pasar el request por los **middlewares globales**
	de su **array _$middleware _**
* Se entrega el request al **router**
* El **router activa el middleware de ruta** que corresponda.
* El router usa su logica o la del **controller** para procesar el request
* El Router o controller **devuelven una respuesta** y esta se envia al cliente


![enter image description here](https://lh3.googleusercontent.com/1hiHL5JaLxKG9eIbT_Gz0bNmNuDrapyCJ5yNMMgCQNexQe23aAmJ3MMzNIm88Gw65DrRWTGIEmvi)

![](https://raw.githubusercontent.com/martov1/DataBank/master/imagenes/flow_laravel_FUz0i4h_0uUbk89.jpg)


## Dependency inyection 


Podes hacer dependency inyection simplemente requiriendo una clase usando **use** y despues colocando una variable con esa clase en el **contructor**
```php
	use App/Respotories/UserRepostory
	
	class MiController extends Controller{

	//pongo alguna variable
		protected $miVariable
	
		//inyector una instancia de UserRepostory
		public function __construct(UserRepostory $miUserRepostory){
			//la guardo en mi nueva instancia de MiController
			$this->miUserRepostory =$miUserRepostory
		}
	}
```
## Service providers



### Registrar nuevos servicios

Los service providers **permiten registrar y bootstrapear servicios**, los servicios contienen logica que no va en el controller.

* Cada **service provider** configura una serie de **binds** que indican como y que se instancia cuando instancias el servicio
	```php
		class MiServiceProvider extends ServiceProvider {
	
			public function register(){
				// Coloca un bind llamado 'files' para poder crear instancias
				//de este service provider.
				
				//OPCION 1
				$this->app->bind('nombreDelBindDelServiceProvider', function(){
					// lo que devuelvas aca es lo que se instancia como service
					// provider
					return new Filesystem
				})
				
				//OPCION 2
				App:bind('Foo', function(){
					return new Filesystem
				})
			
			}
		}
	```
		
* Larvel **registra estos binds:**
	*  leyendo las clases nombradas en **array de providers de app/config/app.php**
	*  Ejecutando la funcion **register()** de cada provider

para hacer eso es necesario que el composer autoloader haya cargado las clases.
*  en el archivo **composer.json** dentro del objeto **autoload**  colocas la **ruta al archivo** con el service provider y el service
*  Ejecutas el comando **composer dumpautoload**

>El autoloader usa la especificacion **psr-4** que pide que **el path y el namespace coincidan**
>**namespace:** App\CustomStuff\CustomDirectory;
>**path:** app/CustomStuff/CustomDirectory/SomeClass.php.


### bootear servicios

Si necesitas que tu siervicio tenga acceso a otro servicio o a alguna clase o funcionalidad que tiene que **haberse cargado con anterioredad** entonces tenes que colocar esto en la funcion **boot()** del service provder, esta funcion **se ejecuta despues de registrar todos los bindings**
	
```php
	use Illuminate\Contracts\Routing\ResponseFactory;
	class ComposerServiceProvider extends ServiceProvider
	{
		//ahora podes usar dependency inyection!!
	    public function boot(ResponseFactory $response)
	    {
			//o otros bindings!
	       app()->otroBinding()
	    }
	}
```




### Instanciar servicios

Podes **crear una instancia de un service provider** en cualquier lado de la app referenciando el nombre de su bind
```php
	//asi
	$miInstancia = App::make('nombreDelBindDelServiceProvider')
	// o asi
	$miInstancia = $app['nombreDelBindDelServiceProvider']
```

### Deferir servicios


Podes deferir servicios, eso implica que **solo se cargara cuando sea utilizado**, para eso necesitas indicar **que clases provee este servicio**, esto lo haces implementando la funcion **provides()**


```php
	class RiakServiceProvider extends ServiceProvider
	{
	    //Indicas que esta deferido
	    protected $defer = true;
	
	    //Indicas el registro como haces siempre
	    public function register()
	    {
	        $this->app->singleton(Connection::class, function ($app) {
	            return new Connection($app['config']['riak']);
	        });
	    }
	
	    //Indicas que clase instancia el metodo register
	    public function provides()
	    {
	        return [Connection::class];
	    }
	}

```


## Views

Estan ubicadas en **resources/views**

**la convencion de nombres es:**

		NOMBRE.blade.php
		
Donde **nombre** sera el nombre del view que **usaremos para referenciarlo en codigo**


### Variables de template

Podes outputear variables de forma similar a Angular
```html
	<div>{{$miVariable}}</div>
```

### Bloques logicos



los bloques logicos se hacen asi

* **foreach:**
	```php
		@foreach($coleccion as $item)
			
			<li>{{$item}}</li>
		
		@endforeach
	```
* **If, else**
	```php
		@if(CONDICION)
		   @extends("template/index")
		@else
		    @extends("template/login")
		@endif
	```
* **While:**
	```php
    	@while (CONDICION)
    	  <li>{{{ $item }}</li>
    	@endforeach
	```
### extends e includes

**Includes:**
Un Includes simplemente trae HTML de otro archivo

archivo1.blade.html
```html
	<p>hola</p>
```
archivo2.html
```html
	@include('archivo1')
	<p>jorge</p>
```
Podes extender un archivo HTML con otro, y podes tener transclusion con datos de uno a otro.

**extends:**
Es un include que tiene la capacidad de traer partes de un archivo.


archivo1.blade.html
```html
	<p>hola</p>
	@yield('nombre')
	<p>como estas</p>
	@yield('respuesta')
```
archivo2.html
```html
	@extends('archivo1')
	@section('nombre')
	<p>jorge</p>
	@endsection
	@section('respuesta')
	<p>muy bien, vos?</p>
	@endsection
```



## Configuracion y credenciales


La configuracion, credenciales, contraseñas y otros valores que puedan ser usados para loguearse a la base de datos o otros servuicios se guardan en el archivo **.env.NOMBREDEENVIRONMENT**

**cosas que van aca:**
* API keys
* credenciales de DB
* timezone y locale
* config de database y sesiones


Seran entonces **Variables de environmente** accesibles a todos los puntos de la aplicacion usando

* **env('nombreVariable','defaultSiNoEstaSeteado')**.
* **$_ENV**

Podes acceder al nombre del environment asi:
```php
	if (App::environment('local')) {
	    // The environment is local
	}
```



## Database

### Migrations

Laravel usa **migraciones**, eso implica que el schema es definido en codigo.

**cada migracion es una clase**

* **artisan crea las tablas definidas en migrations usando el comando:** 

	php artisan migrate

* **Las migraciones estan configuradas en:**

			database/migrations
	* por default vienen dos:
 **users** para usuarios de nuestra futura app
 **passwors resets** para los passwords resets de nuestra futura app
			
### Crear migrations

**Para crear una migracion:**

* una migracion limpia sin nada
		artisan make:migration NOMBRE
* Una migracion con el codigo necesario para crear una tabla
		 artisan make:migration NOMBRE --create=TABLENAME
		 
	Los nombres elegidos siguen una logica, por ejemplo, la migracion que crea la tabla de ventas podria llamarse **create_sales_table** con el comando 
	`artisan make:migration create_sales_table --create=sales`
	
**Una vez creada la migracion se puede editar la migracion:**

```php
public function up(){
Schema::create('sales', function(Blueprint $table){
		$table->increments('id');
		$table->string('nombre');
		$table->integer('salesid');
		$table->timestamps();
		$table->boolean('completed')->default(false); //default por si no
													  //es especificado
	})
}
```


## ORM query builder

Hacer selects con el ORM directamente de la base de datos.
Esto se hace con la clase `DB`

**Selects:**
```php
	//obtener los datos de una tabla
	$tablita = DB::table('miTabla')->get()
	$tablita = DB::table('miTabla')->where('created_at', fecha())->get()
	$tablita = DB::table('miTabla')->where('id','>', 10)
	$tablita = DB::table('miTabla')->lastest()->get()
	$tablita = DB::table('miTabla')->find($id)
```
## Eloquent

**los modelos referencian a las tablas mediante concidencia de nombre**

**los modelos deben ser singulares, las tablas plurales**

### Crear models

Los modelos se encuentran en **app/**

Son representaciones de la base de datos, te permiten tener acceso a **tinkerer** 
**para crear un modelo haces:**

	php artisan make::model miModelo
	
**Tienen esta estructura:**
```php
	use Illuminate/database/eloquent/model
	
	class miModelo extends Model{
	
	}
```
### Crear modelo con migracion

Podes crear un modelo y la migracion usando el atributo -m

	php artisan make:model miModelo -m

### Extender modelos
```php
	class miModelo extends Model{
		Public function miFuncion(){
			//hagoCosas!
		}
		
		//Podes crear funciones estaticas
		Public static function miFuncionEstatica(){
			
			return static::where('completed',true)->get()
			
		}
	}
```
	

### Referenciar modelos

Los modelos se referencian dentro del namespace **"App"** con la subclase **NOMBREDEMODEL**. OSEA **App/usuarios**
```php
	//Hacer uso de la funcion "miFuncion" del modelo "miModelo"
	$resultado = App/miModelo::miFuncion() 
	//pedir las tareas completadas
	$resultado = App/miModelo::where('completado', true)->get() 
```
	
### Guardar datos en base de datos

* **Podes guardar los datos usando model->save()**
	```php
		//creas o obtenes una instancia de un modelo
		$miObjeto = new MiModelo
		//lo modificas
		$miObjeto->titulo = "dato 1"
		//lo guardas
		$miObjeto->save()
	```
	
* **podes crear una instancia de modelo y lo guardas a la vez**
	* Para usar este metodo, tenes que declarar las cosas que se pueden editar en 
	la variable _fillable_ del modelo
	```php
	//En algun lado del codigo, ej: controller
	MiModelo::create([
		'titulo'=> 'hola!',
		'fecha'=>'10/10/2018'
	])
	```

	```php
	// En la clase MiModelo
	
	//whitelist de cosas que dejo modificar	
	protected $fillable=['title', 'fecha']
	// ó blacklist de cosas que no dejo modificar
	protected $guarded=['title', 'fecha']
	```

### Route Model Binding

Si en la funcion del controller colocas un parametro de type Model, por ejemplo `MiModelo $miModelo`, y si el parametro que recibe la funcion desde la ruta es un **Int** entonces **MEDIANTE DEPENDENCY INYECTION el parametro se reemplaza por el modelo con ese id en la tabla **

Si en tu ruta tenes
```php
	//ej usuarios/105545
	Route::get('usuarios/{id}', 'UserController@mostrar')
```
y en el controller
```php
	public function show(User $user){
		//$user es originalmente '105545' representando el ID de un usuario.
		//Al colocarlo en la funcion como de clase "User" con nombre de variable 
		//"user" eloquent sabe que debe buscar una instancia de "user" con ese ID 
		// en la DB y devolverlo
		return $user
		//{id:105545, name:'jorge', surname:'lopez'}
	}
```
	
**podes usar otro campo de la tabla en lugar del id**
	
EJ: usuarios/jorge

Colocas en el model la funcion **getRouteKeyName**, que debe devolver el campo de la tabla que se matcheara con la ruta:
```php
	//El model de users
	public function getRouteKeyName(){
		return 'name'
	}
```

y en el controller
```php
	public function show(User $user){
		
		return $user
		//{id:105545, name:'jorge', surname:'lopez'}
	}
```
	
	
	
	
### Joins con IDs

Si tu modelo tiene un valor con 'modelo2_id' entonces podes hacer esto en tu modelo:


* **One to many:**
EJ: comments tiene un valor post_id

```php
	class Post extends Model{
	
		public function buscarComentarios() {
			//busca los posts con el post_id de este modelo
			return $this->hasMany(app\comment)
		}
	}
```


* **One to one:**
```php
	class Comment extends Model{
	
		public function buscarPost() {
			//busca los posts con el post_id de este modelo
			return $this->belongs(app\post)
		}
		
	
	}
```
* **Guardar algo con el ID de un modelo de forma EXPLICITA:**

```php
	//En el model de Post
	public function addComment($body){
		App\Comment::create([
			'body'=>´mi mensajhe´,
			'post_id'=>$this->id
		])
	}
```

* **Guardar algo con el ID de un modelo de forma IMPLICITA**
```php
		public function obtenerComentarios(){
			return $this->hasMany(App\comment)
		}
		
		public function añadirComentario(){
		
			//Le añade el ID automaticamente, por que esta obteniendo 
			//El modelo desde la funcion hasMany
			$this->obtenerComentarios()->create(['body'=>$body])
		}
```		
* **many to many:**

Aca tenes que tener una tabla intermedia que sea **tabla1_tabla2 con las ids de la primera y segunda tabla**, indicando las relaciones
```php
	//En el modelo Posts
		return $this->belongsToMany(App\tag) //obtener tags asignados a este post
	//Obtener posts y tags
		return App\Post::with('tags')->get()
	//añadir relacion
		$post->tags()->attach('id del tag' | 'instancia del model')
	//remover relacion
		$post->tags()->detach('id del tag' | 'instancia del model')
```





## Repositories


sirven para representar **colecciones de cosas**, de esta forma no las tenes en el controller,**o cosas que se repiten en varios controllers, y que por algun motivo no van en el modelo** (porque por ejemplo es algo que **combina varios modelos**).
```php
	namespace App\Repostories
	
	use App\User
	
	class Users {
		
		public function administrators(){
			//query que devuelve los usaurios administradores
		}
			public function editors(){
			//query que devuelve los usaurios editores
		}
	}
```

Despues podes accederlo por **DI**

```php
	public function hola(Users $users){
		$losAdmins = $users->administrators()
	}
```

o lo podes **instanciar diectamente**
```php
	$users = new \App\Repositories\Users
	$losAdmins = $users->administrators
```

# Webpack


Laravel usa Webpack y un script llamado Webpack mix para precompilar los archivos de frontend, podes precompilar **SASS, Less, minimizar JS, etc**

Los archivos precompilados van en **/resources** y corriendo **node watch** a medida que los cambias los compila en **/public**


# Authentication



# Uso de sesiones

Una vez que el usuario esta autenticado y tiene una sesion, podes guardar datos en la sesion y usarlos durante la navegacion entre paginas del usuario

```php
//guardar algo en la sesion
	session(['miSaludo'=>'holaaaa!!!!'])
//extraer algo de la sesion
	session('miSaludo', 'saludo default por si la variable miSaludo no esta definida')
```
## Flash

Sirve para guardar algo para la proxima pagina que visite el usuario, despues de eso se borra
```php

	//en alguna pagina
	session()->flash('mensaje'=>'hola juan!')
	redirect()->home()


	//en home
	session(mensaje) // tiene el valor de 'hola juan'
```


# Enviar emails


Usas la clase **Mail** para enviar emails, a su vez necesitas instancias de esta clase que representan templates de emails.

**La configuracion del servidor de emails debe estar presente en .env**

**La configuracion esta en config/mail.php**

Podes crear estos templates con **artisan create::mail** y estan en **app/Mail**

```php
	class miMail extends Mailable{
	
		public $parametros
		public function build(){
			//necesitas un blade template que se llame igual que el
			//nombre del nuevo mail
			// Hago cosas con parametros
			return $this->view('emails.miEmail')
		
		}
	}
```
podes enviarlos asi
```php
	\Mail::to($user)->send(new miEmail($parametros))
```

# Events y listeners






<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwODc2MzE5OTQsOTg1NDQwMjQwLDE2Mz
A0OTE5MTQsMTk5OTU1Nzc5Myw3ODY3NTU5NTddfQ==
-->