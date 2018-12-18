
## Terminologia basica 

### Aquisition, behaviour, Conversion

* **Aquisition** - Adquirir el interes de un usuario
* **behaviour** - Cuando el usuario interactua con el sitio
* **Conversion** - Cuando el usuario se transforma en cliente

### Sobre las cuentas

Las cuentas se pueden agrupar en _organizaciones_  jerarquia de como se organizan las cuentas es la siguiente

* Organizacion1
	* Account1
		* Property 1
			* View 1
			* View 2.... 
		* Property 2 ... 
	* Account2... 
* Organizacion 2 ...

Donde:

* **Organization:** Agrupacion de cuentas, los small o medium businesses generalmente usan solo una para agrupar todas sus cuentas
* **Account:** Repres
* **Property:**  recavador de informacion, utiliza un tracking code unico que colocas en la pagina 
* **View:** Vista que permite filtrar visualizar datos de una propiedad. 		 	 
	*  **Solo registran el futuro** - no tienen acceso a los datos del pasado
	* **Los datos son inmutables una vez registrados**
	* **Goals:** condiciones deseables que un VIEW trackea para ver si se cumplen 

# Reportes

## Audience y demographics

Los reportes de audience te permiten comprender datos acerca de tu audiencia, tales como

* **Procedencia geografica** - Ciudad, pais, continente, etc.
* **edad y genero**
* **preferencias y gustos** - entretenimiento, deportes, etc
* **Lenguaje**
* **Tecnologia**
	* **SO**
	* **Device**
	* **marca, resolucion, etc**
* **Active users**
	* **usuarios persistentes en el tiempo**
	* **Bounce rates**   

Ademas te permite visualizar las conversiones, tiempo estimado de sesion, etc ordenandolor usando estas categorias.

## Adquisition

Te permite visualizar informacion acerca de como estas adquiriendo el trafico y ordenarlo por sus fuentes para determinar de donde viene el trafico y de que calidad es. 

Las siguientes dimanesiones se capturan acerca de la adquisicion de trafico

* **medium** - Categoria de como llego el usuario al sitio
	* **Organic** - Trafico organico que viene de medios no pagos como busquedas de google
	* **CPC** - Trafico que viene de medios pagos como campañas de adwords
	* **Referral** - Trafico proveniente de otros sitios web con un HTTP header referral
	* **email** - Trafico proveniente de campañas de mailing.
	* **none** - Otro
* **source** - Provee mas informacion acerca del medium
	* El referrer si la fuente es referral
	* el search engine si el source es organic
* **marketing campaing**

### Channels

Los channels agrupan todos los sources de un medium para mostrar una vision unificada, podes crear custom channels para agrupar cosas cusom.

### Campaigns

Te permite visualizar el  trafico que llego mediante campañas

## Behaviour

Muestra reportes del comportamiento de los usuarios, tales como  **el tiempo de sesion, la navegacion del usuario y que paginas visita, etc.**

* **URI** de paginas visitadas
	* **tiempo de visualizacion**
	* **bounce rate** 
	* **veces visitada**
* **Conversiones**
* **Eventos**
	* **clicks en descargas**
	* **reproduccion de video** 


## Conversions

Muestra reportes relacionado con las conversiones del sitio

### Goals
Los Goals son informes sobre cosas especificas que se toman como conversiones. tienen los siguientes parametros.

>**Podes tener hasta 20 goals por view.**

Goals te permite trackear:
* **Arribo a una pagina en particular**
* **descargas**
* **Subscripciones o pagos**
* **eventos, reproducciones, clicks, etc**
* **Duracion de la sesion**
* **valor de la conversion en $**


### Goals funnel
Te permite visualizar los pasos previos a un goal para ver si los usuarios abandonan en algun momento.

Cada paso en un funnerl step es una pagina previa al goal, una vez configurado podes ver un reporte de hasta donde llego cada usuario.





# Marketing campaigns

## Anatomia de un link de una campaña

Las campañas de marketing se identifican con un tracking code que se coloca en las URLs colocadas en mails y ads.
El script de google analytics toma ese codigo e identifica la campaña.

El codigo se compone de los siguientes URL parameters
* **utm_medium** - El medio al que se desea asociar la campaña (mail, cpc, etc)
* **utm_campaign** - El nombre identificador de la campaña
* **utm_source** - Indica de donde proviene el usuario, por ejemplo una pagina web especifica (lanacion.com.ar)
* **utm_content** - identifica el contenido enviado, por ejemplo podes diferenciar entre 2 piezas graficas para ver cual tiene mejor conversion
* **utm_term** - Identifica keywords para search campaign. EJ: un google search campaign con keyword "inmobiliarios" sera identificado con esa palabra en utm_term


## Adwords- WIP


# Funcionamiento interno
## Hits

Cada ves que el script de google analytics envia informacion a google se lo conoce como un `hit`. Existen tres tipos de hits

### Page view hits

Se dan cuando el usuario visualiza una pagina. 


### Event hits

Se da cuando el usuario realiza un evento customizado

* Poner play a un video
* Registrarse
* Clickear un banner

### Transaction event

Permite guardar datos sobre compras, transacciones, stock, etc en analytics.
Podes guardar datos customizados en analytics.

### Social hits

Permite registrar cuando se colocan likes, comments, etc de redes sociales		

* Page timing hits

Permite determinar el tiempo de carga de un sitio


## Procesamiento de Hits
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNjE5MDU3MzgsLTIxMTQyNTUxOTQsND
QyMTEyMjczLDE1NzQwMTU0MTIsLTIzNDM0MzE3OSwtOTI1OTYz
MjIsMTc2NTAwMDU3Miw3OTg0OTMwMTEsLTI5NjYwODI2MywtND
c3MjUwNTE2LC0xMjI5MDQyODQwLDEwNTE2MTE3MzcsLTE0MjE3
MDE3NDFdfQ==
-->