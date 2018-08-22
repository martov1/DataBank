
**falta**
- [ ] [Validating Arrays](https://laravel.com/docs/5.6/validation#validating-arrays)
- [ ] [Custom Validation Rules](https://laravel.com/docs/5.6/validation#custom-validation-rules)




# Contenido


* Acceder al request desde un controller
* Acceder desde una ruta
* Metodos del request object
	* Obtener el URL del request
	* Obtener el HTTP verb del request
	* Datos del request payload y query string
	* Datos del query string
	* Datos de un form
	* Datos en JSON
	* Obtener algunos datos del request
	* Determinar si un dato esta presente
	* Obtener cookies
	* Obtener archivos
	* Verificar archivo subido
	* Determinar extension
	* Guardar archivos subidos
* Validacion 
	* Validate() y uso basico de validadores
		*  Campos opcionales
		* Manejo de errores
	* Form requests - Validacion avanzada
		* Filtrar campos sin reglas de validacion 
		* Verificar autorizacion
		* Acceder al validador
		* Customizar mensajes de error
	* Trabajar con mensajes de error
	* Reglas de validacion
	* Validacion condicional
		* Validar solo si el campo esta presente
		* Validar de acuerdo a cierta logica



# Acceder al request desde un controller


Podes acceder al request desde un controller inyectandolo con DI. **esto no te impide acceder a los parametros del path**

```php
	namespace App\Http\Controllers;
	use Illuminate\Http\Request;	//Inyectar request
	
	class MiController extends Controller
	{
		//Inyectar request en este metodo, ademas inyectas el parametro
		//id que esta en el path
	    public function guardar(Request $request, $id)
	    {
			//Usas request como te parezca
	        $name = $request->input('name');
	    }
	}
```
	
# Acceder desde una ruta

Podes acceder desde una ruta directamente, tambien usando DI
```php
	use Illuminate\Http\Request;
	
	Route::get('/', function (Request $request) {
	    //
	});
```
	
# Metodos del request object

## Obtener el URL del request
* **Path()**
Podes obtener el path del request **sin el dominio**
	```php
		$uri = $request->path();	// el/path
	```

* **is()**
Te permite hacer un chequeo para ver si estas en un path determinado
	```php
		if ($request->is('admin/*')) {
		    //
		}
	```
* **url()**
Obtiene la URL  **con el dominio** pero sin el query string
	```php
		$url = $request->url(); // www.hola.com/el/path
	```
* **fullUrl()**
Obtiene la URL con el dominio y el query string
	```php
		$url = $request->url(); // www.hola.com/el/?query=lala
	```
## Obtener el HTTP verb del request

Podes obttener el http verb del request asi
```php
	$method = $request->method();
```
Podes comprobar si es un metodo en particular asi
```php
	if ($request->isMethod('post')) {
	    //
	}
```
## Datos del request payload y query string

* **all()**
Devuelve un array con todos los datos del request
	```php
		$input = $request->all();
	```
* **input('dato')**
Devuelve uno de los datos del request, acepta un default en caso de que el dato no exista
	```php
		$name = $request->input('name', 'default opcional');
	```
## Datos del query string


* Podes pedir un **valor del query** string usando
	```php
		$name = $request->query('name');
	```
* Podes colocar un** valor default** en caso de que no exista el query string
	```php
		$name = $request->query('name');
	```
* Podes obtener **todos los query strings** asi
	```php
		$query = $request->query();
	```
## Datos de un form

Podes acceder a un valor de un form con nombre "unNombre" asi:
```php
	$name = $request->unNombre;
```
## Datos en JSON

Si el request tiene datos en JSON podes accederlos de la siguiente manera siempre y cuando el header **Content-type: aplication/json** este presente

**Objeto enviado en el request:**
```php
	{
		child{
			grandchild:"El valor que quier"
		}
	}
```
**accedes asi:**
```php
	$name = $request->input('objeto.child.grandchild');
```
## Obtener algunos datos del request

Podes obtener los datos **que coincidan** con los nombres de un array o aquellos que **no coincidan**. 

```php
	//obtener SOLO username y password
	$input = $request->only('username', 'password');
	// Obtener todo salvo la tarjeta de credito
	$input = $request->except(['credit_card']);
```
> el metodo **only()** no devuelve aquellos datos que no existan en el request.

## Determinar si un dato esta presente

* **Determinar si un dato esta presente y no esta vacio**
	```php
		if ($request->filled('name')) {
		    //
		}
	```
* **Determinar si un dato esta presente** en un request asi.
	```php
		if ($request->has('dato que me interesa')) {
		    //Si esta presente, corre esto
		}
	```
*  **Determinar siuna serie de datos esta presente**
```php
		if ($request->has(['name', 'email'])) {
		    //Si estan presentes, corre esto
		}
```
## Obtener cookies

Podes obtener cookies asi;:
```php
	$value = $request->cookie('nombre de cookie');
```
## Obtener archivos

* Podes obtener los archivos adjuntos en un request asi:
	```php
		//Devuelve una instancia de la clase UploadedFile
		$file = $request->file('photo');
		
		$file = $request->photo;
	```
* Podes determinar si existe un archivo adjunto asi
	```php
		if ($request->hasFile('photo')) {
		    //
		}
	```
### Verificar archivo subido

Podes determinar si el upload fue exitoso asi;
```php
	if ($request->file('photo')->isValid()) {
	    //
	}
```
### Determinar extension

Podes determinar la extension de un archivo a partir de su contenido usando el metodo **extension()**  de la clase UploadedFile.

```php
	$extension = $request->photo->extension();
```
### Guardar archivos subidos

Podes guardar el archivo en un **filesystem** configurado (**una carpeta local, amazon storage, etc**) usando el metodo **store()** de la clase **UploadedFile**

* **Store('ubicacion')** - te permite guardar un archivo con un nombre automatico
	* Acepta un segundo argumento para un **disco o filesystem especifico**
		```php
			//Guardar en la carpeta images del filesystem configurado
			//Devuelve el path donde se guardo
			$path = $request->photo->store('images');
			//Guardar en el disco configuado como "s3" (AWS)
			$path = $request->photo->store('images', 's3');
		```
	
* **storeAs('ubicacion','nombre')** -  te permite guardar un archivo con un **nombre determiado**
	```php
		//Guardar en la carpeta images del filesystem configurado
		$path = $request->photo->storeAs('images', 'filename.jpg');
		//Guardar en el disco configuado como "s3" (AWS)
		$path = $request->photo->storeAs('images', 'filename.jpg', 's3');
	```

# Validacion

>Todos los procesos de validacion forman **validadores**. los metodos para crear validadores y usarlos son:
>* `$request->validate([reglas])` - Crea un validador con las reglas del array y valida el request
>* `Form Requests` - Es una clase que contiene las reglas, genera un validador y valida el request
>* `Validator::make(loQueValidas,Reglas)` - Crea un validador


## Validate() y uso basico de validadores
El Request object tiene una funcion **$request->validate()** que permite validar los datos recibidos en el request
```php
    $validatedData = $request->validate([
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
	    'author.name' => 'required'
    ]);
```
* Las reglas son validadas en el orden en el que estan escritas
* La presencia de la regla **bail** detiene la validacion ante el primer error encontrado despues de su aparicion.
* Podes ubicar elementos anidados usando la notacion **father.child.grandChild**

### Campos opcionales

Para aceptar un campo opcional necesitas colocarlo como **nullable** para permitir que pueda contener un valor null, caso contrario sera validado con el resto de los validadores.
```php
	$request->validate([
	    'publish_at' => 'nullable|date',
	]);
```


### Manejo de errores

Ante un error, laravel automaticamente:
* Triggerea un **redirect** o una **respuesta Json**
* Guarda el error en   **memoria de flash session** por si lo queres usar en blade
	* Aparece en blade como $errors
	* Esta alimentado por el middleware **ShareErrorsFromSession** 

## Form requests - Validacion avanzada

Para procesos de validacion mas complejos podes corear una clase separada llamada **Form request**, por default va en **app/Http/Requests** y se puede crear con el comando:

	php artisan make:request MiRequest
	

**Se ve asi:**
```php
	//MiRequest
	public function rules()
	{
	    return [
	        'title' => 'required|unique:posts|max:255',
	        'body' => 'required',
	    ];
	}
```
Una vez que hiciste eso, podes validar simplemente indicando que el request es de type MiRequest (mi clase validadora).
```php
	public function store(StoreBlogPost $request)
	{
	    // The incoming request is valid...
	
	    // Retrieve the validated input data...
	    $validated = $request->validated();
	}
```
### filtrar campos sin reglas de validacion

Para filtrar todo campo que **no haya sido validado** podes hacer esto
```php
$SoloCamposValidados= $request->validated()
```
### Verificar autorizacion

El form request tiene una funcion en su interfaz destiada a **verificar si el usuario esta autorizado** a realizar una accion. **debe devolver un boolean**
```php
	//Devuelve true para autorizar, si no HTTP 403
	public function authorize()
	{
	    //acciones de verificacion
		$comment = Comment::find($this->route('comment'));
    	return $comment && $this->user()->can('update', $comment);
	}
```
	
### Acceder al validador

Podes acceder al validador generado por el form request definiendo una funcion **withValidator()** dentro del form request. recibis el validador **antes de que sea usado para validar el request** y podes **mutarlo (no hace falta devolver nada)** 
```php
	//Hacer cosas con el validador
	public function withValidator($validator)
	{
		//Hacer cosas despues de que el valodador termine de validar
	    $validator->after(function ($validator) {
	        	//cosas
	    });
		//realizar acciones si falla
		 if ($validator->fails()) {
			//cosas
        }
	}
```

	
### Customizar mensajes de error

Podes customizar los mensajes que son devueltos en caso de un error de validacion definiendo la funcion **messages()**
```php
	public function messages()
	{
	    return [
	        'title.required' => 'A title is required',
	        'body.required'  => 'A message is required',
	    ];
	}
```

### Validadores custom locales

Podes tener validadores creados directamente en el form request para validar algo puntual

```php
use Illuminate\Validation\Factory as ValidationFactory;

class UpdateMyUserRequest extends FormRequest {

    public function __construct(ValidationFactory $validationFactory)
    {

        $validationFactory->extend(
            'foo',
            function ($attribute, $value, $parameters) {
                return 'foo' === $value;
            },
            'Sorry, it failed foo validation!'
        );

    }

    public function rules()
    {
        return [
            'username' => 'foo',
        ];
    }
}
```
## Trabajar con mensajes de error

* **El primer mensaje de error de un campo** (cada rule genera un error distinto para el mismo campo) se puede obtener asi:
	```php
		$validator->errors();
		echo $errors->first('email');
	```
* **Obtener todos los mensajes para un campo:**
	```php
		foreach ($errors->get('email') as $message) {
		    //
		}
	```
* **Obtener todos los mensajes de error:**
	```php
		foreach ($errors->all() as $message) {
		    //
		}
	```
* **Ver su existe un mensaje de error**
	```php
		if ($errors->has('email')) {
		    //
		}
	```		
## Reglas de validacion

* **bail** - Detener validacion ante el primer error


* Comparacion con base de datos
	* **unique:table,column,except,idColumn** - El field es unico en una tabla
	* **exists:TABLE,COLUMN** - El field existe en la DB en la tabla y columna especificadas


* Fechas
	* **after:DATE** - El field es una fecha posterior del valor DATE 
	* **after_or_equal:DATE** - El field es una fecha posterior o igual al valor DATE 
	* **before:DATE** - El field es una fecha anterior al valor DATE
	* **before_or_equal:DATE** - El field es una fecha anterior o igual al valor DATE 
	* **date_equals:DATE** - El field es una fecha igual al valor DATE
	* **date_format:FORMAT** - El field tiene el formato FORMAT


* Patrones
	* **email** - el field es un email
	* **ip** - El field es una direccion IP
	* **ipv4**
	* **ipv6**
	* **active_url** - el field es una URL con un DNS record valido (lo verifica usando dns_get_record


* Requerido / existencia
	* **present** - El field existe en el request, aunque este vacio
	* **filled** - El filed (si existe) no puede estar vacio.
	* **nullable** - El field puede ser NULL
	* **required** - El field esta presente y no esta vacio (null, string vacio, array vacio, uploaded file sin path)
	* **required_if:OTROFIELD,VALOR** - El campo es requerido si otro campo es igual a un valor
	* **required_unless:OTROFIELD,VALOR** - El campo es requerido salvo que otro campo sea igual a un valor
	* **required_with: FIELD1, FIELD2..** - El campo es requerido si alguno de los campos listados estan presentes
	* **required_with_all: FIELD1, FIELD2..** - El campo es requerido si TODOS los campos listados estan presentes
	* **required_without: FIELD1, FIELD2..** - El campo es requerido si alguno de los campos listados NO estan presentes
	* **required_without_ALL: FIELD1, FIELD2..**- El campo es requerido si TODOS los campos listados NO estan presentes


 * Valores
	* **accepted** - El field es 1, "yes" o "true"
	* **alpha** - El field es unicamente caracteres alfabeticos
	* **alpha_dash** - El field es alfabetico u dashes/underscores
	* **alpha_num** - El field el aflanumerico
	* **confirmed** - el valor es blabla_confirmation
	* **distinct** - El array no puede tener valores duplicados
	* numericos
		* **digits:N** - El field es numerico y tiene exactamente N caracteres
		* **digits_between:MIN,MAX** - El field es unmerico y tiene entre MIN y MAX caracteres
		* **between:MIN,MAX** - El field es un numero entre MIN y MAX
	* Comparacion con otro valor
		* **in:foo,bar,..** - El valor esta en esta lista de valores
		* **in_array:anotherfield** - el valor esta en un array de valores
		* **not_in:foo,bar,...** - El field no esta en esta lista de valores
		* **not_regex:REGULAREXP** - El field no devuelve true al pasar por al REGULAREXP
		* **regex:pattern** -  El field devuelve true al pasar por al REGULAREXP
		* **different:VALOR** - El valor es diferent a VALOR



*  files
	* **dimensions** - el archivo es una imagen con las dimensiones especificadas
	_dimensions:min_width=100,min_height=200_
	_dimensions:ratio=3/2_
	* **file** - el campo debe ser un archivo exitosamente uploadeado
	* **image** - El archivo es una imagen
	* **mimetypes:text/plain,...** - El field debe ser de este MIME type
	* **mimes:jpeg,bmp** - El field debe ser del MIME type de estas extensiones


 * Types
 	* **json** - El field es un string Json
	* **integer** - El field es un int
	* **boolean** - El field se puede castear como boolean (false, true, 1,0,"1","0")
	* **array** - El field es un PHP array
	* **date** - El valor es una fecha valida acording to strtotime()
	* **numeric** - El field es numerico
	* **string** - El field es un string
	* **timezone** - El field es un timezone

 
* comprobacion de tamaño
_Estos comparadores usan **PHP size()** para determinar el tamaño de algo _
	* **min:VALOR** - El field debe tener un size mayor a VALOR
	* **max:VALOR** - El field debe tener un size menor a VALOR
	* **size:VALOR** - El field debe tener un size igual a VALOR
 
* Comparacion de tamaño
_Estos comparadores comparan un objeto dado con el FIELD usando PHP size().
El objeto dado debe ser del mismo type que el FIELD_
	* **gt:COMPARADO** - El tamaño del field (array, string, numero, archivo, etc) sera comparado con un elemento del mismo tipo indicado en COMPARADO
	* **gte:COMPARADO** - Igual al anterior, pero mayor o igual
	* **lt:VALOR** - Igual al gt pero menor
	* **lte:VALOR** - Igual a gte pero menor o igual

## Validacion condicional

### Validar solo si el campo esta presente

Con **sometimes** podes valida un campo unicamente si esta presente
```php
	    'email' => 'sometimes|required|email',
```

### Validar de acuerdo a cierta logica

Una vez que tenes el validador podes añadirle una logica para validar.


* Validar el campo "reason" con los validadores `'required|max:500'` solo si el campo games es mayor o igual a 100.
	```php
		$validator->sometimes('campoAValidar', 'Validadores', function ($input) {
		    //Si devolves TRUE, campoAValidar sera validado con los Validadores
		});
	```
	EJ:
	```php
		$v->sometimes('reason', 'required|max:500', function ($input) {
		    return $input->games >= 100;
		});
	```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMTc3OTM3NjYsLTE4ODA1NjgwMzJdfQ
==
-->