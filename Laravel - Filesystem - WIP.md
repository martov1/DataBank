

# Contenido


* Intro




# Intro

Los filesystems estan abstraidos de tal manera que podes cambiar de uno a otro y mantener el resto del codigo igual.

Los filesstems configurados estan en **config/filesystem.php** y se los denomina **disks**, cada disk determina:
* Un storage driver
* Una ubicacion en ese storage driver
* Las credenciales del storage driver, si las hubiere


# Local driver

## Public disk

El public disk esta ubicado en **storage/app/public** y usa el **local driver**, esta diseñado para aquellos datos que deben ser de acceso publico.

**para activarlo hay que crear un symbolic link en la carpeta public/storage**

Esto se puede automatizar con

	php artisan storage:link


**Podes generar una URL de un archivo en el public disk asi:**
```php
$url= asset('storage/file.txt');
```

# manipular archivos

* Para guardar un archivo en **storage/path**  usando el **local drive**
```php
		Storage::disk('DRIVE')->put('file.txt', 'Contents');
```
* Para obtener un archivo hacer
```php
		Storage::disk('DRIVE')->get('file.txt');
```
* Para verificar existencia haces
```php
		$exists = Storage::disk('DRIVE')->exists('file.jpg');
```
* Para forzar una descarga para el usuario, haces
	```	
		return Storage::download('file.jpg');
	
		return Storage::download('file.jpg', $name, $headers);

* Para obtener una URL haces
			$url = Storage::url('file.jpg');

* Para obtener una URL temporal haces
		 $url = Storage::temporaryUrl(
    		'file.jpg', now()->addMinutes(5)
		);
* Obtener metadata
		$time = Storage::lastModified('file.jpg');
		$size = Storage::size('file.jpg');
* Prepend y append a archivos
		Storage::prepend('file.log', 'Prepended Text');
		
		Storage::append('file.log', 'Appended Text');
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjM5NzM0NzVdfQ==
-->