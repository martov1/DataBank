






**me quede en:**
Querying Relations
https://laravel.com/docs/5.6/eloquent-relationships#querying-relations



# Contenido

* Tipos de relaciones
* Declaracion de relaciones
* One to one
	* Declaracion y uso
	* Definir la inversa de la relacion
	* Uso de tablas o keys no default
* One to many
	* Declaracion y uso
	* Definir la inversa de la relacion
	* Uso de tablas o keys no default
* Many to many
	* Declaracion y uso:
	* Uso de tablas o keys no default
	* Leer datos de la tabla pivot
	* Extender el modelo pivot
	* Nombrar el modelo pivot
	* Filtrar usando el modelo pivot
	* Definit un modelo pivot custom
* Has Many Through
	* Declaracion y uso:
 	* Uso de tablas o keys no default
* Relaciones polimorficas
	* Declaracion y uso
* Relaciones polimorficas many-to-many
	* Declaracion
	* Uso
* Hacer querys con las relaciones
* Guardar/crear modelos con relaciones
	* One-to-one / one-to-many / many-to-many
		* Desde un modelo
		* Desde un array
	* One-to-one Inverse / one-to-many inverse
	* Many-to-many
		* Sincronizar relaciones many-to-many
		* Guardar dato en tabla pivot
		* Actualizar timestamp del parent model
* Verificar existencia de una relacion
* Contar la cantidad de relaciones
	* N° de relaciones
	* N° de relaciones que cumplen una condicion
* Precargar relacion - Eager loading


	






# Tipos de relaciones


Elocuent es capaz de varios tipos de relaciones entre modelos

* **One to one**
	* Un usuario $U$ tiene un DNI $D$
	* .$U_1 \Rightarrow D_1$


* **One to many**
	* Un usuario $U$ tiene muchas tarjetas de credito $C$
	* .$U_1 \Rightarrow \{C_1,C_2,C_3\}$


* **Many to Many**
	* Muchos post $P$ comparten muchos tags $T$
	* .$\{P_1,P_2P_3\} \iff \{T_1,T_2,T_3\}$


* **Has many Through**
	* Muchos posts $P$ fueron creados por usuarios $U$ del mismo Pais $C$
	* .$C_1 \Rightarrow \{U_1,U_2,U_3\}\Rightarrow \{P_1,P_2,P_3\}  $


* **Relaciones polimorficas**
	* Un comentario $C$ puede ser de UN video $V$ o de UNA foto$P$
	* .$C_1 \Rightarrow V_1 \quad \text{OR} \quad C_1 \Rightarrow P_1$  


* **Relaciones polimorficas Many to Many**
	* Varios  tags $T$ pueden ser de VARIOS videos $V$ Y de VARIAS fotos $P$
	* .$T_1,T_2,T_3 \iff V_1,V_2,V_3 \quad \text{and} \quad T_1,T_2,T_3 \iff P_1,P_2P_3$  

# Declaracion de relaciones

>Las relaciones simepre se declaran en el modelo usando una **funcion relacion** que devuelve el **mismo modelo pero añadiendole la relacion** usando un metodo de eloquent.
> EJ
```php
class User extends Model
{
	//Funcion relacion
	public function phone()
    {
		//Devolucion del modelo con relacion añadida
        return $this->hasOne('App\Phone');
    }
}
```


# One to one

## Declaracion y uso


La relacion $U_1 \Rightarrow D_1$ es definida por `$this->hasOne('App\Phone')`

* **Si queres una functional dependency la definis en el modelo asi:**
	```php
		class User extends Model
		{
			//Colocas un nombre de funcion que haga referencia al modelo asociado
			public function phone()
		    {
				//Indicas a eloquent que el modelo users tiene una relacion one-to-one
				// con el modelo phone
		        return $this->hasOne('App\Phone');
		    }
		}
	```
	
* **Al declarar esta relacion, eloquent ASUME QUE:**
	* La tabla **users** tiene una columa llamada **phone_id**
	* La relacion esta definida **desde users hacia phones**


* **Una vez declara la relacion en el modelo, la usas asi:**
```php
				$usuario->phone;
```

## Definir la inversa de la relacion

* Las relaciones one-to-one van de $A \Rightarrow B$, podes admeas definir una relacion $B \Rightarrow A$ asi:
```php
		namespace App;
		use Illuminate\Database\Eloquent\Model;
		
		class Phone extends Model
		{
		    //Declaro que la relacion tambien va de Phone->User
		    public function user()
		    {
		        return $this->belongsTo('App\User');
		    }
		}
```
	
	
* **La uso asi:**
```php
		$phone->user
```


* **Puede tener un default en caso de que no exista un modelo:**
```php
		class Phone extends Model
		{
		    //Declaro que la relacion tambien va de Phone->User
		    public function user()
		    {
					$ModeloDefault=['name' => 'Guest Author']
		            return $this->belongsTo('App\User')->withDefault($ModeloDefault);
		    }
		}
```
## Uso de tablas o keys no default

 * **Si queres usar una columna que no se llama modelo_id podes hacer esto:**
```php
		class User extends Model{
			public function phone()
		    {
				// Relacion one-to-one
		        return $this->hasOne('App\number', 'MiColumna');
				// Relacion one-to-one inversa
				return $this->belongsTo('App\User', 'foreign_key');
		    }
		}
```
* **Si Ademas queres crear una relacion que no usa la primary key (esta es ID o la que hayas definido como primary key en el modelo):**
```php
		class User extends Model{
			public function phone()
		    {
				return $this->hasOne('App\number', 'foreign_key', 'local_key');
				return $this->belongsTo('App\User', 'foreign_key', 'local_key');
		    }
		}
```
# One to many

## Declaracion y uso

* la relacion $P_1 \Rightarrow \{C_1,C_2,C_3\}:$ es definida por  `$this->hasMany('App\Comment');`




En el ejemplo: $P=\text{post}$, $C=\text{comment}$, y queres decir que n post tiene varios comments.


```php
		namespace App;
		use Illuminate\Database\Eloquent\Model;
		
		class Post extends Model
		{
		    //Haces una funcion con un nombre que te indique que estas hablando 
			//del modelo B, en este caso Comments
		    public function comments()
		    {
		        return $this->hasMany('App\Comment');
		    }
		}
```
* **uso:**
```php
		$comments = App\Post::find(1)->comments;
```

## Definir la inversa de la relacion

La relacion inversa $\{C_1,C_2,C_3\} \Rightarrow P_1 :$ es definida por la funcion `$this->belongsTo('App\Post');`


Para poder determinar a que post corresponde un comment, necesitas declarar esa relacion

>Notese que **es una relacion one-to-one de tipo** 
$C_1 \Rightarrow P_1$
$C_2 \Rightarrow P_1$
$C_3 \Rightarrow P_1$
Y por consiguiente puedo usar la misma funcion que uso en las inversas de one-to-one, que es **belongsTo()**

* **Declaracion:**
```php
		namespace App;
		use Illuminate\Database\Eloquent\Model;
		//Dentro del modelo C
		class Comment extends Model
		{
		    //Le doy el nombre del modelo P
		    public function post()
		    {
				//Declaro una relacion inversa con el modelo P
		        return $this->belongsTo('App\Post');
		    }
		}
```
* **Uso**
```php
		$comment->post
```
		
		
## Uso de tablas o keys no default


Podes declarar el uso de un foren key diferente de **modelo2_id** o **un primary key diferente del ID o de aquel declarado en $primaryKey** 

```php
	//Usar un foreign key diferente de post_id
	return $this->hasMany('App\Comment', 'foreign_key');
	//Usar un foreign key diferente de post_id y un key diferente de
	//id o de aquel declarado en $primaryKey
	return $this->hasMany('App\Comment', 'foreign_key', 'local_key');


	//Analogos para las relaciones inversas
	return $this->belongsTo('App\Post', 'foreign_key');
	return $this->belongsTo('App\Comment', 'foreign_key', 'local_key');
```

# Many to many


Es una relacion donde dos modelos estan relacionados entre si.
**EJ:** Muchos users $U$ comparten muchos roles $R$
$\{U_1,U_2,U_3\} \iff \{R_1,R_2,R_3\}$

**Para eso podemos dividir la relacion en dos:**
* .$\{U_1\} \Rightarrow \{R_1,R_2,R_3\}$
	*  `belongsToMany('App\Role');`
* .$\{R_1\} \Rightarrow \{U_1,U_2,U_3\}$
	* `belongsToMany('App\User'); `

## Declaracion y uso:

Las tablas **users**, **roles** y **users_roles** que  es la **"tabla pivot"**
![enter image description here](https://lh3.googleusercontent.com/toROiU9phrvqaZBnRNWie87N_udZcu_6BFC6RR4bL7mcd_JMKmv29rOKWPpdXmzHFJxSiD17pkmV)


* **Los modelos:**
```php
		//Modelo uno
		class role extends Model
		{
		    public function users()
		    {
		        return $this->belongsToMany('App\User');
		    }
		}
		//Modelo dos
		class User extends Model
		{
		    public function roles()
		    {
		        return $this->belongsToMany('App\Role');
		    }
		}
```
* **Uso:**
```php
	$user->roles
	$role->users
```

## Uso de tablas o keys no default

* Podes declarar el uso de un foren key diferente de **modelo2_id** o **un primary key diferente del ID o de aquel declarado en $primaryKey** 
```php
		return $this->belongsToMany('App\Role', 'role_user');
```

* A su vez, podes indicar cuales son los nombres de la tabla pivot y sus campos asi
```php
		return $this->belongsToMany('App\Role', 'role_user', 'user_id', 'role_id');
```
## Leer datos de la tabla pivot

* **Si tenes una tabla pivot asi:**

| user_id 	| rol_id 	| created_at 	| updated_at 	|
|---------	|--------	|------------	|------------	|
| 1       	| 2      	| 10/10/10   	| 10/10/10   	|
| 2       	| 1      	| 10/10/10   	| 10/10/10   	|

* La tabla **pivot** tiene su propio **modelo implicito**, si queres acceder a sus propiedades, podes
	* **Ubicar una instancia de la relacion**
	* **Iterar cada elemento de la relacion y acceder a su pivot**
	```php
			foreach ($user->roles as $role) {
			    echo $role->pivot->created_at;
			}
	```
## Extender el modelo pivot

**Tabla ejemplo:**

| user_id 	| rol_id 	| created_at 	| updated_at 	| miCampo1 	| miCampo2 	|
|---------	|--------	|------------	|------------	|----------	|----------	|
| 1       	| 2      	| 10/10/10   	| 10/10/10   	| datos    	| datos    	|
| 2       	| 1      	| 10/10/10   	| 10/10/10   	| datos    	| datos    	|


* **Hacer que la tabla pivot tenga timestamps created_at y pudated_at**
	```php
		return $this->belongsToMany('App\Role')->withTimestamps();
	```


* **Extender el modelo implicito "pivot" con propiedades extra que esten en la tabla pivot**
	```php
		return $this->belongsToMany('App\Role')->withPivot('miCampo1', 'miCampo2');
	```


## Nombrar el modelo pivot

* Podes nombrar tu modelo pivot asi:
	```php
		return $this->belongsToMany('App\roles')->as('rolDeUsuario')
	```
* Lo accedes asi;
	```php
		foreach ($users as $user) {
		    echo $user->rolDeUsuario->created_at;
		}
	```
## Filtrar usando el modelo pivot

Podes filtrar un query usando los datos de la tabla pivot:
```php
		return $this->belongsToMany('App\Role')->wherePivot('approved', 1);
		
		return $this->belongsToMany('App\Role')->wherePivotIn('priority', [1, 2]);
```
## Definit un modelo pivot custom

Podes definir tu propio modelo pivot en caso de que la tabla pivot tenga una complejidad que lo requiera.

* **En el modelo que usara el modelo pivot**
```php
		class Role extends Model
		{
			//Defino la relacion many-to-many
		    public function users()
		    {
				//Defino el uso de un modelo pivot
		        return $this->belongsToMany('App\User')->using('App\UserRole');
		    }
		}
```
* **El modelo pivot customizado**
		namespace App;
		use Illuminate\Database\Eloquent\Relations\Pivot;
		class UserRole extends Pivot
		{
		    //cosas!
		}
		
#Has Many Through

Esta relacion te permite vincular dos tablas mediante una tabla intermedia
$C_1 \Rightarrow \{U_1,U_2,U_3\}\Rightarrow \{P_1,P_2,P_3\}  $
Se declara en $C$ con 
`return $this->hasManyThrough(P, U);`
**Ej:**
Muchos posts $P$ fueron creados por usuarios $U$ del mismo Pais $C$



![](http://i.markdownnotes.com/sdfsdfsdf.jpg)


##Declaracion y uso:

	namespace App;
	use Illuminate\Database\Eloquent\Model;
	//Desde el modelo C
	class Country extends Model
	{
	    //referenciamos el modelo P
	    public function posts()
	    {
			// indicamos los modelos (P,U)
	        return $this->hasManyThrough('App\Post', 'App\User');
	    }
	}
	
##Uso de tablas o keys no default


        return $this->hasManyThrough(
            'App\Post',
            'App\User',
            'country_id', // Foreign key on users table...
            'user_id', // Foreign key on posts table...
            'id', // Local key on countries table...
            'id' // Local key on users table...
        );
		


#Relaciones polimorficas

Son relaciones donde un modelo tiene la posibilidad de estar relacionado con varios otros (pero no mas de uno a la vez), es decir **sostiene mas de una relacion one-to-one**


.$C_1 \Rightarrow V_n \quad \text{XOR} \quad C_1 \Rightarrow P_n$ 




**EJ:**
Un comentario $C$ puede ser de UN video $V$ o (**OR EXCLUSIVO**$\oplus $) de UNA foto$P$
.$C_1 \Rightarrow V_n \quad \text{XOR} \quad C_1 \Rightarrow P_n$  


![](http://i.markdownnotes.com/fhbhhh.png)


##Declaracion y uso:

**Se declara:**
* indicando que $C$ puede tener varias formas definidas por las tablas **NOMBRE_type** y **NOMBRE_id**
				public function NOMBRE(){
					return $this->morphTo();
				}
* Indicando cuales son $V$, $P$, $etc$
		return $this->morphMany('App\Comment', 'NOMBRE');


>Laravel buscara las columnas **NOMBRE_ID** y **NOMBRE_type** con el segundo parametro de la funcion **morphMany()**
>
_return $this->morphMany('App\Comment', '**NOMBRE**');_




* **En el modelo con polimorfismo:**


		use Illuminate\Database\Eloquent\Model;
		use Illuminate\Database\Eloquent\Relations\Relation;

		//Indicas que este modelo esta vinculado a varios modelos
		class Comment extends Model
		{
			//indicas a que modelo hace referencia cada elemento 
			// de la tabla "commentable_type"
			Relation::morphMap([
			    'posts' => 'App\Post',
			    'videos' => 'App\Video',
			]);
			//Declaras la relacion
		    public function commentable()
		    {
		        return $this->morphTo();
		    }
		}




* **En los modelos vinculados al modelo con polimorfismo**
	* Un modelo 
			class Post extends Model
			{
			    public function comments()
			    {
					//Indicas que este modelo esta vinculado a un modelo con polimorfismo
					// Ademas indicas la columna donde esta el nombre de este modelo
					// EJ cuando commentable = Post
			        return $this->morphMany('App\Comment', 'commentable');
			    }
			}
	* Otro modelo
			class Video extends Model
			{
			    public function comments()
			    {	
					//Indicas que este modelo esta vinculado a un modelo con polimorfismo
					// Ademas indicas la columna donde esta el nombre de este modelo
					// EJ cuando commentable = Video
			        return $this->morphMany('App\Comment', 'commentable');
			    }
			}
		
* **Uso:**
		//Obtener los comentarios vinculados polimorficamente
		$post->comments
		$video->comments
		
		//Obtener el video/post al cual esta vinculado un comentario
		$comment->commentable;
		
#Relaciones polimorficas many-to-many


* **Relaciones polimorficas Many to Many **
	* Varios  tags $T$ pueden ser de VARIOS videos $V$ Y de VARIAS fotos $P$
	* .$T_1,T_2,T_3 \iff V_1,V_2,V_3 \quad \text{and} \quad T_1,T_2,T_3 \iff P_1,P_2P_3$  



![](http://i.markdownnotes.com/hfghjhjj.jpg)


##Declaracion

**La relacion se puede dividir en:**

* .$V_n \Rightarrow T_1,T_2,T_3 $  
	* Creamos una funcion **tags()** en el modelo **videos**
		* Que devuelva `$this->morphToMany('App\Tag', 'taggable'); ` 
* .$P_n \Rightarrow  T_1,T_2,T_3$
	* Creamos una funcion **tags()** en el modelo **posts**
		* Que devuelva `$this->morphToMany('App\Tag', 'taggable'); `
* .$T_n \Rightarrow V_1,V_2,V_3 $
	*  Creamos una funcion **posts()** en el modelo **tags** 
		* `return $this->morphedByMany('App\Post', 'taggable');  ` 
* .$T_n \Rightarrow  P_1,P_2,P_3$
	*  Creamos una funcion **videos()** en el modelo **tags** 
		* `return $this->morphedByMany('App\Video', 'taggable'); `

**POST:**

	namespace App;
	use Illuminate\Database\Eloquent\Model;
	class Post extends Model
	{
	    public function tags()
	    {
	        return $this->morphToMany('App\Tag', 'taggable');
	    }
	}

**VIDEO:**

	namespace App;
	use Illuminate\Database\Eloquent\Model;
	class video extends Model
	{
	    public function tags()
	    {
	        return $this->morphToMany('App\Tag', 'taggable');
	    }
	}


**TAG:**

	namespace App;
	use Illuminate\Database\Eloquent\Model;
	class Tag extends Model
	{
	    public function posts()
	    {
	        return $this->morphedByMany('App\Post', 'taggable');
	    }
	
	    public function videos()
	    {
	        return $this->morphedByMany('App\Video', 'taggable');
	    }
	}
	
##Uso

* **Podes traer los tags de un post o video asi:**

		//post
		foreach ($post->tags as $tag) {
		    //
		}
	
		//video
		foreach ($post->tags as $tag) {
		    //
		}
		
* **Y los posts con un tag asi:**

		foreach ($tag->videos as $video) {
		    //
		}
		
#Hacer querys con las relaciones

* Podes usar las relaciones como propiedades
		$user->posts()->where('active', 1)->get();


* O podes hacer querys sobre las relaciones:
		$user->posts()->where('active', 1)->get();

		
		
#Guardar/crear modelos con relaciones

##One-to-one / one-to-many / many-to-many

###Desde un modelo
* **Podes guardar un modelo relacionado asi:**
		$post->comments()->save($comment);

* **Podes guardar multiples modelos asi:**
		$post->comments()->saveMany([$comment1,$comment2]);
		
###Desde un array

* **Podes crear un modelo relacionado asi**
		$comment = $post->comments()->create([
		    'message' => 'A new comment.',
		]);
* Crear varios modelos asi:
		$post->comments()->createMany([
		    ['message' => 'A new comment.'],
			[ 'message' => 'Another new comment'],
		]);
	
##One-to-one Inverse / one-to-many inverse

* **podes declarar que un modelo pertenece a otro asi**
		$user->account()->associate($account);
		$user->save();

* **podes declarar que un modelo ya no pertenece a otro asi:**
		$user->account()->dissociate();
		$user->save();

##Many-to-many


* **Para indicar que un modelo pertenece a otro**
		$user->roles()->attach($roleId);

* **Para hacerlo e incertar un valor en la tabla pivot**
		$user->roles()->attach($roleId, ['expires' => $expires]);
* **Para indicar que un modelo ya no pertenece a otro**
		$user->roles()->detach($roleId);
* **para remover todas las relaciones de un modelo con otro**
		$user->roles()->detach();

>Todas estas funciones aceptar **arrays de ids** o **arrays de ids y valores** 
```
$user->roles()->detach([1, 2, 3]);
$user->roles()->attach([
    1 => ['expires' => $expires],
    2 => ['expires' => $expires]
]);
```

###Sincronizar relaciones many-to-many

Para borrar todas las relaciones many-to-many de un modelo con otro y establecer nuevas, podes hacer asi


	$user->roles()->sync([1, 2, 3]);
	
###Guardar dato en tabla pivot

	$user->roles()->updateExistingPivot($roleId, $attributes);



###Actualizar timestamp del parent model

Si al modificar un child model con una relacion **belongsTo()** o **belongsToMany()** podes hacer que los timestamps **updated_at** y **created_at** del parent se actualicen solos al modificar el child model

	
		//Modelo child
	  //Indico aca que relaciones deben modificar al parent, 
	  //en este caso la relacion "post()"
  	  protected $touches = ['post'];
  	  public function post()
  	  {
  	      return $this->belongsTo('App\Post');
  	  }
	


#Verificar existencia de una relacion


Podes ver si existe una relacion para un elemento determinado asi:

* **Ver si existe una relacion entre dos modelos:**

		//Ver si tiene comentarios
		$posts = App\Post::has('comments')->get();
		//Ver si tiene mas de 3 comentarios
		$posts = App\Post::has('comments', '>=', 3)->get();
		
		//Podes concatenar dos has() statements asi
		//que tenga coments y votes
		$posts = App\Post::has('comments.votes')->get();
	
* **Para mayor capacidad, podes usar un callback:**

		//Buscar posts donde tengas comentarios
		$posts = App\Post::whereHas('comments', function ($query) {
			// con columna content like foo%
    		$query->where('content', 'like', 'foo%');
		})->get();
	
* **Verificar la no existencia de una relacion:**
Son metodos analogos.

		$posts = App\Post::doesntHave('comments')->get();
	
		$posts = App\Post::whereDoesntHave('comments', function ($query) {
   		 $query->where('content', 'like', 'foo%');
		})->get();
		
		$posts = App\Post::whereDoesntHave('comments.author', function ($query) {
    		$query->where('banned', 1);
		})->get();
		
#Contar la cantidad de relaciones

##N° de relaciones

			$posts = App\Post::withCount('comments')->get();
			foreach ($posts as $post) {
			    echo $post->comments_count;
			}

##N° de relaciones que cumplen una condicion

	$posts = App\Post::withCount([
	    'comments',
	    'comments as pending_comments_count' => function ($query) {
	        $query->where('approved', false);
	    }
	])->get();
	echo $posts[0]->comments_count;
	echo $posts[0]->pending_comments_count;

#Precargar relacion - Eager loading

Los **datos de una relacion no son cargados hasta que son requeridos**, eso significa que el siguiente codigo hace $N+1$ llamadas a la base de datos 

	$books = App\Book::all(); //devuelve 10 libros
	
	foreach ($books as $book) {
		//llama a la base de datos una vez por libro
	    echo $book->author->name;
	}
	//Totoal de llamados a DB=11
	
* **Para precargar una relacion**
	
		//dos querys
		//Precargas la relacion "author"
		$books = App\Book::with('author')->get(); //devuelve 10 libros con su autor
		
		//ninguna query
		foreach ($books as $book) {
		    echo $book->author->name;
		}
	
* **Precargar varias relaciones**

		$books = App\Book::with(['author', 'publisher'])->get();

* **Precargar relaciones anidadas**
Cargar todos los autores de los libros
Cargas todos los datos de contacto de cada autor.

		$books = App\Book::with('author.contacts')->get();
		
* **limitar la precarga a ciertos datos**
	Podes limitar aquellos datos que se precargan a los resultados de una query
		$users = App\User::with(['posts' => function ($query) {
		    $query->where('title', 'like', '%first%');
		}])->get();

* **Precargar una relacion dimanicamente:**
	
		if ($someCondition) {
		    $books->load('author', 'publisher');
		}
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk3NTkwOTE0OCwzNDQxNTkxMDldfQ==
-->