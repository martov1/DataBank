
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

## Simbologia del command prompt

### User y super user
la Shell o command line tiene dos modos de funcionamiento

* **Usuario normal:**
El usuario con privilegios normales suele tenes un prompt terminando con un **$**

	    [usuario@hostname: ] $

* **Super usuario**
	El super user o admin en general tiene su prompt terminando con un **#**
	
	    [usuario@hostname: ] #

### Tilde (~) expansion en el prompt

Muchos sistemas usan **~** para simbolizar **el directorio del usuario**.
Los usuarios no necesariamente son humanos, por ejemplo puede ser que exista un usuario para un servidor FTP y su directortorio este en `/srv/ftp`

* `~jason` = /home/jason
* `~pat` =/home/pat
* `~root` =/root
* `~ftp` = /srv/ftp

Cuando cambias de directorio muchas veces se muestra el directorio en referencia a la posicion de **~**

	[juan@host ~]$ pwd
	/home/juan
	[juan@host ~]$ cd musica
	[juan@host musica]$ pwd
	/home/juan/musica

## Commands mas comunes

* **ls** - Lista el contenido del directorio
* **pwd** - Muestra el directorio actual
* **cat** - Muestra el contenido de archivos
* **echo** 
* **man** - Muestra el manual online
	* **man -k busqueda**  - Podes buscar cosas en las man pages
* **clear** - Despeja la consola
* **exit** - Cierra el shell o la sesion actual
* **mkdir nombre** - crea un directorio con ese nombre
	* **mkdir -p /crear/estas/carpetas** - crea una serie de directiorios anidados
* **rm -rf** - Borra recursivamente un directorio

## $PATH  environment variable

Es una variable del shell que contiene una **lista de directorios donde se buscaran los ejecutables de los comandos que tipeas** (EJ: ls, pwd, man, etc).

>Cuando tipeas un comando, se busca un archivo con el nombre de ese comando en los directorios de $PATH, la busqueda se hace en el orden en el que estan puestos los directorios.

**podes visualizarla haciendo:**
Los diferentes directorios quedan separados por **":"**

	[juan@host ~]$ echo $PATH
	/usr/local/bin:/bin:/usr/bin:/usr/local/sbin...

**Podes ver en que directorio de $PATH esta un comando haciendo:**

	[juan@host ~]$ which ls

## Ejecutar comandos fuera de $PATH

Si tenes un comando ejecutable en un directorio y queres llamar a ese comando:

	//Navegando hacia la carpeta y llamando el comando
	[juan@host ~]$ cd /mi/carpeta/loca
	[juan@host loca]$ ./miComando
	
	// Directamente llamando al comando con la ruta
	[juan@host ~]$ cd /mi/carpeta/loca miComando
<!--stackedit_data:
eyJoaXN0b3J5IjpbODE4Njk5MTI0LDIwMzg2Mjc0ODUsLTEyNj
U0OTAwNDksLTIwMDU0OTk4NDIsLTU0ODUwMjkwNCwtNDk5NDgy
NzE4LDE3MDE3NDkwMjksMTYwNzgzNTY4NywzMzc3NTgxNjEsMT
Q0ODc5NTQ5OF19
-->