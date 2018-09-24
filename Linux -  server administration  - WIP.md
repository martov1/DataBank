
ver https://www.udemy.com/linux-administration-bootcamp/

ver https://www.youtube.com/watch?v=bju_FdCo42w&list=PLtK75qxsQaMLZSo7KL-PmiRarU7hrpnwK

**Me quede en:** 
051 SPECIAL PERMISSIONS 
040 System Logging
				

**VER:**
* 018 Finding Files and Directories
* 019 Viewing Files and the Nano Editor  


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
* **cp** - Copia archivos

## Environment variables

### Ver las environment variables

* Podes **Listar** todas las environment variables con **printenv**, las environment variablles determinan el comportamiento del shell y del sistema.
	```
	[juan@host ~]$ printenv
	```
* Podes **Leer** una environment variable usando **$nombreDeLaVariable**
	```
	[juan@host ~]$ echo $home
	```
 ### Crear environment variables

Para crear una environment variable, haces

```bash
	export MIVARIABLE="el valor"
 ```

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

## I/O redirection

Podes redirigir la entrada y la salida de los comandos de consola hacia o desde archivos.

### Tipos de I/O

| Nombre          | Abreviacion | Descriptor | Descripcion                               |
|-----------------|-------------|------------|-------------------------------------------|
| Standard Input  | stdin       | 0          | Lo que entra al  command                  |
| Standard Output | stdout      | 1          | Lo que sale del  command si no hubo error |
| Standard Error  | stderr      | 2          | Lo que sale del  command si hubo  error   |

### Redireccion en la CLI

Podes redirigir el input y output usando los siguientes operadores

* **>** - manda el output a un file sobreescribiendolo
* **>>** - Redirigir el output a un file agregandolo a lo existente
* **<** - Utiliza un archivo como input de un command
* **&** - Indicar que estas usando un descriptor

EJ:


```
# enviar el output al final de un archivo
ls >> files.txt

#usar un archivo para alimentar el comando
sort < cosas.txt

#Enviar los errores a un archivo usando el file descriptor
ls 2> error.txt

#Enviar los errores a un archivo y el output a otro
ls 1> resultado.txt 2> error.txt

#Enviar los errores a la nada misma
ls 2>/dev/null
```

### Pipe |

Pipe te permite pasarle el output de un command al input de otro, por ejemplo 



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
```bash
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

### chmod - Cambiar permisos

el comando chmod te permite **cambiar los permisos de un archivo**

> * Solo **el propietario del archivo** y el **root** pueden cambiar los permisos de un archivo.
> * Solo el **root** puede cambiar el **propietario o grupo de un archivo**


| Parametro  | posible valor                        |
|------------|--------------------------------------|
| categoria  | u - User g - group o - other a - all |
| Accion     | + añade permisos - elimina permisos = elimina todos los permisos y los suplanta por estos |
| permiso    | r - read w - Write x - Execute       |
| file o dir | hola.txt                             |


**EJ:**
Le permito a todos leer y ejecutar pero no editar
		
	chmod ugoa +xr-w miArchivo

le permito al usuario leer, escribir y ejecutar, al grupo solo leer

	chmod u+xwr,g-r miArchivo
	
Le asigno al usuario unicamente permiso de lectura, le saco cualquier otro permiso a ese usuario si lo hubiere

	chmod u=r miArchivo


**Modo octal:**
Los permisos son simbolizados con 3 bits, se traducen a modo octal asi:

![enter image description here](https://lh3.googleusercontent.com/I5WOJE3-5Ur3XMTEysjc8A3VF3Joqesd8dBMu5JgKgwu8lNRVxMJw1fu-PzSRxEAlwwyzURPjFme)

Cada permiso octal que coloques con chmod esta sinendo asignado a User, Group y Other en ese orden

**EJ:**
Le asigno **todos los permisos al user**, **permiso de lectura y escritura al grupo** y **permiso de solo lectura a otros**.

	chmod 754 hola.txt

### chgrp - Cambiar grupo

Todos los archivos en general pertenecen a algun grupo, los usuarios son simepre **miembros de un grupo con su mismo nombre**, llamado tambien **primary group**

Vemos como este archivo esta en el grupo "juan"

 ```bash
	[juan@host ~]$ ls -l hola.txt
	-rw-r--r--. 1 juan 36 feb 6 16:30 hola.txt
```
Si queres cambiarle el grupo a algun archivo, podes hacerlo con **chgrp**

	[juan@host ~]$ chgrp ventas hola.txt
	[juan@host ~]$ ls -l hola.txt
	-rw-r--r--. 1 juan ventas 36 feb 6 16:30 hola.txt 


### chown - Cambiar owner

Podes cambiar el propietario del owner de un archivo siendo **root**

	chown miUser elArchivo.txt

### SETUID	- Permitir a terceros ejecutar como el dueño

el bit SETUID permite que un tercero ejecute un archivo binario con los permisos del usuario dueño del
archivo. Generalmente este es ROOT y este permiso deja que un usuario ejecute un binario para realizar **una tarea especifica, como por ejemplo cambiar su contraseña**

El bit setuid reemplaza el bit execute **x** del usuario por el bit **s**, ya que cumple esa funcion tambien, es decir:
* Indica que el usuario puede ejecutar el archivo
* indica que cualquiera que ejecute el archivo lo hace como si fuese ese usuario

EJ:
```bash
-rwsr--r--. 1 juan ventas 36 feb 6 16:30 hola.txt 
```

Se añade asi;

	chmod u+s /path/to/file
	chmod 4755 /path/to/file

Se remueve asi:


Se añade asi;

	chmod u-s /path/to/file
	chmod 0755 /path/to/file


## Busqueda en el filesystem


### FIND - buscar un archivo o directorio

Se usa asi:

```bash
	find PATH PATTERN
```
 **Opciones:**
 * **-name patron** : Busca archivos y directorios con nombre que matchee ese patron 
 * **-iname patron** : igual que name pero es case-insensitive
* **-ls** : hace un ls en la ubicacion de cada elemento encontrado
* -**-mtime numero** : Buscar por **m** odification **time** en dias
* **-size numero** : Buscar archivos de tamaño num
* **newer archivo** : Busca archivos mas nuevos que el archivo provisto
* **-exec command {}\;** : ejecuta un comando sobre cada archivo encontrado 

### LOCATE - buscar un archivo o directorio

Es una alternativa mas rapida a FIND, funciona con un indice interno de linux que es reconstruido una serie de veces por dia, entonces **Los resultados provistos pueden estar desactualizados**

### GREP - Buscar dentro de un archivo

Grep te permite encontrar cosas dentro de un archivo
parametros:
* **-i** - Case insentive
* **-c** - Contar la cantidad de ocurrencias
* **-n** - Cada match viene precedido del line number donde se encuentra
* **v** - Buscar aquellas lineas que NO coinciden con el patron de busqueda
Se usa asi

```bash
grep -u "mi Patron De Busqueda" miArchivo.txt
```

**Devuelve la linea donde se encontro la ocurrencia**


# Process and job control

 
### Ver procesos - PS
Para ver los procesos usamos el comando **ps** con los siguientes **parametros:**
* **-e** - Mostrar todos los procesos
* **-H** - Mostrar procesos como arbol
* **-f** - mostrar mas informacion
* **-u usuario** - Mostrar los procesos de un usuario en particular
* **-p pid** - mostrar informaciond de un proceso por PID

### Ver procesos - top
Es un visor de procesos interactivo que coloca los procesos con mas consumo de CPU arriba

## Background y foreground processes

* **matar un proceso en foreground** - Ctrl C
* **suspender un proceso en foreground** - Ctrl Z
* **Para enviar un command al background** lo invocas con **&**
	```
    [juan@host ~]$miComando &
    # Responde con job number y PID
    [1] 2375
	```
* **Para mandar al foreground un proceso en background** usas el comando **fg**
	```
    [juan@host ~]fg %1
    procesando en foreground!
	```
* **Para ver los procesos enviados al background** usas el comando **jobs** que muestra el job con su jobId
	```
    [juan@host ~]jobs
    [1] running 	PATH/PATH/PATH
    [2] running 	PATH/PATH/PATH
    [.] running 	PATH/PATH/PATH
	```
* **para mandar al background un proceso suspendido** usas el comando **bg**
	```
    [juan@host ~]$miComando
    Procesando ...   ->Ctrl Z
    [juan@host ~]jobs
    [1] Stopped 	./miComando
    [juan@host ~]bg %1
    [juan@host ~]jobs
    [1] Running	./miComando
	```
## Process control

### kill
Kill mata un proceso, puede matarlo usando diferentes señales, algunas son mas elegantes que otras.
* La señal **15 - SIGTERM** es relativamente elegante y permite que el proceso se finalice de forma normal. es el que se usa de forma default
* La señal **9 - SIGKILL** mata el proceso de forma inmediata, se usa cuando un proceso no esta finalizando de forma normal

**Se usan asi:**

    #Matar elegantemente un proceso con PID 432
    kill -15 432

## Cron

### Crear cron jobs
Cron es un servicio que se ejecuta cada minuto y su funcion es correr ciertos comandos en un momento especifico. 

Para hacer uso de **cron** para realizar tareas automaticamente de forma programada podemos hacer lo siguiente.

**MES HORA DIA AÑO DIADELASEMANA** COMANDO

ej:
	
	#Correr ls en el minuto cero, a las 7AM todos los dias del mes, todos los meses, los martes
	0 7 * * 1 ls

Podes indicar que queres **correr el comando varias veces** usando una **coma**
	
	#Correr el comando en todos los minutos 0 y 30 de cada hora
	0,30 * * * * ls

Podes indicar **intervalor** con **-**

	#Correr el comando una vez por hora entre las 5AM y 7AM
	0 5-7 * * * ls

### administrar cron jobs - crontab

Crontab te permite administrar los trabajos cron, posee los siguientes parametros.
* **-l** Lista los cron jobs
* **-e** edita los cron jobs
* **-r** elimina todos los cron jobs
* **archivo** Crea un cron job a partir de un archivo


# Usuarios

## Usuarios y donde se guardan
Los usuarios siempre tienen

* **Username**
* **User ID (UID)**
	* El root siempre es UID 0 
* **Grupo default**
	* El grupo al que pertenecen los archivos creados por el user 
* **Comentarios**
* **Shell**
	* Lo que se ejecuta cuando el usuario se loguea, no necesariamente tiene que ser un shell, puede ser un programa no interactivo 
* **Un home directory**

**Todos estos datos se guardan en /etc/passwd** de la siguiente manera

	username:password:UID:GID:comments:home_dir:shell
Las contraseñas actualmente se guardan en el _**shadow file**_ ubicado en **/etc/shadow** de manera encriptada.

## SU - Cambiar de usuario

Para cambiar de usuario podes hacer lo siguiente

	su nombreDeUsuario

Si no provees un nombre de usuario entonces linux intenta loguearte en el root.

Tambien podes correr un comando particular como un usuari

		su nombreDeUsuario -c miComando

**Podes usar un guion para indicar que queres usar el environment de ese usuario tambien**

## SUDO - usar root o correr algo como otro usuario

Podes usar SUDO para correr un comando como root

	sudo comando

Tambien podes correr un comando como si fueras un tercero

	sudo -u elusuario comando

o entrar al shell de un tercero

	sudo -u usuario -s

## Administrar usuarios

Podes **añadir usuarios** con **useradd** y colocar una contraseña con **passwd**, esto requirer siempre permisos de **root**

	useradd opciones username
	passwd username
	
Algunas opciones son
* **-c "comentario"** - añade un comment
* **-m** - Crea el home directory
* **-d** - especifica el path del directorio home
* **-s /shell/path** - especifica el shell, puede ser un programa cualquiera
* **-g** - coloca el grupo default
* **-G grupo1,grupo2** - grupos adicionales
* **-r** Indica que es una cuenta de sistema (no para usarse por un humano)
EJ:

	[juan@host ~] useradd -c "oficinista" -m -s /bin/bash miUsuario -g grupo1 -G grupo2,grupo3
	[juan@host ~] passwd miUsuario
	Enter new password:

## Cuentas de aplicacion o de sistema

No todas las cuentas son para ser usadas por usuarios, muchas son simplemente para correr aplicaciones o servidores (como apache)

Para eso podes crear una cuenta que no tenga shell

	useradd -c "cuenta para apache" -d /opt/apache -r -s /usr/sbin/nologin usuarioParaApache

Una vez que hiciste eso, podrias arrancar un programa bajo los permisos de ese usuario usando **SU o SUDO**

 	sudo -u "cuenta para apache" comando


## Contenido default de la carpeta home

El contenido de la carpeta **/etc/skel** se copia en el nuevo directorio home del nuevo usuario

# Grupos 

## Donde se guardan

Los gurpos se guardan en **/etc/groups** con la siguiente configuracion. Los grupos pueden tener contraseñas pero esa funcionalidad no suele ser usada.

	group_name:password:GID:user1,user2,user..






# Logging - WIP

**ver:** 040 System Logging

# Disk management


Las particiones y todos los medios de almacenamiento se montan debajo de **/**, aunque **podes montar particiones en cualquier lugar del file system, tambien pueden estar anidados en otras particiones**


### Ver dispositivos

Para ver los dispositivos de almacenamiento y como estan particionados podes hacer 

	fdisk -l

### Editar  o crear una particion

Para editar una particion tenes que llamar al comando fdisk con la ruta de un dispositivo

	[root@tecmint ~]# fdisk /dev/sda

Esto habilita el _command mode_ donde podes hacer lo que quieras

* a   toggle a bootable flag
* b   edit bsd disklabel
* c   toggle the dos compatibility flag
* d   delete a partition
* l   list known partition types
* m   print this menu
* n   add a new partition
* o   create a new empty DOS partition table
* p   print the partition table
* q   quit without saving changes
* s  create a new empty Sun disklabel
* t   change a partition's system id
* u   change display/entry units
* v   verify the partition table
* w   write table to disk and exit
* x   extra functionality (experts only)

### Crear filesystem

Una vez que tenes una particion, podes formatearla con un sistema de archivos con la utilidad **M**a**k**e **F**ile **S**istem o **mkfs**

	mkfs -t formato dispositivo
	#ej
	mkfs -t ext3 /dev/sdb2

Detras de escena MKFS crea las particiones usando los scripts en **/sbin/** por ejemplo
**/sbin/mkfs**
**/sbin/mkfs.ext2**
**/sbin/mkfs.ext3**
**/sbin/mkfs.minix**

### Montar dispositivos


Podes ver todo aquello que esta montado asi
	
	mount
	
Podes montar dispositivos por la duracion de la sesion asi:

	mount DEVICE MOUNT_POINT
	mount /dev/sdb3 /opt

Para que un dispositivo quede montado permanentemente despues de reiniciar, tenes que agregar una entrada en el archivo **/etc/fstab**

 
 

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk4MzIxNDUwLDQzNDY2OTEyNiwtNTMyND
A0NDI5LDE5OTMyMDA4MjcsLTE2MjUxNTQ2MjcsLTczMzY5NTA1
Niw3OTIyNTYwMTQsLTEwODkwMjIxMDEsMTQ3NzU1NDcyOCw0OT
kwMzUsMTQyNDA0NTU4MCw1NDgxNDAwNjEsLTM5NTQ1MDk1OCwx
ODc2MzQ1NDUzLDE3NTY4ODI1MDcsMTAwMzIzMTA5NCwyMDc5MT
YwMTk0LC04MDcyOTgyNzQsNjI3MDg1MTk2LDE4NjE1MTg1NDdd
fQ==
-->