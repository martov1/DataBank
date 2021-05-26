---


---

<p><strong>Quede en vertical algin por paja</strong><br>
<strong>Tambien me qude en counters</strong></p>
<h1 id="css-2.1">CSS 2.1</h1>
<h2 id="ideologia">Ideologia</h2>
<p>CSS es un lenguaje de estilos pero tambien intenta mantener ciertos ideales, estos son:</p>
<ul>
<li><strong>GENERALIDAD:</strong> CSS es un lenguaje ideado para presentar y describir contenido en <strong>cualquier formato (voz, texto escrito, impreso, audio, imagenes, braille, etc)</strong> aunque sus aplicaciones mas conocidas son la renderizacion visual de paginas web.</li>
<li><strong>BACKWARDS COMPATIBLE:</strong> CSS debe ser compatible con todas sus versiones anteriores</li>
<li><strong>FORWARD COMPATIBLE:</strong> SI una regla css no se conoce se ignora, siempre se preserva el contenido</li>
<li><strong>COMPLEMENTARIO:</strong> Debe ser posible cambiar los estilos con minimos cambios en el contenido/markup</li>
<li><strong>DEVICE/VENDOR INDEPENDENT:</strong> Deben funcionar en todo dispositivo y para toda marca</li>
<li><strong>ACCESIBILIDAD:</strong> CSS proovera de herramientas para que el contenido sea accesbile a personas con inhabilidades</li>
</ul>
<h2 id="terminos">Terminos</h2>
<p>CSS utiliza ciertos terminos propios:</p>
<ul>
<li><strong>Canvas</strong>  - No confundir con el HTML5 canvas, es el area donde css va a renderizar. es infinita en todas las dimensiones y se elige una subarea dependiendo del media type, generalmente es elegido por el user-agent. se define como <strong>El area donde la FORMMATTING STRUCTURE</strong> se renderiza</li>
<li><strong>Source document</strong> - El documento al cual se le aplicaran las stylesheets (ej HTML)</li>
<li><strong>Document tree</strong> - Un arbol de nodos que contiene los elementos del source document antes de ser  aplicadas las reglas de los stylesheets. (generalmente un arbol de elementos html)</li>
<li><strong>Formatting structure</strong> - Una descripcion programatica (generalmente arbol de nodos) de lo que se va a mostrar, se computa a partir de un Document tree y las style sheets</li>
<li><strong>Canvas</strong>  - No confundir con el HTML5 canvas, es el area donde css va a renderizar. es infinita en todas las dimensiones y se elige una subarea dependiendo del media type, generalmente es elegido por el user-agent. se define como <strong>El area donde la FORMMATTING STRUCTURE</strong> se renderizara.</li>
<li><strong>Selector</strong> - Algo que te permite indicar un elemento o elementos del document tree y/o
<ul>
<li>relaciones entre ellos</li>
<li>sus atributos</li>
<li>Su estado (:hover)</li>
<li>Partes de su contenido (:first-line)</li>
</ul>
</li>
</ul>
<h2 id="procesamiento-y-formatting-structure">procesamiento y formatting structure</h2>
<h3 id="unidades-de-medida">Unidades de medida</h3>
<blockquote>
<p><strong>ATENCION: Esta parte fue reemplazada por CSS 3!!!</strong></p>
</blockquote>
<p><strong>ABOLUTAS:</strong></p>
<ul>
<li><strong>in</strong>: inches — 1in is equal to 2.54cm.</li>
<li><strong>cm</strong>: centimeters</li>
<li><strong>mm</strong>: millimeters</li>
<li><strong>pt</strong>: points — the points used by CSS are equal to 1/72nd of 1in.</li>
<li><strong>pc</strong>: picas — 1pc is equal to 12pt.</li>
<li><strong>px</strong>: pixel units — 1px is equal to 0.75pt.</li>
</ul>
<blockquote>
<p><strong>Las medidas se aproximan dependiendo del css media type basado en una medida de referencia (EJ:px para pantalla, mm para impresion)</strong></p>
<ul>
<li><strong>Px</strong> Se mide como el pixel de referancia en dispositivos, que puede no ser un pixel fisico. se usa tambien el pixel de referencia para deducir el tamaño al pasar a mm para imprimir medidan en px<br>
<strong>mm</strong> Se mide en mm reales para impresion y se aproxima en px fisicos para renderizar en pantallas<br>
<strong>PIXEL DE REFERECIA:</strong> Es el tamaño de un pixel caluclado como 1/96 inch a una distancia de un brazo y con un angulo de vision,</li>
</ul>
</blockquote>
<p><strong>RELATIVAS:</strong></p>
<ul>
<li>
<p><strong>em</strong> The ‘em’ unit is equal to the computed value of the <a href="https://www.w3.org/TR/CSS2/fonts.html#propdef-font-size">‘font-size’</a> property of the element on which it is used. The exception is when ‘em’ occurs in the value of the ‘font-size’ property itself, in which case it refers to the font size of the parent element.</p>
</li>
<li>
<p><strong>%</strong> es un procentaje,  <strong>su valor computado depende de cada propiedad</strong> y no hay regla general.</p>
</li>
</ul>
<h3 id="colores">Colores</h3>
<p>Los colores se implementan siempre en <strong>RGB</strong>, hay dos maneras de escribirlos pero <strong>siempre</strong> simbolizan RGB</p>
<ul>
<li><strong>rgb(255,255,255)</strong> - Byte en rojo, verde y azul en numeros 0-255</li>
<li><strong>#rrggbb</strong> - Byytes en hexadecimal con dos caracteres para cada color de RGB ej ff=255</li>
<li><strong>#rgb</strong> bytes en exadecimal acortado, un caracter para cada color de RGB ej f=ff=255</li>
</ul>
<blockquote>
<p>A su vez hay colores mapeados en keywords, ej <strong>red, green, blue</strong></p>
</blockquote>
<h3 id="document-tree-y-formatting-structure">Document tree y formatting structure</h3>
<p>La especificacion propone un modelo de procesamiento  que funciona de la siguiente manera</p>
<ul>
<li>Se lee el documento html/xml y se genera un arbol de nodos llamado <strong>Document tree</strong> con un nodo por cada elemento</li>
<li>Se identifica el <strong>media type</strong></li>
<li>Se juntan todas las stylesheets y se extrae  el valor computado final de cada propiedad para cada elemento</li>
<li>Se añade al <strong>document tree</strong> las propiedades y valores css</li>
<li>Se genera un nuevo arbol de nodos llamado <strong>Formatting structure/tree</strong> que indica los elementos que se mostraran. <strong>este se puede parecer mucho al Document tree pero puede haber elementos de mas (:after, :before, los bullets de un elemento &lt;li&gt;) o de menos (display:none)</strong></li>
<li>Se Muestra el resultado en el medio elegido (pantalla, papel, etc)</li>
</ul>
<h3 id="computo-de-valores">Computo de valores</h3>
<h4 id="valores-que-se-calculan">Valores que se calculan</h4>
<p>Para cada propiedad se debe calcular una serie de valores:</p>
<ul>
<li><strong>Valor especificado:</strong> El valor de la propiedad que se obtiene despues de las herencias, cascada, etc.
<ul>
<li><strong>Valor computado / a heredar:</strong> El valor que se heredara a los elementos hijos, llamado <em>computed value</em>
<ul>
<li><strong>Valor usado/absoluto:</strong> El valor que se calcula en terminos absolutos a partir del valor a heredar. ej: de % a pixeles para mostrar en pantalla.</li>
</ul>
</li>
</ul>
</li>
</ul>
<h4 id="valores-especificados">Valores especificados</h4>
<p>Se calculan de la siguiente manera</p>
<ol>
<li>Si la  <a href="https://www.w3.org/TR/CSS2/cascade.html#cascade">cascade</a> resuelve un valor,  se usa ese.</li>
<li>Si hay una propiedad <a href="https://www.w3.org/TR/CSS2/cascade.html#inheritance">inherited</a> se usa el <em>computed value</em> del elemento padre.</li>
<li>Se usa la propiedad <em>default</em> o <em>initial</em></li>
</ol>
<h4 id="valores-a-heredar--computados">Valores a heredar / computados</h4>
<ul>
<li>Las URIs se hacen absolutas</li>
<li>Se pasan todas las medidas posibles a Px (em, %, etc) (salvo las heredadas)</li>
<li>Las propiedades se computan de acuerdo a cada una de sus funciones de computo especificas.</li>
</ul>
<h4 id="valores-absoluto">Valores <strong>absoluto</strong></h4>
<p>Muchos valores no pueden ser computados por que dependen de que los elementos del padre sean pasados a valor abosluto para calcular sus valores y asi calcular los valores absolutos. En esta insatancia se hace eso.</p>
<h3 id="herencia">Herencia</h3>
<p>Para muchas propiedades se hereda su valor de <strong>A</strong> a <strong>B</strong> siempre que la propiedad del <strong>B</strong> no tenga un valor explicito declarado.<br>
Si la propiedad no hereda el valor de forma default se lo puede forzar usando el valor <code>'inherit'</code></p>
<blockquote>
<p>Es importante aclarar que el valor heredado es siempre el <strong>Valor a heredar / computado</strong>  y no el <strong>valor especificado ni absoluto</strong></p>
</blockquote>
<p>Este valor se transforma en el nuevo <strong>valor especificado Y valor computado</strong> del elemento <strong>B</strong>.</p>
<p><strong>EJ:</strong></p>
<pre><code>body { font-size: 10pt }
h1 { font-size: 130% }
&lt;BODY&gt;
  &lt;H1&gt;A &lt;EM&gt;large&lt;/EM&gt; heading&lt;/H1&gt;
&lt;/BODY&gt;
</code></pre>
<p>El <strong>valor computado y entonces heredado</strong> en el h1 es <strong>13pt</strong>, entonces el EM <strong>hereda el valor 13p y NO 130%</strong></p>
<h3 id="the-cascade">The cascade</h3>
<p>El user agent colocara un peo a cada regla declarada y luego seleccionara la regla con mayor peso. Se calculan con la siguiente prioridad.</p>
<h4 id="calculo-de-cascada">Calculo de cascada</h4>
<ul>
<li><strong>Busqueda:</strong> Buscar todas las reglas que apliquen a un elemento.</li>
<li><strong>Origen:</strong> Ordenar en orden de prioridad por
<ol>
<li><strong>user-agent</strong> declarations</li>
<li><strong>user</strong> normal declarations</li>
<li><strong>author</strong> normal declarations</li>
<li><strong>author</strong> important declarations</li>
<li><strong>user</strong> important declarations (para accesibilidad)</li>
</ol>
</li>
<li><strong>Especificidad:</strong> Tomar las de mayor prioridad y ordenarlas por especificidad tomando la mas especifica.</li>
<li><strong>Orden:</strong> Si aun quedan valores de igual prioridad, tomar el ultimo declarado.</li>
</ul>
<h4 id="calculo-de-especificidad">Calculo de especificidad</h4>
<p>La especificidad que se usa en el calculo de cascada se computa con las siguientes prioridades.</p>
<ol>
<li><strong>Styles=</strong> Estilos indicados en atributo <em>styles</em></li>
<li><strong>#Id</strong> Estilos indicados mediante referencia al Id</li>
<li><strong>Cantidad de selectores usados</strong> Mayor cantidad de selectores, atributos y pseudo-clases se considera como mas especifico <strong>ej</strong> <code>.Conteneodor .parrafo .enfasis{}</code></li>
<li><strong>Cantidad de nombres de elementos usados</strong> Cuantos mas nombres de elementos usados mas especificidad <strong>ej</strong> <code>div h1{}</code></li>
</ol>
<h2 id="selectores">Selectores</h2>
<p>CSS 2.1 provee la siguiente lista de selectores para ubicar uno o varios elementos dentro del <strong>Document tree</strong></p>
<h3 id="por-orden-de-los-elementospor-orden-de-los-elementos">Por orden de los elementos<strong>POR ORDEN DE LOS ELEMENTOS</strong></h3>
<ul>
<li><strong>*</strong> - Cualquier elemento, cuando no se especifica un elemento en un selector se presume que se utiliza este</li>
<li><strong>E</strong> - Donde E es un tipo de elemento ej “div”, selecciona los elementos de ese tipo</li>
<li><strong>E F</strong> elementos de tipo F que sean descendientes de un elemento tipo E</li>
<li><strong>E &gt; F</strong> elemento tipo F que sea hijo directo de F</li>
<li><strong>E + F</strong> elemento de tipo F cuyo hermano inmediato precedente sea E (semanticamente tiene sentido entonces E + F)</li>
<li><strong>E:first-child</strong> Elemento E que ademas sea el primer hijo  de su elemento padre</li>
</ul>
<h3 id="por-atributo-de-los-elementospor-atributo-de-los-elementos">Por atributo de los elementos<strong>POR ATRIBUTO DE LOS ELEMENTOS:</strong></h3>
<blockquote>
<p><strong>ATENCION:</strong></p>
<ul>
<li>las <strong>clases de CSS</strong> son atributos y se povee el <strong>shorthand .foo</strong> para referirse a clases, pero <strong>la forma original seria *[class~=“foo”]</strong></li>
<li>Cuando no se provee elemento <strong>E</strong> se presume <strong>*</strong></li>
</ul>
</blockquote>
<ul>
<li><strong>E[foo]</strong> Elemento E con un atributo foo (sin importar el valor)</li>
<li><strong>E[foo=“warning”]</strong> Elemento E con atributo foo valor ‘warning’</li>
<li><strong>E[foo~=“warning”]</strong> elemento E con atributo foo que tiene una lista de valores separado por espacios entre los cuales esta ‘warning’</li>
<li><strong>E[foo|=“warning”]</strong> elemento E con atributo foo que tiene una lista de valores separado por guiones entre los cuales esta ‘warning’</li>
<li><strong>E#myid</strong> Elemmento E con id #myid</li>
</ul>
<h3 id="pseudo-clasespseudo-clases">Pseudo-clases<strong>PSEUDO-CLASES</strong></h3>
<p>Son la forma que tiene CSS de acceder a informacion que no esta explicitamente provista en el lenguaje de markup o el arbol de nodos <strong>Document tree</strong>, por ejemplo el primer renglon de un parrafo</p>
<ul>
<li><strong>E:link</strong>  si E es un achor NO visitado</li>
<li><strong>E:visited</strong> si E es un achor SI visitado</li>
<li><strong>E:active, E:hover, E:focus</strong> Si el elemento es sujeto a una accion del usuario</li>
</ul>
<p>Podes combinar selectores uno despues del otro para indicar mas especificamente que deseas seleccionar.</p>
<h3 id="pseudo-elementos">Pseudo-elementos</h3>
<ul>
<li><strong>E:first-line</strong> La primera linea de texto del contenido del elemento E se enmarca en un pseudo elemento al que le podes poner estilos</li>
<li><strong>E:first-letter</strong> La primera letra del elemento E se enmarca en un pseudo elemento al que le podes poner estilos</li>
<li><strong>E:after</strong> Inserta un pseudo elemento despues del elemento E el cual debe tener contenido usando <em>content:""</em> y se le pueden agregar estilos</li>
<li><strong>E:before</strong> Inserta un pseudo elemento antes del elemento E el cual debe tener contenido usando <em>content:""</em> y se le pueden agregar estilos</li>
</ul>
<h2 id="media-types">Media types</h2>
<p>Una de las propiedades de CSS es que describe la presentacion del contenido en cualquier formato (audio, braile, texto, impreso, digital).</p>
<p>Algunas propiedades de CSS aplican a uno o varios media types, otros pueden aplicar a todos.</p>
<blockquote>
<p><strong>Las propiedades no declaradas para un media type especifico aplican a todos los media types.</strong></p>
</blockquote>
<p><strong>Se declara asi:</strong></p>
<pre><code>@media print, scree, otros {
  /* style sheet for print goes here */
}
</code></pre>
<p><strong>Los media types validos son:</strong></p>
<ul>
<li><strong>all</strong> Suitable for all devices.</li>
<li><strong>braille</strong> Intended for braille tactile feedback devices.</li>
<li><strong>embossed</strong> Intended for paged braille printers.</li>
<li><strong>handheld</strong> Intended for handheld devices (typically small screen, limited bandwidth).</li>
<li><strong>print</strong> Intended for paged material and for documents viewed on screen in print preview mode.</li>
<li><strong>projection</strong> Intended for projected presentations, for example projectors.</li>
<li><strong>screen</strong> Intended primarily for color computer screens.</li>
<li><strong>speech</strong> Intended for speech synthesizers.</li>
<li><strong>tty</strong> Intended for media using a fixed-pitch character grid (such as teletypes, terminals, or portable devices with limited display capabilities).</li>
<li><strong>tv</strong> Intended for television-type devices (low resolution, color, limited-scrollability screens, sound available).</li>
</ul>
<h2 id="box-model">Box model</h2>
<p>TODOS los elementos en CSS se representan como CAJAS. El modelo de cajas se basa en que <strong>un elemento consiste en varias cajas una dentro de la otra</strong>, esas cajas son:</p>
<ul>
<li>El tamaño del contenido</li>
<li>El padding</li>
<li>El border</li>
<li>El Margen</li>
</ul>
<p><img src="https://lh3.googleusercontent.com/BSdXPy1iKoW_RdmcsEKVAomZV7hcOWc2t3DHqPnHPZeBrjYYxV3JsN2BzdoCs8BlIPchL5dprAH6" alt="enter image description here" title="ff"></p>
<ul>
<li>El tamaño del contenido</li>
<li>El padding</li>
<li>El border</li>
<li>El Margen</li>
</ul>
<h3 id="margen">Margen</h3>
<ul>
<li>Siempre es <strong>transparente</strong></li>
<li>Su <strong>%</strong> se calcula en base al ancho del <strong>contianing block</strong>.</li>
<li>Para elementos <strong>inline-block se ignoran</strong> los margenes <strong>Top y Bottom</strong></li>
</ul>
<p>Tiene las siguientes caracteristicas</p>
<blockquote>
<ul>
<li><strong>Value:</strong> length | percentage |auto | inherit</li>
<li><strong>Initial:</strong> 0</li>
<li><strong>Applies to:</strong> all elements except elements with table display types other than table-caption, table and inline-table</li>
<li><strong>Inherited:</strong> no</li>
<li><strong>Percentages:</strong> refer to width of containing block</li>
<li><strong>Media:</strong> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a></li>
<li><strong>Computed value:</strong> the percentage as specified or the absolute length</li>
</ul>
</blockquote>
<h4 id="valor-auto---wip">Valor auto - WIP</h4>
<p><strong>AUTO</strong> tiene diferentes comportamientos dependiendo del tipo de elemento<br>
<strong>PARA MARGIN-LEFT:AUTO Y/O MARGIN-RIGHT:AUTO</strong></p>
<ul>
<li><strong>inline/replaced inline/inline-block:</strong> Auto es el valor 0</li>
<li><strong>block/replaced block</strong> si estas en <strong>normal flow</strong> y
<ul>
<li>los margenes + padding + borders+ content es <strong>mayor que el containing block</strong> entonces los <strong>margenes auto valen 0</strong></li>
<li>Si los valores computados de width, padding y un margen estan calculados y el margen restante es auto, se añade el ancho faltante para completar el containing box</li>
<li><strong>Si ambos son auto</strong> se centra horizontalmente el elemento</li>
<li><strong>si el elemento es float</strong> los margenes auto son 0</li>
</ul>
</li>
<li><strong>Absolutely positioned</strong>
<ul>
<li><strong>Si left, right y width tienen valores</strong>: Margenes auto centran el elemento<br>
*<strong>Caso contrario</strong>: Margenes auto son cero</li>
</ul>
</li>
</ul>
<p><strong>PARA MARGIN-TOP:AUTO Y/O MARGIN-BOTTOM:AUTO</strong></p>
<p>Resuelve siempre en 0</p>
<h4 id="collapsing-margins">Collapsing margins</h4>
<p><a href="https://www.youtube.com/watch?v=uEfH6qnFF6Y&amp;t=944s">VER VIDEO PARA ENTENDER BIEN</a></p>
<p>Los margenes <strong>verticales</strong> colapsan en uno solo <strong>siempre que se tocan y son block o inline block elements Y participan del mismo BFC</strong>. para evitar que se toquen hay que colocar algo en el medio (ej border)<br>
<a href="https://www.w3.org/TR/CSS2/box.html#collapsing-margins">hay varias posibles condiciones para que los margenes colapsen</a></p>
<blockquote>
<p>Este mecanismo pemite que los textos esten separados por margenes siempre de por lo menos un cierto tamaño (ej que no se sumen)</p>
</blockquote>
<p><strong>Eso puede ocurrir con:</strong></p>
<ul>
<li><strong>Siblings</strong> si se toca el margin-bottom de uno con el margin-top de otro</li>
<li><strong>parent-child/grandchild SUPER ANTI-INTUITIVO</strong> si los dos margenes top se tocan y estan en el mismo BFC (no hay padding o border)
<ul>
<li><strong>En este caso si el margen colapsado es el del child se genera un margen adentro del elemento hijo que empuja al parent y todos los children hacia abajo</strong></li>
</ul>
</li>
</ul>
<h3 id="padding">Padding</h3>
<ul>
<li>Es del color del background</li>
<li>Su <strong>%</strong> se calcula en base al ancho del <strong>contianing block</strong>.</li>
<li>A diferencia del margen, no puede ser negativo</li>
</ul>
<p>Tiene las siguientes caracteristicas:</p>
<blockquote>
<p><strong>Value:</strong> length | percentage |auto | inherit| inherit<br>
<strong>Initial:</strong> 0<br>
<strong>Applies to:</strong> all elements except table-row-group, table-header-group, table-footer-group, table-row, table-column-group and table-column<br>
<strong>Inherited:</strong> no<br>
<strong>Percentages:</strong> refer to width of containing block<br>
<strong>Media:</strong> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a><br>
<strong>Computed value:</strong> the percentage as specified or the absolute length</p>
</blockquote>
<h3 id="border">Border</h3>
<p>Los bordes son lineas de un color unico que van entre el margen y el padding.</p>
<h4 id="border-width"><strong>Border-Width</strong></h4>
<p>especifica el ancho del border y tiene las siguientes caracteristicas</p>
<blockquote>
<ul>
<li><strong>Value:</strong> Thin  | Medium | Thick | &lt;Length&gt; | inherit</li>
<li><strong>Initial:</strong> medium</li>
<li><strong>Applies to:</strong> all elements</li>
<li><strong>Inherited:</strong> no</li>
<li><strong>Percentages:</strong> N/A</li>
<li><strong>Media:</strong> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a></li>
<li><strong>Computed value:</strong> absolute length; ‘0’ if the border style is ‘none’ or ‘hidden’</li>
</ul>
</blockquote>
<h4 id="border-color"><strong>Border-Color</strong></h4>
<p>especifica el color del border y tiene las siguientes caracteristicas</p>
<blockquote>
<ul>
<li><strong>Value:</strong> &lt;color&gt; | transparent  | inherit</li>
<li><strong>Initial:</strong> see individual properties<br>
Applies to:all elements</li>
<li><strong>Inherited:</strong> no</li>
<li><strong>Percentages:</strong> N/A</li>
<li><strong>Media:</strong> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a></li>
<li><strong>Computed value:</strong> see individual properties</li>
</ul>
</blockquote>
<h4 id="border-style"><strong>Border-style</strong></h4>
<p>Especifica el tipo de linea del border</p>
<p><strong>none:</strong> No border; the computed border width is zero.<br>
<strong>hidden:</strong> Same as ‘none’, except in terms of <a href="https://www.w3.org/TR/CSS2/tables.html#border-conflict-resolution">border conflict resolution</a> for <a href="https://www.w3.org/TR/CSS2/tables.html">table elements</a>.<br>
<strong>dotted:</strong> The border is a series of dots.<br>
<strong>dashed:</strong> The border is a series of short line segments.<br>
<strong>solid:</strong> The border is a single line segment.<br>
<strong>double:</strong> The border is two solid lines. The sum of the two lines and the space between them equals the value of <a href="https://www.w3.org/TR/CSS2/box.html#propdef-border-width">‘border-width’</a>.<br>
<strong>groove:</strong> The border looks as though it were carved into the canvas.<br>
<strong>ridge:</strong> The opposite of ‘groove’: the border looks as though it were coming out of the canvas.<br>
<strong>inset:</strong> The border makes the box look as though it were embedded in the canvas.<br>
<strong>outset:</strong> The opposite of ‘inset’: the border makes the box look as though it were coming out of the canvas.</p>
<h2 id="visual-formatting-model">Visual formatting model</h2>
<p>Es el algoritmo por el cual CSS determina donde colocar los elementos del markup.</p>
<h3 id="terminos-1">Terminos</h3>
<ul>
<li>
<p><strong>containing box:</strong>  La caja dentro de la cual vive  un elemento, generalmente definida por la caja del elemento padre.</p>
</li>
<li>
<p><strong>Block-level boxes</strong> son boxes que participan del block formatting context</p>
</li>
<li>
<p><strong>Block container box</strong> osea que solo puede contener <em><strong>una</strong></em> de estas dos opciones de contenido.</p>
<ul>
<li>Solamente block-level boxes</li>
<li>Solo inline-level boxes<br>
<strong>Es decir que si tenes un elemento con blocks y inline elements los inline elements se transforman en block denominado BLOCK ANONIMO</strong></li>
</ul>
</li>
<li>
<p><strong>Line box</strong> La caja que representa un renglon con uno o mas inline elements en su interior</p>
</li>
<li>
<p><strong>positioned box</strong> Una caja con un valor de position diferente de static</p>
</li>
</ul>
<h3 id="posicionamiento">Posicionamiento</h3>
<p>Hay 3 formas de posicionamiento</p>
<ul>
<li><strong>Normal flow:</strong>
<ul>
<li><strong>En Block formatting contexts (BFC)</strong></li>
<li><strong>En inline formatting contexts (IFC)</strong></li>
<li><strong>En relative positioning contexts (RPC)</strong></li>
</ul>
</li>
<li><strong>Floats:</strong> Se arma la caja como si estuviera en flow, luego se remueve de flow y se coloca a la izquierda/derecha del parent o float mas proximo</li>
<li><strong>Absolute positioning:</strong> Se remueve la caja del flow y se coloca en una posicion con respecto al Containing box.
<ul>
<li><strong>Fixed:</strong> es un tipo de  Absolute positioning pero siempre con respecto al viewport</li>
</ul>
</li>
</ul>
<h3 id="containing-box">Containing box</h3>
<p>El containing box es el lugar donde <strong>vive un elemento</strong> y <strong>apartir del cual se calculan los valores de</strong></p>
<ul>
<li><strong>Height y width</strong> al usar %</li>
<li><strong>margin</strong> al usar %</li>
<li><strong>top, bottom, left, right</strong> al usar %</li>
</ul>
<p>El containing box de un elemento depende del valor de posicion de ese objeto:</p>
<ul>
<li><strong>position: static | relative</strong>  el contennt box del elemento padre</li>
<li><strong>position: absolute</strong> el padding box del ancestro mas proximo con
<ul>
<li><code>position: absolute|relative| fixed | sticky</code></li>
<li><code>transform</code> ,  <code>perspective</code> o <code>filter</code> con valor diferente de <code>none</code></li>
<li><code>contain</code> con valor igual a <code>paint</code></li>
<li>Si ninguno de estos existe entonces es el ancestro mas proximo</li>
</ul>
</li>
<li><strong>Position:fixed</strong> el viewport para screen o la hoja de papel para print</li>
</ul>
<h3 id="normal-flow">Normal Flow</h3>
<p>En el normal flow <strong>cada elemento siempre pertenece a un y solo un formatting context</strong> que dictara cual es la posicion de ese elemento.</p>
<blockquote>
<p>Un elemento crea un Inline formatting context <strong>IFC</strong> si contiene solamente elementos inline, de lo contrario forma un Block formatting context <strong>BFC</strong>.</p>
</blockquote>
<p>si hay <strong>inline elements</strong> y <strong>block elements</strong> mezclados en el <strong>mismo formatting context</strong> entonces se usa el motor CSS coloca los inline elements en bloques para que participen del block formatting context. Esos blocks se denominan <strong>anonymous blocks</strong> y en su interior puede existir un <strong>IFC</strong></p>
<h4 id="block-elements">Block Elements</h4>
<p>Los block elements son elementos que:</p>
<ul>
<li><strong>se comportan como bloques</strong> (son siempre cuadrados)</li>
<li>Generalmente colocan su contenido dentro de un <strong>Block-level box</strong>, es decir que participan del <strong>BFC</strong></li>
<li>Generalmente se comporta como un <strong>Block container box</strong>, osea que su contenido sea solamente block-level boxes o inline-level boxes</li>
</ul>
<h4 id="block-formatting-context-bfc">Block Formatting Context (BFC)</h4>
<p><a href="https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/">Ver mas</a></p>
<p>El BFC  es <strong>el area donde varios block  elements (parent,siblings, children, etc) estan contenidos e interactuan entre si</strong>.</p>
<p>En un BFC:</p>
<ul>
<li><strong>LAYOUT:</strong>
<ul>
<li>los elementos van <strong>uno encima del otro.</strong> y <strong>ocupan todo el ancho</strong></li>
<li>Los elementos <strong>tocan el borde izquierdo</strong> del contenedor, aun si hay floats</li>
<li>Los elementos <strong>inline SE TRANFORMAN EN BLOCKS</strong> mediante <strong>anonymous box generation</strong></li>
</ul>
</li>
<li><strong>COLLAPSING MARGINS:</strong> Solo los <strong>margenes</strong> de los elementos dentro del mismo BFC pueden <strong>colapsar</strong> entre si</li>
</ul>
<p>Algunas propiedades de CSS hacen que un elemento pueda crear su propio BFC.</p>
<ul>
<li><code>overflow: auto</code></li>
<li><code>display: flow-root</code> - <a href="https://caniuse.com/#search=display:%20flow-root">ver support</a></li>
</ul>
<h4 id="anonymous-box-generation">Anonymous box generation</h4>
<p>Un <strong>BFC</strong> organiza todos los elementos en su interior como Blocks, sin embargo es obvio que podes tener un elemento con childs que sean inline y blocks mezclados.</p>
<p>Cuando pasa esto <strong>el BFC genera cajas alrededor de los inline elements</strong> para poder tratarlos como blocks. estas cajas no pueden ser seleccionadas con selectores, por eso se las llama <strong>anonymous boxes</strong></p>
<p><img src="https://lh3.googleusercontent.com/6HHOcEXZOGCGZaLLmVILN10fBSsdlwTgcjSNKYmXpttNk3UPKcowHE03Cjab-poZXA9BhPU7n2Or" alt="enter image description here"></p>
<h4 id="inline-elements">Inline elements</h4>
<p>Son aquellos elementos que</p>
<ul>
<li>Se distribuyen <strong>Horizontalmente</strong> uno al lado del otro</li>
<li>Participan del <strong>inline formatting context</strong></li>
<li><strong>Su alto y ancho</strong> estan totalmente definidos por el contenido y <strong>NO PUEDEN MODIFICARSE</strong></li>
<li><strong>Se distribuyen en renglones llamados line box</strong> que contienen uno o mas inline elements (ej texto y alguna palabra con negritas son line elements separados pero estan en el mismo renglon)</li>
</ul>
<p>Generalmente el texto y los links son inline elements<br>
<strong>Inline-Block</strong> es un block colocado como si fuera un inline element.</p>
<h4 id="inline-formatting-context-ifc">Inline Formatting Context (IFC)</h4>
<p>El IFCes <strong>el area donde varios inline elements estan contenidos e interactuan entre si</strong> se distribuyen de izquierda a derecha hasta llegar al final del contenedor (o del contenido) y se lo coloca en un <strong>line box</strong>, luego se continua con ese proceso en un <strong>line box</strong> inmediatamente por debajo del al anterior .</p>
<p>Entonces <strong>un parrafo es una pila de line boxes</strong>.</p>
<p><strong>En un IFC:</strong></p>
<ul>
<li><strong>Los elementos van uno a la derecha del otro</strong> en normal flow, comenzando desde el lado superior izquierdo del containing box.</li>
<li><strong>Se agrupan en un LINE BOX por cada renglon</strong>. un Line box puede tener uno o mas inline elements (ej texto y negrita)
<ul>
<li><strong>Los elementos en un LINE BOX pueden ser alineados verticalmente</strong> de formas diferentes (ej: textos de diferentes tamaños alineados centrado quedan mal, los alineas en baseline para que queden en el mismo renglon)</li>
</ul>
</li>
</ul>
<p>Cada renglon es un <strong>line box:</strong><br>
<img src="https://lh3.googleusercontent.com/LF-qMyJATr4tKbLvzjCnab0L7Qv1kSLAusVHMn-apAwi9YuF-Nv0KQXtI-OifhH3Ycz5sWJ6pABn" alt="enter image description here"></p>
<p>Cada <strong>line box</strong> tiene uno o varios <strong>inline elements</strong><br>
<img src="https://lh3.googleusercontent.com/_a6ZSJrsRblNZx_mkxnYc0Vfz6b3tcUIOrg5gcgwoz1HDalJTFAqt-OFSY2MWb-5CwyM57aMByvF" alt="enter image description here"></p>
<h3 id="relative-positioning">Relative positioning</h3>
<p>El Relative positioning es una forma de posicionamiento que coloca los objetos de manera relativa al lugar donde irian en su posicion en normal flow conservando ademas el lugar originalmente reservado para ellos</p>
<ul>
<li>Mueve el elemento con respecto a su posicion en normal flow</li>
<li>Preserva el lugar que ocuparia en el normal flow</li>
</ul>
<blockquote>
<p><strong>El tamaño del elemento no puede cambiar como resultado del posicionamiento relativo!</strong></p>
</blockquote>
<p><strong>Posicionamiento:</strong></p>
<ul>
<li><strong>Left y Right:</strong> Son para posicionar el elemento. Solo podes usar <strong>una de las dos propiedades a la vez</strong> ya que el tamaño del elemento no puede cambiarse</li>
<li><strong>Top y bottom</strong> tambien son para posicionar el lemento y solo puede usarse <strong>una de las dos</strong> ya que el tamaño del elemento no puede cambiarse</li>
<li>Usar <strong>auto</strong> como valor equivale a usar 0.</li>
</ul>
<h3 id="float">Float</h3>
<p>El proposito de un float es que el contenido (block sibling inmediato o inlines) pueda fluir a a lo largo de su altura.</p>
<h4 id="funcionamiento">Funcionamiento</h4>
<p>Un float opera e interactua con otros elementos <strong>solo si estan en el mismo BFC</strong></p>
<p><strong>Un float:</strong></p>
<ul>
<li><strong>Se corre a</strong> a la derecha o izquierda hasta
<ul>
<li>tocar el borde de su contenedor</li>
<li>Tocar el borde de otro float</li>
<li><strong>Si no entra a la derecha o izquierda del float mas proximo</strong>, se coloca debajo de este y tocando el borde del contenedor</li>
</ul>
</li>
<li>No forma parte del <strong>Normal flow</strong> entonces
<ul>
<li><strong>El parent no puede determinar su altura solo usando los floats</strong></li>
<li><strong>Otros block elements se pueden posicionan debajo del float como si el float no existiera</strong></li>
</ul>
</li>
<li>Aquellos blocks que <strong>queden detras del float ( parents, grandparents etc en el mismo BFC) acortan sus  line boxes</strong> para que queden <strong>entre el ultimo float y el borde del contenedor</strong> generando inline elements a su alededor, aunque esten en otro bloque</li>
<li><strong>Los sibling inline elements</strong> acortan sus line boxes para  <em>fluir</em> al costado del float</li>
</ul>
<p><img src="https://lh3.googleusercontent.com/ErhVqPIW1uIV_EJKhx1CCpssJdVrAKpjlpyeOiiGyaWsqEcDYlpxrJ7hIIrlC4ZCh81we80j1C8p" alt="enter image description here"></p>
<ul>
<li><strong>El contenido circundante:</strong>
<ul>
<li>Su box siempre <strong>pasa por atras del float</strong> para estar <strong>tocando el left side del contenedor</strong> siempre que el ancho maximo del elemento lo permita (sino pasa a la siguiente linea).</li>
<li>Los inline elements se colocan al costado del float siempre que formen parte del mismo BFC (no necesitan ser siblings grandparents, etc, se puede dar con cualquier jerarquia)</li>
</ul>
</li>
</ul>
<h4 id="clearing">Clearing</h4>
<p>La propiedad <em>Clear</em> permite que un <strong>bloque</strong> que normalmente quedaria <strong>encimado por el float</strong> quede <strong>debajo del float</strong>.</p>
<p>Lo hace mediante un <strong>margen invisible extendido</strong>  (ver imagen de arriba) que se genera <strong>despues del margen normal del elemento</strong> y se lo llama <strong>CLEARANCE</strong></p>
<ul>
<li><strong>Cuaquiera de los dos</strong>
<ul>
<li><strong>Si tiene clear left o right</strong> El elemento no puede estar a continuacion de un float (dentro del mismo BFC)</li>
</ul>
</li>
</ul>
<h3 id="absolute-positioning">Absolute positioning</h3>
<p>En el modelo de absolute positioning:</p>
<ul>
<li>Se posiciona la caja con respecto a su <strong>containing block</strong>
<ul>
<li>El <strong>padding box</strong> del <strong>ancestro</strong> con <strong>position no static mas proximo</strong></li>
</ul>
</li>
<li>Se lo remueve del <strong>normal flow</strong></li>
<li>Establece un <strong>nuevo BFC en su interior</strong></li>
<li><strong>Ignora page-breaks en printed media e imprime como si fuera un documento continuo</strong></li>
<li>Se posicionan los lados de la <strong>margin box</strong> del elemento de acuerdo al <strong>padding box</strong> del elemento padre usando <strong>top, bottom, left, right</strong>, pudiendo usar las 4 a la vez</li>
</ul>
<blockquote>
<p><strong>IMORTANTE:</strong> Para absolute positioning el <strong>containing block</strong> sigue varias relas, ver la seccion <strong>containing block</strong> para mas detalles</p>
</blockquote>
<h3 id="fixed-positioning">Fixed positioning</h3>
<p>Fixed positioning:</p>
<ul>
<li>Es <strong>una subcategoria de absolute positioning</strong></li>
<li>Su <strong>containing block</strong> es
<ul>
<li>el viewport en screen</li>
<li>cada pagina en print</li>
</ul>
</li>
<li><strong>En screen media:</strong> No se mueven cuando se scrollea el viewport</li>
<li><strong>en print media:</strong> el elemento se repite para cada pagina.</li>
</ul>
<h3 id="stacking-context-y-layering">Stacking context y layering</h3>
<p>Todas las cajas en CSS tienen una posicion Z que determina cual se pinta sobre cual. <strong>Para las positioned boxes es posible determinar la posicion z manualmente con la propiedad Z-index</strong> mientras que para las demas se coloca un <strong>valor Z defaut de 0</strong></p>
<p>Los Z-index son valores en el eje z, pero se usan dentro de un <strong>stacking context</strong>,  es decir que <strong>no son valores absolutos</strong></p>
<blockquote>
<p>un elemento con z-index 99 puede <strong>estar abajo</strong> de un elemento con z-index 1 si <strong>no comparten el mismo stacking context</strong></p>
</blockquote>
<h4 id="terminos-2">Terminos</h4>
<p>El <strong>Stacking context</strong> y los <strong>Stack levels</strong> determinan como se apilan aquellas cajas que se superponen gracias a que son <strong>positioned boxes (absolute, fixed o relative)</strong></p>
<ul>
<li><strong>Stacking context:</strong> Es el lugar donde interactuan y se ordenan los elementos que poseen un Stack level.
<ul>
<li><strong>Son atomicos</strong>
<ul>
<li>los elementos de un stacking context estan siempre atras o adelante de todos los elementos en otro static context</li>
<li>Cada caja solo puede estar en un stacking context</li>
</ul>
</li>
<li><strong>Se crean nuevos Stacking contexts con</strong>
<ul>
<li>caja con z-index, sus childs estan en otro stacking context</li>
<li>Positioned box: sus childs tienen su propio stacking context</li>
</ul>
</li>
</ul>
</li>
<li><strong>Stack level:</strong> Es el orden en el cual se muestran los elementos que comparten un stack context
<ul>
<li><strong>Mayor stacking</strong> level es mas cerca del usuario</li>
<li><strong>Stacking levels iguales</strong> implica que se usa el orden del documento HTML</li>
</ul>
</li>
</ul>
<h4 id="propiedad-z-index">Propiedad z-index</h4>
<p>Para controlar estos parametros se usa la propiedad <strong>z-index</strong></p>
<blockquote>
<ul>
<li><strong>Value:</strong>  int | auto | inherit</li>
<li><strong>Initial:</strong> auto</li>
<li><strong>Applies to:</strong>  SOLO POSITIONED ELEMENTS</li>
<li><strong>Inherited:</strong> no</li>
<li><strong>Percentages:</strong> N/A</li>
<li><strong>Media:</strong> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a></li>
<li><strong>Computed value:</strong> as specified</li>
</ul>
</blockquote>
<ul>
<li><strong>Intiger:</strong>
<ul>
<li>Es el <strong>stack level</strong> del elemento</li>
<li>Especifica que dentro del elemento <strong>se generara un nuevo stacking context</strong></li>
</ul>
</li>
<li><strong>auto:</strong>
<ul>
<li>El <strong>stack level</strong> es zero</li>
<li>No se crea un nuevo <strong>stacking context</strong></li>
</ul>
</li>
</ul>
<h4 id="orden-de-apilado">Orden de apilado</h4>
<p>El orden final de los elementos en el eje Z  <strong>DENTRO DE  un stacking context</strong> es el siguiente</p>
<ol>
<li>el background y borders del elemento que genera el stacking context</li>
<li>Elementos de <code>z-index &lt;0</code></li>
<li>elementos  <code>no-inline</code> con <code>position: static</code></li>
<li><code>Floats</code> en position static.</li>
<li>elementos <code>inline</code> con <code>position: static</code></li>
<li>elementos con <code>z-index=0</code> o <code>posicion NO static</code></li>
<li>Elementos con <code>z-index &gt;0</code></li>
</ol>
<p><img src="https://lh3.googleusercontent.com/Nz7JT7spqEsAI0CiLnQxW8b21jDDaan6UxvfD-B9byqi7Sb0H_jwwNJNBUXVBB4yXITfcRAHYKbB" alt="" title="stacking order"><br>
A su vez los stacking contexts anidados no pueden cambiar su posicion con respecto a los stacking contexts por encima de ellos.</p>
<blockquote>
<p>Osea que <strong>los hijos de dos stacking contexts diferentes no cambiaran de posicion entre si</strong> aunque tengan z-index 0 y z-index 9999</p>
</blockquote>
<p><img src="https://lh3.googleusercontent.com/dlzr1P25LoDz5GCmfEm2-qNlYuPfryRTw4JmdVwpJ0jFvsQAXHEVfm3MVtOn_gBV2q_IYFUfEcO4" alt="" title="context"><br>
<img src="https://lh3.googleusercontent.com/iJECytv2wy2PjY94nniKuV-PbtrnjfwY7eyXoVjc9nW3bphaTspapVtMKh04chaWz6TaIYsu44Rx" alt="" title="context2"></p>
<h3 id="width-y-height">Width y height</h3>
<h4 id="width">Width</h4>
<p>Determina el ancho del <strong>content box</strong> de un elemento, <strong>no tiene efectos en inline elements</strong></p>
<blockquote>
<ul>
<li><strong>Value:</strong>  length | v% | auto | inherit</li>
<li><strong>Initial:</strong> auto</li>
<li><strong>Applies to:</strong>  elementos no-inline, table rows y row groups</li>
<li><strong>Inherited:</strong> no</li>
<li><strong>Percentages:</strong> el ancho del containing block</li>
<li><strong>Media:</strong> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a></li>
<li><strong>Computed value:</strong> as specified</li>
</ul>
</blockquote>
<ul>
<li><strong>Length:</strong> ancho en unidades de medida</li>
<li><strong>%</strong> porcetaje del ancho del *<em>containing block</em></li>
<li><strong>auto</strong> depende del valor de otras propiedades
<ul>
<li><strong>inline</strong> No aplica, se usa el valor del contenido</li>
<li><strong>inline replaced y block replaced elements</strong>
<ul>
<li><strong>width y height son auto</strong>: el ancho intrinseco del elemento (ej una imagen)</li>
<li><strong>width auto y el elemento tiene ancho intrinseco</strong> ancho intrinseco del elemento</li>
<li><strong>height tiene valor especificado o intrinseco, width auto y el elemento tiene un aspect ratio establecido</strong>: height * aspect ratio (ej una imagen consera su aspect ratio)</li>
</ul>
</li>
<li><strong>block</strong>
<ul>
<li>Los valores <strong>auto</strong> para margins, paddings y borders pasan a 0 y se calcula el ancho con la equacion <strong>margins+widths+borders+paddings = containter box</strong></li>
</ul>
</li>
<li><strong>inline block</strong>: shrink to fitt</li>
<li><strong>Position absolute</strong>
<ul>
<li>Dada la siguiente equacion : <code>'left'+ 'right' + 'margins' + 'borders' + 'paddings' + 'width' = width of containing block</code></li>
<li><strong>Si width es auto y no hay left Y right definidos</strong>: width es shrink-to-fit</li>
<li><strong>Caso contrario</strong>: se usa la equacion para definir el width</li>
</ul>
</li>
</ul>
</li>
</ul>
<h4 id="height">Height</h4>
<p>Permite especificar el alto de un elemento,  <strong>no sirve para los inline elements</strong></p>
<blockquote>
<p><em>Value:</em>   | auto | inherit<br>
<em>Initial:</em> auto<br>
<em>Applies to:</em> Todo salvo  non-replaced inline elements, table columns, and column groups<br>
<em>Inherited:</em> no<br>
<em>Percentages:</em> Ver detalles<br>
<em>Media:</em> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a><br>
<em>Computed value:</em> the percentage or ‘auto’ (see prose under <a href="https://www.w3.org/TR/CSS2/syndata.html#value-def-percentage"></a>) or the absolute length</p>
</blockquote>
<p><strong>Valores:</strong></p>
<ul>
<li><strong>Length:</strong> una cantidad en px, em, etc que determina el alto</li>
<li><strong>%:</strong>
<ul>
<li><strong>Containing block tiene height explicito:</strong> Procentaje del containing block height</li>
<li><strong>Containing block sin height:</strong> resuelve a <em>auto</em></li>
</ul>
</li>
<li><strong>auto:</strong>
<ul>
<li><strong>inline</strong> no aplica, el alto es siempre el del contenido</li>
<li><strong>replaced elements (Inline , block, inline-block, float):</strong>
<ul>
<li><strong>con intrinsic value y width auto</strong> se usa intrinsic value</li>
<li><strong>con instrinsic ratio y width definido</strong> se usa <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mtext>width&nbsp;</mtext><mi>x</mi><mtext>&nbsp;ratio&nbsp;</mtext></mrow><annotation encoding="application/x-tex">\text{width } x \text{ ratio }</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.69444em; vertical-align: 0em;"></span><span class="mord text"><span class="mord">width&nbsp;</span></span><span class="mord mathnormal">x</span><span class="mord text"><span class="mord">&nbsp;ratio&nbsp;</span></span></span></span></span></span></li>
</ul>
</li>
<li><strong>Blocks en  normal flow con ‘<code>overflow:visible</code>’</strong> tamaño en base al contenido
<ul>
<li>Ultimo line box (en IFC)</li>
<li>Ultimo block element en flow (en BFC)</li>
<li>zero  para los otros casos</li>
</ul>
</li>
<li><strong>Absolutely positioned, non-replaced</strong>
<ul>
<li><strong>Top o bottom establecidos:</strong> se calcula height igual que en blocks en normal flow</li>
<li><strong>Top y bottom establecidos</strong> El alto usado es el que falte para llenar el containing block</li>
<li><strong>Top auto:</strong> se usa el top que se usaria en normal flow</li>
<li><strong>Otros auto:</strong> se resuelve llevando el elemento al tamaño del container block usando la equacion <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>c</mi><mi>o</mi><mi>n</mi><mi>t</mi><mi>a</mi><mi>i</mi><mi>n</mi><mi>e</mi><mi>r</mi><mi>H</mi><mi>e</mi><mi>i</mi><mi>g</mi><mi>h</mi><mi>t</mi><mo>=</mo><mi>m</mi><mi>a</mi><mi>r</mi><mi>g</mi><mi>i</mi><mi>n</mi><mi>s</mi><mo>+</mo><mi>p</mi><mi>a</mi><mi>d</mi><mi>d</mi><mi>i</mi><mi>n</mi><mi>g</mi><mi>s</mi><mo>+</mo><mi>t</mi><mi>o</mi><mi>p</mi><mo>+</mo><mi>b</mi><mi>o</mi><mi>t</mi><mi>t</mi><mi>o</mi><mi>m</mi><mo>+</mo><mi>h</mi><mi>e</mi><mi>i</mi><mi>g</mi><mi>h</mi><mi>t</mi></mrow><annotation encoding="application/x-tex">containerHeight=margins+paddings+top+bottom+height</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.88888em; vertical-align: -0.19444em;"></span><span class="mord mathnormal">co</span><span class="mord mathnormal">n</span><span class="mord mathnormal">t</span><span class="mord mathnormal">ain</span><span class="mord mathnormal">erHe</span><span class="mord mathnormal">i</span><span style="margin-right: 0.03588em;" class="mord mathnormal">g</span><span class="mord mathnormal">h</span><span class="mord mathnormal">t</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 0.85396em; vertical-align: -0.19444em;"></span><span class="mord mathnormal">ma</span><span style="margin-right: 0.02778em;" class="mord mathnormal">r</span><span style="margin-right: 0.03588em;" class="mord mathnormal">g</span><span class="mord mathnormal">in</span><span class="mord mathnormal">s</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 0.88888em; vertical-align: -0.19444em;"></span><span class="mord mathnormal">p</span><span class="mord mathnormal">a</span><span class="mord mathnormal">dd</span><span class="mord mathnormal">in</span><span style="margin-right: 0.03588em;" class="mord mathnormal">g</span><span class="mord mathnormal">s</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 0.80952em; vertical-align: -0.19444em;"></span><span class="mord mathnormal">t</span><span class="mord mathnormal">o</span><span class="mord mathnormal">p</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 0.77777em; vertical-align: -0.08333em;"></span><span class="mord mathnormal">b</span><span class="mord mathnormal">o</span><span class="mord mathnormal">tt</span><span class="mord mathnormal">o</span><span class="mord mathnormal">m</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 0.88888em; vertical-align: -0.19444em;"></span><span class="mord mathnormal">h</span><span class="mord mathnormal">e</span><span class="mord mathnormal">i</span><span style="margin-right: 0.03588em;" class="mord mathnormal">g</span><span class="mord mathnormal">h</span><span class="mord mathnormal">t</span></span></span></span></span></li>
</ul>
</li>
</ul>
</li>
</ul>
<h2 id="propiedades-de-inline-elements">Propiedades de inline elements</h2>
<h3 id="line-height">Line-height</h3>
<p>Line Height es el alto calculado de cada <strong>line box</strong> en un <strong>IFC</strong>.<br>
La propiedad line-height indica <strong>el alto minimo del line box</strong></p>
<p>El line height se basa en uno de los siguientes segun corresponda</p>
<ul>
<li><strong>inline</strong> Contenido / La fuente / tamaño intrinseco</li>
<li><strong>inline-block</strong> Height property</li>
</ul>
<p><img src="https://lh3.googleusercontent.com/MrF_yNXGS5d398e0WZ6Iv5R7BbqcdwHQapAMB4yT15Ru88vTC9hRzyC4zEQ_ERGzGV_M0Y9LsNf3" alt="enter image description here"></p>
<blockquote>
<p><em>Value:</em>   | auto | inherit<br>
<em>Initial:</em> normal<br>
<em>Applies to:</em> Todo salvo  non-replaced inline elements, table columns, and column groups<br>
<em>Inherited:</em> no<br>
<em>Percentages:</em> porcentaje del font size<br>
<em>Media:</em> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a><br>
<em>Computed value:</em> absolute length o <em>normal</em></p>
</blockquote>
<h3 id="vertical-align---wip">Vertical-align - WIP</h3>
<h2 id="visual-efects">Visual efects</h2>
<h3 id="overflowing">Overflowing</h3>
<p><strong>Overflowing:</strong> es cuando el contenido queda fuera su container box</p>
<blockquote>
<p><em>Value:</em> visible | hidden | scroll | auto | inherit<br>
<em>Initial:</em> Visible<br>
<em>Applies to:</em> block containers<br>
<em>Inherited:</em> no<br>
<em>Percentages:</em> N/A<br>
<em>Media:</em> <a href="https://www.w3.org/TR/CSS2/media.html#visual-media-group">visual</a><br>
<em>Computed value:</em>   Lo indicado en value</p>
</blockquote>
<ul>
<li><strong>visible:</strong> EL contenido overflowea<br>
<strong>hidden:</strong> No se overflowea<br>
<strong>scroll:</strong> Muestra un scrollbar, no se overfowea<br>
<strong>auto:</strong> depende del user agent, debe mostrar un scroll mechanism si hay overflow.</li>
</ul>
<blockquote>
<p>El tamaño del scrollbar se usa de el <strong>width/height del elemento</strong> y el scrollbar <strong>se coloca entre el border y el padding</strong>.</p>
</blockquote>
<p>The behavior of the ‘auto’ value is user agent-dependent, but should cause a scrolling mechanism to be provided for overflowing boxes.</p>
<h3 id="visibility">Visibility</h3>
<p>Te permite ocultar un elemento, pero mantiene el espacio reservado para el</p>
<h2 id="generated-content">Generated content</h2>
<p>El <strong>Generated content</strong> es el contenido que es generado por CSS y no viene del source document. por ejemplo los bullets de una lista</p>
<h3 id="content-y-before----after">Content y :before  - :After</h3>
<p>Podes incertar contenido arbitrario a un elemento usando la propiedad <strong>content</strong> en conjunto con los pseudoelementos <strong>:before</strong> y <strong>:after</strong> que crean un elemento <strong>justo antes o despues del contenido del elemento en cuestion</strong></p>
<ul>
<li><strong>:Before y :After</strong> son pseudoelementos incertados antes o despues del contenido de un elemento y tendran el contenido que fue colocado en <strong>content</strong></li>
<li><strong>Content:</strong> Un contenido arbitrario colocado en el pseudoelemento :Before o :After</li>
</ul>
<blockquote>
<p>El contenido dinamico se inserta <strong>DENTRO</strong> del elemento en cuestion pero <strong>ANTES O DESPUES</strong> de su <strong>contenido</strong></p>
</blockquote>
<pre class=" language-css"><code class="prism  language-css"><span class="token selector">p<span class="token class">.note</span><span class="token pseudo-element">:before</span> </span><span class="token punctuation">{</span> <span class="token property">content</span><span class="token punctuation">:</span> <span class="token string">"Nota: "</span> <span class="token punctuation">}</span>
</code></pre>
<h3 id="counters---wip">Counters - WIP</h3>
<h2 id="rules">Rules</h2>
<h2 id="rules-1">@ Rules</h2>

