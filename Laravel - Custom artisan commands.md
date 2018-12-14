

# Comandos default

* php artisan list - Muestra lista de los comandos disponibles


# Custom commands

Para crear un custom command haces:

```php
php artisan make:command SendEmails
```

El comando creado tiene las siguientes caracteristicas.
```php
class nombreDe Command extends Command
{
	//Signature para mostrar en php artisan list
    protected $signature = 'mi:command {argument1} {argumentOpcional?} {argumentOpcionalcondefautl=hola} {--opcionTrueFalse} {--opcionConValor=default}' ;
	//Descripcion para el user
    protected $description = 'Send drip e-mails to a user';
    //Constructor del command
    public function __construct(DripEmailer $drip)
    {
        parent::__construct();
        $this->drip = $drip;
    }
    //La funcion que se ejecuta 
    public function handle()
    {
        $this->drip->send(User::find($this->argument('user')));
    }
}
```


## Inputs

Los inputs se definen en el signature

```php
protected $signature = 'mi:command {argument1} {argumentOpcional?} {argumentOpcionalcondefautl=hola} {--opcionTrueFalse} {--opcionConValor=default}' ;
```


### Arguments y options

Los **Arguments** Van despues del comando, pueden ser

**Requeridos:** `- {argument1}`
**Opcionales:** `{argumentOpcional?}` 
**Opcionales con default:** `{argumentOpcionalcondefautl=hola}`

Las **Opciones** van despues del argument

**Booleana:** `{--opcionTrueFalse}`
**con valor:** `{--opcionConValor=default}` 


Para **leer las opciones y argumentos colocados haces:**


Y los lees asi:

```php
public function handle()
{
	//leo mi argumento
    $userId = $this->argument('miArgumento');
    //Leo todos los argumentos como array
	$arguments = $this->arguments();
	
    //Leo mi opcion
	$queueName = $this->option('miOpcion');
	//Leo todas las opciones como array
	$options = $this->options();
}
```
### Input de varios datos

Podes expectear que te coloquen N datos y obtenerlos como un array.

```php
email:send {user*}
```

Entonces el usuario puede colocar N parametros foo bar
```php
php artisan email:send foo bar
```
y obtenes en tu funcion la variable $user con el valor
`['foo', 'bar']`:

Tambien podria ser una opcion con N valores
```php
email:send {user} {--id=*}

//El usuario coloca
php artisan email:send --id=1 --id=2
```

### Documentar opciones

Podes documentar tus opciones asi.
```php
email:send  {user : Mi descripcion}
```

### Prompts al usuario

* Podes **pedirle un input al usuario asi**
```php
public function handle()
{
    $name = $this->ask('What is your name?');
}
```
* Si necesitas que la opcion sea **secreta** (no se muestre en la pantalla, como una pass)

```php
$password = $this->secret('What is the password?');
```


* Si necesitas pedir **confirmacion**

```php
if ($this->confirm('Do you wish to continue?')) {
    //
}
```

* Si necesitas **Multiple choice**
```php
$name = $this->choice('What is your name?',
 ['Taylor', 'Dayle'], $defaultIndex);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NDEwNjUwOTEsLTEyNjk0NjAzNjUsMT
I3NzgxNjIxNSwtMjE4OTQ2MDQ3LC0xMDEwNDI3NTIsLTY0NzU0
NzQwNSw5NjUzNDA3MTAsMTk4Nzk1OTYyMCw3MzA5OTgxMTZdfQ
==
-->