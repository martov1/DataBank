
**ATENCION USAR OOP:** https://www.youtube.com/watch?v=KITZ_88EDTI

**Me quede en**
lynda: 01 creating custom taxonomies.
Udemy:  05 Custom Post Types and Advanced Custom Fields

**TODO:**
reordenar todo!:  

# Contenido


* Folder structure - wordpress
* Folder structure - Themes


## Folder structure - wordpress

* **cgi-bin**
* **wp-admin**
* **wp-content**
	* **plugins** - Contiene los plugins, cada plugin es en general una carpeta
	* **themes** - Contiene los themes, cada theme es una carpeta
	* **upgrade**
	* **uploads** - Los archivos subidos se cargan aca
* **wp - includes**  


## Folder structure - Themes

La siguiente referencia es sobre el contenido de la carpeta `themes/nombreDeMiTemplate`
* **header.php** - Contiene un template del header del sitio.
	* Contiene la precarga de css, js, etc con wp_header() 
* **footer.php** - Contiene un template del footer del sitio
	* Contiene carga de css,js, etc mediante wp_footer() 
* **sidebar.php** - Contiene el template del sidebar, que tiene los widgets 
* **index.php** - Contiene un template que deberia ser lo suficientemente generico como para poder mostrar todo lo que no tenga una pagina propia o generica definida.
	* Contiene get_header(), get_sidebar(), get_footer() etc que llaman a las respectivas header.php, footer.php, sidebar.php, etc 
* **category-nombre.php** - Contiene un template para mostrar todos los posts de la cotegoria "nombre"
* **category.php** - Contiene un template para mostrar todos los posts de una catgoria que no tiene su propio archivo de template 
* **Single.php** - Determina como se muestra un solo post en el sitio 
* **functions.php** - Contiene la logica de la template 
* **Search.php** - Determina como se muestran los resultados de busqueda
* **page.php** - Contiene el template para mostrar una pagina generica cualquiera
*  **style.css** - Contiene los estilos globales. Tiene que tener el **Theme name como metadata** para ser reconocido.+
![enter image description here](https://lh3.googleusercontent.com/lT0TdrVmIl8YBQPpnUIHo4VJbEHkI4jRC8huA1A0CNo9w7IyarKGl5yN_G9I3BZmemTa8BAU2etZ "styles")

# Theme development - WIP

Crear themes es basicamente crear un conjunto de templates y un conjunto de logica.


## Estructura de un theme

Los themes se componen principalmente de **template files**, hay:
*  **Templates ESPECIFICOS para una pagina en particular**
	* **cualquiera.php** - Cualquier template que podes asignar a la pagina que vos quieras
	* **categories-miCategoria.php** - Para la lista de posts de una categoria en particular 
	* **single-customPostTypeSlug.php** - Para cada post de un type en particular.
	* **Front-NOMBRE.php** - La pagina principal del sitio, si configuraste el home desde el admin para una pagina estatica
	* **home.php** - La pagina principal del sitio, si configuraste el home desde el admin para mostrar los posts mas recientes. Es lo que se muestra en `www.pagina.com/blog`
	* **taxonomy-nombre.php** - Listado de posts con la taxonomia NOMBRE EJ: los posts con la taxonomia UBICACION
	* **taxonomy-nombre-termino.php** - Listado de posts con la taxonomia NOMBRE y el termino TERMINO ej: ubicacion - san isidro
	* **search.php** - Listado de posts resultantes de una busqueda
* **Templates GENERALES para varias paginas en comun**
	*  **page.php** - Para todas las paginas sin template particular
	* **category.php** - para mostrar cualquier categoria en particular sin un template especifico
	* **tag-nombre.php** - Muestra los posts del tag "nombre"
	* **tag.php** - Muestra los posts de cualquier tag
	* **taxonomy.php** - Para todas las taxonomias que no son ni categorias ni tags, osea que para las taxonomias no default 
	* **single.php** - Para mostrar cualquier post en particular
	* **index.php** - Para mostrar cualqueir contenido en general que no tenga template puntual
	* **404.php** - Template que se muestra cuando la url no es valida

## Template styles y scripts

los styles pueden estar declarados
* **styles.css** - Styles generales para toda la theme, en el root del theme
* **Otros archivos** 
### Cargar style sheets

Podes cargar style sheets usando **wp_enqueue_style()**

```php
//En functions.php, en alguna funcion que se triggerea con
//una accion
$templatePath = get_template_directory();
$cssPath = $templatePath . '/css/myEstilo.css';
wp_enqueue_style(nombre,$cssPath);
```


## Template hirarchy

Las jerarquias de wordpress indican que template file se va a usar cuando wordpress se encuentra con un URL tal que

    miSitio/blog/category/movies

Busca el template de manera jerarquica asi
* **category-movies.php**
* **category-4.php** - donde el ID de la categoria MOVIES es 4
* **category.php** - Intenta usar el archivo generico de categorias
* **archive.php** - Intenta usar el archivo generico archive.php
* **index.php** - Si no encuentra nada de eso, intenta mostrar el contenido usando index.php

**De manera generalizada, este es el orden jerarquico de cada tipo de parte del sitio wordpress:**
![enter image description here](https://lh3.googleusercontent.com/jq0NL0bpQbIoUgCd8ue0EbMzK1OSRpx2YbeM6ZJpPJMyNyGvLP6hkHp7XhgaKQLg11HHo43hrszx)



## Template tags

Te permiten colocar contenido en los templates


#### [Listado total](https://codex.wordpress.org/Template_Tags)

los template tags son **SENSIBLES AL CONTEXTO DEL WORDPRESS LOOP**

* **wp_head()** - coloca JS, css, etc en el template, hay que ponerlo en el HTML <head>
* **body_class()** - Coloca las clases css con el nombre de la wordpress page/ post type, etc. Con esas clases despues podes estilar el contenido
* **wp_list_categories()** - Permite listar categorias/tags/taxonomias (no necesariamente todas), genera un menu con hipervinculos a cada categoria.
* **Contenido**
	* **the_title()** - Devuelve el titulo de la pagina o post 
	* **the_content()**  - Devuelve el contenido del post/page
	* **the_author()** - Devuelve el autor
	* **the_excerpt()** - Devuelve las primeras palabras del contenido
	* **the_category()** - Muestra la categoria del post con un link
	* **the_permalink()** - el permalink de este post/page en el loop
	* **the_post_thumbnail(size)** - Muestra la imagen del post/page
	* **get_template_part('path al template','continuacion del path')** - incerta un archivo php en ese lugar del template, en general sirve para dividir un template en mas pedazos, ej: el template  de cada post en el loop.
		* El path tiene dos atributos para combinarlo con otras funciones de wordpress
		*  `get_template_part('templates/content','get_post_format()')`obtiene por ejemplo:
			*  `templates/content-page.php` 
			*  `templates/content-video.php`
			* `templates/content-search.php`
		* Si el post no tiene formato especifico, entonces queda `templates/content.php` por que `get_post_format()` devuelve `null`

### GET_the_title() vs the_title() y similares

Cuando hay un GET en una funcion de contenido, **devuelve un objeto que representa el contenido, con toda su metadata**. cuando no hay un GET wordpress toma el contenido y lo coloca en la pagina (img tag, string, etc)

Por ejemplo:
```php
	the_title();
```
Equivale a 
```php
	echo get_the_title();
```

## Conditional tags

Son tags similares a los wordpress tags, pero te permiten checkear condiciones 

* **is_home()** - true si es home
* **is_front_page()** - true si es front page
* **is_single()**
* etc..

## Wordpress loop

Es un sistema que te permite iterar una serie de objetos en la base de datos (posts, pages, etc) y mostrarlos.

**El loop se puebla solo dependiendo de la URL donde estes parado, podes poblar el loop con otro query usando WP_query();**

> Es imperativo que exista un loop en **index.php**, ya que es la ultima linea de defensa cuando wordpress no encuentra como mostrar contenido.
```php
    if (have_posts())
	    while (have_posts()) : the_post() 
		    //Los tags se pueblan con 
		    //el post en cada iteracion
		    the_title();
		    the_content();
	    endwhile;
    endif; 
```


### wp-query

Te permite modificar el loop para devolver los posts/pages/etc que encajen con un query

>Cuando usas un custom query tenes que resetear las variables del post para el siguiente post en el loop. para eso al final de tus acciones en el loop llamas a  `wp_reset_postdata();`

```php
$args = array(
	'post_type' => 'post',
	'tax_query' => array(
		'relation' => 'OR',
		array(
			'taxonomy' => 'category',
			'field'    => 'slug',
			'terms'    => array( 'quotes' ),
		),
		array(
			'taxonomy' => 'post_format',
			'field'    => 'slug',
			'terms'    => array( 'post-format-quote' ),
		),
	),
);
$query = new WP_Query( $args );
```
Una vez que configuraste el query, podes usarlo en un loop asi
```php

<?php if ( $the_query->have_posts() ) : ?>

	<?php while ( $the_query->have_posts() ) : $the_query->the_post(); ?>
	<!--Mostrar cosas-->
	<?php endwhile; ?>
	<!-- Resetear las variables del loop-->
	<?php wp_reset_postdata(); ?>
<?php endif; ?>
```

### Reset_post_data vs rewind_post_data

Cuando usas un custom query estas sobreescribiendo los resultados de las template tags (the_title(), etc) 

* Para hacer que esas **tags vuelvan a su comportamiento normal en el post loop general** (determinado por la URL donde estas parado) usas	`Reset_post_data()`
* Si queres volver a usar el mismo loop desde el comienzo, usas  `Rewind_post_data()`

## Page Templates

Para hacer un template para una pagina lo unico que tenes que hacer es un archivo php con 

    /*
     * Template Name: mi template
    /* 
Una vez hecho esto, podes elegir el template desde el backend de wordpress

![enter image description here](https://lh3.googleusercontent.com/Mr1L7XMgnaQ6WsL7CmYUby8_xtyuVAHlR3Gp-MYaEWtmAC3K-qObptig3IDA6YGhxTNTfjhi8Pm1)





## Images y  sizes

Wordpress genera los siguientes tamaños por default cropeando la imagen
* Thumbnail
* Medium
* Large
* Full-size

**Hay dos formas de cropear la imagen**
* **Soft-crop:** Cropea y resizea la imagen a un tamaño **similar** al solicitado, siempre evita sacar partes de la imagen
* **Hard-Crop:** Cropea y resizea la imagen para llegar al tamaño **exacto** solicitado. removera partes de la imagen si es necesario


Podes pedirle a wordpress que genere dimensiones especificas 
```php
//En functions.php
// add_image_size(name, height, width, hardcrop)

//cortar con hardcrop
add_image_size('mi-tamaño', 500, 400, true)

//Cortar con hardcrop, hacer el cropping desde el
// centro, manteniendo el borde superior tal como esta
add_image_size('mi-tamaño', 500, 400, ['center','top'])
```


## Custom Side bars

Te permiten colocar contenido a los costados, abajo o donde necesites, en su interior se colocan widgets con funcionalidades puntuales.


### dynamic sidebar

Los sidebars dinamicos son aquellos cuyo outpput es unicamente los widgets que agregaste desde el admin panel.
>Cuando creas un nuevo dynamic sidebar este automaticamente aparece en el admin panel para que le coloques widgets

**Podes añadir una custom sidebar asi:**
```php
function miSideBar(){
$params = [
	'name' =>'el nombre del sidebar',
	'id'=>'id_del_sidebar',
	'description'=>'la descripcion',
	'before_widget'=>'HTML antes de cada widget'
	'after_widget'=>'HTML despues de cada widget'
]
register_sidebar($params)
}
add_action('widgets_init', 'miSidebar')
```

Una vez declarada la sidebar, aparece en apearence->sidebar

![enter image description here](https://lh3.googleusercontent.com/UzEPdoO0HN54FZeauOB-HuUS6rEGbXIGf0TKuPEr2AUimpIR1_uz5u7n_1yxZiMPn8ina_BUc0jf)

**Podes mostrar tu sidebar en un template asi:**
```php
dynamic_sidebar('nombre del side bar')
```

### static sidebars

Los static sidebars son sidebars cuyo output es otro archivo PHP. Se llaman static por que originalmente estaba pensado para que tenga contenido estatico HTML, pero gracias a PHP podes incluso meter un dynamic side bar dentro del static side bar.

Funcionan con un archivo  que funciona como el template del sidebar que se llamara **sidebar-nombre.php**

**En el template:**
```php
//El nombre del sidebar, 
//WP buscara el archivo sidebar-miSideBar.php
get_sidebar('miSideBar')
```

**en sidebar-miSideBar.php**
```php
//Contenido de mi sidebar
<p>lalalalaa</p>
//Puedo meter un dynamic side bar si quiero
```php
dynamic_sidebar('nombre del side bar')
```

## Menues

### Colocar menu puntual
Los menues son listas editables en el admin para colocar links 
Podes colocar un menu especifico en el theme asi:

```php
//En el template colocas la ubicacion o directamente un menu
$args=[
	//si queres que sea un menu definido
	'menu'=>'nombre del menu, id, etc',
	'menu_class'=>'clase css para el <ul> de elementos',
	'container'=>true //colocar el menu en un div
	'container_class'=>'clase css para el container',
]
wp_nav_menu($args)
```


### Custom menu location

Los menues se muestran en ubicaciones de menu que se colocan en el theme y cuyo contenido se configura en el admin panel.


**Para crear una nueva ubicacion de menu:**
```php
//En functions.php, adosado a alguna funcion con un hook
register_nav_menus([
	'nombre'=>
])

//En el template colocas la ubicacion o directamente un menu
$args=[
	'theme_location'=>'nombre del theme location que definiste antes',
	'menu_class'=>'clase css para el <ul> de elementos',
	'container'=>true //colocar el menu en un div
	'container_class'=>'clase css para el container',
	
]
wp_nav_menu($args)
```

Una vez creado te figura en el wordpres admin


Ahora podes crear menues en el admin y asignarlos a esa ubicacion



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIzNTU5NTc1LDE4ODAzODQxNzYsLTY1Nj
E1NTkwMV19
-->