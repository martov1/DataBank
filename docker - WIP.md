---


---

<p><strong>Quede aca:</strong> <a href="https://docs.docker.com/develop/develop-images/baseimages/">https://docs.docker.com/develop/develop-images/baseimages/</a></p>
<h1 id="intro-y-referencia">Intro y referencia</h1>
<h2 id="arquitectura">Arquitectura</h2>
<p>Docker se compone de 3 elementos</p>
<ul>
<li>Un servidor / daemon que administra todo
<ul>
<li><code>dockerd</code></li>
</ul>
</li>
<li>Un cliente que interactua con ese servidor y le dice que hacer
<ul>
<li>el CLI <code>docker</code></li>
<li>Docker REST API</li>
</ul>
</li>
<li>Docker objects que representan los elementos relevantes
<ul>
<li>Imagenes (un filesystem read-only)</li>
<li>Containers (un filesystem basado en una imagen, que ademas es writable y corre procesos)</li>
<li>Volumes</li>
<li>Networks</li>
</ul>
</li>
</ul>
<p>Ademas podes agrupar <strong>containers instanciados en diferentes  daemons (osea probablemente en diferentes pcs)</strong> a esto se lo llama <strong>“service”</strong> y te permiten tener  tener <strong>Computacion distribuida</strong></p>
<h2 id="images-containers-y-layers">Images, containers y layers</h2>
<ul>
<li>Las <strong>IMAGES</strong> son <strong>un Read-only filesystem</strong>  que son el punto de partida para crear un container</li>
<li>Un <strong>CONTAINER</strong> es un conjunto de <strong>procesos</strong> corriendo en un <strong>filesystem</strong> que es <strong>una copia de una imagen cuando se creo el container</strong></li>
</ul>
<blockquote>
<p>Podes ver los containers como <strong>instanciaciones de una imagen</strong>, cuando creas un container estas <strong>copando</strong> el filesystem de una <strong>imagen</strong> y colocandolo en un <strong>read/write filesystem</strong> que ademas tiene <strong>funcionando ciertos procesos</strong> (el container).</p>
</blockquote>
<p>El sistema docker funciona con <strong>layers</strong> que consisten en</p>
<ul>
<li><strong>Una serie de imagenes</strong>, cada una <strong>sobreescribiendo y añadiendo</strong> cosas de la anterior generando un filesystem final
<ul>
<li>Ej una añade el SO, otra añade apache, otra añade wordpress</li>
</ul>
</li>
<li>Un <strong>contanier</strong> que copia el <strong>filesistem final</strong> en un <strong>filesystem read/write</strong> y lo corre con ciertos <strong>procesos</strong></li>
</ul>
<p><img src="https://lh3.googleusercontent.com/5npNSbJiLcpmwCDMq2bYr_VG2BasVuv8QwJvr8Pxm4TcqiobhQAoXJ6ZYyDyWj-p22WCr8PinX61" alt="enter image description here"></p>
<h2 id="referencia-de-comandos-utiles">Referencia de comandos utiles</h2>
<ul>
<li><code>docker info</code> Muestra el estado del servicio docker (contenedores corriendo, pausados, detenidos, imagenes, version)</li>
<li><code>docker ps &lt;-param&gt;</code>  Lista los containers que estan en funcionamiento
<ul>
<li><strong>-a</strong> Muestra containers que fueron iniciados y ahora estan detenidos</li>
<li><strong>-q</strong> Solo muestra los containers id</li>
</ul>
</li>
<li><code>docker run &lt;-param&gt; &lt;imagen&gt; &lt;comando&gt;</code> Crea un container desde una imagen, si no la encuentra la descarga del repositorio
<ul>
<li><strong>-param</strong>
<ul>
<li><strong>–name nombre</strong> Le asigna un nombre al container que podes usar en lugar de su <strong>ID</strong></li>
<li><strong>-it</strong> Hace que el container sea interactivo (te conecta a su consola)</li>
<li><strong>-d</strong> run in background (daemon)</li>
<li><strong><code>-p &lt;hostport&gt;:&lt;containerport&gt;</code></strong> mapea un puerto a otro</li>
</ul>
</li>
<li><strong>imagen</strong> Nombre de la imagen desde la que se crea el container</li>
<li><strong>comando</strong> El comando que correr apenas el container termine de crearse. <strong>overridea el comando default del dockerfile (CMD)</strong></li>
</ul>
</li>
<li><code>docker image ls</code> Lista las imagenes disponibles en el OS para crear containers</li>
<li><code>docker container ls</code> Lista containers
<ul>
<li><code>docker container ls --all</code>muestra containers funcionando</li>
</ul>
</li>
<li><code>docker logs &lt;id&gt;</code> Muestra el log de stdout de un container</li>
<li><code>docker container stop &lt;id&gt;</code> Detiene el contenedor gracefully</li>
<li><code>docker container kill &lt;id&gt;</code> detiene el contenedor no gracefully</li>
<li><code>docker pull &lt;image name&gt;:&lt;TAG&gt;</code> descarga de dockerhub una imagen, las tags indican variaciones de una imagen</li>
<li><code>docker diff &lt;id&gt;</code> muestra las diferencias entre el container y su base image</li>
<li><code>docker commit &lt;id&gt;</code> crea una imagen del container</li>
<li><code>docker tag &lt;imageId&gt; &lt;tuTag&gt;</code> coloca un nombre (tag) a una imagen</li>
<li><code>docker rm &lt;id&gt;</code> Elimina un container</li>
<li><code>docker rmi &lt;idImagen&gt;</code> Elimina una imagen</li>
<li><code>docker port &lt;id&gt;</code> muestra el mapping de puertos para un contianer</li>
</ul>
<h2 id="notas-de-instalacion">Notas de instalacion</h2>
<h3 id="acerca-del-uso-de-sudo">Acerca del uso de SUDO</h3>
<p>Para evitar el uso de <strong>SUDO</strong> es critico agregar al usuario que va a administrar docker al grupo <code>docker</code> que se crea en el sistema al instalarlo.</p>
<h3 id="ip-de-containers-en-windows">IP de containers en windows</h3>
<p>En windows no podes usar localhost para comunicarte con un container usando un puerto mapeado, tenes que usar <strong>la ip del container y el puerto mapeado</strong>,  la obtenes con el comando <code>docker-machine ip</code></p>
<h3 id="detener-contenedor-en-windows">Detener contenedor en windows</h3>
<p>En windows <code>CTRL-C</code> no detiene el contenedor, tenes que detenerlo con <code>docker container stop &lt;Container NAME or ID</code></p>
<h1 id="operacion">Operacion</h1>
<h2 id="containers---wip">Containers - WIP</h2>
<h3 id="instanciacion">Instanciacion</h3>
<p>Una buena analogia de los containers es que son como objetos    instanciados de una clase (<strong>la imagen</strong>). son iguales a la imagen al momento de crearse, pero luego a lo largo de su vida son modificados.</p>
<p>Para instanciar un container desde una imagen usas.<br>
<em>Si no tenes la imagen cargada entonces docker intenta bajarla de dockerhub</em></p>
<p><strong><code>docker run &lt;-param&gt; &lt;imagen&gt; &lt;comando&gt;</code></strong></p>
<ul>
<li><strong>-param</strong>
<ul>
<li><strong>- -name nombre</strong> Le asigna un nombre al container que podes usar en lugar de su <strong>ID</strong></li>
<li><strong>-it</strong> Hace que el container sea interactivo (te conecta a su consola)</li>
<li><strong>-d</strong> run in background (daemon)</li>
<li><strong><code>-p &lt;hostport&gt;:&lt;containerport&gt;</code></strong> mapea un puerto a otro</li>
</ul>
</li>
<li><strong>imagen</strong> Nombre de la imagen desde la que se crea el container</li>
<li><strong>comando</strong> El comando que correr apenas el container termine de crearse. <strong>overridea el comando default del dockerfile (CMD)</strong></li>
</ul>
<h3 id="nombrar">Nombrar</h3>
<p>Los containers y las imagenes siempre tienen <strong>ids</strong> que <strong>se ven como un hash</strong>, pero ademas  pueden tener:</p>
<ul>
<li><strong>nombres</strong> en el caso de los <strong>containers</strong></li>
<li><strong>tags</strong> en el caso de las <strong>imagenes</strong></li>
</ul>
<blockquote>
<p><strong>Donde sea que puedas usar un ID podes usar el nombre o el tag</strong></p>
</blockquote>
<p><strong>Para nombrarlos</strong> usamos el parametro <strong><code>--name</code></strong></p>
<pre><code>docker run --name miNombre &lt;imagen&gt; 
</code></pre>
<h3 id="control-de-procesos">Control de procesos</h3>
<p>Podes controlar los containers que tenes usando</p>
<ul>
<li><code>docker container stop &lt;id&gt;</code>
<ul>
<li>Detiene el proceso</li>
</ul>
</li>
<li><code>docker container start &lt;id&gt;</code></li>
<li><code>docker container pause&lt;id&gt;</code></li>
</ul>
<h3 id="container-logs">Container logs</h3>
<p>El stdout de un container va a los logs de docker, accesibles desde<br>
<code>docker logs &lt;id&gt;</code></p>
<h3 id="daemon">Daemon</h3>
<p>En produccion vas a querer mantener los containers funcionando como <strong>daemons</strong> usando  <code>docker run -d &lt;imagen&gt;</code></p>
<h3 id="conectarte-con-bash">Conectarte con bash</h3>
<p>Simplemente ejecutas un bash en el container y pedis que sea interactivo</p>
<pre><code>docker exec -t -i container_name /bin/bash
</code></pre>
<h2 id="crear-imagesguardar-container">Crear images/guardar container</h2>
<h3 id="mejores-practicas">Mejores practicas</h3>
<ul>
<li>Los containers deben ser <strong>stateless</strong> y deben poder ser detenidos, reiniciados o reinstanciados de su imagen en todo momento</li>
<li>Cada container debe tener un unico <strong>concern</strong></li>
</ul>
<h3 id="modo-interactivo">Modo Interactivo</h3>
<blockquote>
<p><strong>CRITICO:</strong> Los containers son <strong>efimeros</strong>, si el server se apaga su estado se pierde.</p>
</blockquote>
<p>Para crear una imagen</p>
<ul>
<li>Creas un container en base a una o varias imagenes</li>
<li>haces tus cambios</li>
<li>corres <strong><code>docker commit &lt;idContainer&gt; &lt;tag&gt;</code></strong> y docker guarda una nueva imagen basada en tu container (usando el <code>id</code>) con el nombre que coloques en <code>TAG</code></li>
</ul>
<h3 id="modo-programatico---dockerfile">Modo programatico - DockerFile</h3>
<h4 id="resumen-rapido-para-crear-imagenes">Resumen rapido para crear imagenes</h4>
<p>Para crear una imagen de docker de forma programatica usamos un <strong>dockerfile</strong> junto con <strong>archivos que querramos copiar al contenedor</strong>.</p>
<p>Los necesitas a todos en la misma carpeta y a esta la llamaremos <strong>build context</strong>.</p>
<blockquote>
<p>Cada comando instancia un container copiando el container del comando anterior. el container del comando anterior es borrado.</p>
</blockquote>
<pre class=" language-dockerfile"><code class="prism  language-dockerfile"><span class="token keyword">FROM</span> &lt;imagen base<span class="token punctuation">&gt;</span>
<span class="token keyword">RUN</span> &lt;comandos ej<span class="token punctuation">:</span> apt<span class="token punctuation">-</span>get update<span class="token punctuation">&gt;</span>
<span class="token keyword">RUN</span> &lt;comandos ej<span class="token punctuation">:</span> apt<span class="token punctuation">-</span>get install <span class="token punctuation">-</span>y wget<span class="token punctuation">&gt;</span>
</code></pre>
<blockquote>
<p><strong>Tips:</strong> Conviene siempre colocar los comandos de tal forma que las cosas con menos cambios vayan arriba y las de mayor frecuencia de cambios vayan abajo. Esto permite aprovechar el <strong>build cache</strong> para hacer los builds mas rapidos.</p>
</blockquote>
<p><strong>En tu dockerfile probablemente quieras:</strong></p>
<ul>
<li><strong>usar una imagen</strong> oficial de base usando <code>FROM</code></li>
<li><strong>Copiar archivos</strong> al contenedor usando <code>COPY</code></li>
<li><strong>instalar dependencias</strong> con algun package manager <code>RUN</code> usando algun package.json que copiaste usando copy
<ul>
<li>apt-get</li>
<li>npm</li>
<li>pip</li>
</ul>
</li>
<li><strong>Exponer puertos</strong> usando <code>EXPOSE</code></li>
<li><strong>Setear variables de entorno</strong>
<ul>
<li>usando <code>ENV</code> <em>no recomendado</em></li>
<li>copiando archivos <strong>.sh</strong> a  <strong>/etc/profile.d</strong></li>
</ul>
</li>
</ul>
<pre class=" language-dockerfile"><code class="prism  language-dockerfile"><span class="token comment"># Use an official Python runtime as a parent image</span>
<span class="token keyword">FROM</span> python<span class="token punctuation">:</span>2.7<span class="token punctuation">-</span>slim

<span class="token comment"># Set the working directory to /app</span>
<span class="token keyword">WORKDIR</span> /app

<span class="token comment"># Copias cosas del directorio del dockerfile al contenedor</span>
<span class="token keyword">COPY</span> . /app

<span class="token comment"># Install any needed packages specified in requirements.txt</span>
<span class="token keyword">RUN</span> pip install <span class="token punctuation">-</span><span class="token punctuation">-</span>trusted<span class="token punctuation">-</span>host pypi.python.org <span class="token punctuation">-</span>r requirements.txt

<span class="token comment"># Make port 80 available to the world outside this container</span>
<span class="token keyword">EXPOSE</span> 80

<span class="token comment"># Define environment variable</span>
<span class="token keyword">ENV</span> NAME World

<span class="token comment"># Run app.py when the container launches</span>
<span class="token keyword">CMD</span> <span class="token punctuation">[</span><span class="token string">"python"</span><span class="token punctuation">,</span> <span class="token string">"app.py"</span><span class="token punctuation">]</span>

</code></pre>
<p><strong>Finalmente usas el dockerfile asi:</strong><br>
Para crear tu imagen entonces haces lo siguiente<br>
<strong><code>Docker build --tag &lt;miTag&gt;:&lt;version&gt; &lt;pathHaciaElBuildContext&gt;</code></strong></p>
<h4 id="build-context">Build context</h4>
<p>Una vez que tenes un Dockerfile podes crear tu imagen. <u><code>Docker build</code> necesita dos cosas para crear una imagen</u></p>
<ul>
<li>EL <strong>DockerFile</strong> que describe que hacer</li>
<li>Un <strong>Build context</strong> que es una carpeta con:
<ul>
<li>El <strong>dockerFile</strong></li>
<li>Todos los <strong>archivos que podrias necesitar</strong> copiar al container con comandos como <code>COPY</code>, <code>ADD</code>, etc</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>EL build context agranda la imagen</strong> (no asi el container) ya que <u>se copia todo el build context para tenerlo disponible a futuros layers que pudieran querer correr comandos como <code>COPY</code>. es por eso que <strong>te conviene mantenerlo chiquito</strong></u><br>
Para eso podes usar el archivo <code>.dockerignore</code> para <strong>ignorar</strong> los archivos que no queres que formen parte del <strong>build context</strong></p>
</blockquote>
<h4 id="build-process">Build process</h4>
<p>Para crear tu container entonces haces lo siguiente<br>
<strong><code>Docker build --tag &lt;miTag&gt;:&lt;version&gt; &lt;pathHaciaElBuildContext&gt;</code></strong></p>
<p>Una vez creado, podes ver el historial de containers intermedios y comandos corridos con</p>
<p><strong><code>docker history &lt;id imagen&gt;</code></strong></p>
<h4 id="build-cache-cache-busting-y-apt-get">Build cache, cache busting y apt-get</h4>
<p>Docker guarda un cache de las operaciones para hacer los build processes mas rapidos.</p>
<p>El cache funciona de la siguiente manera:</p>
<ul>
<li>Si la <strong>base image</strong> es la misma, uso cache</li>
<li><strong>linea por linea del dockerfile</strong> voy usando los layers en el cache a medida que veo que <strong>las instrucciones fueron las mismas</strong>
<ul>
<li>Para las instrucciones <code>COPY</code> y <code>ADD</code> hago un <strong>checksum de los archivos</strong>, si los checksums son iguales a los del cache entonces lo uso</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>NOTA IMPORTANTE SOBRE APT-GET:</strong> Notese que esto se cachea</p>
<pre class=" language-dockerfile"><code class="prism  language-dockerfile"><span class="token keyword">RUN</span> apt<span class="token punctuation">-</span>get update  
<span class="token keyword">RUN</span> apt<span class="token punctuation">-</span>get install <span class="token punctuation">-</span>y nginx
</code></pre>
<p>Por lo tanto cambiar el <code>apt-get install</code> <strong>no genera</strong> que se vuelva a correr el <code>apt-get update</code>. Te conviene entonces poner <strong>todo junto en un comando</strong></p>
<pre class=" language-dockerfile"><code class="prism  language-dockerfile"><span class="token keyword">RUN</span> apt<span class="token punctuation">-</span>get update &amp;&amp; apt<span class="token punctuation">-</span>get install <span class="token punctuation">-</span>y \
   aufs<span class="token punctuation">-</span>tools \
  automake \
  ETC ETC<span class="token punctuation">...</span>
</code></pre>
</blockquote>
<h4 id="mas-comandos-de-docker-file">Mas comandos de docker file</h4>
<ul>
<li><strong><code>FROM:&lt;imagen&gt;</code></strong> Indica la imagen de base</li>
<li><strong><code>LABEL:&lt;key&gt;=&lt;value&gt;</code></strong> el label para la imagen, algo human friendly, <u>podes tener varios labels<u>.
</u></u><ul>
<li><code>key</code> deberia ser prefixeado por un dominio que controles (Best practice), puede tener puntos o guiones</li>
<li><code>Value</code> puede ser cualquier cosa (dominio, etc)</li>
</ul>
</li>
<li><strong><code>WORKDIR:&lt;PATH&gt;</code></strong> establece el woring directory del container desde este punto en adelante (ej <code>RUN</code> o <code>CMD</code> arrancan con ese path)</li>
<li><strong><code>USER: &lt;username|UID&gt;</code></strong> indica con que usuario se correra el servicio, es para no correr el servicio como root.
<ul>
<li>Precio a esto necesitas crear el usuario, ej: <code>RUN useradd --no-log-init -r -g postgres postgres</code></li>
</ul>
</li>
<li><strong><code>CMD &lt;comando&gt;</code></strong> indica un comando default que correr al iniciar el container (de bash) .
<ul>
<li>Si se corre un <strong>comando</strong> al iniciar el container entonces overrideas al <code>CMD</code>.  ej: <code>docker run &lt;-param&gt; &lt;imagen&gt; &lt;comando&gt;</code></li>
<li><strong>solo puede haber un CMD command en todo el docker file</strong>, si hay mas de uno entonces se corre el ultimo.</li>
</ul>
</li>
<li><strong><code>ENTRYPOING ["&lt;command&gt;","&lt;option1&gt;","&lt;option2&gt;"...]</code></strong>
<ul>
<li>Es como <code>CMD</code></li>
<li>no se overridea al insertar un comando con <code>docker run</code></li>
<li><code>ENTRYPOING ["wget","-o","-q"]</code></li>
<li>Lo que se coloque como comando en <code>docker run &lt;-param&gt; &lt;imagen&gt; &lt;comando&gt;</code> se <strong>appendea al final del comando seteado en entrypoint</strong></li>
</ul>
</li>
<li><strong><code>EXPOSE &lt;portNumber&gt;</code></strong> expone un puerto del container al host.</li>
<li><strong><code>ADD &lt;path host&gt; &lt;path container&gt;</code></strong> Permite copiar un archivo/directorio del host al container</li>
<li><strong><code>COPY &lt;path host&gt; &lt;path container&gt;</code></strong> Igual que add</li>
<li><strong><code>ENV NAME World</code></strong> define variables de entorno</li>
<li><strong><code>WORKDIR &lt;pathEnContainer&gt;</code></strong> setea el working directory</li>
</ul>
<h2 id="docker-networking">Docker networking</h2>
<h3 id="exponer-puertos-vs-mapear-puertos">Exponer puertos vs mapear puertos</h3>
<p>Los contenedores de docker normalmente son cerrados y no pueden escuchar con ningun puerto salvo que lo <strong>expongas</strong> usando <strong><code>EXPOSE</code></strong>.</p>
<ul>
<li><strong>EXPONER:</strong> expone un puerto del contenedor  para que el contenedor pueda escucharlo, solo otros contenedores pueden comunicarse con el puerto, no es accesible fuera del host.</li>
<li><strong>MAPEAR</strong>: Mapea un puerto <strong>expuesto</strong> a un puerto del host. De esta manera el contenedor puede comunicarse con el mundo exterior usando la ip y un puerto del host.</li>
</ul>
<h3 id="mapeo-de-puertos">Mapeo de puertos</h3>
<p>Normalmente los containers pueden comunicarse con el mundo exterior <strong>usando la ip del host</strong>, pero <strong>el mundo exterior no puede comunicarse con ellos</strong> (ya que los paquetes los recibe el host).</p>
<p>Para solucionar esto usamos <strong>port mapping</strong>, que es <strong>tomar un puerto del host y mapearlo a un puerto del container</strong>.</p>
<blockquote>
<p><strong>POR EJEMPLO:</strong> podemos mapear el puerto 555555 del host al puerto 80 del container, para que los paquetes que lleguen al puerto 555555  del host sean redirigidos al container como si vinieran de su puerto 80</p>
</blockquote>
<p><strong>Para realizar el mapeo  usamos</strong></p>
<ul>
<li>el flag <strong><code>--publish-all</code></strong>  para autodetectar los puertos activos del container y mapearlos automaticamente a puertos random del host
<ul>
<li><code>docker run &lt;-param&gt; --publish-all &lt;imagen&gt; &lt;comando&gt;</code></li>
</ul>
</li>
<li>el flag <strong><code>-p &lt;puerto container&gt;:&lt;puerto host&gt;</code></strong></li>
</ul>
<p>Ahora podemos <strong>ver los puertos mapeados</strong> por docker para ese container usando <strong><code>docker port &lt;id&gt;</code></strong>.</p>
<h3 id="comunicar-containers-entre-si">Comunicar containers entre si</h3>
<p>Podes comunicar containers simplemente indicando</p>
<p><code>docker run &lt;-param&gt; --link &lt;containerId&gt;:&lt;aliasEnNuevoContainer&gt; &lt;imagen&gt; &lt;comando&gt;</code><br>
Ahora si miras el host file de este container vas a encontrar una enrutacion con el host name <code>aliasEnNuevoContainer</code> y la IP interna del container <code>containerId</code></p>
<h2 id="volumenes">Volumenes</h2>
<blockquote>
<p><strong>CRITICO:</strong> Es importante tener en cuenta que los volumenes compartidos no se commitean como parte de una imagen</p>
</blockquote>
<h3 id="entre-host-y-container-permanente">Entre host y container (permanente)</h3>
<p>Para montar un directorio del host  como un volumen en un container podes hacer:</p>
<ul>
<li><code>docker run &lt;-param&gt; -v path/en/el/container:path/en/el/host&lt;imagen&gt; &lt;comando&gt;</code></li>
<li>Podes agregar permisos <code>docker run &lt;-param&gt; -v path/en/el/container:path/en/el/host:rw- &lt;imagen&gt; &lt;comando&gt;</code></li>
</ul>
<p>Esto te permite tener <strong>archivos pemanentes</strong> que no se eliminan si el container se detiene.</p>
<h3 id="entre-containers">Entre containers</h3>
<p>Podes compartir los volumenes de un container con otros, incluso si este no esta corriendo.</p>
<p>Para crear un volumen compartible usas el siguiente comando</p>
<ul>
<li><code>docker run &lt;-param&gt; -v path/en/el/container &lt;nombreDeVolumen&gt; &lt;imagen&gt; &lt;comando&gt;</code></li>
</ul>
<p>Para usar los volumenes de otro container</p>
<ul>
<li><code>docker run &lt;-param&gt; -volumes-from &lt;containerId&gt; &lt;imagen&gt; &lt;comando&gt;</code></li>
</ul>
<h2 id="docker-compose---wip">Docker compose - WIP</h2>
<p>Docker compose te permite instanciar y configurar multiples contenedores desde un solo archivo denominado <strong>dockerCompose</strong> en el formato <strong>.yml</strong></p>
<p>En lugar de ejecutar <code>docker run &lt;-param&gt; -volumes-from &lt;containerId&gt; &lt;imagen&gt; &lt;comando&gt;</code>  manualmente para cada container declaras</p>
<pre class=" language-yml"><code class="prism  language-yml"><span class="token key atrule">version</span><span class="token punctuation">:</span> <span class="token number">2 </span><span class="token comment">#Version de sintaxis de dockercompose</span>
<span class="token comment">#Declaras una red de load balancers (opcional)</span>
<span class="token key atrule">networks</span><span class="token punctuation">:</span> 
  <span class="token key atrule">nombreDeLoadBalancer</span><span class="token punctuation">:</span>
<span class="token comment">#Declaras servicios</span>
<span class="token key atrule">services</span><span class="token punctuation">:</span>
	<span class="token comment"># Cada servicio es un contenedor, en este caso </span>
	<span class="token comment">#"web" y "database" </span>
	<span class="token key atrule">web</span><span class="token punctuation">:</span>
	  <span class="token key atrule">name</span><span class="token punctuation">:</span> "nombre del contenedor" <span class="token comment">#como --name</span>
	  <span class="token key atrule">image</span><span class="token punctuation">:</span> "miwilfly<span class="token punctuation">:</span>7" <span class="token comment">#imagen usada</span>
	  <span class="token key atrule">ports</span><span class="token punctuation">:</span> <span class="token comment">#el mapeo de puertos</span>
	   <span class="token punctuation">-</span> <span class="token string">"80:8000"</span>
	   <span class="token punctuation">-</span> <span class="token string">"21:300"</span>
	  <span class="token key atrule">links</span><span class="token punctuation">:</span> ·<span class="token comment">#aliases</span>
	   <span class="token punctuation">-</span> basedatos<span class="token punctuation">:</span>miAliasVisibleParaWeb
	  <span class="token key atrule">volumes</span><span class="token punctuation">:</span> 
	   <span class="token punctuation">-</span> <span class="token string">"&lt;path en container&gt;:&lt;pathHost&gt;"</span>
	  <span class="token key atrule">deploy</span><span class="token punctuation">:</span>
	    <span class="token key atrule">placement</span><span class="token punctuation">:</span> <span class="token comment">#ej Solo correr en swarm manager</span>
	      <span class="token key atrule">constraints</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>node.role == manager<span class="token punctuation">]</span>
	  <span class="token key atrule">command</span><span class="token punctuation">:</span> &lt;comando<span class="token punctuation">,</span> equivalente a CMD<span class="token punctuation">&gt;</span>
	  <span class="token key atrule">networks</span><span class="token punctuation">:</span> 
	    <span class="token punctuation">-</span> nombreDeLoadBalancer
	<span class="token key atrule">basedatos</span><span class="token punctuation">:</span>
		image<span class="token punctuation">:</span><span class="token string">"mysql:lastest"</span>
		<span class="token key atrule">ports</span><span class="token punctuation">:</span>
		 <span class="token punctuation">-</span> <span class="token string">"3306:3306"</span>

</code></pre>
<h2 id="dockerhub">DockerHub</h2>
<p>Dockerhub funciona como github pero para containers.</p>
<ul>
<li><strong>Push</strong> - podes publicar tus imagenes tagueandolas  con el nombre de usuario de dockerhub, tu repositiorio y un tag para identificarlo (una version posiblemente)<pre><code>docker tag &lt;imagen&gt; username/repository:tag
docker push username/repository:tag
</code></pre>
</li>
<li><strong>Pull</strong> - Podes tomar imagenes tuyas o de otro repositorio haciando un pull con la sintaxis <code>username/repository:tag</code><pre><code>docker run -p 4000:80 username/repository:tag
</code></pre>
</li>
</ul>
<h1 id="distributed--load-balancing">Distributed / load balancing</h1>
<h3 id="conceptos">Conceptos</h3>
<p>Distributed systems se basa principalmente en el concepto de <strong>services</strong> o de <strong>micro-services</strong>, es decir dividir el sistema en varias partes que sea stateless y corran en diferentes servidores. <strong>cada servicio va en uno o varios containers funcionando en paralelo</strong></p>
<p><strong>Nomenclatura:</strong></p>
<ul>
<li><strong>SWARM WORKER</strong> nodo con un docker daemon que corre algunos o todos los tasks de uno o varios services. se comunica mediante DOCKER API</li>
<li><strong>SWARM MANAGER</strong> computadora que dirige el swarm y le dice a cada node que task de cada servicio instanciar. se comunica mediante DOCKER API</li>
<li><strong>SWARM:</strong> conjunto de nodes.</li>
<li><strong>NODE:</strong> computadora que esta corriendo un docker daemon</li>
<li><strong>STACK:</strong> Conjunto de services. configurado en <strong>dockerCompose</strong></li>
<li><strong>SERVICE:</strong> La descripcion de cuantos tasks de <strong>una misma imagen</strong> se deben mantener instanciados a lo largo del swarm en todo momento (ej 10 apache servers). configurado en <strong>dockerCompose</strong>.</li>
<li><strong>TASK:</strong> un container</li>
<li><strong>LOAD-BALANCER:</strong> El sistema que se encarga de distribuir los requests entre ciertos containers</li>
</ul>
<h3 id="consideraciones-previas">Consideraciones previas</h3>
<p>Necesitas que cada host  tenga abiertos los puertos</p>
<ul>
<li>Port 7946 TCP/UDP for container network discovery.</li>
<li>Port 4789 UDP for the container ingress network.</li>
</ul>
<h3 id="usando-docker-compose-y-swarm">Usando docker compose y swarm</h3>
<h4 id="generar-el-swarm">Generar el swarm</h4>
<ul>
<li>Para transformar este nodo en un <strong>swarm manager</strong> hacemos
<ul>
<li><code>docker swarm init</code></li>
<li>El comando devolvera un comando <code>docker join --token &lt;token&gt; &lt;ip&gt;</code> que podemos usar para <strong>unir workers al swarm</strong></li>
</ul>
</li>
<li>Para ver los nodos hacemos <code>docker node ls</code></li>
<li>para <strong>apagar docker swarm</strong> haces <code>docker swarm leave --force</code></li>
</ul>
<blockquote>
<p>Una vez creado el swarm todos tus <strong>comandos de docker</strong> los vas a realizar en el <strong>swarm manager</strong> y este se encargara de coordinar los <strong>workers</strong></p>
</blockquote>
<h4 id="configurar-el-stack">Configurar el stack</h4>
<p>DockerCompose te permite  <strong>configurar  un stack</strong> indicando  <strong>servicios</strong> que se componen de una <strong>cierta cantidad de contenedores instanciados de la misma imagen</strong> de ciertas <strong>caracteristicas</strong> y con ciertas <strong>limitaciones</strong></p>
<pre class=" language-yml"><code class="prism  language-yml"><span class="token key atrule">version</span><span class="token punctuation">:</span> <span class="token string">"3"</span>
<span class="token comment">##Listado de los servcios:</span>
<span class="token key atrule">services</span><span class="token punctuation">:</span>
  <span class="token comment">##Servicio 1, llamado "web" y su descripcion</span>
  <span class="token key atrule">web</span><span class="token punctuation">:</span>
    <span class="token key atrule">image</span><span class="token punctuation">:</span> username/repo<span class="token punctuation">:</span>tag
    <span class="token key atrule">deploy</span><span class="token punctuation">:</span>
      <span class="token key atrule">replicas</span><span class="token punctuation">:</span> <span class="token number">5 </span><span class="token comment">#Correr 5 contenedores</span>
      <span class="token key atrule">resources</span><span class="token punctuation">:</span>
        <span class="token key atrule">limits</span><span class="token punctuation">:</span>
          <span class="token key atrule">cpus</span><span class="token punctuation">:</span> "0.1" <span class="token comment"># cada uno usa max 10% de 1 CPU core</span>
          <span class="token key atrule">memory</span><span class="token punctuation">:</span> 50M <span class="token comment"># cada uno usa max 50mb ram</span>
      <span class="token key atrule">restart_policy</span><span class="token punctuation">:</span>
        <span class="token key atrule">condition</span><span class="token punctuation">:</span> on<span class="token punctuation">-</span>failure <span class="token comment"># Reiniciar si hay error</span>
    <span class="token key atrule">ports</span><span class="token punctuation">:</span> <span class="token comment">#Mapeo de puertos</span>
      <span class="token punctuation">-</span> <span class="token string">"4000:80"</span>
    <span class="token key atrule">networks</span><span class="token punctuation">:</span> <span class="token comment">#Web va a usar el load-balancer "webnet"</span>
      <span class="token punctuation">-</span> webnet
   <span class="token comment">#Aca colocarias otro servico</span>
  <span class="token key atrule">otroServicio</span><span class="token punctuation">:</span>
<span class="token key atrule">networks</span><span class="token punctuation">:</span> <span class="token comment">#Defino el load-balancer network llamado "webnet"</span>
  <span class="token key atrule">webnet</span><span class="token punctuation">:</span>
  

</code></pre>
<h4 id="desplegar-el-stack-en-el-swarm">Desplegar el stack en el swarm</h4>
<ul>
<li>Para <strong>desplegar un stack en el swarm</strong> hacemos<br>
<code>docker stack deploy -c docker-compose.yml &lt;nombreDelSwarm&gt;</code></li>
<li>Para <strong>eliminar</strong> el stack haces <code>docker stack rm getstartedlab</code></li>
</ul>
<h4 id="ver-servicios-tasks-nodes-y-stacks-activos-en-swarm">Ver servicios, tasks, nodes y stacks activos en swarm</h4>
<p>Podes ver los <strong>servicios corriendo en un stack</strong> asi</p>
<pre><code>docker stack services &lt;nombreDelSwarm&gt;
</code></pre>
<p>Para ver los <strong>tasks corriendo en un service</strong>, haces</p>
<pre><code>docker service ps getstartedlab_web
</code></pre>
<p>Para ver los <strong>tasks corriendo en un stack</strong></p>
<pre><code>docker stack ps &lt;stackname&gt;
</code></pre>
<p>Para ver los <strong>nodos</strong> hacemos</p>
<pre><code>docker node ls
</code></pre>
<h4 id="escalar-y-distribuir">Escalar y distribuir</h4>
<p>Podes escalar el servicio cambiando la cantidad de replicas en el docker-compose y corriendo:</p>
<pre><code>docker stack deploy -c docker-compose.yml &lt;nombreStack&gt;
</code></pre>
<p>No hay necesidad de hacer nada mas, <strong>los contenedores se distribuiran en todo el swarm y el load balancer va a distribuir la carga equitativamente.</strong></p>
<h4 id="acceder">Acceder</h4>
<p>Podes acceder con la ip de cualquier <strong>worker</strong> o el <strong>swarm manager</strong>, el <strong>load balancer</strong> se va a hacer cargo de todo</p>
<h4 id="shared-files-y-volumes">shared files y volumes</h4>
<p>Si necesitas compartir archivos entre los containers (ej archivos subidos por suers) tenes que tener <strong>un container en un solo nodo que tenga un volumen compartirdo con ese nodo</strong></p>
<p>Ejemplo de docker-composer</p>
<pre class=" language-yml"><code class="prism  language-yml"><span class="token key atrule">redis</span><span class="token punctuation">:</span>
    <span class="token key atrule">image</span><span class="token punctuation">:</span> redis
    <span class="token key atrule">ports</span><span class="token punctuation">:</span>
      <span class="token punctuation">-</span> <span class="token string">"6379:6379"</span>
    <span class="token key atrule">volumes</span><span class="token punctuation">:</span>
      <span class="token punctuation">-</span> <span class="token string">"/home/docker/data:/data"</span>
    <span class="token key atrule">deploy</span><span class="token punctuation">:</span> <span class="token comment">##Solo existira en el swarm manager</span>
      <span class="token key atrule">placement</span><span class="token punctuation">:</span>
        <span class="token key atrule">constraints</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>node.role == manager<span class="token punctuation">]</span>
</code></pre>

