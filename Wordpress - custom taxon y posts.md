
# Taxonomies

Es un metodo de clasificacion, puede ser jerarquico o no jerarquico. ejemplos de taxonomias son

* Categorias
	*  Jerarquicas
* Tags

## Custom taxonomies

Podes crear custom taxonomies, jerarquicas o no jerarquicas y pueden aplicarse a ciertos post types o todos

Algunas taxonomias que podrias crear son:
* tipo de producto o servicio
* tipo de inmueble
* tipo de producto
* etc

**Para hacer una taxonomia custom**

```php
//Definis una funcion que registre la taxonomia
function mi_taxonomia(){
	$params = [
				'label'=>'human readable name',
				//Nombre para URL
				'rewrite'=>['slug'=>'el-slug-de-URL'],
				//jerarquico como pages o no jerarq
				//como posts
				'hierarchical'=>true/false
			]
			
	register_taxonomy(
		 	'nombre-computer-friendly',
			'post-types a losque aplica',
			$params
			);
}
//Añadis una accion para llamar a la funcion que
//definiste cuando wordpress se inicializa
add_action('init', 'mi_taxonomia');
```




# Post customization

## Post formats

Los posts formats te permiten encajar los posts en ciertos "formatos" para despues en el theme visualizar posts de form ligeramente diferentes, te permiten por ejemplo visualizar los posts en el listado con una imagen, un video, etc out-of-the-box

Tenes que habilitar los post formats para tu theme, los formats disponibles **ya vienen predefinidos**

```php
//En alguna funcion que llamas desde un hook
add_theme_support('post-formats',[
			'aside',
			'images',
			'video'
])
```
![enter image description here](https://lh3.googleusercontent.com/Kh0DOd3y1wZMTrSPe25d5yrtYWFbj7fjkXJEoAO1lU99LTNf8suhwLjYEv1eu2iC8sZ8Qid7Vb1r)


### Ejemplo
```php
//En el loop
$formato = get_post_format();
//Traer el template posts-formato.php
//por ejemplo posts-video.php
get_template_part('posts',$formato)
```


## Post types

Los post types son categorias de posts en wordpress, algunos ejemplos son:

* **pages**
	* Tienen relaciones parent-child
	* Aparecen generalmente en el main menu 
* **posts**
	* no son jerarquicos
	* tienen autor
	* tienen por lo menos una categoria
	* Pueden tener tags
	* Aparecen en orden cronologico inverso 


## Custom post types

### Crear CPT 

>**Los custom post types aparecen en el admin menu!**
>
>**TODOS LOS MENUES DEL ADMIN SON CUSTOM POST TYPES, INCLUIDO LOS SETTINGS ETC**
>[Documentacion sobre custom post types](https://codex.wordpress.org/Custom_Post_Types#Changesets)

* Pueden heredar las funcionalidades de posts o pages
* Pueden organizarse con categories, tags o custom taxonomies
* Puede tener un index page separado con template separado
* Puede combinar features
* **Podrian ir en un plugin para mejor organizacion**

**Para registrar un nuevo post type:**
```php
function cursosPostType(){
$params =[ 
	// hay mil propiedades documentadas
	'public'=>true,
	'show_in_menu'=>true,
	'labels'=>[
		//Los nombres que se usaran, son un monton
		'name' => 'cursos',
		'singular_name'=>'curso',
		'menu_name'=>'cursos',
		'new_item'=>'nuevo curso',
		'not_found'=>'no se encontro el curso',
		'menu_icon'=>'dashicon-id-alt'
		// www.blog.com/secciondeurl/miCurso
		'rewrite'=>'secciondeurl',
		'hierarchical'=>true // es jerarquico como las pages
		]
]
register_post_type('miCurso',$params)
}
```
[Ver todos los argumentos disponibles](https://codex.wordpress.org/Function_Reference/register_post_type#Arguments)
[iconos disponibles](https://developer.wordpress.org/resource/dashicons/#editor-ol)

### Permalinks

Si vas a usar el atributo  _rewrite_ para cambiar los permalinks, tenes que indicarle a wordpress que re-escriba los permalinks al cargar el plugin
```php

function my_rewrite_flush() {
	//Registra el custom post type
	cursosPostType();
	//Re-escribi los permalinks
    flush_rewrite_rules();
}
//corre la funcion SOLO al cargar el plugin
register_activation_hook( __FILE__, 'my_rewrite_flush' );
```

### Columnas custom para posts en admin

Para poder indicarle a WP que columnas queres que se muestren en el listado de posts en el admin panel podes hacer lo siguiente

```php
/**
* Determinar las columnas que se van a mostrar
*  para un post type
*/
add_filter('manage_TU-POST-TYPE_posts_columns', 'miFuncion');
//WP te inyecta las columnas que el post type ya tiene
function miFuncion($columns){
//hay columnas que se llenan solas, por ej
//title, date, author, etc
	$nuevasColumnas=[
		'title'=>"Title",
		'columnaCustom1'=>"Columna Custom1",
		'columnaCustom2'=>"Columna Custom2",
		'date'=>"Date"
	]
return $nuevasColumnas;
}

/**
* Configurar una columna custom
*/

add_action(
			'manage_TU-POST-TYPE_posts_custom_column',
			'miFuncion2',
			10,
			2
			)
// Esta funcion loopea en cada post y cada columna
// y devuelve el contenido de cada columna custom
 miFunction2($column, $post_id){
	 switch ($column){
		case 'columnaCustom1':
			echo "resultado de la columna!"
		break;
	
		case 'columnaCustom2':
			echo "resultado de la columna!"
		break;
	}
}
 

```

### Meta boxes, campos custom para post types

Los meta-boxes son inputs customizados para el post type, por ejemplo el precio de un curso, el nombre del profesor, etc.
**Hacen uso de los custom fields/post metadata**
* añadis una accion que crea un metabox
* El metabox tiene una funcion que determina
	* El output HTML del metabox 
* Declaras una funcion que se corre con cada _post_save_ y guardas el metadato del metabox


**Definis el metabox:**
```php
/**
* Declaras el metabox
*/
add_action('add_meta_boxes','miMetaBox()' )

//Funcion que se llama con un hook
function miMetaBox(){
	add_meta_box('nombreUnico',
				'titulo',
				'miFuncion',
				'ElCustomPostType',
				'Donde aparece (sidebar, normal)',
				'Prioridad (posicion donde aparece');
}
```

**Declaras el HTML del metabox y la funcion que va a guardar los datos al post**
```php
/**
* Aca hay que devolver el contenido del meta box
*/
function miFuncion($post){
	//Agregas el nonce
	wp_nonce_field('DescripcionDeLaAccion',
	'NombreDelNonceField')
	//Obtenes el valor custom que este post ya tenia
	//para mostrarlo en el UI
	$value = get_post_meta($post->ID, '_laKey', true);
	
	//Generas el input del metabox
echo '<input type="email" id=unId" 
		name ="miMetaboxField" value="'.$value.'" >'
}


```

**La funcion que va a guardar los metadatos**
Notese que esta funcion va en un hook que corre **cada vez que se guarda un post,** y entonces tiene que **verificar la autorizacion del usuario** 
```php
// La funcion de guardado corre cada 
// vez que se guarda un post
add_action('save_post','funcionguardarDato');
/**
*La funcion que va a guardar los datos
*//
function funcionguardarDato($post_id){
	//Esto esta definido en el HTML del metabox
	$field = $_POST['miMetaboxField']
	
	//Verifico el nonce, si no es adecuado, return
	$nonce = $_POST['nombreDelNonce'];
	if (!wp_verify_nonce($nonce,'funcionguardarDato' )){
		return;
	}
	
	//No guardar esto si es un autosave de wordpress
	if(defined('DOING_AUTOSAVE') && DOING_AUTOSAVE){
		return;
	}
	
	//El user tiene los permisos necesarios
	if (!current_user_can('edit_post', $post_id){
		return;
	}
	//si no se modifico el campo no guardo
	if (!isset($field)){return;}
	//Guardo los datos
	$misDatos = sanitize_text_field($field);
	update_post_meta($post_id,'_laKey',$misDatos)
}
```




# Custom fields - WIP

>El plugin **advanced custom fields** te asiste mucho en esto para poder tener un UI para ciertos posts con fields de cierto type, requeridos o no, etc.

## Vanilla wordpress
Podes añadir datos adicionales a los posts con **custom fields** y mostrarlos en un template.

Wordpress ya trae un UI para cargar custom fields en **un post particular**

![enter image description here](https://lh3.googleusercontent.com/rUwxSe7oxo4X6a58T04bAxt3t7FmI6yk0jZAYPew_O1A5UWR6dwhXBXKtLq-_mrsSL9qMxC_MNT7)

Una vez colocado, podes accederlo en el template


```php
//La meta data puede ser un array, si es un solo valor
//podes marcar true en el ultimo parametro y te da el valor
//en lugar de un array con un solo valor.
get_post_meta(idDelPost,'nombreDelField', 
			devolverUnSoloValor)
get_post_meta($post->ID,'clima', true)
```

>Si no existe el custom field, devuelve null o un array vacio, dependiendo del ultimo parametro

## Programatic custom fields - WIP
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0Mjk4Mzk4MjMsMjgwMDQxODg5XX0=
-->