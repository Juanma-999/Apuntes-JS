# JavaScript
## Comentarios
    // Esto es un comentario
    /* Esto también
    es un comentario */
## Variables
3 tipos de variables: var, let y const.
Para comprender por qué hay 3 tipos de variables debemos entender el concepto de hoisting. Normalmente el hoisting se define erróneamente como ue las declaraciones de variables y funciones son físicamente movidas al comienzo del código, pero esto no es lo que ocurre en realidad. Lo que sucede es que las declaraciones de variables y funciones son asignadas en memoria durante la fase de compilación, pero quedan exactamente en donde las has escrito en el código. Una de las ventajas en JavaScript de colocar (ponerlas en memoria) las declaraciones de funciones antes de ejecutar cualquier otro segmento de código es que permite utilizar una función antes de declararla en el código. Por ejemplo:
```javascript
function nombreDelGato(nombre) {
    console.log("El nombre de mi gato es " + nombre);
}
nombreDelGato("Maurizzio"); // EL nombre del gato es Maurizzio
```
El código escrito arriba está escrito de la manera que sería esperada para que funcione. Ahora, veamos qué sucede cuando llamamos a la función antes de escribirla:
```javascript
nombreDelGato("Dumas"); // El nombre del gato es Dumas
function nombreDelGato(nombre) {
    console.log("El nombre de mi gato es " + nombre);
}
```
Como se puede observar, aunque primero llamamos a la función en el código, antes de que sea escrita, el código aún funciona. Esto sucede por la manera en la que el contexto de ejecución trabaja en JavaScript. El hoisting también ocurre con otros tipos de datos y variables. Observemos el siguiente ejemplo:
```javascript
var x = 5;
(function () {
    console.log("x:", x); // no obtenemos '5' sino 'undefined'
    var x = 10;
    console.log("x:", x); // 10
})();
```
Como la declaración de variables se procesa antes de ejecutar el código, declarar una variable en cualquier parte del código es igual a declararla al inicio del mismo.Lo que ocurre aquí es que la variable se eleva y pasa a declararse al comienzo de su contexto, en este caso la función que la contiene. El ejemplo anterior se entiende implícitamente como:
```javascript
var x = 5;
(function () {
    var x; // Se elevó la declaración
    console.log("x:", x); // undefined
    x = 10;
    console.log("x:", x); // 10
})();
```
***JavaScript sólo utiliza el hoisting en declaraciones, no inicializaciones.*** Si está utilizando una variable que es declarada e inicializada después (está después en el código) de usarla, el valor será undefined. El siguiente ejemplo demuestra ese comportamiento:
```javascript
var x = 1; // Inicializa x
console.log(x + " " + y); // '1 undefined'
var y = 2; // Inicializa y
```
Como se puede apreciar la elevación afecta la declaración de variables, pero no su inicialización. El valor será asignado exactamente cuando la sentencia de asignación sea alcanzada. El ejemplo anterior se entiende implícitamente como:
```javascript
var x = 1; // Inicializa x
var y; // Se elevo la declaración
console.log(x + " " + y); // '1 undefined'
y = 2; // Inicializa y
```
### Variables var
Su ámbito es global o de función, dependiendo de dónde se defina. Puede ser redeclarada. Si se usa la variable antes de su definición se inicializa con valor indefinido.

### Variables let
Su ámbito es de bloque. No puede ser redeclarada pero puede actualizarse. Se pueden declarar variables let con el mismo nombre si están en distintos bloques. Si se usa la variable antes de su definición ocurre un error.

### Variables const
Su ámbito es de bloque. Debe ser inicializada cuando se declara y no puede ser redeclarada.

***¡NO USAR VAR, SOLO USAR LET Y CONST!***

## Tipos de datos
Javascript es un lenguaje de programación con tipado dinámico, lo cual quiere decir que existen tipos de datos pero las variables no están ligadas a ninguno de ellos. Tipos de datos: undefined, null, boolean, string, symbol, bigint, number y object.

### Number
Abarca tanto números enteros como decimales. Además existen valores numéricos especiales como Infinity o NaN. Infinity es un número mayor que cualquier otro número, se obtiene dividiendo entre 0 o referenciándolo directamente. NaN quiere decir Not a Number, cualquier operación matemática que involucre NaN tiene como resultado NaN.
```javascript
alert( 1 / 0 ); // Infinity
alert( Infinity ); // Infinity
alert( NaN + 1 ); // NaN
alert( "not a number" / 2 - 1 ); // NaN
```
### BigInt
Number no permite representar de manera precisa números mayores que 2^53-1 (9007199254740991), o menores que -2^53-1.
```javascript
console.log(9007199254740991 + 1); // 9007199254740992
console.log(9007199254740991 + 2); // 9007199254740992
const bigInt = 1234567890123456789012345678901234567890n; // La "n" al final significa que es BigInt
```
### String
Deben estar entre comillas.
```javascript
let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed another ${str}`;
```
Las comillas inversas permiten ña introducción de variables y expresiones mediante el uso de ${...}.
```javascript
let name = "John";
alert(`Hello, ${name}!`); // Hello, John!
alert(`the result is ${1 + 2}`); // the result is 3
```
Algunos de los métodos más usados para manipular strings:
- length: devuelve el número de caracteres de un string.
```javascript
let length = text.length; // 26
```
- at: devuelve el caracter situado en la posición especificada.
```javascript
let text = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
let capitalA = text.at(0); // "A"
```
- slice: devuelve una parte de un string especificada entre una posición inicial y una final. Se puede omitir un parámetro y se cortará el resto del string. Si se utiliza un índice negativo la posición se cuenta desde el final del string.
```javascript
let text = "Apple, Banana, Kiwi";
let part = text.slice(7, 13); // "Banana"
let part = text.slice(7); // "Banana, Kiwi"
let part = text.slice(-12); // "Banana, Kiwi"
```
- toUpperCase: convierte en mayúsculas.
- toLowerCase: convierte en minúsculas.
- concat: une dos o más strings. hace lo mismo que el operador +.
```javascript
let text1 = "Hello";
let text2 = "World";
let text3 = text1.concat(" ", text2); // "Hello World"
text = "Hello" + " " + "World!";
text = "Hello".concat(" ", "World!"); // "Hello World"
```
- trim: elimina los espacios en blanco.
```javascript
let text1 = "      Hello World!      ";
let text2 = text1.trim(); // "Hello World"
```
- replace: reempalza un valor por otro.
```javascript
let text = "Please visit Microsoft!";
let newText = text.replace("Microsoft", "W3Schools"); // "please visit W3Schools"
```
- split: convierte el string en un array. Si el separador es "" se devuelve un array de caracteres.
```javascript
text.split(",")    // Divide por comas
text.split(" ")    // Divide por espacios
text.split("|")    // Divide por barras
```
### Boolean
Posee dos valores: true o false.
```javascript
let nameFieldChecked = true;
let ageFieldChecked = false;
let isGreater = 4 > 1;
alert( isGreater );
```
### Null
Es un tipo especial que solo contiene un valor, null, y que representa la nada, la ausencia o un valor desconocido. No representa una referencia a un objeto inexistente como en otros lenguajes.

### Undefined
Representa que no se ha asignado un valor. Si se declara una variable pero no se le asigna un valor, su valor pasa a ser undefined.
```javascript
let age;
alert(age); // undefined
```
### Operador typeof
Devuelve el tipo del operando.
```javascript
typeof undefined // "undefined"
typeof 0 // "number"
typeof 10n // "bigint"
typeof true // "boolean"
typeof "foo" // "string"
```
## Condicionales
Son iguales que en Java.

## Funciones
Las funciones son bloques de código reutilizables. Los métodos son funciones que forman parte de un objeto. Funcionan de la misma manera que en Java, solo que no hay que especificar el tipo del parámetro en la definición de la función. La sintaxis de las funciones es como sigue:
```javascript
function myFunction() { // definición de la función
    console.log("hello");
}
myFunction(); // llamada a la función
function favoriteAnimal(animal) {
    return animal + " is my favorite animal!"
}
console.log(favoriteAnimal('Goat'))
```
### Parámetros opcionales
Si estamos definiendo una función y queremos que los parámetros que si se introduce un parámetro en la función ésta se compirte de una manera, pero que si no se introduce se comporte de otra, usaremos la siguiente sintaxis:
```javascript
function hello(name = "Chris") {
    console.log(`Hello ${name}!`);
}
hello("Ari"); // Hello Ari!
hello(); // Hello Chris!
```
### Funciones anónimas y funciones flecha
Las funciones anónimas se utilizan cuando una función espera que se le pase otra función como parámetro. Esa función que se pasa como parámetro es una función anónima y se llama así porque no tienen nombre. Pongamos que queremos que cada que el usuario pulse una tecla en una caja de texto se imprima qué tecla ha pulsado. Para hacer eso añadiremos un event listener a la caja de texto mediante el método addEventListener, que toma dos parámetros. El primero de ellos es el nombre del evento que se quiere escuchar y el segundo es la función que ejecutará lo que queremos que pase cuando se pulse una tecla. En lugar de escribir lo siguiente:
```javascript
function logKey(event) {
    console.log(`You pressed "${event.key}".`);
}
textBox.addEventListener("keydown", logKey);
```
Podemos hacer esto:
```javascript
textBox.addEventListener("keydown", function (event) {
    console.log(`You pressed "${event.key}".`);
});
```
Hay una sintaxis alternativa para pasar una función anónima como parámetro que se denomina 'función flecha'.
```javascript
textBox.addEventListener("keydown", (event) => {
    console.log(`You pressed "${event.key}".`);
});
```
Si la función flecha toma un solo parámetro se pueden omitir los paréntesis a su alrededor.
```javascript
textBox.addEventListener("keydown", event => {
    console.log(`You pressed "${event.key}".`);
});
```
Por último, si la función solo contiene una setnecia return, se pueden omitir tanto los parémtesis como la palabra clave return. En el siguiente ejemplo se usa el método map, que  aplica una función sobre el contenido de un array.
```javascript
const originals = [1, 2, 3];
const doubled = originals.map(item => item * 2);
console.log(doubled); // [2, 4, 6]
```
Su equivalente sería:
```javascript
function doubleItem(item) {
    return item * 2;
}
```
### Ámbito de una función y pila de llamadas
La pila de llamadas (call stack) es la manera que tiene JavaScript de realizar un seguimiento de por dónde se está ejecutando un código que hace llamadas a múltiples funciones. También usa una pila de llamadas para administrar el contexto de ejecución.
Se trata de una pila LIFO (last-in-first-out). Cuando se ejecuta un script el motor de JavaScript crea un contexto de ejecución global y lo coloca en la parte superior de la pila de llamadas.
Cada vez que se llama a una función, el motor de JavaScript crea un contexto de ejecución de función para la función, lo coloca en la parte superior de la pila de llamadas y comienza a ejecutar la función.
Si una función llama a otra función, el motor de JavaScript crea un nuevo contexto de ejecución de función para la función que se está llamando y lo coloca en la parte superior de la pila de llamadas.
Cuando la función actual se completa, el motor de JavaScript la elimina de la pila de llamadas y reanuda la ejecución donde se quedó.
El script se detendrá cuando la pila de llamadas esté vacía.
Ejemplo:
```javascript
function add(a, b) {
    return a + b;
}
function average(a, b) {
    return add(a, b) / 2;
}
let x = average(10, 20);
```
Cuando el motor de JavaScript ejecuta este script, coloca el contexto de ejecución global (indicado por la función main() o global()) en la pila de llamadas.
El contexto de ejecución global entra en la fase de creación y pasa a la fase de ejecución.
El motor de JavaScript ejecuta la llamada a la función average(10, 20) y crea un contexto de ejecución de función para la función average(), colocándolo en la parte superior de la pila de llamadas.
El motor de JavaScript comienza a ejecutar average(), ya que la función average() está en la parte superior de la pila de llamadas.
La función average() llama a la función add(). En este punto, el motor de JavaScript crea otro contexto de ejecución de función para la función add() y lo coloca en la parte superior de la pila de llamadas.
El motor de JavaScript ejecuta la función add() y la elimina de la pila de llamadas.
En este momento, la función average() está en la parte superior de la pila de llamadas. El motor de JavaScript la ejecuta y la elimina de la pila de llamadas.
Ahora, la pila de llamadas está vacía, por lo que el script deja de ejecutarse.

## Errores

## Arrays
Un array es una colección de elementos. Normalmente se declaran mediante 'const'. Si se utilizan índices nombrados (const otherPerson = {firstName:"Juanma", lastName:"Villaverde"}) JavaScript redefine el array a un objeto. La diferencia entre los objetos y los arrays en JavaScript es que los arrays utilizan índices numerados y los objetos índices nombrados. Para saber si una variable es un array se usa el método Array.isArray() al que se le introduce la variable que queremos comprobar como argumento.
```javascript
const cars = ["Saab", "Volvo", "BMW"];
const moreCars = [];
cars[0]= "Seat";
cars[1]= "Mitsubishi";
cars[2]= "Volkswagen";
console.log(cars[0]); // Saab
console.log(cars[-1]); // BMW
cars.push("Tesla");
console.log(cars[-1]); // Tesla
console.log(moreCars.toString()); // Seat,Mitsubishi,Volkswagen

const person = ["John", "Doe", 46];
console.log(person.length); // 3
const otherPerson = {firstName:"María", lastName:"Pérez", age:32};
const anotherPerson = [];
person["firstName"] = "Fulanito";
person["lastName"] = "Gómez";
person["age"] = 46;
person.length; // 0
person[0]; // undefined
Array.isArray(person); // true
Array.isArray(otherPerson); // false
```

## Bucles
Son iguales que en Java.

## Manipulación del DOM
El DOM (o Modelo de Objetos del Documento) es una representación en forma de árbol del contenido de una página web, es decir, un árbol de "nodos" con diferentes relaciones según cómo estén dispuestos en el documento HTML.
```html
<div id="container">
    <div class="display"></div>
    <div class="controls"></div>
</div>
```
En el ejemplo anterior, el div display es un hijo del div container y un hermano del div controls. El DOM es como un árbol genealógico, donde el div container es un padre, con sus hijos en el siguiente nivel.
Para apuntar a nodos se utilizan selectores. Si quisiésemos seleccionar algún nodo del ejemplo anterior podríamos hacer lo siguiente:
```javascript
const container = document.querySelector('#container'); // selects the #container div (don't worry about the syntax, we'll get there)
console.dir(container.firstElementChild); // selects the first child of #container => .display
const controls = document.querySelector('.controls'); // selects the .controls div
console.dir(controls.previousElementSibling); // selects the prior sibling => .display
```

### Métodos del DOM
El código HTML se convierte en el DOM cuando es analizado por un navegador. Una de las principales diferencias entre los elementos HTML y los nodos es que éstos últimos son objetos que tienen propiedades y métodos asociados a ellos. Estas propiedades y métodos son las herramientas principales que vamos a utilizar para manipular nuestra página web con JavaScript. Comenzaremos con los selectores de consulta, aquellos que te ayudan a apuntar a los nodos.

#### Selectores de consulta
- `element.querySelector(selector)` - devuelve una referencia al primer elemento coincidente con el selector.
- `element.querySelectorAll(selectors)` - devuelve un nodelist que contiene referencias a todos los elementos coincidentes con los selectores.
Existen varios otros queries más específicos que ofrecen posibles beneficios de rendimiento marginales, pero no los revisaremos en este momento. Es importante señalar que al usar querySelectorAll, el valor de retorno no es un array. Parece un array y se comporta de alguna manera como un array, pero en realidad es un nodelist. La gran diferencia es que varios métodos de array están ausentes en los nodelists. Una solución, si surgen problemas, es convertir el nodelist en un array. Puedes hacer esto con Array.from().

#### Creación de elementos
`document.createElement(tagName, [options])` - crea un nuevo elemento del tipo de etiqueta `tagName`. [options] en este caso significa que puedes agregar algunos parámetros opcionales a la función. No te preocupes por ellos en este momento.
```javascript
const div = document.createElement('div');
```
Esta función NO coloca tu nuevo elemento en el DOM; lo crea en la memoria. Esto te permite manipular el elemento (agregar estilos, clases, ids, texto, etc.) antes de colocarlo en la página. Puedes colocar el elemento en el DOM con uno de los siguientes métodos.

#### Agregar elementos
- `parentNode.appendChild(childNode)` - añade `childNode` como el último hijo de `parentNode`.
- `parentNode.insertBefore(newNode, referenceNode)` - inserta `newNode` en `parentNode` antes de `referenceNode`.

#### Eliminar elementos
- `parentNode.removeChild(child)` - elimina `child` de `parentNode` en el DOM y devuelve una referencia a `child`.

#### Modificación de elementos
Cuando tienes una referencia a un elemento, puedes usar esa referencia para modificar las propiedades propias del elemento. Esto te permite realizar muchas alteraciones útiles, como agregar/eliminar y modificar atributos, cambiar clases, agregar información de estilo en línea y más.

```javascript
const div = document.createElement('div'); // crea un nuevo div referenciado en la variable 'div'
```

#### Añadir estilo en línea
```javascript
div.style.color = 'blue'; // agrega la regla de estilo indicada
div.style.cssText = 'color: blue; background: white;'; // agrega varias reglas de estilo
div.setAttribute('style', 'color: blue; background: white;'); // agrega varias reglas de estilo
```
Ten en cuenta que si estás accediendo a una regla CSS con guiones en JavaScript, deberás usar camelCase o usar notación de corchetes en lugar de notación de guiones.
```javascript
div.style.background-color // no funciona - intenta acceder al color de div.style.background
div.style.backgroundColor // accede al estilo background-color del div
div.style['background-color'] // también funciona
div.style.cssText = "background-color: white;" // establece el fondo del div
```

#### Editar atributos
```javascript
div.setAttribute('id', 'theDiv'); // if id exists, update it to 'theDiv', else create an id with value "theDiv"
div.getAttribute('id'); // returns value of specified attribute, in this case "theDiv"
div.removeAttribute('id'); // removes specified attribute
```

#### Uso de clases
Es una buena práctica editar clases CSS en lugar de añadir o eliminar estilos en línea.
```javascript
div.classList.add('new');// adds class "new" to your new div
div.classList.remove('new');// removes "new" class from div
div.classList.toggle('active');// if div doesn't have class "active" then add it, or if it does, then remove it
```

#### Añadir texto y elementos HTML
Es preferible usar textContent a innerHTML ya que este último puede causar problemas de seguridad.
```javascript
div.textContent = 'Hello World!' // creates a text node containing "Hello World!" and inserts it in div
div.innerHTML = '<span>Hello World!</span>'; // renders the HTML inside div
```
Ejemplo:
```html
<!-- your HTML file: -->
<body>
    <h1>
        THE TITLE OF YOUR WEBPAGE
    </h1>
    <div id="container"></div>
</body>
```
```javascript
// your JavaScript file
const container = document.querySelector('#container');

const content = document.createElement('div');
content.classList.add('content');
content.textContent = 'This is the glorious text-content!';

container.appendChild(content);
```
```html
<!-- The DOM -->
<body>
    <h1>
        THE TITLE OF YOUR WEBPAGE
    </h1>
    <div id="container">
        <div class="content">
            This is the glorious text-content!
        </div>
    </div>
</body>
```

## Eventos
Los eventos permiten manipular el DOM de manera dinámica. Existen tres tipos de eventos:
1. Se pueden añadir atributos función a elementos HTML. Esta manera no es idónea porque solo puede añadirse una propiedad onclick por cada elemento.
```javascript
<button onclick="alert('Hello World')">Click Me</button>
```
2. Se pueden añadir propiedades tipo on[eventType] (onclick, onmousedown, etc.) en los nodos del DOM desde el archivo JavaScript. Tiene el mismo problema que el anterior método, solo se puede añadir una propiedad on click por cada elemento.
```html
<!-- the HTML file -->
<button id="btn">Click Me</button>
```
```javascript
// the JavaScript file
const btn = document.querySelector('#btn');
btn.onclick = () => alert("Hello World");
```
3. Se pueden agregar event listeners a los nodos del DOM desde el archivo JavaScript. Esta es la forma correcta de añadir eventos.
```html
<!-- the HTML file -->
<button id="btn">Click Me Too</button>
```
```javascript
// the JavaScript file
const btn = document.querySelector('#btn');
btn.addEventListener('click', () => {
    alert("Hello World");
});
```

## Objetos
Los objetos permiten guardar colecciones de varios tipos de datos con índices nombrados y entidades más complejas. Se crean usando corchetes y opcionalmente unalista de propiedades. Las propiedades son pares clave : valor donde la clave es un string y el valor puede ser cualquier cosa.
```javascript
let user = {};
let otherUser = {   // an object
    name: "John",   // by key "name" store value "John"
    age: 30,    // by key "age" store value 30
    isAdmin = true,
};
console.log(otherUser.name); // John
delete otherUser.isAdmin;

function makeUser(name, age) {
  return {
    name,// same as name: name
    age,  // same as age: age
    // ...other properties
  };
}

let anotherUser = makeUser("María", 26);
alert(anotherUser.name); // María
```
Una de las peculiaridades de JavaScript en comparación con otros lenguajes es que se puede acceder a propiedades no existentes de objetos, lo cual devuelve undefined. Podemos saber si una propiedad existe mediante el operador 'in'. Ha de tenerse en cuenta que 'in' solo comprueba si la propiedad existe pero no su valor, es decir, que si la propiedad existe pero su valor es indefined devolverá true.
```javascript
let user = { name: "John", age: 30 };

alert("age" in user); // true, user.age exists
alert("blabla" in user); // false, user.blabla doesn't exist
```
Para iterar los contenidos de un objeto se utiliza un bucle for con una sintaxis ligeramente distinta. Cuando se itera un objeto si las claves son números se ordenan automáticamente de manera ascendente, mientas que si las claves no son números el orden que siguen es el de creación.
```javascript
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  alert( key );  // name, age, isAdmin
  alert( user[key] ); // John, 30, true
}
```
### Constructores
```javascript
function Player(name, marker) {
  this.name = name;
  this.marker = marker;
  this.sayName = function() {
    console.log(this.name)
  };
}

const player = new Player('steve', 'X');
console.log(player.name); // steve
steve.sayName(); // steve
```
### Herencia con prototipos
Todos los objetos poseen un prototipo del que heredan. Podemos definir funciones o atributos en el prototipo de un objeto para que todas las instancias de dicho objeto posean esos atributos y funciones. La herencia prototípica es util si queremos un comportamiento similar a la herencia múltiple.
```javascript
Player.prototype.sayHello = function() {
   console.log("Hello, I'm a player!");
};

player1.sayHello(); // logs "Hello, I'm a player!"
player2.sayHello(); // logs "Hello, I'm a player!"
```
### Por qué usar fábricas en lugar de constructores
Las fábricas son funciones que devuelven un nuevo objeto cuando se las llama. Cuando usas funciones fábrica no es necesario utilizar el operador new para crear instancias de objetos. Olvidar el new al usar un constructor puede llevar a errores difíciles de depurar. En funciones fábrica no hay que preocuparse por el cambio del contexto this, ya que simplemente devuelven un nuevo objeto. En los constructores el uso de this puede causar confusiones.
```javascript
const User = function (name) {
    this.name = name;
    this.discordName = "@" + name;
}

function createUser (name) {
    const discordName = "@" + name;
    return { name, discordName };
}
```
El uso de funciones fábrica también permite el uso de variables privadas.
```javascript
function createUser (name) {
  const discordName = "@" + name;

  let reputation = 0;
  const getReputation = () => reputation;
  const giveReputation = () => reputation++;

  return { name, discordName, getReputation, giveReputation };
}

const josh = createUser("josh");
josh.giveReputation();
josh.giveReputation();

console.log({
  discordName: josh.discordName,
  reputation: josh.getReputation()
}); // logs { discordName: "@josh", reputation: 2 }
```

### Herencia con funciones fábrica
```javascript
function createPerson(name, age) {
    let privateName = name;
    let privateAge = age;

    return {
        getName: function() {
            return privateName;
        },
        getAge: function() {
            return privateAge;
        },
        celebrateBirthday: function() {
            privateAge++;
        }
    };
}

const person = createPerson('John', 30);
console.log(person.getName());  // Output: John
console.log(person.getAge());   // Output: 30
person.celebrateBirthday();
console.log(person.getAge());   // Output: 31

function createEmployee(name, age, position) {
    // Crear un objeto Person utilizando la función fábrica de Person
    const person = createPerson(name, age);

    // Agregar propiedades específicas para Employee
    person.position = position;

    // Métodos adicionales específicos para Employee
    person.getPosition = function() {
        return this.position;
    };

    return person;
}

const employee = createEmployee('Jane', 25, 'Developer');
console.log(employee.getName());         // Output: Jane
console.log(employee.getAge());          // Output: 25
console.log(employee.getPosition());     // Output: Developer
employee.celebrateBirthday();
console.log(employee.getAge());          // Output: 26
```

### Patrón módulo
Muchas veces no se necesita una función fábrica para producir múltiples objetos sino que se utilizando para envolver secciones de código, ocultando las variables y funciones que no necesitas en otros lugares. Esto se logra envolviendo la función fábrica entre paréntesis y llamándola inmediatamente. Esta llamada inmediata de función se conoce comúnmente como una Expresión de Función Inmediatamente Invocada (IIFE, por sus siglas en inglés) Este patrón se se denomina patrón módulo. Al encapsular el código en módulos evitamos exponer ese fragmento de código al cuerpo principal del programa, lo cual se denomina "namespacing". Se trata de una técnica que ayuda a evitar coincidencias de nombres.
```javascript
const calculator = (function () {
  const add = (a, b) => a + b;
  const sub = (a, b) => a - b;
  const mul = (a, b) => a * b;
  const div = (a, b) => a / b;
  return { add, sub, mul, div };
})();

calculator.add(3,5); // 8
calculator.sub(6,2); // 4
calculator.mul(14,5534); // 77476
```

### Clases
JavaScript no tiene clases en el mismo sentido que otros lenguajes de programación orientados a objetos como Java, sin embargo, recientemente se ha introducido sintaxis para la creación de objetos que usa la palabra clave 'class'. Lo cierto es que funciona de la misma manera que los constructores aunque posee algunas ventajas sobre estos. Algunas de ellas son que la sintaxis es más moderna y parecida a la de otros lenguajes, dan mejor soporte a los métodos estáticos, permiten el encapsulamiento y permiten el uso de las palabras clave 'extends' y 'super'.
```javascript
class MyClass {
  // class methods
  constructor() { ... }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}

class User {

  constructor(name) {
    this.name = name;
  }

  sayHi() {
    alert(this.name);
  }

}

let user = new User("John");
user.sayHi();

class User {
  constructor(name) { this.name = name; }
  sayHi() { alert(this.name); }
}

// class is a function
alert(typeof User); // function

// ...or, more precisely, the constructor method
alert(User === User.prototype.constructor); // true

// The methods are in User.prototype, e.g:
alert(User.prototype.sayHi); // the code of the sayHi method

// there are exactly two methods in the prototype
alert(Object.getOwnPropertyNames(User.prototype)); // constructor, sayHi
```
Ejemplo de herencia con clases:
```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }

    speak() {
        console.log(`${this.name} makes a sound`);
    }
}

class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks`);
    }
}

const dog = new Dog('Buddy');
dog.speak(); // Output: Buddy barks
```
Ejemplo de método estático:
```javascript
class MathUtils {
    static square(x) {
        return x * x;
    }
}

const result = MathUtils.square(5);
```

## Package managers (npm), module bundlers (node.js) y ES6 modules
Los package managers son herramientas que facilitan el proceso de descargar y actualizar librerías. npm es un package manager creado para node.js, un runtime de JavaScriptn diseñado para ejecutarse del lado del servidor en lugare de del lado del cliente, lo cual lo convierte en una elección un tanto extraña para un package manager para librerías que deben ejecutarse en el navegador.