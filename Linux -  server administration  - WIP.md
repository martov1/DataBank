
**documentacion linux:**http://www.tldp.org/guides.html

**WARGAMES!:**http://overthewire.org/wargames/
**SERVER BUG SIMULATOR:**http://trouble-maker.sourceforge.net/

magnet link red hat sys admin
magnet:?xt=urn:btih:5ff1563ff871dd642eb45049404feadbde4ec6a8&dn=VTC-Red.Hat.Certified.System.Administrator.RHCSA-JAVAPSYCHE&tr=udp%3a%2f%2ftracker.leechers-paradise.org%3a6969&tr=udp%3a%2f%2fzer0day.ch%3a1337&tr=udp%3a%2f%2fopen.demonii.com%3a1337&tr=udp%3a%2f%2ftracker.coppersurfer.tk%3a6969&tr=udp%3a%2f%2fexodus.desync.com%3a6969

Magnet link red hat sys engineer
magnet:?xt=urn:btih:8e8a461a27dc401e9991f0d15980c4c1402c742a&dn=Red%20Hat%20Certified%20Engineer&tr=udp%3a%2f%2ftracker.leechers-paradise.org%3a6969&tr=udp%3a%2f%2fzer0day.ch%3a1337&tr=udp%3a%2f%2fopen.demonii.com%3a1337&tr=udp%3a%2f%2ftracker.coppersurfer.tk%3a6969&tr=udp%3a%2f%2fexodus.desync.com%3a6969

**Estoy usando este, esta copado:**
https://www.youtube.com/watch?v=c0HxEeLyXmM&list=PLjGbUPQu3fSR2wOhTD5on_BBJh2HlCEAQ


RED HAT SYSTEM ENGINEER
https://www.udemy.com/linux-academy-red-hat-certified-engineer-prep/

FILESISTEM STRUCTURE STANDARD
http://www.pathname.com/fhs/pub/fhs-2.3.html

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


## Environment variables y configuracion

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

### $PATH  environment variable

Es una variable del shell que contiene una **lista de directorios donde se buscaran los ejecutables de los comandos que tipeas** (EJ: ls, pwd, man, etc).

>Cuando tipeas un comando, se busca un archivo con el nombre de ese comando en los directorios de $PATH, la busqueda se hace en el orden en el que estan puestos los directorios.

**podes visualizarla haciendo:**
Los diferentes directorios quedan separados por **":"**

	[juan@host ~]$ echo $PATH
	/usr/local/bin:/bin:/usr/bin:/usr/local/sbin...

**Podes ver en que directorio de $PATH esta un comando haciendo:**

	[juan@host ~]$ which ls

### Ejecutar comandos fuera de $PATH

Si tenes un comando ejecutable en un directorio y queres llamar a ese comando:

	//Navegando hacia la carpeta y llamando el comando
	[juan@host ~]$ cd /mi/carpeta/loca
	[juan@host loca]$ ./miComando
	
	// Directamente llamando al comando con la ruta
	[juan@host ~]$ cd /mi/carpeta/loca miComando


### Archivos que modifican el environment

Hay una serie de archivos que se ejecutan en ciertos momentos para **modificar el environment del shell** para, por ejemplo, añadir una ruta al $PATH o para cualquier otra tarea administrativa 

**Apertura de un shell de inicio de sesion:**
* **/etc/profile**  -- modificable por root
	* Corre todos los scripts en **/etc/profile.d**    -- modificable por root
* **home/username/.bash_profile**   -- modificable por user
	* Corre el script **home/username/bashrc**  -- modificable por user

**Apertura de shells hijos del shell de inicio de sesion:**
* **home/username/.bashrc**  -- modificable por user
	* Corre el script **/etc/bashrc** -- modificable por root
 	* Corre todos los scripts en **/etc/profile.d**    -- modificable por root



>Cuando se dice que un usuario "inicia sesion" se habla de su bash madre (que puede instanciar bash hijos) a partir de la cual hace todo, aunque tengas una interfaz grafica esta corre encima de un bash shell

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

**el bit SETUID permite que un tercero ejecute un archivo binario con los permisos del usuario dueño delarchivo.** 
Generalmente este es ROOT y este permiso deja que un usuario ejecute un binario para realizar **una tarea especifica, como por ejemplo cambiar su contraseña**

El bit setuid reemplaza el bit execute **x** del usuario por el bit **s**, ya que cumple esa funcion tambien, es decir:
* Indica que el usuario puede ejecutar el archivo
* indica que cualquiera que ejecute el archivo lo hace como si fuese ese usuario

EJ:
```bash
-rwsr--r--. 1 juan ventas 36 feb 6 16:30 hola.txt 
```
Si **setuid** esta activado pero el archivo **no tiene permiso de ejecucion** (esto no tiene sentido, pero podria suceder) entonces aparece una S mayuscula
```bash
-rwSr--r--. 1 juan ventas 36 feb 6 16:30 hola.txt 
```


Se añade asi;

	chmod u+s /path/to/file
	chmod 4755 /path/to/file

Se remueve asi:

	chmod u-s /path/to/file
	chmod 0755 /path/to/file

### SETGUID - Permitir a terceros correr como grupo

De la misma manera que SETUID te permite ejecutar un archivo como si fueras el dueño del mismo, **SETGUID te permite ejecutar un archivo como si formaras parte del grupo del archivo** se indica con una **s** en el lugar de ejecucion de grupo

EJ:
```bash
-rwxr-sr--. 1 juan ventas 36 feb 6 16:30 hola.txt 
```

Si el permiso para ejecucion no esta colocado pero el SETGUID si (situacion que no tiene sentido practico) entonces el permiso se ve asi:
```bash
-rwxr-Sr--. 1 juan ventas 36 feb 6 16:30 hola.txt 
```

Se añade asi:

```bash
chmod g+s /path/to/file
```
Se saca asi:

```bash
chmod g-s /path/to/file
```



**CRITICO:**
> Colocar SETGID en una carpeta hace que **los nuevos archivos generados hereden ese grupo** y que los subdirectorios **hereden el permiso setgid**

### STICKY-BIT - evitar borrado o renombrado 

El sticky bit te permite **asegurarte que solo el owner y el root puedan borrar o renombrar un archivo/directorio**
De esta manera podes evitar que ciertos archivos sean renombrados o brrados si aunque los permisos del directorio lo permitan.

Se indica con una **t** en el permiso de ejecucion para terceros.

```bash
-rwxr-sr-t. 1 juan ventas 36 feb 6 16:30 hola.txt 
```

Si el sticky bit esta activado pero los terceros no tienen permiso de ejecucion, la T se hace mayuscula.
```bash
-rwxr-sr-T. 1 juan ventas 36 feb 6 16:30 hola.txt 
```

Para agregarlo:
```bash
chmod o+s /path/to/file
```
Para sacarlo:
```bash
chmod o-s /path/to/file
```

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

 	sudo -u "cuenta para apa che" comando


## Contenido default de la carpeta home

El contenido de la carpeta **/etc/skel** se copia en el nuevo directorio home del nuevo usuario

# Grupos 

## Donde se guardan

Los gurpos se guardan en **/etc/groups** con la siguiente configuracion. Los grupos pueden tener contraseñas pero esa funcionalidad no suele ser usada.

	group_name:password:GID:user1,user2,user..


## Groups - ver los grupos de un user

Podes ver a que grupos pertenece un usuario asi;

	groups usuario

## Administrar grupos

Podes **añadir** grupos con groupadd

	groupadd migrupo
Podes **borrar** grupos con groupadel

	groupdel migrupo
	
podes **modificar** el grupo con groupmod

	groupmod [opciones] migrupo
las opciones que podes usar son
 * **-g** cambia el GID del grupo
 * **-n** Renombra el grupo  

# Logging


## Estandar syslog

El logueo en linux funciona con un estandar y protocolo denominado **Syslog** que permite que **multiples aplicaciones dentro o fuera del server escriban en el log** permitiendo un **Logueo centralizado**

Los logs se categorizan por:

* **Facility** - Indica quien genero el log
	* 0 - Kernel (el kernel escribio en el log)
	* 1 - Usuario (el user escribio en el log)
	* 2 - Mail   (el mail sistem escribio)
	* 3 - daemon  (un sistem daemon)
	* 4 - auth (un mensaje realcionado con autorizacion/seguridad)
	* 5 - syslog (un mensaje interno de syslog)
	* 6 - lpr
	* 7 - news
	* 8 - uucp
	* 9 - clock
	* 10- authpriv
	* 11- ftp
	* **16 a 23** - **Libres para el uso que le quieras dar.**
* **Severidad** - Indica que tan severo es el mensaje
	*  0 - Emergency
	* 1 - Alert
	* ...
	* 7 - Debug

## Syslog server y su configuracion

El servidor Syslog toma los mensajes recibidos de otras aplicaciones dentro y fuera del servidor y los escribe en los logs teniendo en cuenta una serie de reglas. 

Existen multiples servidores para el protocolo Syslog, el mas comun es  **rsyslog** cuya configuracion se encuentra en **/etc/rsyslog.conf**

**CRITICO:**
>La configuracion default en **/etc/rsyslog.conf** tiene una directiva `include /etc/rsyslog.d`, implicando que cualquier archivo de configuracion en esa carpeta tambien se lee y se levanta.
**Esto permite a cualquier aplicacion del servidor escribir un archivo de configuracion para especificar como desea loguear sus mensajes (EJ mysql)**


* **Logging rules de rsyslog:**
La configuracion del servidor rsyslog se realiza agregando al archivo de configuracion:
	*  **selectores** - indican que se esta logueando
		* Se compone de **facility y severity**
		*  Varios selectores pueden llevar a la misma accion
	* **Acciones** - Indican como procesar ese log

**Estos se colocan de forma:**

> FACILITY.SEVERITY 	ACTION


EJ:
```bash
	#Facility mail y severidad emergency
     mail.emergency -var/logs/mail.log
     #Facility mail y cualquier severidad 
     mail.* -var/logs/mail.log
     #Facility kernel, severidades emergency y alert
     kernel.emergency;kernel.alert -var/logs/badnews.log
     #Todos los facilities salvo mail
     *.*;mail.none -var/log/general.log
     # Loguear mail y kernel con severity emergency}
     mail,kernel.emergency - var/log/unarchivo.log
```



## Loguear un mensaje

Podes pedirle al servidor syslog que loguee un mensaje en tu nombre con el comando 
```bash
	
	logger [-pt] message
```
**donde:**
* **p** - permite indicar **facility y severity**
	* Si no indicas ninguno se loguea como **user.notice** 
	`logger -p mail.info "el mensaje!"`
* **t** - indica un TAG
	* Te permite añadir un tag
	`logger -t untag "el mensaje!"` 

**EJ:**
```bash
	#Loguear un mensaje
	logger "mensaje!"
	#Loguear un mensaje indicando facility, severity y tag
	logger -p mail.info -t untag "el mensaje!"
```

## Rotacion de logs

Para no guardar logs eternamente (ya sea de syslog o cualquier otro) existe una aplicacion llamada **logrotate** que <u>**corre una vez al dia usando cron**</u> y  permite
* Que los logs lleguen a cierto tamaño
* Comprimir
* Dividir los logs en archivos por fecha
* Eliminar logs viejos


La configuracion de logrotate  suele encontrarse en **/etc/logrotate.conf**, ademas normalmente este archivo contiene la directiva `include /etc/logrotate.d`, esto implica que:

**CRITICO:**
> **Las aplicaciones que deseen loguear contenido colocan un archivo de configuracion para log rotate en /etc/logrotate.d** y si la configuracion de logrotate.conf es la estandar entonces **se levantaran esas configuraciones**.


**Directivas para configurar logrotate**
* **weekly** - Rota los logs semanalmente
* **rotate 4** - Guardar 4 semanas de logs, borra aquellos mas viejos
* **create** - Crear archivo nuevo cuando se rote el log
* **compress** - Comprimir logs

**Se usan indicando el archivo al cual se aplican:**

```
/home/miAplicacion/*.log
{
	weekly
	rotate 4
}
/var/log/mail
{
	weekly
	rotate 2
}

```




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

 
 
# Shell scripting

Los script shells son una manera de automatizar lo que se puede hacer en la consola


### Seleccion de interprete

Para seleccionar un interprete para el script usas la sintaxis

```bash
    #!/path/al/interprete
    #!/usr/bin/python
    #!/bin/csh
    #!/bin/ksh
 ```
 
### Variables

Las variables se declaran de la siguiente manera: 
```bash
MI_VARIABLE="pan de salvado"
#Guardar el output de un comando en una variable
MI_VARIABLE = $(MiComando)
```
**Es importante que:**
* No haya espacios de ninguno de los lados del igual
* Los nombres van en mayusculas por convencion
* No empezar el nombre de la variable con un nuemro
* No usar **@** o **-**
Para usar una variable:
```bash
#Hay dos formas, la segunda no te deja poner algo inmediatamente despues del nombre de la variable, en este caso la coma.
echo "me gusta el ${MI_VARIABLE}, es riquisimo"
echo "me gusta el $MI_VARIABLE , es riquisimo"
```

### Tests

Los tests te permiten ejercer logica condicional para tomar una decision.
**Los tests deben colocarse entre corchetes**

```bash
#Checkeo existencia de archivo
if [ -e /etc/passwd] then
#Hago cosas!
else
#otras cosas

elif [ OTRO TEST ]
fi
```

**Tests de filesystem:**
* **-d** True si el archivo es un directorio
* **-e** True si el archivo existe
* **-f** true si el archivo existe y no es un directiorio
* **-r** True si el script tiene permisos para leer el archivo
* **-s** True si el archivo existe y no esta vacio
* **-w** True si el script tiene permisos para escribir el archivo
* **-x** True si el script tiene permisos para ejecutar el archivo 

**Tests de strings:**
* **-z** True si el strng esta vacio
* **-n** true si el string no esta vacio
* **string1 = string2** true si los strings son iguales
* **string1 != string2** true si los strings no son iguales

**Tests de numberos:**
* **10 -eq 20** True si son iguales
* **10 -ne 20**  True si no son iguales
* **10 -lt 20** True si 10 es less than 20
* **10 -le 20** True si 10 es less than or equal to 20
* **10 -gt 20** true si greater than
* **10 ge 20** true si greater or equal

### Loops

Podes hacer un loop asi

```bash
for COLOR in ROJO AZUL NEGRO
	echo $COLOR
done
```

### Parametros

Tu script puede aceptar parametros del usuario cuando se lo invoca.
Los parametros se obtienen con **$0, $1, $2, etc** para el primer argumento, segundo y asi sucesivamente

Para obtener un array de parametros (ej para iterarlo en un loop) podes usar **$@**

```bash
echo "el primer parametro es $1"
echo "todos los parametros $@"
```


### Interceptar STDIN

Podes interceptar el **standard input** del usuario o de otro comando, por ejemplo si queres que el usuario escriba algo durante la ejecucion del script.

Podes interceptar el input y guardarlo en una variable asi:

```bash
	read -p "indique el usuario:" MI_VARIABLE
	echo "el usuario es: $MI_VARIABLE"
```

# SystemD
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU3OTQyMTU4MCw1MDk1NTEyMSwxMzcyMT
AwMzIyLDc0OTMzMzE1MCwyNTk2NTMzNDAsNjcyOTk2MTIwLC03
MjAyMDUyMjYsLTI2MTEwNDEwNSwxNTc1MTk0ODUwLDQ2Mzk5Nz
U2MCwxOTY3NjQzNDY0LDEyMjA3NjI1OTIsMTczNDE0NzQ2OSwt
ODcyNDQxNzMsLTM0MDk5OTIxNCwtMjA0NzQzNDgzNywtMjA0Nj
A0OTE3MiwxOTA5OTM0MTcyLC0xMTU0MDcwMTMsMzA2MjA3NDM3
XX0=
-->