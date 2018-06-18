


**Me quede en:**
Adding Custom Guards


# Content

* Intro
* Auth out of the box
	* Redirecciones
	* Username para autenticar
	* Validado y guardado del usuario 
	* Acceder al usuario autenticado
		* Determinar si el usuario esta autenticado
* Proteger rutas - Auth middleware
	* Redirigir al usuario no autenticado
	* Especificar un guard
* Autenticacion manual
	* Autenticacion con condiciones adicionales
	* Autenticacion con un guard especifico
	* Remember user
	* Log out 
	* Logout de todos los dispositivos
* Login programatico
* Guards customizados
* Providers customizados **wip**
* UserProvider contract **wip**

.

* API authentication
	* Instalacion 
	* Configuracion
	* Oauth flows de passport
	* Crear clientes
		* localmente
		* Via una API
	* Authentication code flow - **web clients con backchannel y servers usan esto**
		* Obtencion del Authorization code
		* Obtencion del Access token
	* Password grant tokens	- **clients que controlas totalmente pueden usar esto**
		* Obtener un token
	*  Implicit grant tokens - **web clients sin backchannel**
	* Client credentials grant token - **comunicacion entre servers usan esto**
		* Obtener un token
	* Personal access tokens - **mis web clients en mi dominio usan esto**
		* Crear tokens
		* API para personal access tokens
	* Proteger rutas
	* Scopes
		* Definir scopes
		* Solicitar un token con cierto scope
		* Filtrar ruta por token scope
		* Determinar si un token tiene un scope

		





# Intro

La configuracion para autenticacion esta en **config/auth.php**

**La aunticacion consta de dos partes:**
* **guards** - determina como los usuarios son autenticados en cada request
* **providers** - Determina como los usuarios son obtenidos del persistent storage (DB, facebook etc)

**Laravel viene con varios controllers que se encargan de diversas partes de la autenticacion:**
* **RegisterController**  - Maneja la creacion de nuevos usuarios
* **LoginController** - Maneja la autenticacion
* **ForgotPassowrdController** - Maneja el envio de links para reseteo de contraseña via email


# Auth out of the box

Laravel puede preparar todo lo necesario para una autenticacion inicial asi:

	php artisan make:auth

Este comando prepara

* Un Layout view con bootstrap que los otros views usaran
* **Registration** view
* **Login** views
* **Rutas** para los endpoints
* **HomeController** para enviar al usuario logueado a _algun lado_

Los views creados se colocan en `resources/views/auth`

## Redirecciones

Los controllers de autenticacion indican a donde redirigen cuando el usuario se loguea con la propiedad **$redirectTo**
```php
	protected $redirectTo = '/un/path';
```
o con la funcion **redirectTo()** si necesitas algo dinamico
```php	protected function redirectTo()
	{
	    return '/path';
	}
```
## Username para autenticar

Por default laravel usa el **email** como username, pero esto puede modificarse por otro campo configurando la funcion **username()** en el **loginController**
```php
	public function username()
	{
	    return 'username';
	}
```
	
## Validado y guardado del usuario

El controller **RegisterController** se encarga de validar, crear y guardar nuevos usuarios.

* **validator()** - contiene la logica que valida los datos del usuario
* **create()** - Contiene la logica que guarda los datos del usuario en la DB, generalmente usando el modelo **App/User**


## Acceder al usuario autenticado

Podes acceder al usuario autenticado que fue autenticado con los controllers de la siguiente manera:
```php
	Auth::user() //Obtener el usuario
	Auth::id() //Obtener el id del usuario
	$request->user() //Obtener el usuario a partir de un request
```
### Determinar si el usuario esta autenticado

Podes determinar si el usuario esta autenticado asi
```php
	Auth::check() //True si esta autenticado
```

# Proteger rutas 


El **Auth middleware**  tiene la capacidad de permitir acceso a ciertas rutas solo a usuarios autenticados. El middleware esta en `Illuminate\Auth\Middleware\Authenticate`

**Para bloquear el acceso a usuarios no autenticados a una ruta:**
```php
	Route::get('profile',MiController@unaAccion)->middleware('auth');
```
**En un controller**
```php
	public function __construct()
	{
	    $this->middleware('auth');
	}
```
## Especificar un guard

Usando el middleware **Auth** podes **especificar el guard que vas a usar**
```php
	 public function __construct(){
	    $this->middleware('auth:MiGuard');
	}
```
## Redirigir al usuario no autenticado

Si el usuario no esta autenticado, laravel puede:
* **Responder** con JSON **code 401** si es un request AJAX
* **Redireccionar** a la ruta con nombre **login**


Podes cambiar este comportamiento en el handler de exceptions **app/exceptions/Handler.php** definidiendo la funcion **unAuthenticated()**

```php
	protected function unauthenticated($request, AuthenticationException $exception)
	{
	    return $request->expectsJson()
	                ? response()->json(['message' => $exception->getMessage()], 401)
	                : redirect()->guest(route('login'));
	}
```
# Autenticacion manual

Podes autenticar manualmente usando las clases de laravel.

La funcion **Auth::attempt($credentials)** acepta un array de key-value pairs y va a internar encontrar un usuario con esos valores, si lo encuentra:
* devuelve **true** 
* añade una **sesion y cookie** a la respuesta que sera enviada al usuario

```php
	class LoginController extends Controller
	{
	    public function authenticate(Request $request)
	    {
			//Tomas las credenciales del request
	        $credentials = $request->only('email', 'password');
			//intentar encontrar al usuario en la base de datos con esas credenciales
			//Laravel hashea la passowrd solo
	        if (Auth::attempt($credentials)) {
	            // Si las credenciales son correctas, hacer cosas!
				// intended() devuelve al usuario a donde intentaba acceder
				// y acepta un default value
	            return redirect()->intended('dashboard');
	        }
	    }
	}
```
## Autenticacion con condiciones adicionales

Podes exigir durante el login que otras condiciones se cumplan en la tabla de usuarios
```php
	//Quiero que el usuario tenga en la columna "active" un 1
	Auth::attempt(['email' => $email, 'password' => $password, 'active' => 1])
```
## Autenticacion con un guard especifico

Podes usar un **guard** customizado para tener diferente autenticacion en diferentes partes de la aplicacion
```php
	if (Auth::guard('miGuard')->attempt($credentials)) {
	    //
	}
```
## Remember user

>Esto ya viene de manera automatica en el **LoginController**

Esta funcionalidad te permite **mantener al usuario loguardo indefinidamente** y hace uso de la comulma **remember_token** de la table USERS


**Podes mantener al usuario logueado indefinidamente asi:**
```php
		$remember=true;
		if (Auth::attempt(['email' => $email, 'password' => $password], $remember)) {
		    // The user is being remembered...
		}
```
**Podes determinar si el usuario envio la cookie de remember me y loguardlo asi**
```php
		if (Auth::viaRemember()) {
		    //
		}
```

	
## Log out

Podes desloguarte y borrar la info de sesion asi
```php
	Auth::logout();
```
## Logout de todos los dispositivos

Podes desloguear al usuario de todos los dispositivos (no solo del actual) asi:

* activar `Illuminate\Session\Middleware\AuthenticateSession::class` en el **HTTP KERNEL, grupo WEB**
	```php
		'web' => [
		    // ...
		    \Illuminate\Session\Middleware\AuthenticateSession::class,
		    // ...
		],
	```
* Usas el metodo **logoutOtherDevices** que necesita **la contraseña del user**
	```php
		use Illuminate\Support\Facades\Auth;
		Auth::logoutOtherDevices($password);
	```
		

# Login programatico

Podes loguear a un usuario programaticamente pasandole  a la funcion **login()**
* Una instancia de un user
* El ID de un user
	```php
		//Con una instancia de USER
		Auth::login($user);
		// Login and "remember" the given user...
		Auth::login($user, true);
		
		//Con un guard especifico
		Auth::guard('admin')->login($user);
		
		//con el ID del usuario
		Auth::loginUsingId(1);
		// Login and "remember" the given user...
		Auth::loginUsingId(1, true);

		//Autenticar al usuario solo por este request
		Auth::once($credentials)
	```


# Guards customizados

Para añadir guards customizados tenes que **extender el Auth facade**, esto lo tenes que hacer dentro del **boot()** de un **serviceProvider**, generalmente es comodo hacerlo dentro del provider **AuthServiceProvider**.

Una vez que extendes el Auth faccade, tu extension tiene que devolver una instancia de la **clase Guard** en  `Illuminate\Contracts\Auth\Guard`
```php
	public function boot()
	    {
	        $this->registerPolicies();
			//Extendes el Auth Faccade
	        Auth::extend('jwt', function ($app, $name, array $config) {
	            // Return an instance of Illuminate\Contracts\Auth\Guard...
	
	            return new JwtGuard(Auth::createUserProvider($config['provider']));
	        });
	    }
	}
```
Una vez definido el guard, lo podes usar en la configuracion de autenticacion en **auth.php**


# API authentication

## Instalacion

La autenticacion para apis en general se hace usando el modelo Oauth2 usando **passport**

**se instala asi:**

* Instalar passport, inicializar sus tablas
			`composer require laravel/passport=~4.0`
			`php artisan migrate`
			`php artisan passport:install`

* Agregar las clases **HasApiTokens** y **Notifiable** al **modelo Users**
	```php
		class User extends Authenticatable
		{
		    use HasApiTokens, Notifiable;
		}
	```
* Llamar a **Passport::toutes** desde el **boot()** de **AuthServiceProvider**
	```php
   	 public function boot()
   	 {
   	     $this->registerPolicies();
	
   	     Passport::routes();
   	 }
	 ```
* En **config/auth.php**, usar **passport** como **driver** en el listado de guards
	```php
		'guards' => [
		    'web' => [
		        'driver' => 'session',
		        'provider' => 'users',
		    ],
		
		    'api' => [
		        'driver' => 'passport',
		        'provider' => 'users',
		    ],
		],
	```
* Al pasar a produccion, generar **keys nuevas**
		`php artisan passport:keys`

## Configuracion
	
Por default los tokens de laravel **expiran despues de un año**, esto se puede cambian usando **tokensExpireIn()** y **refreshTokensExpireIn()**. Estos metodos deben llamarse desde el **boot()** del **AuthServiceProvider**
```php
	public function boot()
	{
	    Passport::tokensExpireIn(now()->addDays(15));
	    Passport::refreshTokensExpireIn(now()->addDays(30));
	}
```
### Rutas preconfiguradas

Las siguientes rutas ya vienen configuradas en **Passport::routes** y por eso no necesitan ser definidas manualmente.

* **/oauth/token** - Token Endpoint
* **/oauth/authorize** - Authorization Endpoint
* **/oauth/clients** - Client API
* **GET /oauth/scopes**  - Lista todos los scopes de la aplicacion

## Oauth flows de passport

Todos los metodos de autenticacion **necesitan** la creacion de un **client**

Los metodos de autenticacion provistos por passport son los siguientes, junto con los parametros que necesita cada uno:

* **Password grant token**
	* Client ID
	* Client Secret
	* Username
	* Password 
* **Client Credentals Grant token**
	* Client id
	* Client secret 
* **Authentication code**
	* client ID
	* redirect uri 
	* Client secret (para cambiar Authorization code por Access token en el back channel)
* **Implicit Grant Token**
	* client_id
	* redirect_uri
* **Personal access token**
	* proveer token a Usuario ya autenticado por otro medio


## Crear clientes

Los **clientes** son aquellos que consumen el sistema de autenticacion Oauth, podria ser **otra aplicacion**, **el usuario a travez de tu web app** o **otro de tus servers**

### Localmente
**Para crear un cliente localmente haces:**

	php artisan passport:client

### Via una API


Podes usar una JSON API que viene predefinida para permitir que terceros creen clientes (o usarla con tu propio frontend).

**Los endpoints predefinidos son:**
* **GET /oauth/clients**
	Permite ver los clientes del usuario autenticado
* **POST /oauth/clients payload={name:clientName, redirectUrl:URL}**
	Permite que un usuario registrado añada nuevos clientes. redirecciona al usuario al redirectUrl con un clientID y clientSecret
* **PUT /oauth/clients/{client-id} payload={name:clientName, redirectUrl:URL}**
	Permite actualizar los datos del cliente
* **DELETE /oauth/clients/{client-id}**
	Permite borrar un cliente	
* **GET /oauth/scopes** 
	Devuelve todos los scopes de la aplicacion
	
	
	
## Authentication code flow

>Este procedimiento es **para que un third party** pueda **obtener un access token en nombre de un usuario**.
>Durante el proceso el usuario sera **redireccionado a tu app para loguearse** y luego **redireccionado a la app original** con un **Authentication code**.
>El third-party luego debera usar el Authentication code para obtener un Access token
>usando su clientID y ClientSecret

### Obtencion del Authorization code
El desarrollador cuya aplicacion quiere acceder en nombre de un usuario a tu aplicacion debera hacerte un request a **/oauth/authorize** con:

* Client_id
* Redirect_uri = Callback de la third-party aplication
* Response_type=code
* Scope

>En el momento de creacion del client se especifico un Redirect_uri, este debera ser igual al de este request, esto evitar un **open redirect**


Al llegar este request a laravel, se mostrara una **pantalla de login** para que el user s**e autentique y apruebe el scope** solicitado.

**Para editar este view, tenes que:**

* Publicar los views de passport
		php artisan vendor:publish --tag=passport-views
* Editar el view ubicado en:
		resources/views/vendor/passport
		
### Obtencion del Access token

El desarrollador ahora debera enviar un **POST** a la ruta **/oauth/token** de tu aplicacion para pedir un **Access token** con la siguiente informacion
```php
            'grant_type' => 'authorization_code',
            'client_id' => 'client-id',
            'client_secret' => 'client-secret',
            'redirect_uri' => 'http://example.com/callback',
            'code' => AUTHROIZATION TOKEN ACA,
```
Laravel contestara con
* **Access token**
* **Refresh token**
* **exipres in** en segundos

### Refreshing tokens

Para refrescar tokens, se envia un **POST** a la ruta **/oauth/token** 
```php
        'grant_type' => 'refresh_token',
        'refresh_token' => 'the-refresh-token',
        'client_id' => 'client-id',
        'client_secret' => 'client-secret',
        'scope' => '',
```
Laravel contestara con
* **Access token**
* **Refresh token**
* **exipres in** en segundos

## Password grant tokens

Este tipo de grant usa las credenciales del cliente y del user para obtener un access token

Si no corriste	  **_php artisan passport:install_** entonces para crear un cliente que consuma **password grants** necesitas correr.

		php artisan passport:client --password


### Obtener un token

El third party debe enviar un **POST** a **/oauth/token**. 

```php
 		'grant_type' => 'password',
        'client_id' => 'client-id',
        'client_secret' => 'client-secret',
        'username' => 'taylor@laravel.com',
        'password' => 'my-password',
        'scope' => '',
```
Laravel contestara con
* **Access token**
* **Refresh token**
* **exipres in** en segundos

## Implicit grant tokens


Permite a un tercero si backchannel solicitar un access token.
Para activarlo es necesario agregar la funcion **Passport::enableImplicitGrant()** en la funcion **boot()** del **AuthServiceProvider**
```php
	public function boot()
	{
		//Activar implicit grants
	    Passport::enableImplicitGrant();
	}
```
Una vez habilitado, un tercero puede redireccionar a tu authorization endpoint **/oauth/authorize** con el siguiente request
```php
        'client_id' => 'client-id',
        'redirect_uri' => 'http://example.com/callback',
        'response_type' => 'token',
        'scope' => '',
```
**El authorization endpoint:**
* Le pedira al usuario loguearse y aceptar el scope
* Una vez hecho, el usuario es redireccionado a la aplicacion original usando la **redirect_uri** y se añade el **access token** en un fragment de esta URL para ser consumido por el third party.


## Client credentials grant token


Se usa principalmente para comunicacion entre servidores, muchas veces para cosas que **no necesitan permiso de un user** sino que estan dentro de las cosas permitidas a **un cliente puntual**

Para habilitarlo hace falta añadir el middleware **CheckClientCredentials** a aquellas rutas en las que desees habilitarlo

**en el http kernel:**
```php
		protected $routeMiddleware = [
		    'client' => CheckClientCredentials::class,
		];
```
**En la ruta:**
```php
	Route::get('/user', function(Request $request) {
	    ...
	})->middleware('client');
```
### Obtener un token


Para botener un token tenes que hacer un **POST** al endpoint **oauth/token**

        'grant_type' => 'client_credentials',
        'client_id' => 'client-id',
        'client_secret' => 'client-secret',
        'scope' => 'your-scope',

##Personal access tokens

>Este flow **no es para third partys**
>**los personal access tokens siempre tienen expiracion de UN AÑO, sin importar lo
>indicado en tokensExpireIn()**

Se usan cuando un usuari desea proveerse de un token, por ejemplo **un usuario logueado con autenticacion comun necesita un token para acceder a una API**. 


Si no corriste	  **_php artisan passport:install_** entonces para crear un cliente que consuma **Personal access tokens** necesitas correr.

		php artisan passport:client --personal

###Crear tokens

Podes crear un token para un usuario, asi:

	//Encontras el modelo de un usuario
	$user = App\User::find(1);
	
	// Creating a token without scopes...
	$token = $user->createToken('Token Name')->accessToken;
	
	// Creating a token with scopes...
	$token = $user->createToken('My Token', ['place-orders'])->accessToken;

Se lo podes enviar en el mismo request para que el usuario haga lo que desee con el.


###API para personal access tokens

Laravel viene con una API para permitir que el la aplicacion (ej: angular) o el usuario administren sus personal acccess tokens


* **GET /oauth/personal-access-tokens** 
Muestra todos los access tokens creados por el usuario logueado.
* **POST /oauth/personal-access-tokens  payload={name: 'Token Name', scopes: []}**
Crea un nuevo Access token
* **DELETE /oauth/personal-access-tokens/{token-id}**
Permite al usuario borrar un token


##Proteger rutas

**Passport tiene su propio driver para el API guard, el cual ya colocaste durante la instalacion**, asi que solamente indicando que vas a usar el api guard en la ruta es suficiente.

**permite el acceso si:**
* tiene un token valido
* Esta en el header **Authorizartion: Bearer ELTOKEN**

**La ruta se proteje asi:**

	Route::get('/user', function () {
	    //
	})->middleware('auth:api');
	

##Scopes

Los scopes te permiten definir permisos que tiene un token para hacer acciones que puede hacer le user.

###Definir scopes
Para definir scopes, haces lo siguiente en el **AuthServiceProvider**

	Passport::tokensCan([
		//'Nombre-De-Scope'=>'Descripcion'
	    'place-orders' => 'Place orders',
	    'check-status' => 'Check order status',
	]);


###Solicitar un token con cierto scope

Cuando pedis un token, lo podes pedir con ciertos scopes, **el server determinara si te da acceso a esos scopes o no**.

        'client_id' => 'client-id',
        'redirect_uri' => 'http://example.com/callback',
        'response_type' => 'code',
        'scope' => 'place-orders check-status',
		
**Si asignas un personal token, lo podes entregar con cualquier scope:**

	$token = $user->createToken('My Token', ['place-orders'])->accessToken;




###Filtrar ruta por token scope
podes usar los middleware **CheckScopes** y **CheckForAnyScope**

	'scopes' => \Laravel\Passport\Http\Middleware\CheckScopes::class,
	'scope' => \Laravel\Passport\Http\Middleware\CheckForAnyScope::class,

* **scopes** - Determinar si tiene TODOS los scopes de una lista
* **scope** - Determinar si tiene AL MENOS UNO de los scopes de una lista

**Uso:**

	//Determinar si tiene TODOS los scopes de una lista
	Route::get('/orders', 'controller@accion'})
	->middleware('scopes:scope1,scope2');
	
	//Determinar si tiene AL MENOS UNO de los scopes de una lista
	Route::get('/orders', 'controller@accion'})
	->middleware('scope:scope1,scope2');


###Determinar si un token tiene un scope

Podes determinar si un token tiene un scope determinado en codigo asi:

	$request->user()->tokenCan('mi-scope')

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY4MTAwMzU3MV19
-->