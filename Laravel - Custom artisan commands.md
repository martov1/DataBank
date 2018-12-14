

# Comandos default

* php artisan list - Muestra lista de los comandos disponibles


## Custom commands

Para crear un custom command haces:

```php
php artisan make:command SendEmails
```

```php
class nombreDe Command extends Command
{
	//Signature para mostrar en php artisan list
    protected $signature = 'email:send {user}';
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
eyJoaXN0b3J5IjpbLTIyOTEzOTA5NiwxOTg3OTU5NjIwLDczMD
k5ODExNl19
-->