
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
	* **ls -l** muestra informacion detallada del directorio 
	* **ls -t** lista archivos en orden temporal
	* **ls --color** muestra la informacion con colores
	* **ls -r** Muestra archivos en orden inverso 
	* **ls -R** muestra el contenido de el direcotorio y todos los subdirectorios
	* **ls  -F** - Muestra el type de cada archivo
		* @ system link
		* / directorio
		* \*  Ejecutable
* **tree** - como ls -R pero muestra los archivos y carpetas de forma grafica
	* **tree -d** muestra solo las carpetas en el arbol
	* **tree -C** muestra el arbol con colores 
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



# File system

## Hidden files

Los **archivos que comienzan con un punto** se consideran archivos ocultos, y no son mostrados por default.

Para mostrar archivos ocultos podes hacer
		
	[juan@host ~]$ ls -a
	.oculto.doc noOculto.doc

## Symbolic links

* Son pointers que apuntan a un archivo o directorio.
* A los usos practicos actuan como si fueran el archivo o directorio

## Permissions

### read, write, execute
Los permisos tienen la siguiente simbologia


| Simbolo | Permiso | Archivo              | Directorio                                                                                                                               |
|---------|---------|----------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| r       | Read    | Leer el archivo      | Leer los nombres de los archivos en el dir                                                                                               |
| w       | Write   | Modificar el archivo | Crear, renombrar, borrar archvos en el dir                                                                                               |
| x       | Execute | Ejecutar el archivo  | hacer cd al directorio, traversearlo, leer el contenido (sin r o w lo estas haciendo a ciegas y tenes que saber los nombres de antemano) |

EJ:
```
$ mkdir -p dir/
$ echo 'Hello World!' > dir/file
$ chmod 000 dir/
$ ls -al dir/
ls: cannot open directory dir: Permission denied
$ cat dir/file
cat: dir/file: Permission denied
$ chmod +x dir/
$ ls -al dir/
ls: cannot open directory dir: Permission denied
$ cat dir/file
Hello World!
```

### Permission categories

los permisos (read, write, execute) se pueden asignar a diferentes categorias, por ejemplo a **usuarios, grupos, etc**

> Todos los usuarios pertenecen a por lo menos una categoria

**Las categorias son:**

| Simbolo | Categoria |
|---------|-----------|
| u       | User      |
| g       | Group     |
| o       | Other     |
| a       | all       |



**Para ver los grupos disponibles en el equipo podes hacer:**
	
	groups

### Permission string

Cuando haces **ls -l** para ver la info detallada de un directorio, te muestra el string de permisos

![enter image description here](https://lh3.googleusercontent.com/qRlC-MV-z7E_q38W_5hG52Nq6oMs6sk-t_MnPMvKmQXrgUX1leW1q5ZYdp9yVoxkoxk-tM8worRX)

Consiste en
* **type** el tipo de archivo
	* **@** link
	* **\*** executable
	* **/** directory 
* **User** Los permisos del usuario actual
* **group** - Los permisos del grupo al que el usuario pertenece
* **other** - Los permisos disponibles para todos los usuarios 

### chmod 

el comando chmod te permite **cambiar los permisos de un archivo**


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ5MDA3NTg3OCw2NzI1MzI3OSwxMTY2Nz
I2ODk2LDE4MTU1NjE1Niw2OTg3NDgwNjQsLTE5NTM5ODYwMzUs
LTEwNzcyMDg0MjIsNjkxNTc1Nzg2LDc3MDg3MzY0Nyw4MTg2OT
kxMjQsMjAzODYyNzQ4NSwtMTI2NTQ5MDA0OSwtMjAwNTQ5OTg0
MiwtNTQ4NTAyOTA0LC00OTk0ODI3MTgsMTcwMTc0OTAyOSwxNj
A3ODM1Njg3LDMzNzc1ODE2MSwxNDQ4Nzk1NDk4XX0=
-->