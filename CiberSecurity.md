[**CNIT 123: Ethical Hacking and Network Defense**](https://samsclass.info/123/123_F15.shtml)

**Me quede en http/https**
https://www.youtube.com/watch?v=NiQC8loJew4&index=2&list=PLgM-HeZKXSWo6LLFmHA-hm5lcnUqxY1z5


[**CNIT 124: Advanced Ethical Hacking**](https://samsclass.info/124/124_F15.shtml)



## Firewalls

Los firewalls te permiten bloquear trafico desde ciertos origenes.

A pesar de que se supone que tenes control sobre tu servidor, es probable que exista **algun proceso (normal o malicioso)** que este a la escucha de un puerto TCP. 

> Recordemos que un puerto  TCP es una manera que tiene TCP de indicarle al receptor **que programa debe interpretar el paquete**

Por eso es buena practica utilizar un firewall para **bloquear todos los puertos que sabes que no necesitas por si existiera algun proceso que este a la escucha de paquetes y no lo supieras** 

>como siempre, es ideal usar un **WHITELIST** para determinar que puertos habilitar y bloquear todos los otros.
>**WHITELIST TENTATIVA DE PUERTOS**
>* 80 - HTTP 
>* 443 - HTTPS
>* 22 - SSH
>* 53 - DNS
>* 587 - SMTP con TLS
>**DUDOSOS**
>* 119 - POP (dudoso, obsoleto, sin encriptacion)
>* 145 - IMAP4

.

 ### Port scanning
Se considera que un puerto esta **abierto** cuando el protocolo TCP puede terminar el handshake e intercambiar un numero de sincronizacion o **SYN**

http://systemadmin.es/2009/12/diferencia-entre-open-closed-y-filtered-en-nmap


### Redes de servidores

Muchas veces tenes una serie de servidores que necesitan interactuar entre ellos con puertos que no queres abrir al mundo.

Para eso podes indicarle a tu firewall que acepte solo **los sockets TCP** que esten dentro de un whitelist con
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNDgzMDA2NiwtNjE4NTAyOTg2LC0xNj
YzMTYyMjg2LDkzOTgxNDQ0OCwxMTc5NTA2MzcyLDc4NDI2NjU2
NF19
-->