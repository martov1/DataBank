
# Contenido


* Intro
* Jobs
	* Anatomia de un job
	* Jobs y serializacion
	* Retrasar jobs
	* Job chaining
	* Agrupar jobs en diferentes queues
	* Enviar un job a un connection en particular
	* Retries y errores en un job
		* Retries
		* Errores
		* Failed jobs
	* Memory leaks
* queues
	* Database driver
	* Correr queues desde artisan
	* Priorizar queues
	* Reiniciar queue workers




# Intro

* **Los jobs** son aquellas operaciones que se pueden colocar en un **queue** para realizarse en otro momento.
* **Los queues** son listas de jobs que se deben realizar de manera asincronica
	* Los jobs en diferentes queues pueden tener:
		* Diferente prioridad de procesamiento
		* Procesarse en fechas/intervalos distintos
	* Podes tener todos los jobs en un solo queue sin nombre
	* Podes tener jobs de un queue con diferentes conexiones 
* **Los connections** son el lugar donde se guardan las listas de jobs
	* DB
	* redis
	* sqlite
	* AWS 





# Jobs


Los **jobs** son aquellas operaciones que se pueden colocar en un **queue** para realizarse en otro momento.

**Podes crear un job asi:**
	
	php artisan make:job MiJob
	
	
**En general se ve asi:**
```php
	//MiJob
	public function __construct(cosaNecesaria $cosa){
		$this->$cosa
	}
	
	public function handle(){
	
	//Haces tus cosas
	
	}
```
**Podes pedir que el job sea ralizado asicronicamente en un request asi:**
```php
	//Un controller
	$this->dispatch(new miJob($cosa))
	//a un queue especifico
	MiJob::dispatch()->onQueue('emails');
```

## Anatomia de un job

Los jobs tienen una interfaz que los obliga a tener dos metodos
* **handle()**
	* Contiene la logica del job, osea lo que queres hacer.
	* Acepta dependency inyection
* **__construct($param1, $param2...)**
Es el contructor, levanta los **parametros que son enviados al job cuando es agregado al queue** ej: `Job::dispatch()->onQueue('param1, param2');`

## Jobs y serializacion

Como las variables que le pasas a un job en un request tienen que ser **guardadas en la base de datos** entonces tenes que **serializarlas (pasarlos a strings)**.

**Los modelos de eloquent se serializan solos.**
	
## Retrasar jobs

Podes retrasar un job por un tiempo determinado usando **delay**
```php
        ProcessPodcast::dispatch($podcast)
                ->delay(now()->addMinutes(10));
```

## Job chaining

Te permite especificar una lista de jobs que deben hacerse de forma secuencial **uno despues de otro**
```php
	ProcessPodcast::withChain([
	    new OptimizePodcast,
	    new ReleasePodcast
	])->dispatch();
```

**Si queres especificar la conexion o el queue de todos los jobs:**

	ProcessPodcast::withChain([
	    new OptimizePodcast,
	    new ReleasePodcast
	])->dispatch()->allOnConnection('redis')->allOnQueue('podcasts');

## Agrupar jobs en diferentes queues

Podes indicar que un job _pertenece_ a un queue en particular como **una forma de agrupar los jobs de manera logica**.
Podes indicar a que queue va un job asi:
```php
	ProcessPodcast::dispatch($podcast)->onQueue('processing');
```




## Enviar un job a un connection en particular
Podes especificar a que connection va un job asi
```php
        ProcessPodcast::dispatch($podcast)->onConnection('sqs');
```
## Retries y errores en un job

### Retries
* **Si queres que un job tenga un numero maximo de retries, podes:**
```php
		class MiJob implements ShouldQueue
		{
		    public $tries = 5;
		}
```	

* **podes indicar hasta que momento se puede reintentar el job**
```php	
	public function retryUntil()
		{
		    return now()->addSeconds(5);
		}
```
* **Podes indicar cuanto tiempo puede tomar el job en realizarse antes de matar el proceso:**
```php
    	public $timeout = 120;
```
### Errores

Si ocurre un error, el **job se deja en el queue para ser reintentado mas tarde**.
Si colocaste un **numero maximo de retries** entonces el job sera **borrado del queue despues de ese numero de retiries**



### Failed jobs
Cuando un job no puede realizarse y se le acaban la cantidad de retires, podes ejecutar una pieza de logica para:
* limpiar lo que el job dejo atras
* alertar al usuario o a un admin
* loguear lo sucedido, etc


**Podes indicar la logica a correr definidiendo una funcion failed() en el job:**
```php
		public function failed(Exception $exception)
		{
			// Send user notification of failure, etc...
		}
```
## Memory leaks

Los queue workers no liberan la memoria entre jobs, por lo que tenes que liberar la memoria manualmente, por ejemplo con **imagedestroy()** y **unset()**




# queues

 Los queues son las listas donde se guardan los jobs que se deben realizar. 
Cada job despachado se agrega a un queue, dependiendo del driver configurado, los jobs de un queue se guardan en **una base de datos, redis, sqlite, etc**

* La configuracion de queues esta en **config/queue.php**
* Podes crear multiples queues, aunque usen la misma _conexion_, osea la misma _DB_

## Database driver

Podes pasar estos comandos para que artisan genere una tabla para colocar los jobs y la use con el driver **_database_**

	php artisan queue:table
	
	php artisan migrate
	
## Correr queues desde artisan

* **podes correr los jobs de TODOS los queues asi:**

		php artisan queue:work 
		
* **podes correr los jobs de UN queue asi:**	

		php artisan queue:work --queue=emails


* **Podes correr los jobs con un maximo numero de retries asi:**

		php artisan queue:work --tries=3
		php artisan queue:work --timeout=30
		
* **Podes correr el primer job del queue asi:**

		php artisan queue:work --once
* **Podes indicar que connection y que queue puntual correr asi**

		php artisan queue:work redis --queue=emails

## Priorizar queues

Podes priorizar un queue sobre otro con el orden que le des en el artisan command

		php artisan queue:work --queue=primerQueue,segundoQueue

## Reiniciar queue workers

Los queue workers son procesos que pueden quedar activos mucho tiempo con una copia de la aplicacion en memoria. **si cambias algo en la app deberias reiniciarlos para que tomen los cambios**.

	php artisan queue:restart

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjYyMTQ0MjU2LC0xNjM4NzUwMDUwXX0=
-->