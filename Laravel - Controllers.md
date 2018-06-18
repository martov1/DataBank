

#Contenido




* Creacion
	* Controllers y namespaces 
	* Single action controllers
	* Acceder al request
* Dependency inyection 
* Validacion de datos
* Controllers y namespaces
* Middleware en controllers
	* Middleware para rutas especificas
 	* Middlewares declarados en el controller
* Resource controllers para CRUD
	* Resources con route model binding
	* Resources con menos acciones
	* API resource
	* Renombrar las acciones de un resource
	* Renombrar verbos del resource
	* Renombrar parametros de URL
	* Añadir metodos customizados al resource




#Creacion

Los controladores pueden existir entre los **routes** y los **views** para determinar comportamiento.

Se guardan por default en la ruta **app/http/controllers** y **bajo el mismo namespace**

**Los podes crear asi:**

	php artisan make:controller MiController
	

**Se ven asi:**

	class UserController extends Controller{
		
		//El id es un parametro que me dio el router, queda por DEPENDENCY INYECTION
		public function listarUsuario($id) {
			$usuarios = app/Usuario::all()
			//Devolver un view
			return view('dashboard/listarusuaruios', compact('usuarios'))
			//Devolver un Json
			return $usuarios
		}
	}


**En el Router:**

Notese que la sintaxis es **NombreDeController@FuncionDelController**

		Route::get('usuarios/{id}', 'UserController@mostrar')

##Controllers y namespaces

Es importante notar que Laravel autematicamente identifica los controllers relativos al namespace **App/Http/Controllers**, esto se puede cambiar en el **RouteProviderService**

* Si tenes controllers en subcarpeta (**App/Http/Controllerss/feature1**) **tenes que especificar el namespace**

		Route::get('foo', 'feature1\MiController@method');

* Si queres tener los **controllers fuera de la carpeta controllers**, es necesario cambiar el namespace desde el **RouteProviderService**

    	protected $namespace = 'App\Http\Controllers';
    	//to
    	protected $namespace = 'App\Http\Features'
	
	Y en la ruta usas el namespace a partir de esa carpeta
		// App\Http\Features\miController.php
		Route::get('phicq', 'MyController@index');
		// App\Http\Features\feature1\miController.php
		Route::get('phicq', 'feature1\MyController@index');



##Single action controllers

Si queres un controller que solo tenga una **unica funcion**, podes definir una funcion **__invoque()**

	class MiController extends Controller
	{
	    public function __invoke($id)
	    {
	        //Hacer cosas
	    }
	}
	
Despues al llamarla desde una ruta, **no necesitas decir que funcion del controller llamar**, por que estas explicitamente indicando que hay una sola

	Route::get('user/{id}', 'MiController');




	
## Acceder al request

Podes tener acceso al request desde el controller usando **dependency inyection**

* **Inyeccion del request en el controller**


	//Colocas la clase y el request se inyecta solo por DI
	use Illuminate\Http\Request
	
	class miController extends Controller{
		 
		//la request queda inyectada en la variable $request de type Request
		public function show(Request $request, $id){
		
		}
	}
	
* **Obtener campos puntuales del request**


	use Illuminate\Http\Request
	//Obtener dos campos del request
	$loQueQuiero = request([´campo1','campo2'])
	
	//los mismo pero de otra forma
	$loQueQuiero = [request()->campo1, request()->campo2]
	
---

#Dependency inyection

Los controllers tienen acceso a dependency inyection de forma natural



	namespace App\Http\Controllers;
	use App\Repositories\UserRepository; //lo que quiero inyectar
	
	class UserController extends Controller
	{
	    protected $users;
		//Coloco lo que quiero inyectar en el contructor indicando su clase
	    public function __construct(UserRepository $users)
	    {
			//Lo guardo en mi instancia del controller
	        $this->users = $users;
	    }
	}


---

# Validacion de datos


La funcion `validate` toma una variable como primer parametro y una serie de validadores en un array del otro.

Si no logra validar:
* Si el http header **Accept application/json** esta, entonces devuelve un error JSON
* redirecciona a la pagina anterior
	* A su vez en la pagina anterior puebla la variable `$errors` para que la puedas usar en blade 


	//En el controller
	public function guardar(){
	
		$this->validate(request(),[
			'title' =>'requeired|max:10'
		])
	}
	
---
	
#Middleware en controllers

Si bien podes asignar middleware en el Router asi

	Route::get('profile', 'UserController@show')->middleware('auth');

Tambien podes asignarlo en el controller usando la **funcion middleware en el constructor del controller**, ademas poder **correr middleware para rutas con nombre especificas**

	class UserController extends Controller
	{
	    public function __construct()
	    {
			//Correr el middleware "auth" para todas las rutas 
			//que van a este controller
	        $this->middleware('auth');
	    }
	}


##Middleware para rutas especificas

Si **un controller recibe requests desde varias rutas diferentes**, podes** correr middlewares diferentes dependiendo del nombre de la ruta** que lleva a ese controller.

	class UserController extends Controller
	{
	    public function __construct()
	    {
			//Correr el middleware "auth" para todas las rutas 
			//que van a este controller
	        $this->middleware('auth');
			// Correr el middleware "log" solo para la ruta "index"
	        $this->middleware('log')->only('index');
			//Correr el middleware "subscribed" para todas las rutas
			//que van a este controller excepto para la ruta "store"
	        $this->middleware('subscribed')->except('store');
	    }
	}
	
##Middlewares declarados en el controller

Si necesitas un middleware que es muy especifico y solo se usa en un controller **lo podes declarar dentro del mismo controller asi.**

	$this->middleware(function ($request, $next) {
	    return $next($request);
	});
	
#Resource controllers para CRUD

Podes generar controllers que y **vienen con los metodos CRUD** y pueden usarse como un **shorthand en el router**

**Para hacer un resource controller en artisan:**
		
	php artisan make:controller PhotoController --resource
	

**En el router:**

	Route::resource('photos', 'PhotoController');
	
**Los siguientes metodos y rutas son creados:**

![](http://i.markdownnotes.com/resourcemethodslaravel.jpg)

##Resources con route model binding

Si queres usar route model binding, podes indicarlo al momento de la creacion del resource en artisan. 

	php artisan make:controller PhotoController --resource --model=Photo


Con rutas en lugares diferentes

	php artisan make:controller \App\Http\Users\UserController --resource 
	--model=\App\Http\Users\User
##Resources con menos acciones

Si no queres usar todas las acciones 

**EJ:**
* Queres que los usuarios puedan **create y retrive**, mientras que el admin pueda hacer **CRUD**
	* /admin/photos - **CRUD**
	* /photos - **CR**


**Podes declarar estas limitaciones asi:**

	Route::resource('photos', 'PhotoController')->only([
	    'index', 'show', 'store'
	]);
	
	Route::resource('admin/photos', 'PhotoController')
	
##API resource

El API resource es una version de resource que prescinde de las acciones **create** y **edit**, ya que estas apuntan a un **HTML template** y esto no es necesario para una API

**Para crear un API resource:**

	php artisan make:controller API/PhotoController --api


##Renombrar las acciones de un resource

Si no te gusta que las acciones se llamen _photos.update, photos.index, etc_ las **podes renombrar**

	//renombre photos.create a photos.crearLaFoto
	Route::resource('photos', 'PhotoController')->names([
	    'create' => 'photos.crearLaFoto'
	]);


##Renombrar verbos del resource

Podes renombrar los verbos usados en los resources el el **boot method** del **appServiceProvider**

	public function boot()
	{
	    Route::resourceVerbs([
	        'create' => 'crear',
	        'edit' => 'editar',
	    ]);
	}


##Renombrar parametros de URL

Por default el nombre del parametro de URL es el nombre del modelo en singular, pero puede cambiarse

	Route::resource('user', 'AdminUserController')->parameters([
	    'user' => 'admin_user'
	]);
	
Renombra la ruta de:
	
	user/{user}
	
a

	user/{admin_user}
	
##Añadir metodos customizados al resource

Podes añadir metodos customizados directamente en el controller, Pero es importante que **coloques las rutas hacia los metodos customizados antes que las del resource**

	//Ruta custom
	Route::get('photos/popular', 'PhotoController@method');
	//Rutas del resource
	Route::resource('photos', 'PhotoController');	
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgyMzQxNDQ3NF19
-->