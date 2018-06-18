

# Contenido






# Intro

La funcion **URL()** te permite generar URLs para la aplicacion.
```php
	echo url("/posts/{$post->id}");
	
	// http://example.com/posts/1
```
# Obtener datos de la URL actual

```php
	// Get the current URL without the query string...
	echo url()->current();
	
	// Get the current URL including the query string...
	echo url()->full();
	
	// Get the full URL for the previous request...
	echo url()->previous();
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkxNDQxMjM0OV19
-->