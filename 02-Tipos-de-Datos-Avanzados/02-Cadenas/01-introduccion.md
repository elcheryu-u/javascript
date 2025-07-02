# Cadenas (Strings) en JavaScript

Las cadenas de texto (Strings) son uno de los tipos de datos primitivos más fundamentales en JavaScript. Se utilizan para representar y manipular secuencias de caracteres, como palabras, frases o cualquier texto.

## Características Clave de las Cadenas

* **Inmutables:** Una vez que se crea una cadena, no se puede modificar directamente. Cualquier operación que parezca modificar una cadena (como añadir o eliminar caracteres) en realidad crea y devuelve una **nueva** cadena.
* **Secuencias de Caracteres:** Internamente, una cadena es una secuencia ordenada de caracteres.
* **Primitivas:** Son un tipo de dato primitivo, a diferencia de los objetos, aunque pueden comportarse como objetos gracias al concepto de "object wrapper".

## Declaración de Cadenas

Las cadenas se pueden declarar utilizando comillas simples (`' '`), comillas dobles (`" "`), o comillas invertidas (backticks ``` `` ```) para los literales de plantilla (Template Literals).

### 1. Comillas Simples y Dobles

Son las formas tradicionales de definir cadenas. Ambas funcionan de la misma manera.

```javascript
const nombre = 'Alicia';
const mensaje = "Hola, mundo!";
const cita = 'Ella dijo: "JavaScript es genial."'; // Puedes usar comillas dobles dentro de simples
const otraCita = "Él exclamó: '¡Qué buen día!'";   // O comillas simples dentro de dobles

console.log(nombre);    // Salida: Alicia
console.log(mensaje);   // Salida: Hola, mundo!
console.log(cita);      // Salida: Ella dijo: "JavaScript es genial."
console.log(otraCita);  // Salida: Él exclamó: '¡Qué buen día!'
```

**[Ver ejemplo en vivo](https://playcode.io/2444394)**

#### Escape de Caracteres:

Si necesitas usar el mismo tipo de comilla que encierra la cadena dentro de la cadena misma, debes "escaparlas" usando una barra invertida (`/`).

```javascript
const problema = 'No se puede decir 'Esto es un 'ejemplo' directamente.'; // Error de sintaxis
const solucion1 = 'Sí se puede decir \'Esto es un \'ejemplo\' directamente.'; // Con comillas simples escapadas
const solucion2 = "Sí se puede decir \"Esto es un \"ejemplo\" directamente."; // Con comillas dobles escapadas

console.log(solucion1); // Salida: Sí se puede decir 'Esto es un 'ejemplo' directamente.
console.log(solucion2); // Salida: Sí se puede decir "Esto es un "ejemplo" directamente.
```

**[Ver ejemplo en vivo](https://playcode.io/2444403)**

### 2. Comillas invertidas (Template Literals / Literales de Plantilla)

Introducidas en ES6 (ECMAScript 2015), las comillas invertidas (`` ` ``) ofrecen una forma más flexible de trabajar con cadenas, permitiendo:

- **Multilinea:** Las cadenas pueden abarcar múltiples lineas sin necesidad de caracteres de escape especiales (ej. `\n`).
- **Interpolación de Expresiones:** Se pueden incrustar expresiones de JavaScript (variables, cáculos, llamadas a funciones) directamente dentro de la cadena usando la sintaxis `${expresion}`.

```javascript
const producto = "Laptop";
const precio = 1200;

// Cadena multilínea
const descripcion = `
Este es un
producto de alta calidad:
${producto} con un precio de $${precio}.
`;
console.log(descripcion);
/* Salida:
Este es un
producto de alta calidad:
Laptop con un precio de $1200.
*/

// Interpolación simple
const nombreCompleto = `Juan ${'Pérez'}`;
console.log(nombreCompleto); // Salida: Juan Pérez

// Expresión dentro de la plantilla
const a = 5;
const b = 10;
console.log(`La suma de ${a} y ${b} es ${a + b}.`); // Salida: La suma de 5 y 10 es 15.
```

**[Ver ejemplo en vivo](https://playcode.io/2444408)**

_**Nota:** Los literales de plantilla son un tema importante y los cubriremos con más detalle en un archivo aparte._

## Propiedad `length`

La propiedad `length` devuelve el número de caracteres en una cadena.

```javascript
const texto = "JavaScript";
console.log(texto.length); // Salida: 10

const vacio = "";
console.log(vacio.length); // Salida: 0
```

**[Ver ejemplo en vivo](https://playcode.io/2444413)**

## Acceso a Caracteres

Puedes acceder a caracteres individuales de una cadena utilizando la notación de corchetes `[]` y el índice del carácter (basado en cero).

```javascript
const palabra = "programación";
console.log(palabra[0]); // Salida: 'p'
console.log(palabra[3]); // Salida: 'g'
console.log(palabra[palabra.length - 1]); // Salida: 'n' (último carácter)

// Intentar acceder a un índice fuera de rango devuelve `undefined`
console.log(palabra[100]); // Salida: undefined
```

**Importante:** Aunque puedas acceder a caracteres individuales, recuerda que las cadenas son inmutables. Intentar modificar un carácter de esta manera no tendrá efecto.

```javascript
let miCadena = "hola";
miCadena[0] = "H"; // Esto NO cambia la cadena
console.log(miCadena); // Salida: "hola" (sigue siendo la misma)

// Para cambiar la cadena, debes crear una nueva
miCadena = "H" + miCadena.slice(1);
console.log(miCadena); // Salida: "Hola"
```

**[Ver ejemplo en vivo](https://playcode.io/2444416)**

## Concatenación de Cadenas

La concatenación es el proceso de unir dos o más cadenas para formar una nueva cadena.

### 1. Usando el operador `+`

Es el método más común y sencillo para unir cadenas.

```javascript
const saludo = "Hola";
const nombre = "Mundo";
const mensajeCompleto = saludo + " " + nombre + "!";

console.log(mensajeCompleto); // Salida: "Hola Mundo!"

const num = 10;
const textoNum = "El número es: " + num; // El número se convierte a cadena implícitamente
console.log(textoNum); // Salida: "El número es: 10"
```

**[Ver ejemplo en vivo](https://playcode.io/2444418)**


### 2. Usando el Método `concat()`

El método [`concat()`](../01-Arreglos/metodos-comunes.md#concat) también se puede usar para unir cadenas. Es menos común que el operador `+` para concatenaciones simples.

```javascript
const parte1 = "JavaScript";
const parte2 = " es";
const parte3 = " asombroso.";

const frase = parte1.concat(parte2, parte3);
console.log(frase); // Salida: "JavaScript es asombroso."
```

**[Ver ejemplo en vivo](https://playcode.io/2444422)**

### 3. Usando Literales de Plantilla (Template Literals)

Para concatenaciones más complejas o que involucran variables, los literales de pantilla ofrecen una sintaxis más limpia y legible.

```javascript
const firstName = "Jane";
const lastName = "Doe";
const edad = 30;

const userInfo = `La usuaria ${firstName} ${lastName} tiene ${edad} años.`;
console.log(userInfo); // Salida: "La usuaria Jane Doe tiene 30 años."
```

**[Ver ejemplo en vivo](https://playcode.io/2444423)**

La elección del método de concatenación dependerá de la complejidad y la legibilidad que busques en tu código. Para concatenaciones simples, el operador `+` es rápido y claro. Para cadenas más complejas que involucren múltiples variables y expresiones, los literales de plantilla son superiores.