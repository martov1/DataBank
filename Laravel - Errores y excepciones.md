



# Contenido


* Excepciones y errores
	* Logueo de errores
		* Errores ignorados:
	* Respuesta HTTP ante errores
	* Excepciones customizadas
	* Triggerear excepciones HTTP (ej 404)
	* Templates para excepciones HTTP
* Logging

# Excepciones y errores


Las excepciones se manejan y loguean desde la clase **App/Exceptions/Handler**

**La clase tiene dos metodos:**

* **report()** - loguea las excepciones o las envia a servicios de terceros (bugsnag, senry
* **render()** - Transforma las excepciones en respuestas HTTP para el browser


La clase tiene configuraciones en  `config/app.php` que determina cuanta informacion de la excepcion se muestra al usuario. La configuracion se guarda en **.env**

* Para **development** usar **APP_DEBUG** en **TRUE**

## Logueo de errores

El logueo de errores se maneja en la funcion **report()** de la clase **Handler**
```php
	public function report(Exception $exception)
	{
		//Si la excepcion es custom, hacer esto
	    if ($exception instanceof CustomException) {
	        //
	    }
		
	    return parent::report($exception);
	}
```

**Podes loguear una excepcion sin detener el request con Report():**
```php
	public function miFuncion($value)
	{
	    try {
	        // Validate the value...
	    } catch (Exception $e) {
	        report($e);
	
	        return false;
	    }
	}
```
### Errores ignorados:

Hay una lista de excepciones ignoradas en la variable **$dontReport**, podes añadir o substraer excepciones
```php
	protected $dontReport = [
	    \Illuminate\Auth\AuthenticationException::class,
	    \Illuminate\Auth\Access\AuthorizationException::class,
	    \Symfony\Component\HttpKernel\Exception\HttpException::class,
	    \Illuminate\Database\Eloquent\ModelNotFoundException::class,
	    \Illuminate\Validation\ValidationException::class,
	];
```
## Respuesta HTTP ante errores

El metodo **render()** se encarga de enviar una respuesta HTTP ante la aparicion de excepciones. si queres una **respuesta diferente a las respuestas default**, podes configurarlas en la funcion render()
```php
	public function render($request, Exception $exception)
	{
	    if ($exception instanceof CustomException) {
	        return response()->view('errors.custom', [], 500);
	    }
	
	    return parent::render($request, $exception);
	}
```
## Excepciones customizadas

Podes crear tus propias excepciones, estas pueden tener su propios metodos **report()** y **render()** o pueden usar los que estan en la clase **Handler**

```php
	namespace App\Exceptions;
	use Exception;
	
	class RenderException extends Exception
	{
	    public function report()
	    {
	    }
	
	    public function render($request)
	    {
	        return response(...);
	    }
	}
```
## Triggerear excepciones HTTP (ej 404)

Hay respuestas predefinidas que corresponden a HTTP codes, podes triggerearlas desde cualquier lugar de tu aplicacion asi
```php
	abort(404);
	abort(403, 'Unauthorized action.');
```

### Templates para excepciones HTTP

Podes crear tus templates para mostrarle al usuario en condiciones de excepcines HTTP solamente creando templates con el nombre del HTTP code

`resources/views/errors/404.blade.php`

```html
	<h2>{{ $exception->getMessage() }}</h2>
```
	
# Logging

la configuracion del sistema de logging se encuentra en **config/logging.php**, alli se indican los **logging channels:**

* Slack
* Text file
* Whatsapp
* Stack (una combinacion de otros channels)

## Channels

los channels son los receptores de los logs, pueden ser

* **Stack** - Una combinacion de varios channels
* **Single** - Un archivo o un path a un archivo
* **saily** - Un archivo por dia
* **slack** - El chat _slack_
* **syslog**
* **errorlog**
* **monolog**
* **custom**

Ejemplo de configuracion de channels en **config/logging.php**
```php
	'channels' => [
	    'stack' => [
	        'driver' => 'stack',
	        'channels' => ['syslog', 'slack'],
	    ],
	
	    'syslog' => [
	        'driver' => 'syslog',
	        'level' => 'debug',
	    ],
	
	    'slack' => [
	        'driver' => 'slack',
	        'url' => env('LOG_SLACK_WEBHOOK_URL'),
	        'username' => 'Laravel Log',
	        'emoji' => ':boom:',
	        'level' => 'critical',
	    ],
	],
```
## Log levels

Existen varios niveles de logs, dependiendo de la configuracion algunos levels van a un canal y otros a otro canal.

los niveles son: 
* emergency
* alert
* critical
*  error
*  warning
*  notice
*  info
*  ebug.

## Loguear informacion

**podes loguar algo en cualquier punto de la aplicacion asi:**
```php
	Log::emergency($message);
	Log::alert($message);
	Log::critical($message);
	Log::error($message);
	Log::warning($message);
	Log::notice($message);
	Log::info($message);
	Log::debug($message);
```

**Ademas podes agregar informacion adicional con un array de valores:**
```php
	Log::info('User failed to login.', ['id' => $user->id]);
```
**Podes especificar el canal para hacer un override del canal default:**
```php
	Log::channel('slack')->info('Something happened!');
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg3MjcwNDM5LC0xNTgyNTUzMTcyXX0=
-->