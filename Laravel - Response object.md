


# Content

* Responses simples
* Response object instances
	* Añadir HTTP headers
	* Añadir cookies
	* Añadir cookies desencriptadas
* Redirects
* Responses con views
* Responses con JSON
* File downloads
* File responses





# Responses simples

Son aquellas donde no devolves un response object, sino que **laravel se encarga de generar un response en base a datos simples**

**Laravel automaticamente convierte:**
* Los **strings** en HTTP responses 
	```php
		Route::get('/', function () {
		    return 'Hello World';
		});
	```
* Los **arrays** en HTTP responses con un **JSON** payload
	```php
		Route::get('/', function () {
		    return [1, 2, 3];
		});
	```
* Las **Colecciones** de eloquent en HTTP responses con un **JSON** payload

# Response object instances



El response object te da gran control sobre la respuesta HTTP generada por laravel, tales como

* **headers**
* **HTTP status codes**

```php
	Route::get('home', function () {
	    return response('Hello World', 200)
	                  ->header('Content-Type', 'text/plain');
	});
```
## Añadir HTTP headers

Podes añadir HTTP headers asi

```php
	return response($content)
	            ->header('Content-Type', $type)
	            ->header('X-Header-One', 'Header Value')
	            ->header('X-Header-Two', 'Header Value');
```	

## Añadir cookies 

Por default **las cookies estan ecriptadas**

Podes añadir cookies con el metodo **cookie()**
```php
	->cookie($name, $value, $minutes, $path, $domain, $secure, $httpOnly)
```
Ej de uso:
```php
	return response($content)
	                ->cookie('name', 'value', $minutes);
```
## Añadir cookies desencriptadas

Por default las cookies estan encriptadas, podes añadir cookies en plain text colocando las excepciones en el **EnriptCookie** middleware localizado en `app/Http/Middleware`


En el **EncriptCookie middleware**
```php
	//Cookies que se deben enviar en plain text
	protected $except = [
	    'cookie_name',
	]; 
```

# Redirects

* Podes enviar un response que **redireccione a otra ruta**
	```php
		redirect('home/dashboard');
	```
* Enviar a la persona a la **pagina anterior** (requiere sesiones)
	```php
		//Enviar al usuario atras
		 return back()
		 //Enviar al usuario atras y poblar el form automaticamente
		 return back()->withInput();
	```
* Redireccionar a un **named route**
	```php
		//sin parametros
		return redirect()->route('login');
		//Con parametros
		return redirect()->route('profile', ['id' => 1]);
		//con parametros cargados con eloquent
		return redirect()->route('profile', [$user]);
	```
* Redirigir a un **Controller**
	```php
		//Sin parametros
		return redirect()->action('HomeController@index');
		//Con parametros
		return redirect()->action(
		    'UserController@profile', ['id' => 1]
		);
	```	
* Redirigir a **otro dominio**
	```php
		return redirect()->away('https://www.google.com');
	```
* Redirigir con **datos en flash session**
	```php
	    return redirect('dashboard')->with('status', 'Profile updated!');
	```
# Responses con views

* Podes enviar un response con un view usando la funcion **view()**
	```php
		  return view('user.profile', ['user' => User::findOrFail($id)]);
	```
* Podes generar un response con un view **teniendo control granular de la respuesta** asi asi
	```php
		return response()
		            ->view('hello', $data, 200)
		            ->header('Content-Type', $type);
	```
# Responses con JSON

Podes colocar automaticamente el header **content-type:aplication/json** y encodear data con Json asi:
```php
	return response()->json([
	    'name' => 'Abigail',
	    'state' => 'CA'
	]);
```
# File downloads

Es una respuesta que triggerea que el browser quiera descargar un archivo

Laravel guarda los archivos con un ID si se usa la funcion **store()**, pero se puede colocar un nombre human-friendly para el usuario usando el segundo parametro de **download()**
```php
	//Descargar archivo como esta
	return response()->download($pathToFile);
	//Descargar archivo colocandole un nombre y headers a la respuesta
	return response()->download($pathToFile, $nameForHumans, $headers);
	//Borrar el archivo una vez descargado
	return response()->download($pathToFile)->deleteFileAfterSend(true);
```
# File responses

Permiten que el usuario **visualice algo (PDF, JPG, etc) en el browser sin triggerear una descarga**
```php
	return response()->file($pathToFile);
	
	return response()->file($pathToFile, $headers);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU4ODQ4NzY4XX0=
-->