




# Contenido


* Intro
* Definir modelos
	* Definir tabla o primary key para un model
		* Primary keys que no son integers
	* Definir/configurar timestamps
	* Definir otra DB para un modelo
* Lectura de datos
* Creacion y edicion de datos
	* Por modificacion del modelo - SAVE()
	* Usando array como fuente de datos
		* Seguridad
		* Creacion de modelos usando arrays
		* Modificacion de modelos usando arrays
* Borrar datos
	* Hard delete
	* Soft delete
* Procesamiento de grandes volumenes
	* Por chunks
	* Usando cursores
* Query Scopes
	* Global scopes
		* En su propia clase 
		* Global scopes en closures 
		* Remover global scope
	* local scopes
* Eloquent API resources 


# Intro

En eloquent cada tabla tiene un **modelo** que es usado para interactuar conla tabla.

Cada **modelo actua como un query builder para una tabla o tablas**

# Definir modelos

Eloquent asume que
* Los **modelos** son singulares y la tabla sera **plural**
* Las tablas tienen 
	* una **columan ID**
	* Una columna **created_at**
	* Una columna **updated_at**





* **Para crear un modelo con artisan podes hacer:**

		php artisan make:model Flight

* **Si queres crear una migracion, haces:**

		php artisan make:model Flight --migration
	
* **Se ve asi:**
```php
		namespace App;
		use Illuminate\Database\Eloquent\Model;
		class Flight extends Model
		{
		    
		}
```
## Definir tabla o primary key para un model

Podes definir que un modelo **use una tabla especifica** o un **primary key especifico** asi
```php
		class Flight extends Model
		{	
		    protected $table = 'MiTabla';
			protected $primaryKey = 'miColumna'
		}
```
### Primary keys que no son integers

Si queres usar in ID que
* no es un **integer** 
* No **autoincrementa** 
 
podes especificarlo asi:
```php
		class Flight extends Model
		{	
			//No autoincrementa
		    protected $incrementing = false;
			//no es un int
			protected $keyType = 'string'
		}
```

## Definir/configurar timestamps

Por default laravel espera que en las tablas exista
* **created_at**
* **updated_at**

* Podes eliminar esta conducta asi:
	```php
		class Flight extends Model
		{
		    public $timestamps = false;
		}
	```
* Podes editar el formato de fechas asi
	```php
		class Flight extends Model
		{
		    protected $dateFormat = 'U';
		}
	```
* Podes indicar que las timestamps se guarden en otra columa asi
	```php
		class Flight extends Model
		{
		    const CREATED_AT = 'miColuma1';
		    const UPDATED_AT = 'miColuma2';
		}
	```
## Definir otra DB para un modelo

Podes determinar que u modelo usa una conexion a una DB determinada asi:
```php
	class Flight extends Model
	{
	    protected $connection = 'connection-name';
	}
```

# Lectura de datos

Aquellos metodos que sacan mas de un modelo usan **colecciones**, las colecciones **tienen muchos helper methods similares a LoDash**

* **BUSQUEDA:**
	* **MiModel::find(id)**
		* Busca el modelo por ID - **find(id)**
		* Busca varios modelos con IDS- **find([id1, id2, id3])**
	* **MiModel::where('active', 1)->first()**
		* Busca el modelo con un where, y trae el primero que devuelve la DB
	* **MiModel::where('active', 1)**
		* Devuelve una coleccion de modelos


* **BUSQUEDA O EXCEPCION:**
	* **MiModel::findOrFail(1);**
		* Busca el modelo por ID
		* Si no lo encuentra, triggerea una **excepcion HTTP 404**
	* **MiModel::where('legs', '>', 100)->firstOrFail();**
		* Busca el primer modelo resultante de una query
		* Si no encuentra ninguno, triggerea una **excepcion HTTP 404**


* **AGREGACION:**
	* **MiModel::where('active', 1)->count();**
		* Cuenta la cantidad de instancias que salen del query
	* **MiModel::::where('active', 1)->max('price');**
		* Determina la instancia de mayor valor 
	* **MiModel::::where('active', 1)->sum('price');**
		* Determina la suma de todas las instancias. 

# Creacion y edicion de datos

## Por modificacion del modelo - SAVE()

Podes instanciar un nuevo modelo o obtener un modelo de la base de datos y luego llamar a la funcion **save()**

* **save()**
	* Si instanciaste un modelo nuevo, lo **crea en la DB**
	* Si obtuviste una instancia de un modelo que existe en la DB, **lo actualiza** 



* **Modificacion de modelo existente:**
	* **Instancias** el modelo
	* Lo **poblas** con datos
	* usas la funcion **save()**
		* se actualizan automaticamente **created_at** y **updated_at**
			```php
				$flight = new Flight;
				$flight->name = $request->name;
				$flight->save();
			```


* **Creacion de un nuevo modelo:**
	* **Obtenes** la instancia del modelo a actualizar
	* **cambias** los datos
	* usas la funcion **save()**
		* se actualiza automaticamente **updated_at** 
			 ```php
				$flight = App\Flight::find(1);
				$flight->name = 'New Flight Name';
				$flight->save();
			```

## Usando array como fuente de datos

Podes usar un **array de key,value pairs para definir un modelo que crear o actualizar**

### Seguridad 

>Es impresciendible entonces que **los nombres y valores del array sean los que crees que son**, para que un **request malicioso** que es colocado directamente en una de estas funciones no pueda añadir arbitrariamente coas a todas las columnas de ese modelo.

**Permitir modificar todos los campos del modelo pasando un array es peligroso, entonces:**

Para Indicar que campos pueden modificarse (**whitelist**) o que campos prohibis modificar (**blacklist**).
```php
		//En el modelo
			//whitelist
			$fillable = ["columna1", "columna2"]
			//blacklist
			$guarded = ["columna1", "columna2"]
```
### Creacion de modelos usando arrays


* **create():**
	* Crea un modelo a partir de los datos de un array
		*  lo **guarda en DB**
			```php
				//Pueblo un array con los datos que quiero en la instancia del modelo
				$LoQueQuierCrear = [
				'columna1' => 'Flight 10',
				'columna2' => 'Flight aa' 
				]
				//lo creo y lo guardo en la DB
				$flight = MiModelo::create($LoQueQuierCrear);
			```
.
* **firstOrCreate()**
	* Intenta ubicar un modelo con los datos provistos
	* si no lo encuentra entonces crea uno nuevo con los datos del array
		* **lo guarda en DB**
			```php
				// buscar, si no existe, crearlo y guardarlo
				$AtributosDeBusqueda =  ['name' => 'Flight 10'], ['delayed' => 1]
				$flight = App\Flight::firstOrCreate($AtributosDeBusqueda);
			```	
.
* **firstOrNew()**
	* Intenta ubicar un modelo con los datos provistos  
	* si no lo encuentra entonces crea uno nuevo con los datos del array
		```php
			// buscar, si no existe, crearlo pero no guardarlo
			$AtributosDeBusqueda =  ['name' => 'Flight 10'], ['delayed' => 1]
			$flight = App\Flight::firstOrNew($AtributosDeBusqueda);
		```

### Modificacion de modelos usando arrays



* **fill():** 
	* Te permite actualizar los datos de un modelo usando un array 
		```php
			$loQueQuieroModificar = [
			'columna1' => 'Flight 10',
			'columna2' => 'Flight aa' 
			]
			$flight->fill($loQueQuieroModificar);
		```
.
* **update()**
	* Te permite actualizar una **coleccion de modelos** usando un array
		```php
			MiModel::where('active', 1)
			->update(['col1' => "unValor", col2=> 3]); 
		```	
			
* **updateOrCreate()**
	*  Intenta actualizar un modelo con ciertos datos, si no lo encuentra entonces
		* Crea uno nuevo 
		* lo guarda en la DB
				// If there's a flight from Oakland to San Diego, set the price to $99.
				// If no matching model exists, create one.
				$flight = App\Flight::updateOrCreate(
				    ['departure' => 'Oakland', 'destination' => 'San Diego'],
				    ['price' => 99]
				);
				


##Borrar datos 

###Hard delete
un Hard delete borra los modelos de la base de datos


* **Borrar modelos instanciandolos por ID:**
	
		//obtener un modelo y despues borrarlo
			$flight = App\Flight::find(id);
			$flight->delete();
* **Borrar modelos por IDsin instanciarlos:**
		//borrar modelos sin instanciarlos
			//un solo modelo
			App\Flight::destroy(id);
			//varios modelos
			App\Flight::destroy([id1, id2, id3]);
* **Borrar modelos por query o coleccion:**		
		$deletedRows = App\Flight::where('active', 0)->delete();

###Soft delete
Un soft delete no borra los modelos de la base de datos, solamente evita que puedan ser querieados por eloquent a menos que lo podas especificamente. ademas setea la columna **deleted_at** con la fecha en la que se borro

>Una vez que activas soft delete para un modelo, cada vez que borras una instancia de ese modelo se usa un soft delete

* **para usar soft delete:**
	* usar **Illuminate\Database\Eloquent\SoftDeletes** en el modelo
	* agregar "deleted_at" a la variable **$dates**


		namespace App;
		use Illuminate\Database\Eloquent\Model;
		use Illuminate\Database\Eloquent\SoftDeletes;
		
		class Flight extends Model
		{
		    use SoftDeletes;
		    protected $dates = ['deleted_at'];
		}
		
* **Para determinar si una instancia de modelo fue soft-deleted**
		$flight->trashed() //true si fue soft-deleted
		
* **obtener elementos que fueron soft-deleted**
		$flights = App\Flight::withTrashed()
		                ->where('account_id', 1)
		                ->get();
* **Obtener SOLO elementos soft-deleted**
		$flights = App\Flight::onlyTrashed()
		                ->where('airline_id', 1)
		                ->get();
* **Restaurar elementos soft-deleted**
		//restaurar un modelo
		$flight->restore();
		//restaurar varios modelos
		App\Flight::withTrashed()
				->where('airline_id', 1)
				->restore();
* **usar hard-delete en un modelo con soft-delete activado**
		$flight->forceDelete();


#Procesamiento de grandes volumenes


##Por chunks
Si tenes que procesar muchos records, podes usar la funcion **chunk()** que te permite computar un **closure** por partes para no saturar el server

	MiModelo::chunk(CantidadDeRecordsPorVez, functionProcesadora(){});
	
**Ej:**

	Flight::chunk(200, function ($flights) {
		//hacer cosas con los 200 records de cada tanda
	    foreach ($flights as $flight) {
	        //hacer cosas
	    }
	});
	
	
##Usando cursores

Podes usar un cursor que itera por la base de datos haciendo **un request a la vez**, esto te **evita tener que cargar todos los datos a la vez**

	foreach (Flight::where('foo', 'bar')->cursor() as $flight) {
	    //Hacer cosas con cada record
	}

#Query Scopes

Los scopes te permiten agregar limitaciones a las querys de un modelo. Por ejemplo los elementos soft-deleted tienen un query scope para no ser encontrados por las querys de todos los modelos.

##Global scopes

###En su propia clase
Las global scopes **limitan a todos los querys de un modelo en particular**.

Utilizan la **intefrace Illuminate\Database\Eloquent\Scope** que requiere la implementacion de la funcion **apply()**

Para usarla necesitas definir el global scope en la **funcion boot()** del **modelo**

* **Definir global scope:**

		namespace App\Scopes;
		use Illuminate\Database\Eloquent\Scope;
		use Illuminate\Database\Eloquent\Model;
		use Illuminate\Database\Eloquent\Builder;
		
		class AgeScope implements Scope
		{
		    
		    public function apply(Builder $builder, Model $model)
		    {
				//Aca le añadis constrains a lo que seria el resultado normal del
				//Modelo
		        $builder->where('age', '>', 200);
		    }
		}
	
	
* **Usar global scope en un model:**

		use App\Scopes\AgeScope;
		use Illuminate\Database\Eloquent\Model;
		class User extends Model
		{
			protected static function boot()
			{
				parent::boot();
				static::addGlobalScope(new AgeScope);
			}
		}
		
###Global scope en closure

Podes añadir un global scope como un closure en un modelo en particular


	class User extends Model
	{
	    protected static function boot()
	    {
	        parent::boot();
	        static::addGlobalScope('age', function (Builder $builder) {
	            $builder->where('age', '>', 200);
	        });
	    }
	}
	
###Remover global scope

Para remover un global scope para un query, podes:

* **Remover un solo closure asi:**
		User::withoutGlobalScope(MiScope::class)->get();
	
*  **si el scope es un closure**
		User::withoutGlobalScope('MiScope')->get();

* **Remover todos los scopes**
		User::withoutGlobalScopes()->get();

* **Remover algunos de los global scopes:**
		User::withoutGlobalScopes([
		    PrimerScope::class, SegundoScope::class
		])->get();
		
##Local scopes

Los local scopes te permiten definir limitaciones que puedas usar libremente en tu aplicacion sin forzar a los modelos a usarla.

>los scopes 
>*	deben llamarse **scopeNombre** 
>*	son usados por eloquent como **modelo()->Nombre**
>*  Pueden usar **parametros adicionales**



* **Los definis como funciones dentro del scope:**

		class User extends Model
		{
			public function scopePopular($query)
			{
				return $query->where('votes', '>', 100);
			}

			public function scopeActive($query, $algunparametro)
			{
				return $query->where('$algunparametro', 1);
			}
		}
		
* **Los usas asi:**

		$users = App\User::popular()->active('MiParametro')
		->orderBy('created_at')->get();



#Eloquent API resources

Son una manera de **expresar un modelo** de eloquent en una **respuesta JSON**.
Fuenciona como un **template** para el modelo.
Tambien te permite **combinar modelos**
	
	//Devuelve una coleccion de modelos
	php artisan make:resource Users --collection
	//devuelve un modelo
	php artisan make:resource UserCollection


>Podes generar una coleccion ad-hoc asi
>UserResource::collection(User::all());

**Uso en el controller:**

	return new MiModelResource($MiModel)
	//Devuelve un JSON del modelo
	
**Configuracion del resource:**
En **http/resource/MiModelResource**

	use Illuminate\Http\Resources\Json\JsonResource;
	class User extends JsonResource
	{
		//Esta funcion devuelve un array que indica la estructura del JSON
	    public function toArray($request)
	    {
	        return [
	            'id' => $this->id,
	            'name' => $this->name,
	            'email' => $this->email,
				'posts' => PostResource::collection($this->posts),
	            'created_at' => $this->created_at,
	            'updated_at' => $this->updated_at,
	        ];
	    }
		
	}
		
		
##Condicionales

Podes enviar cosas usando condicionales

* **un condicional:**
		public function toArray($request)
		{
		    return [
		        'id' => $this->id,
		        'name' => $this->name,
		        'email' => $this->email,
		        'secret' => $this->when(Auth::user()->isAdmin(), 'secret-value'),
		        'created_at' => $this->created_at,
		        'updated_at' => $this->updated_at,
		    ];
		}
* **varios condicionales:**

	public function toArray($request)
	{
	    return [
	        'id' => $this->id,
	        'name' => $this->name,
	        'email' => $this->email,
	        $this->mergeWhen(Auth::user()->isAdmin(), [
	            'first-secret' => 'value',
	            'second-secret' => 'value',
	        ]),
	        'created_at' => $this->created_at,
	        'updated_at' => $this->updated_at,
	    ];
	}
	
##Modificar la HTTP response del resource

	new UserResource(User::find(1)))
	                ->response()
	                ->header('X-Value', 'True');
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTI2MDYwOTE3XX0=
-->