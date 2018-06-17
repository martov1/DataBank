---


---

<h1 id="contenido">Contenido</h1>
<h1 id="tests">Tests</h1>
<h2 id="variables-globales-y-de-environment">Variables globales y de environment</h2>
<p>Cuando son guardadas hay que guardarlas con <strong>JSON.stringify()</strong> y extraerlas con <strong>JSON.parse()</strong></p>
<h3 id="environment">Environment</h3>
<p>Es una serie de key-value pairs, te permiten <strong>customizar los requests usando variables que pueden ser cambiadas facilmente</strong></p>
<pre class=" language-js"><code class="prism  language-js">	<span class="token comment">//guardar variables</span>
	pm<span class="token punctuation">.</span>environment<span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"variable_key"</span><span class="token punctuation">,</span> <span class="token string">"variable_value"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token comment">//recuperar variable</span>
	pm<span class="token punctuation">.</span>environment<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">"variable_key"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	
	<span class="token comment">//guardar arrays o objetos</span>
	<span class="token keyword">var</span> array <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
	pm<span class="token punctuation">.</span>environment<span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"array"</span><span class="token punctuation">,</span> JSON<span class="token punctuation">.</span><span class="token function">stringify</span><span class="token punctuation">(</span>array<span class="token punctuation">,</span> <span class="token keyword">null</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token comment">//recuperar array o objeto</span>
	<span class="token keyword">var</span> array <span class="token operator">=</span> JSON<span class="token punctuation">.</span><span class="token function">parse</span><span class="token punctuation">(</span>pm<span class="token punctuation">.</span>environment<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">"array"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token comment">//borrar variable</span>
	pm<span class="token punctuation">.</span>environment<span class="token punctuation">.</span><span class="token function">unset</span><span class="token punctuation">(</span><span class="token string">"variable_key"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="globals">Globals</h3>
<p>Las globals son variables que estan accesibles en todos los scopes.</p>
<pre class=" language-js"><code class="prism  language-js">	<span class="token comment">//colocar global variable</span>
	pm<span class="token punctuation">.</span>globals<span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"variable_key"</span><span class="token punctuation">,</span> <span class="token string">"variable_value"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token comment">//sacar variable </span>
	pm<span class="token punctuation">.</span>globals<span class="token punctuation">.</span><span class="token function">unset</span><span class="token punctuation">(</span><span class="token string">"variable_key"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="otras-variables">Otras variables</h3>
<ul>
<li><strong>pm</strong> - Variable PostMan, permite acceder a todo lo relacionado con postman
<ul>
<li><strong>pm.response</strong> - Contiene la respuesta del request
<ul>
<li><strong>.to.have.status(200)</strong></li>
</ul>
</li>
<li><strong>pm.environment.get(‘nombre del environment’)</strong> - obtiene una variable de environment</li>
<li><strong>pm.expect(valor).to.equal(valor)</strong></li>
</ul>
</li>
</ul>
<p>Tests</p>
<pre class=" language-js"><code class="prism  language-js">	pm<span class="token punctuation">.</span>response<span class="token punctuation">.</span>to<span class="token punctuation">.</span>not<span class="token punctuation">.</span>be<span class="token punctuation">.</span>error<span class="token punctuation">;</span> 
	pm<span class="token punctuation">.</span>response<span class="token punctuation">.</span>to<span class="token punctuation">.</span>have<span class="token punctuation">.</span><span class="token function">jsonBody</span><span class="token punctuation">(</span><span class="token string">""</span><span class="token punctuation">)</span><span class="token punctuation">;</span> 
	pm<span class="token punctuation">.</span>response<span class="token punctuation">.</span>to<span class="token punctuation">.</span>not<span class="token punctuation">.</span>have<span class="token punctuation">.</span><span class="token function">jsonBody</span><span class="token punctuation">(</span><span class="token string">"error"</span><span class="token punctuation">)</span><span class="token punctuation">;</span> 
	
pm<span class="token punctuation">.</span><span class="token function">test</span><span class="token punctuation">(</span><span class="token string">"response must be valid and have a body"</span><span class="token punctuation">,</span> <span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
     <span class="token comment">// assert that the status code is 200</span>
     pm<span class="token punctuation">.</span>response<span class="token punctuation">.</span>to<span class="token punctuation">.</span>be<span class="token punctuation">.</span>ok<span class="token punctuation">;</span> <span class="token comment">// info, success, redirection, clientError,  serverError, are other variants</span>
     <span class="token comment">// assert that the response has a valid JSON body</span>
     pm<span class="token punctuation">.</span>response<span class="token punctuation">.</span>to<span class="token punctuation">.</span>be<span class="token punctuation">.</span>withBody<span class="token punctuation">;</span>
     pm<span class="token punctuation">.</span>response<span class="token punctuation">.</span>to<span class="token punctuation">.</span>be<span class="token punctuation">.</span>json<span class="token punctuation">;</span> <span class="token comment">// this assertion also checks if a body  exists, so the above check is not needed</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	 pm<span class="token punctuation">.</span><span class="token function">expect</span><span class="token punctuation">(</span>pm<span class="token punctuation">.</span>response<span class="token punctuation">.</span><span class="token function">text</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span>to<span class="token punctuation">.</span><span class="token function">include</span><span class="token punctuation">(</span><span class="token string">"string_you_want_to_search"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	 pm<span class="token punctuation">.</span><span class="token function">test</span><span class="token punctuation">(</span><span class="token string">"Your test name"</span><span class="token punctuation">,</span> <span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	     <span class="token keyword">var</span> jsonData <span class="token operator">=</span> pm<span class="token punctuation">.</span>response<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	     pm<span class="token punctuation">.</span><span class="token function">expect</span><span class="token punctuation">(</span>jsonData<span class="token punctuation">.</span>value<span class="token punctuation">)</span><span class="token punctuation">.</span>to<span class="token punctuation">.</span><span class="token function">eql</span><span class="token punctuation">(</span><span class="token number">100</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	 <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>

