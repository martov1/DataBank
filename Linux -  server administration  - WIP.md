
ver https://www.udemy.com/linux-administration-bootcamp/

ver https://www.youtube.com/watch?v=bju_FdCo42w&list=PLtK75qxsQaMLZSo7KL-PmiRarU7hrpnwK

**Me quede en:** 013 Getting Help at the Command Line

# Directory structure

* **/** - Root, la parte superior del file sistem
	*  **/bin** - Binaries y otros executables
	* **/etc** - Archivos de configuracion
	* **/home** - Contiene los archivos de los usuarios
		* **/user1**
		* **/user2**
	*   **/opt** - Programas opcionales o third party (EJ: google maps)
	* **/tmp**  - Archivos temporales, generalmente borrados en el reboot
	* **/usr** - programas relacionados con el usuario
		* **/local**
			* **/nombreDePrograma** - carpeta de un programa  
	* **/var** - Datos que varian mucho, ej; Logs
	* **/boot** - Archivos necesarios para bootear
	* **/cdrom** - Mount point para cd-roms
	* **/dev** - device files


# Command line

## User y super user
la Shell o command line tiene dos modos de funcionamiento

* **Usuario normal:**
El usuario con privilegios normales suele tenes un prompt terminando con un **$**

	    [usuario@hostname: ] $

* **Super usuario**
	El super user o admin en general tiene su prompt terminando con un **#**
	
	    [usuario@hostname: ] #

## Tilde (~) expansion

Muchos sistemas usan **~** para simbolizar subdirectorios de usuarios.
Los usuarios no necesariamente son humanos, por ejemplo puede ser que exista un usuario para un servidor FTP y su directortorio este en `/srv/ftp`

* `~jason` = /home/jason
* `~pat` =/home/pat
* `~root` =/root
* `~ftp` = /srv/ftp


## Commands

* **ls** - Lista el contenido del directorio
* **pwd** - Muestra el directorio actual
* **cat** - Muestra el contenido de archivos
* **echo** 
* **man** - Muestra el manual online
	* **man -k busqueda**  - Podes buscar cosas en las man pages
* **clear** - Despeja la consola
* **exit** - Cierra el shell o la sesion actual

## $PATH  environment variable

Es una variable del shell que contiene una **lista de directorios donde se buscaran los ejecutables de los comandos que tipeas** (EJ: ls, pwd, man, etc).

>Cuando tipeas un comando, se busca un archivo con el nombre de ese comando en los directorios de $PATH, la busqueda se hace en el orden en el que estan puestos los directorios.

**podes visualizarla haciendo:**
Los diferentes directorios quedan separados por **":"**

	echo $PATH
	/usr/local/bin:/bin:/usr/bin:/usr/local/sbin...

**Podes ver en que directorio de $PATH esta un comando haciendo:**

	which ls


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM4NTE2OTUyNywxNzAxNzQ5MDI5LDE2MD
c4MzU2ODcsMzM3NzU4MTYxLDE0NDg3OTU0OThdfQ==
-->