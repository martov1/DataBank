


# Contenido

* Drivers






# Drivers

Los mailing drivers determinan que se usara para enviar los mail, estan configurados en **config/mail.php**

ejemplos: 

*  mailgun
*  SparkPost 
*  SES
*  SMTP


# Mailable

En laravel cada tipo de mail se representa con una clase denominada **mailable**

	php artisan make:mail MiMailable
	
	
Se caracterizan por tener una funcion **build()** dentro de la cual podes llamar a los metodos:

* **from('senderexample.com')** - Indica en nombre de quien esta siendo enviado el mail
* **subject('titulo')** - Titulo del mail
* **view(path.al.view)**
* **attach('path/a/un/archivo', ['as'->'nombre.pdf', 'mime' ->'application/pdf'])**
* **text('contenido')** - Indica la version del mail en plain text


## View data

Las variables que podes colocar en el template de view son las que esten defindas en el mailable como variables publicas.

```php 
	class MiMailable extends Mailable
	{
	    use Queueable, SerializesModels;
		//Esta variable va a estar accesible en el blade template del mail
	    public $order;
	
	    public function __construct(Order $order)
	    {
	        $this->order = $order;
	    }
	
	    public function build()
	    {
	        return $this->view('emails.orders.shipped');
	    }
	}
```

# Enviar email

* **Mail::to()** acepta:
	* Una **direccion de email**
	* Un **usuario**
	* Una **coleccion de usuarios**

Enviar email a usuario
```php 
        Mail::to($request->user())->send(new MiMailable($order));
```

Con CC o CCO
```php 
	Mail::to($request->user())
	    ->cc($moreUsers)
	    ->bcc($evenMoreUsers)
	    ->send(new MiMailable($order));
```

# Renderizar un mail

pasar un mail a HTML asi:

```php 
	return (new App\Mail\InvoicePaid($invoice))->render();
```

# Enviar mail asincronicamente

Enviar un mail puede retrasar un rquest, para hacerlo de **forma asyncronica** hacelo asi:

	Mail::to($request->user())
	    ->cc($moreUsers)
	    ->bcc($evenMoreUsers)
	    ->queue(new MiMailable($order));

para **hacerlo en una fecha especifica**

	$when = now()->addMinutes(10);
	Mail::to($request->user())
		->cc($moreUsers)
		->bcc($evenMoreUsers)
		->later($when, new OrderShipped($order));
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA2MjE4MjA2OF19
-->