

# Contenido


* Intro
* gates
	* Crear un gate 
		* Como un closure
		* Como una clase separada
	* Usar un gate
	* Usar gate para un resource
	* Verificar si un user pasa un gate
		* Correr logica antes o despues de los gates 
* Policies
	*  Escribir policies
		* Reglas generales
		* Logica previa a las reglas
	* Usar policies
		* Determinar si un user tiene autorizacion
		* Usar policies como Middleware
		* Usar policies en controllers




# Intro

Laravel tienedos formas de autorizar acciones
 
* **Gates** 
	* Autorizacion usando closures 
	* Para cosas simples
* **policies** 
	*  Autorizacion basada en una clase
	*  Para cosas compejas
	*  Puede compartirse entre varias rutas, modelos o recursos



# Gates

## Crear un gate
Los gates se definen en la **funcion boot()** del **AuthServiceProvider** usando la **Gate facade** y reciben **una instancia del usuario como primer argumento**.

Puede recibir otros argumentos, como por ej algun **modelo de eloquent**


### Como un closure
**El gate debe devolver un BOOLEAN**

```php
	public function boot()
	{
	    $this->registerPolicies();
	
	    Gate::define('MiGate', function ($user, $post) {
			//Devolver un boolean!
	        return $user->id == $post->user_id;
	    });
	}
```

### Como una clase separada

Podes definir tu gate en una clase separada y despues acceder a sus metodos igual que como haces con un controller. **es mucho mas limpio**

**En tu clase separada**
```php
	namespare App/misClases/MiGate
	
	class MiPostGate{
	
		function actualizar($user, $post){
		//hacer cosas
		}
		
		function crear($user, $post){
		//hacer cosas
		}
	
	}
```
**En AuthServiceProvider**
```php
	public function boot()
	{
	    $this->registerPolicies();
	
	    Gate::define('actualizar-post', MiPostGate@actualizar);
		Gate::define('crear-post', MiPostGate@crear);
	}
```
## Usar un gate

Una vez que creaste un gate, para usar un gate para decidir algo cuando un usuario esta loguead:
```php
	// Si el gate devuelve true
	if (Gate::allows('MiGate', $post)) {
	    // The current user can update the post...
	}
	
	// Si el gate devuelve false
	if (Gate::denies('MiGate', $post)) {
	    // The current user can't update the post...
	}
```
**laravel pasa la instancia de este usuario al gate automaticamente**
	
## Usar gate para un resource

Podes abreviar con una sola linea todos los gates para las operaciones CRUD
```php
	Gate::resource('posts', 'App\Policies\PostPolicy');
```
**Equivale a:** 
```php
	Gate::define('posts.view', 'App\Policies\PostPolicy@view');
	Gate::define('posts.create', 'App\Policies\PostPolicy@create');
	Gate::define('posts.update', 'App\Policies\PostPolicy@update');
	Gate::define('posts.delete', 'App\Policies\PostPolicy@delete');
```


## Verificar si un user pasa un gate

Si tenes un model de un usuario y queres ver si pasa un gate, haces:
```php
	if (Gate::forUser($user)->allows('update-post', $post)) {
	    // The user can update the post...
	}
	
	if (Gate::forUser($user)->denies('update-post', $post)) {
	    // The user can't update the post...
	}
```
### Correr logica antes o despues de los gates

Podes correr una pieza de codigo **antes de que se corra cualquier gate** usando la **funcion gate::before()**

>Si la funcion devuelve algo **que no es NULL** entonces **se considera a ese valor el resultado de los gates**
```php
	Gate::before(function ($user, $ability) {
	    if ($user->isSuperAdmin()) {
			//Los gates no se corren, esta sera la respuesta del gate
	        return true;
	    } else{
			//Los gates que vienen despues se corren normalmente
			return null
		}
	});
```

**Correr algo despues de los gates:**
```php
	Gate::after(function ($user, $ability, $result, $arguments) {
	    //
	});
```
# Policies

>Son clases que **organizan la logica de autorizacion alrededor de un modelo o recurso.** Por lo que estan **necesariamente atadas a un model**

Se guardan en **app/Policies**

* **Para crearlos:**
	* Un policy generico
				```php artisan make:policy MiPolicy```
	* Un policy con metodos CRUD armados
			`php artisan make:policy PostPolicy --model=Post`
			
.
* **Se registran en el AuthServiceProvider asi:**
como un policy esta atado a un model necesariamente, hay que registrar el policy junto con el model.
	```php
		//En el AuthServiceProvider
    	protected $policies = [
    	    MiModelo::class => MiModeloPolicy::class,
    	];
	```

* **Se ven asi:**
	```php
		namespace App\Policies;
		use App\User;
		use App\Post;
		
		class PostPolicy
		{
		    
		    public function editarElPost(User $user, Post $post)
		    {
		        return $user->id === $post->user_id;
		    }
		}
	```
* **Se usan asi:**
	```php
		if ($user->can('editarElPost', $post)) {
		    //
		}
	```
## Escribir policies

### Reglas generales

Las policies estan constituidas por 

* Metodos que **describen que es lo que se esta autorizando**
	* Reciben como parametros:
		* Al **user** 
		* Una **instancia particular del modelo** (opcional)
	* Devuelven
		* **True** si se autoriza la accion a ese user en ese modelo
		* **false** si no.

Las funciones deben devolver **true o false** dependiendo de si la accion fue autorizada o no.
```php
		class PostPolicy
		{
		    //El usuario puede ACTUALIZAR este post?
		    public function actualizar(User $user, Post $post)
		    {
				//Si el user creo este post, entonces si
		        return $user->id === $post->user_id;
		    }
			
			//El usuario puede CREAR este post?
		    public function CREAR(User $user)
		    {
				// si una columna en la DB llamada "puedePostear" es true
		        return $user->puedePostear === true;
		    }
		}
```
### Logica previa a las reglas

Podes tener logia antes de que se ejecute cualquiera de las funciones de la policy con la funcion **before()**.
```php
	// El usuario y la habilidad solicitada son parametros
	public function before($user, $ability)
	{
		//Si el user es admin, autorizar todo y no correr ninguna regla
	    if ($user->isSuperAdmin()) {
	        return true;
	    }
	}
```


## Usar policies

### Determinar si un user tiene autorizacion

podes usar el helper function del modelo **user**, que pide el nombre del metodo del policy y el nombre del modelo a modificar.

>como hay un solo policy por modelo, laravel sabe cual es el policy de $post solamente sabiendo su modelo.
```php
	//Editar un modelo
	if ($user->can('actualizar', $post)) {
    // ejecuta ACTUALIZAR() en el policy
	}
	
	//Crear una instancia de un modelo
	if ($user->can('create', Post::class)) {
    // ejecuta "CREAR()" en el policy
	}
```
### Usar policies como Middleware

Podes hacer uso del Middleware **Illuminate\Auth\Middleware\Authorize** para determinar si un usuario puede hacer algo indicando:
* **can** o **cant**
* La **funcion del policy** que quier correr
* Un **route parameter** que enviar a la funcion (generalmente un ID)
* El nombre del modelo que queres crear

**Para editar un modelo:**
```php
		Route::put('/post/{miParametro}', MiController@update)
		->middleware('can:ACTUALIZAR,miParametro');
```
**Para crear un modelo:**
```php
		Route::post('/post',MiController@create)
		->middleware('can:CREAR,App\Post');
```

### Usar policies en controllers

Dentro del controller podes usar el metodo **authorize()** para determiar si una accion tiene el permiso necesario. 

**Tiene como parametros:**
* El nombre de la **funcion del policy**
* La **instancia del Modelo** para editar modelos
* La **clase del modelo** para crear modelos

**Concecuencias:**
* **Si autoriza:** el codigo continua normalmente
* **Si no autoriza:** 
	* Se genera una **aurhotization exception**
	* Se devuelve un **HTTP code 403**


```php
	//Editar modelos
    public function update(Request $request, Post $post)
    {
        $this->authorize('ACTUALIZAR', $post);

        // Hacer el update!
    }
	
	//crear modelos
	public function create(Request $request)
	{
	    $this->authorize('CREAR', Post::class);
	
	    // Crear el elemento!
	}
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYyOTczNDI0OCwxMzI5OTY0NTY4XX0=
-->