---


---

<p><strong>Design patterns</strong><br>
<a href="https://www.youtube.com/watch?v=vNHpsC5ng_E&amp;list=PLF206E906175C7E07">https://www.youtube.com/watch?v=vNHpsC5ng_E&amp;list=PLF206E906175C7E07</a></p>
<h2 id="oop">OOP</h2>
<h3 id="criterios-generales">Criterios generales</h3>
<ul>
<li>Los objetos son instanciados desde clases y tienen constructores</li>
<li><strong>las propiedades de los objetos son privadas</strong>
<ul>
<li>No se puede cambiar las variables de los objetos sino mediante <strong>getters</strong> and <strong>setters</strong></li>
</ul>
</li>
</ul>
<h3 id="herencia">Herencia</h3>
<ul>
<li>Las clases <strong>heredan</strong> <strong>propiedades</strong> y <strong>metodos</strong> de otras clases</li>
<li>Regla <strong>“is a”</strong> sirve para determinar si una clase hereda de otra
<ul>
<li><strong>cat is an animal</strong>, cat hereda de animal</li>
</ul>
</li>
</ul>
<h3 id="polymorfismo">Polymorfismo</h3>
<p>Polimorfismo es <strong>proveer de una interfaz unica  a  objetos de diferente tipo</strong>, se da generalmente cuando una clase <strong>sobreescribe un metodo que heredó</strong></p>
<p>Esto implica tambien que <strong>perro</strong> y <strong>gato</strong> no solo son sus propias clases sino que tambien son de tipo <strong>animal</strong>, ya que heredan una interfaz aunque su implementacion sea diferente.</p>
<p><strong>Ejemplo:</strong></p>
<ul>
<li><strong>animal.moverse()</strong> puede tener una implmentacion x
<ul>
<li><strong>Perro.moverse()</strong> puede usar la misma implementacion que animal (la hereda)</li>
<li><strong>pajaro.moverse()</strong> heredara el metodo pero lo sobreescribira para poder volar en vez de caminar</li>
</ul>
</li>
</ul>
<h3 id="clases-abstractas-y-interfaces">Clases abstractas y interfaces</h3>
<p><strong>Abstract class:</strong><br>
Una clase abstracta es una clase que no puede ser instanciada por si misma, sino que esta hecha para ser un blueprint de otras clases que la extenderan.</p>
<p>Las clases abstractas pueden tener metodos , metodos estaticos y etodos abstractos (metodos sin una implementacion)</p>
<p>El compiler demandara que todos los metodos de la clase abstracta sea implementados en la clase que hereda</p>
<p><strong>Interface:</strong></p>
<ul>
<li>Es un <strong>abstract class</strong> en la que todos los metodos son <strong>abstract methods</strong></li>
<li>Una clase puede implementar infinitas interfaces.</li>
</ul>
<h2 id="strategy-pattern-ej-passport.js">Strategy pattern (ej passport.js)</h2>
<p>El strategy pattern se trata de <strong>separar una familia de  algoritmos (strategies)</strong> de <strong>la clase que los va a utilizar(client)</strong> para que el algoritmo sea <strong>intercambiable</strong> en runtime.</p>
<p>Por ejemplo en la clase <strong>Encriptador</strong>, los algoritmos (estrategias) de encriptacion tendrian cada uno una clase separada (<strong>AES</strong>, <strong>RSA</strong>, <strong>DES</strong>).</p>
<pre class=" language-c"><code class="prism # language-c"><span class="token comment">//Declaras la estrategia (RSA,AES,etc) del encriptador</span>
Encriptador<span class="token punctuation">.</span>estrategiaDeEncriptacion <span class="token operator">=</span> new <span class="token function">AES</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">//Ahora el metodo encriptar internamente usa</span>
<span class="token comment">// esa nueva estrategia</span>
Encriptador<span class="token punctuation">.</span><span class="token function">encriptar</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
<p><strong>Fijate:</strong>  podes modificar los algoritmos (denominados <strong>strategies</strong>)  sin que esto afecte a las clases que los usan (denominadas <strong>clients</strong>)</p>
<p><strong>EJEMPLO PRACTICO:</strong><br>
Passport.js usa este patron para separar los algoritmos que te loguearn a cada provider.</p>

