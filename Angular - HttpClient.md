
Quede en XSRF Protection
https://angular.io/guide/http#security-xsrf-protection


# Contenido

* Setup
* Comunicacion
	* GET y parametros generales de todos los requests
	* POST
	* PUT
	* DELETE
	* URL parameters y headers 
* Error handling  
* Interceptors
	* Uso sobre requests
	* Uso sobre responses
	* Error handling en interceptor
	* Configuracion en provider 
	* Orden
	* Modificar un request (inmutabilidad del request)
	* Cache
* Progress events 
* Best practices





# Setup

Antes que nada tenes que importar el modulo, hay que importarlo **despues de BrowserModule**

````js
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [
    BrowserModule,
    // import HttpClientModule after BrowserModule.
    HttpClientModule,
  ]
})
````

Despues lo inyectas en tus componentes o servicios

````js
import { HttpClient } from '@angular/common/http';

@Injectable()
export class ConfigService {
  constructor(private http: HttpClient) { }
}

````

# Comunicacion

Todos los requests se hacen mediante observables. es importante recordar:

* **cada vez que subscribis a un observable, este se ejecuta**
	* podes terminar haciendo varias veces el mismo HTTP request, para evitarlo podes usar behavioural subjects (ver RxJS)
* **Si no subscribis, el observable no se ejecuta**
	* Un HTTP DELETE no parece tener necesidad de leer el valor de retorno, pero si no te subscribis entonces nunca se envia.  

## Get() y parametros generales de todos los requests
Podes hacer una solicitud **get**:

* Usas la **funcion get()**
* Deberias tener una **interfaz** que describa la respuesta del server
* Deberias colocarla como **generic** en la funcion **get()** para que typescript pueda hacer typechecking en la respuesta del server



sintaxis:
````js
  http.get<MiInterfaz>('Mi url donde hacer la solicitud');
````

Parametros:
````js
      
      
get(
		url: string, 
		options: {
			headers:{
        		NombreDeHeader: valor
    		}
			// si el valor es 'response' obtenes todo el response, no solo JSON
    		observe?: HttpObserve;
			//Parametros/querys a enviar
    		params?: {
   			     nombreDeParametro:valor
   			};
    		reportProgress?: boolean;
   		 responseType?: 'arraybuffer' | 'blob' | 'json' | 'text';
			//Determina si se enviaran credenciales 
   			withCredentials?: boolean;
		};
}): Observable<any>

    
````


Ejemplo:
````js
// esta interfaz permite a typescript determinar como se vera la respuesta del server
// y hacer typechecking
  interface misDatos {
  	nombre: string,
	apellido: string,
  }
  constructor(private http: HttpClient) { 
  // Coloco misDatos como generic para poder 
  this.http.get<misDatos>('/miserver/misdatos.json');

  }
````

## Post()

Tiene los mismos parametros que GET pero ademas acepta algo que enviar. principalmente un **js object** que envias como **json**

````js
  return this.http.post<MiInterfaz>(URL, objetoEnviado, httpOptions)
    .pipe(
      catchError(this.handleError('addHero', hero))
    );

````

## Delete()

````js
return this.http.delete(url, httpOptions)
    .pipe(
      catchError(this.handleError('deleteHero'))
    );
````

## Put()

````js

  return this.http.put<Hero>(this.heroesUrl, hero, httpOptions)
    .pipe(
      catchError(this.handleError('updateHero', hero))
    );
````

## URL parameters y headers

Podes añadir parametros ó headers bien encodeados haces asi:

````js
misParametros =  new HttpParams()
	.set('nombreDeParametro1', Valor1) 
	.set('nombreDeParametro2', Valor2) 

misHeaders = new HttpHeaders(
		{
    	'Content-Type':  'application/json',
    	'Authorization': 'my-auth-token'
 		 })

this.http.get<Hero[]>(this.heroesUrl, {params: misParametros, headers: misHeaders })

````



# Error handling

si hay un error entonces el **Observer** debera estar en condiciones de manejarlo.recibira un **error object**. **esto es algo que queremos hacer en un servicio**

Esto es algo propio de los **Observables**, si no te acordas anda a mirar el documento de RxJS

````js

  this.miServicio.obtenerDatos()
    .subscribe(
      data => this.config = { ...data }, // success path
      error => this.error = error // error handling
    );
````

## Posibles estrategias

### Retry

Podes usar el **RxJS** operator **Retry()** para reintentar un par de veces un request.

````js
return this.http.get<Config>(URL)
    .pipe(
      retry(3), // retry a failed request up to 3 times
      catchError(this.handleError) // then handle the error
    );
````

# Interceptors

## Uso sobre requests
Te permite interceptar una serie de requests http, muchas veces se usa para no tener que implementar autenticacion en cada get/post. para esto hay que implementar la funcion **interept()** de la interfaz **HttpInterceptor**

>acordate que esta bueno tener una interfaz que te deterine el type de la respuesta esperada, en este caso la simbolizamos como **MiInterfaz**

Un interceptor:

* Puede **pasarle el request** al siguiente **interceptor**
* Puede **finjir devolver una respuesta del server**
* Puede **pasarle un request totalmente diferente al siguiente interceptor**.
* **Devuelven objetos HttpEvent** y no **HttpResponse**

sintaxis
````js
// se importa de
import {HttpInterceptor, HttpHandler, HttpRequest} from '@angular/common/http';
//acordate que tenes que IMPLEMENTAR intercept, NO llamarla
interept(miRequestInterceptada<MiInterfaz>, SiguienteHandler){
// hacer cosas

//Opcion 1: pasar el request al siguiente handler 
	return next.handle(miRequestInterceptada);
//opcion 2: devolver una respuesta "falsa" del server
return Observable.of(algoDeTipoHTTPREQUEST)
// Opcion 3: devolver OTRA request
//miRequestInterceptada2 se envia, miRequestInterceptada se pierde
miRequestInterceptada2 = miRequestInterceptada.clone()
return next.handle(miRequestInterceptada2);
}
````

Ejemplo:
````js
import {
  HttpEvent, HttpInterceptor, HttpHandler, HttpRequest
} from '@angular/common/http';

/** Pass untouched request through to the next request handler. */
@Injectable()
export class miInterceptor implements HttpInterceptor {

  intercept(req: HttpRequest<MiInterfaz>, next: HttpHandler):Observable<HttpEvent<any>> {
    //**tu proceso aca**
	
	//Pasar el request al proximo interceptor, si no hay mas se envia.
	return next.handle(req);
	
  }
}

````


### Uso sobre responses

El interceptor usado para modificar la respuesta es el mismo que el que se usa para modificar la request. lo unico que tenes que hacer es usar el observable **next.handle(req)**, lo que coloques como operador despues de el se ejecuta **despues de todos los intercepts de salida y de que la request haya salido y vuelto del server** y por lo tanto funcionara sobre la **respuesta del server**

````js
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    
    return next.handle(req).map((event: HttpEvent<any>) => {
	// Verificas si es una respuesta
      if (event instanceof HttpResponse) {
        // do stuff with response if you want
      }
    })
}
````

### Error handling en interceptor

>Atencion:
>El error handling podria hacerse en donde estas llamando el http request, esto es lo mas normal!, pero hay casos (Autenticacion por ejemplo) donde es preferible que el interceptor sea el que maneje el error, **o que _masajee_ el error para devolver directamente un mensaje de error al observer**, esto ademas permite un **global error handling**

Si algo falla en el observable **next.handle(req)** entonces podes **atajar el error dentro del observer al final del http request**.

PERO Si quisieras **manejarlo dentro del interceptor, podes!** solo tenes que usar el RxJS operator **catch()** que hace que **en lugar de ir a la funcion error del observer, correr una funcion y devolver otro observable**

````js
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    
    return next.handle(req)
	.catch(err => {
      if (err instanceof HttpErrorResponse {
          if (err.status === 401) {
             // me expiro el token, hace tu logica aca.
			 // en este caso, hay que implementar que el observer muestre esto 
			 //en pantalla
             Observable.throw("la sesion expiro!");
          }
        }
    })
}
````

### Configuracion en provider

Una vez que tenes tu clase que implementa **interceptor()**, tenes que** proveerla para que pueda ser inyectada**. 
**Esto lo hacemos con un provider.**

>Internamente los providers actuan como dependencias de HttpClient, asi que **hay que definirlos antes de que angular instancia HttpClient**

**Para añadir interceptors a un array de providers, hay que hacerlo asi:**
````js
{ provide: HTTP_INTERCEPTORS, useClass: miInterceptor, multi: true },
{ provide: HTTP_INTERCEPTORS, useClass: miInterceptor2, multi: true },
{ provide: HTTP_INTERCEPTORS, useClass: miInterceptor3, multi: true }
````

**O ponerlos todos en un solo provider**
````js
/** en alguna clase: */
export const MisInterceptores = [
  { provide: HTTP_INTERCEPTORS, useClass: miInterceptor, multi: true },
	{ provide: HTTP_INTERCEPTORS, useClass: miInterceptor2, multi: true },
	{ provide: HTTP_INTERCEPTORS, useClass: miInterceptor3, multi: true }
];

/** en el modulo: */
providers: [  MisInterceptores],
````

### Orden

El orden de los interceptors en el array de privders es el orden en el que seran usados.
Si los interceptores son $A,B,C$ y **estan en ese orden en el array de providers**, entonces:

**los requests fluyen:** $A \Rightarrow B \Rightarrow C$
**Los responses fluyen:** $A \Leftarrow B \Leftarrow C$


### Modificar un request (inmutabilidad del request)

Los requests son inmutables despues de que son creados, si queres modificar algo en un request que ya existe (que es lo que sucede en un interceptor) tenes que clonarlo, no vas a poder modificar sus propiedades

````js
// Clonar y hacer nuestras modificaciones a la nueva instancia
const secureReq = req.clone({
  url: req.url.replace('http://', 'https://')
});
// Pasarle la nueva instancia al handler
return next.handle(secureReq);

````


### Cache

Podes cachear respuestas.
````js
const noHeaderReq = req.clone({ headers: new HttpHeaders() });
	// le sacas los headers
  return next.handle(noHeaderReq).pipe(
    tap(event => {
      // There may be other events besides the response.
      if (event instanceof HttpResponse) {
	  	// guardas en el cache o lo actualizas
        cache.put(req, event); // Update the cache.
      }
    })
````


y usar las respuestas del cache
````js

  intercept(req: HttpRequest<any>, next: HttpHandler) {
    // Si la respuesta no es cacheable segun HTTP, seguir de largo
    if (!isCachable(req)) { return next.handle(req); }
	
	//Si lo es, intentar obtenerla de nuestro cache
    const cachedResponse = this.cache.get(req);
	
	//Si la obtuvimos, usamos esa, si no, enviamos el request tal como lo obtuvimos
    return cachedResponse ?
      of(cachedResponse) : sendRequest(req, next, this.cache);
  }

````

---

## Progress events

[Mas detalle aca](https://angular.io/guide/http#listening-to-progress-events)
Cuando estas subiendo o bajando archivos podes obtener status reports del browser activando el flag **reportProgress**

````js
const req = new HttpRequest('POST', '/upload/file', file, {
  reportProgress: true
});

//en analizarEvento interpreas el HttpEvent y generas algun mensaje para el usuario

return this.http.request(req).pipe(
  map(event => this.analizarEvento(event)),
  tap(message => this.mostrarProgreso(message)),
  last(), // return last (completed) message to caller
  catchError(this.handleError(file))
);
````

# Best practices

* Separar en un servicios y no en un componentes
	* Comunicacion con servidores
	* Error handling, interpretation y resolution de las comunicaciones
* Que los HttpRequest tengan una interfaz de la respuesta esperada
	* En gets, posts, interceptors, etc 



<!--stackedit_data:
eyJoaXN0b3J5IjpbNDIzNTk2ODA1LDU0NjE3NjMzNiwtMTI4Mj
cwNTAzNl19
-->