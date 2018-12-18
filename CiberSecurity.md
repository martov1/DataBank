[**CNIT 123: Ethical Hacking and Network Defense**](https://samsclass.info/123/123_F15.shtml)

[**CNIT 124: Advanced Ethical Hacking**](https://samsclass.info/124/124_F15.shtml)



## Firewalls

Los firewalls te permiten bloquear trafico desde ciertos origenes.

A pesar de que se supone que tenes control sobre tu servidor, es probable que exista **algun proceso (normal o malicioso)** que este a la escucha de un puerto TCP. 

> Recordemos que un puerto  TCP es una manera que tiene TCP de indicarle al receptor **que programa debe interpretar el paquete**

Por eso es buena practica utilizar un firewall para **bloquear todos los puertos que sabes que no necesitas por si existiera algun proceso que este a la escucha de paquetes y no lo supieras** 

>como siempre, es ideal usar un **WHITELIST** para determinar que puertos habilitar y bloquear todos los otros.
>**WHITELIST TENTATIVA DE PUERTOS**
* 80 - web 
* 22 - SSH
* 53 - DNS
* 587 - SMTP con TLS

 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMTg0NzA0NjYsMTE3OTUwNjM3Miw3OD
QyNjY1NjRdfQ==
-->