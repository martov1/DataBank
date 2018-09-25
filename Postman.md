


# Contenido



# Tests


## Variables globales y de environment

Cuando son guardadas hay que guardarlas con **JSON.stringify()** y extraerlas con **JSON.parse()**

### Environment
Es una serie de key-value pairs, te permiten **customizar los requests usando variables que pueden ser cambiadas facilmente**
```js
	//guardar variables
	pm.environment.set("variable_key", "variable_value");
	//recuperar variable
	pm.environment.get("variable_key");
	
	//guardar arrays o objetos
	var array = [1, 2, 3, 4];
	pm.environment.set("array", JSON.stringify(array, null, 2));
	//recuperar array o objeto
	var array = JSON.parse(pm.environment.get("array"));
	//borrar variable
	pm.environment.unset("variable_key");
```



### Globals

Las globals son variables que estan accesibles en todos los scopes.
```js
	//colocar global variable
	pm.globals.set("variable_key", "variable_value");
	//sacar variable 
	pm.globals.unset("variable_key");
```


### Otras variables

* **pm** - Variable PostMan, permite acceder a todo lo relacionado con postman
	* **pm.response** - Contiene la respuesta del request
		*  **.to.have.status(200)**
	* **pm.environment.get('nombre del environment')** - obtiene una variable de environment 
	* **pm.expect(valor).to.equal(valor)**
	
Tests
```js
	pm.response.to.not.be.error; 
	pm.response.to.have.jsonBody(""); 
	pm.response.to.not.have.jsonBody("error"); 
	
pm.test("response must be valid and have a body", function () {
     // assert that the status code is 200
     pm.response.to.be.ok; // info, success, redirection, clientError,  serverError, are other variants
     // assert that the response has a valid JSON body
     pm.response.to.be.withBody;
     pm.response.to.be.json; // this assertion also checks if a body  exists, so the above check is not needed
});
	 pm.expect(pm.response.text()).to.include("string_you_want_to_search");
	 pm.test("Your test name", function () {
	     var jsonData = pm.response.json();
	     pm.expect(jsonData.value).to.eql(100);
	 });
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzcxMjE3NzIsMTI4MTcwMjA1M119
-->