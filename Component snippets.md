


# Contenido:

* burger menu
* carousel slider



## Burguer menu

JS

Solo cambia algunas clases cuando cickeas en el boton.

````js
/* burguer Header toggle */
document.getElementById('mobile-nav__burgerbutton').onclick = function () {
	 /*Cuando el user hace click, agregar o quitar la clase menu-hidden para mostrar
	 o ocultar el menu, fijate que es un TOGGLE*/
     document.getElementById('mobile-nav__side-menu-contaner').classList.toggle('menu-hidden');
	 /* Tambien cambiar la hamburguesa por una cruz o viceversa*/
     document.getElementById('mobile-nav__burgerbutton').classList.toggle('fa-bars');
     document.getElementById('mobile-nav__burgerbutton').classList.toggle('fa-times');
}

```` 

HTML

```` html
 <!-- Necesito font-awesome para el icono del burguer -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" crossorigin="anonymous">
 
 <!-- Markup del burger menu -->	
	<nav id="mobile-nav">
        <i id="mobile-nav__burgerbutton" class="fa fa-bars " aria-hidden="true"></i>
        <div id="mobile-nav__side-menu-contaner" class="menu-hidden">
            <div id="mobile-nav__side-menu-contaner__menu">
                <a >Quienes somos</a>
                <a>Ramas</a>
				 <!-- submenues un poco mas a la derecha -->
                <a class="mobile-nav__side-menu-contaner__menu__submenus"> manada</a>
                <a class="mobile-nav__side-menu-contaner__menu__submenus"> Unidad</a>                <a class="mobile-nav__side-menu-contaner__menu__submenus"> Caminantes</a>
                <a class="mobile-nav__side-menu-contaner__menu__submenus"> Rovers</a>
                <a>El Scoutismo</a>
                <a>Descargas</a>
            </div>
        </div>
    </nav>
````

SCSS

```` scss

 #mobile-nav {
 		 /* Hacer aparecer el menu cuando la pantalla es pequeña */
        @media screen and (max-width: 944px) {
            display: flex;
        }
		/* 
		Por default el menu esta plegado, se despliega si la clase .menu-hidden 
		es removida por el javascript, eso pasa cuando el user clickea en el hamburger
		button
		*/
        .menu-hidden {
            #mobile-nav__side-menu-contaner__menu {
                display: none;
            }
        }
		
		       
        display: none;
        color: white;
        width: 100%;
        justify-content: flex-end;
        align-items: center;
		
        #mobile-nav__side-menu-contaner__menu {
            height: 100%;
            position: fixed;
            top:0px;
            left: 0px;
            background-color: $headerColor;
            z-index: 100;
            display: flex;
            flex-direction: column;
            padding-top: 20px;
            a, a:visited{
                font-size: 1.1rem;
                margin: 10px;
                margin-left: 5vw;
                border-bottom: 1px solid white;
                padding-bottom: 15px;
                text-decoration: none;
                color: white;
            }
			/* los submenues estan mas a la derecha */
            .mobile-nav__side-menu-contaner__menu__submenus{
                margin-left: 10vw;
            }
        }
        
        i {
            font-size: 3rem;
            align-items: flex-end;
            margin-right: 10%;
        }
    }
````


## Carousel Slider

**Esto se puede hacer mucho mas minimalista! fijate en [ACA](https://pawelgrzybek.com/siema/)** 

Dependencias:
https://pawelgrzybek.com/siema/
http://fontawesome.io (OPCIONAL, solo para iconos de los botones)

Cosas que le añadi:
* **Botones** a los costados
* **Timer** que va cambiando el slide cada 5 segundos hasta que el usuario use un boton
* **Responsive** dps de 1500px wide tenes 4 slides, dps de 900px tenes 3, dps de 700 tenes 2, despues de 100 tenes 1 slide

HTML

````html
        <!-- DEPENDENCIAS  -->
		<script src="{{site.baseurl}}/assets/js/siema.min.js"></script>
	  
	  <!-- carousel propiamente dicho  -->
	   <div class="carousel ">
		<!-- Boton de anterior-->
            <button class="carousel__siema__prev ">
                <i class="fa fa-chevron-left" aria-hidden="true"></i>
            </button>
			<!-- slides -->
            <div class="carousel__siema ">
                <div class="carousel__siema__slide">slide 1</div>
                <div class="carousel__siema__slide">slide 2</div>
                <div class="carousel__siema__slide">slide 3</div>
                <div class="carousel__siema__slide">slide 4</div>
                <div class="carousel__siema__slide">slide 5</div>
                <div class="carousel__siema__slide">slide 5</div>
                <div class="carousel__siema__slide">slide 6</div>
            </div>
			<!-- Boton de siguiente-->
            <button class="carousel__siema__next "> 
                <i class="fa fa-chevron-right" aria-hidden="true"></i>
                </button>
        </div>
		
       
````

js

```js
 <!-- script de siema -->
            const elscoutismo_carousel = new Siema({
                selector: '.carousel__siema',
                duration: 200,
                easing: 'ease-out',
				// responsive design, a los 1500 px wide hay 4 slides
				// a los 900px ahy 3, a los 700px hay 2 etc
                perPage: {
                    100: 1,
                    700: 2,
                    900: 3,
                    1500: 4,
                },
                startIndex: 0,
                draggable: true,
                threshold: 20,
                loop: true,
            });
			//Logica de los botones next y anterior y de el sliding con cronometro 
			
			var timer = setInterval(function () { elscoutismo_carousel.next(); }, 5000);
			
			// los botones mueven el slider y tambien detienen el slide automatico
            document.querySelector('.carousel__siema__next')
			.addEventListener('click', () => {
                clearInterval(timer);
                elscoutismo_carousel.next()
            });
			
            document.querySelector('.carousel__siema__prev')
			.addEventListener('click', () => {
                clearInterval(timer);
                elscoutismo_carousel.prev()
            });


```

SCSS

````scss
.carousel {
	
	/*Centrar el carousel en la pagina*/
    width: 100%;
    display: flex;
    justify-content: center;
	
	/*Sacar los estilos estandar a los botones*/
    button {
        border: none;
        background: none;
        width: 10%;
    }
	
	/* Darle un tamaño  al carousel que permita los botones a los costados */
    .carousel__siema {
        width: 80%;
        .carousel__siema__slide {
            padding: 15px;
        }
    }
}

````
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzM1ODM4MjQyLC0xOTQwODk4MTg1XX0=
-->