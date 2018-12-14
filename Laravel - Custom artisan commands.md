

# Comandos default

* php artisan list - Muestra lista de los comandos disponibles


## Custom commands

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


### Inputs

Los inputs se definen en el signature

```php
protected $signature = 'mi:command {argument1} {argumentOpcional?} {argumentOpcionalcondefautl=hola} {--opcionTrueFalse} {--opcionConValor=default}' ;
```

#### Arguments y options

Los **Arguments** Van despues del comando, pueden ser

**Requeridos:** `- {argument1}`
**Opcionales:** `{argumentOpcional?}` 
**Opcionales con default:** `{argumentOpcionalcondefautl=hola}`

Las **Opciones** van despues del argument

**Booleana:** `{--opcionTrueFalse}`
**con valor:** `{--opcionConValor=default}` 

#### Input de varios datos

Podes expectear que te coloquen N datos y obtenerlos como un array.

```php
email:send {user*}
```

Entonces el usuario puede colocar N parametros foo bar
```php
php artisan email:send foo bar
```
y obtenes `['foo', 'bar']`:

```php
email:send {user} {--id=*}

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTQzNDIxMDgsLTY0NzU0NzQwNSw5Nj
UzNDA3MTAsMTk4Nzk1OTYyMCw3MzA5OTgxMTZdfQ==
-->