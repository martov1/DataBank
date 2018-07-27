
**Me quede en**
 Create Custom Options with Settings API
https://www.youtube.com/watch?v=pTegcB9zMSM&index=5&list=PLriKzYyLb28kpEnFFi9_vJWPf5-_7d3rX

# Intro

## Arquitectura
* Los plugins van en `wp-content/plugins/nombreDePlugin`
* El **archivo principal** del plugin va en `wp-content/plugins/nombreDePlugin/nombreDePlugin.php`
* El archivo de precaucion **index.php** en blanco, que evita que apache sirva el contenido de la carpeta
* Cualquier otro archivo que quieras, requiriendolo con
 `require_once plugin_dir_path(__file__).'subcarpeta/archivo.php'` o usando el **composer autoloader**



## Metadata

En el **archivo principal del plugin**, hay que darle algo de data a wordpres acerca del plugin, minimamente el nombre del plugin de forma human friendly

```php
/**
 * Plugin Name: Mi plugin
 * Plugin URI: http://alecadd.com
 * Description: blabla
 * Author: blabla
 * Author URI: www.blabla.com
*/
```

## Plugin structure


Hay infinitas formas de armar un plugin, una posibilidad simple es armar una clase en el archivo principal, pero tambien podes incluir los archivos, clases y funciones que quieras desde otros archivos.
```php

//Plugin que funciona con el patron singleton
class MyPlugin{
	
	function __constructor(){
	}
	
	function activate(){
		//Remove rewrite rules and then recreate rewrite rules.
		//Para cuando creas nuevos post types o taxonomies
		flush_rewrite_rules();
	}
	
	function deactivate(){
	}
	
	function uninstall(){
	}
}

$myPlugin = new MyPlugin;

//Registrar una funcion que se correra al activar el plugin
//El registro de estas funciones es lo unico enforceado
register_activation_hook(__file__, [$myPlugin, 'activate'])
register_deactivation_hook(__file__, [$myPlugin, 'deactivate'])
register_uninstall_hook(__file__, [$myPlugin, 'uninstall '])

```




## Funcionamiento basico

Los plugins tienen que registrar funciones con hooks para tener algun efecto en el momento indicado cada vez que se carga wordpress. recordemos que **wordpress se carga en cada request**, por lo que tenes que **añadir acciones para que el plugin haga algo**. 

>Lo que escribas en el plugin se ejecuta **en algun momento indeterminado durante la carga** por lo que **necesitas usar hooks para hacer cosas utiles**

>todo lo que no esta en un hook no se esta ejecutando.

## Desinstalacion de plugins

Podes implementar la desinstalacion

* En un metodo dentro del archivo principal,  que se active con el hook `register_uninstall_hook`
* En un archivo **uninstall.php** en la carpeta del plugin, que se llama solo

## Carga de scripts y css

podes cargar css o scripts asi:
```php
function cargarCosas(){
	wp_enqueue_style(
				'miEstilo',
				 plugins_url('/assets/miEstilo.css',__file__)
				);
	wp_enqueue_script(
				'miScript',
				 plugins_url('/assets/miScript.js',__file__)
				);
}
//Colocarlo en un hook
 add_action('wp_enqueue_scripts', [$this, 'cargarCosas'])
```
## Composer   y Autoloader

Podes usar composer para manejar las dependencies, tambien podes usar el composer autoload para autocargar las clases. Esto permite

* usar PSR-4 (como laravel)
* Autocargar las clases
* cargar clases solo con namespaces que se corresponden con los nombres de carpetas

[Ver mas](https://www.youtube.com/watch?v=nbF4hWJ1hJA&list=PLriKzYyLb28kR_CPMz8uierDWC2y3znI2&index=11)

```php
use miCarpeta/miClase
```


# API

## Posts

* **get_posts(args)** - Te permite obtener una serie de posts
* **wp_delete_post()** - Te permite borrar posts

## SQL

Podes interactuar con la base de datos llamando a la variable global **$wpdb**

```php
global $wpdb;
$wpdb->query("Tu SQL va aca")
```


# Admin menus


## Añadir al menu de admin

**Podes añadir menues en la pagina de administracion asi:**

```php
add_menu_page(
			'titulo de la pagina',
			'titulo de menu',
			'manage_options',
			'slug_del_menu',
			contenido(),
			'iconoEnCss',
			$posicionEnElMenu)

//La funcion que devuelve el contenido
function contenido(){
require_once plugin_dir_path(__file__).'carpeta/miPag.php'
}
```

**Podes añadir sub-paginas asi:**

>Si queres que la primera sub-pagina no se llame igual que la pagina parent entonces tenes que ponerle a la sub-pagina el mismo titulo, slug y funcion generadora de contenido
```php
add_sub_menu_page(
			'parent_slug',
			'titulo de pagina',
			'titulo de menu',
			'manage_options',
			'menu_slug',
			'iconoEnCss',
			$contenido)

//La funcion que devuelve el contenido
function contenido(){
require_once plugin_dir_path(__file__).'carpeta/miPag.php'
}
```

## Settings API

### Generar forms
La settings API te permite generar menues en las paginas de administracion capaces de guardar settings que puedas usar en otros lugares del theme.
* Logica
	* Registrar un **setting** y el grupo al que pertenece con **register_setting()**
* UI
	* Registras secciones de fields dentro del grupo con **add_settings_section()**.
	* Registras campos con **add_settings_fields()**
* Vinculo **Logica** $\iff$ **UI** 
	* El HTML de cada campo esta vinculado con un **setting** con el HTML attribute "name"

![enter image description here](https://lh3.googleusercontent.com/u_nB4BNuDkB7Y0sUUzln2DPotcxUF_DLpIgl939ca-CEPCXerbjKjChGCJNKB1QzFSPhX_e8Qx0G)



**Dentro de una funcion que se ejecute en el hook de admin_init**
```php
//En la logica (plugin/functions.php/etc)
add_action('admin_init','miFuncion');

function miFuncion(){
```

**Declaras los settings y definis que esten dentro de algun _grupo_**
```php
	/**
	* GRUPO y setting
	*/
	//Declaro miSetting1 
	register_setting(
					'nombreDeGrupoDeSettings',
					,'miSetting1');
	//Declaro miSetting1 
	register_setting(
					'nombreDeGrupoDeSettings',
					,'miSetting2');
	
```

**Declaras una seccion, que es un agrupamiento de fields HTML**
```php
	/**
	* SECCION
	*/
	add_settings_section(	
							//Un id unico
							'nombreUnicoDeConjunto',
							//El titulo
							'human Friendly Name',
							//la funcion que devuelve
							//el contenido
							'funcionDeContenido',
							//slug de la pagina de admin.
							'page_slug'
						);
	//Funcion que devuelve el contenido del
	//form para ese conjunto de settings
	function funcionDeContenido(){
		echo 'Settings;'
	}

```

**Declaras cada campo dentro de alguna seccion.**
El HTML de cada campo indica a que setting pertenece usando el atributo "name"
```php
	/**
	* FIELDS
	*/
	
	//miSetting1
	add_settings_field(
						'nombreUnico1',
						'Titulo',
						'funcionDeContenido2',
						'page_slug',
						'nombreDeLaSeccion',
						)
	function funcionDeContenido2(){
		echo '<input type="text"
		 name="miSetting1"
		 value="">'
		 
	}
	// miSetting2
	add_settings_field(
						'nombreUnico2',
						'Titulo',
						'funcionDeContenido2',
						'page_slug',
						'nombreDeLaSeccion',
						)
	function funcionDeContenido2(){
		echo '<input type="text"
		 name="miSetting2"
		 value="">'
		 
	}
}
```

**En el template de la pagina de admin colocas esto**
```php
<form method="post" action="options.php">
	<!-- los mensajes de error/confirmacion se
	 inyectan aca -->
	<?php settings_errors() ?>
	<!-- Indica que aca van a estar los settings del
	grupo nombreDeGrupoDeSettings-->
	<?php settings_fields('nombreDeGrupoDeSettings') ?>
	<!-- Colocas las secciones de este slug, los inputs
	de los campos son automaticamente inyectados-->
	<?php do_settings_section('page_slug') ?>
	<?php submit_button(); ?>

</form>
```

### Obtener settings

Podes obtener settings asi

```php
get_option('miSetting1')

```


# Plugin boilerplate - WIP


Este boilerplate define todo de manera muy limpia.
https://github.com/DevinVinson/WordPress-Plugin-Boilerplate
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk0OTMwNjI3MV19
-->