

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
    protected $signature = 'mi:command {argument1} {argumentOpcional?} {argumentOpcionalcondefautl=hola} {--opcionTrueFalse} {--opcionConValor=}' ;
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgyMzI0MjQwMywtNjQ3NTQ3NDA1LDk2NT
M0MDcxMCwxOTg3OTU5NjIwLDczMDk5ODExNl19
-->