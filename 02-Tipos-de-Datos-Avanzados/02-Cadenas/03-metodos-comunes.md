# Métodos Comunes de Cadenas (Strings) en JavaScript

Las cadenas en JavaScript, a pesar de ser inmutables, ofrecen una rica colección de métodos para realizar operaciones como buscar, extraer, reemplazar, transformar y validar texto. Estos métodos siempre devuelven una **nueva cadena** o un valor derivado, ya que la cadena original no puede modificarse.

## 1. Obtener Subcadenas

### `substring(indiceInicio, indiceFin)`

Extrae los caracteres de una cadena entre dos índices (el `indiceFin` no está incluido). Si `indiceFin` se omite, extrae hasta el final de la cadena.

```javascript
const texto = "JavaScript es divertido";

console.log(texto.substring(0, 10)); // Salida: "JavaScript"
console.log(texto.substring(14));    // Salida: "divertido"
console.log(texto.substring(4, 1));  // Salida: "ava" (intercambia índices si el inicio es mayor que el fin)
```

**[Ver ejemplo en vivo](https://playcode.io/2445428)**

### `slice(indiceInicio, indiceFin)`

Similar a `substring`, pero puede aceptar índices negativos para contar desde el final de la cadena.

```javascript
const texto = "JavaScript es divertido";

console.log(texto.slice(0, 10));   // Salida: "JavaScript"
console.log(texto.slice(14));      // Salida: "divertido"
console.log(texto.slice(-9));      // Salida: "divertido" (los últimos 9 caracteres)
console.log(texto.slice(0, -9));   // Salida: "JavaScript es " (desde el inicio hasta los últimos 9)
```

**[Ver ejemplo en vivo](https://playcode.io/2445434)**

### `substr(indiceInicio, longitud)` (Obsoleto/Desaconsejado)

Extrae un número `longitud` de caracteres a partir de `indiceInicio`. Es importante mencionar que este método es **obsoleto** y se recomienda usar [`substring`](#substringindiceinicio-indicefin) o [`slice`](#sliceindiceinicio-indicefin) en su lugar.

```javascript
const texto = "JavaScript es divertido";
console.log(texto.substr(0, 10)); // Salida: "JavaScript"
console.log(texto.substr(14, 9)); // Salida: "divertido"
```

**[Ver ejemplo en vivo](https://playcode.io/2445638)**

## 2. Búsqueda de Cadenas

### `indexOf(subcadena, desdeIndice)`

Devuelve el índice de la primera ocurrencia de la `subcadena` especificada, o `-1` si no se encuentra. El segundo argumento es opcional y especifica desde qué índice comenzar la búsqueda.

```javascript
const frase = "Hola mundo, hola universo!";

console.log(frase.indexOf("mundo"));    // Salida: 5
console.log(frase.indexOf("hola"));     // Salida: 0
console.log(frase.indexOf("hola", 1));  // Salida: 12 (busca desde el índice 1)
console.log(frase.indexOf("JavaScript")); // Salida: -1
```

**[Ver ejemplo en vivo](https://playcode.io/2445643)**

### `lastIndexOf(subcadena, desdeIndice)`

Similar a `indexOf`, pero devuelve el índice de la última ocurrencia de la subcadena. La búsqueda se realiza hacia atrás desde `desdeIndice`.

```javascript
const frase = "Hola mundo, hola universo!";

console.log(frase.lastIndexOf("hola"));    // Salida: 12
console.log(frase.lastIndexOf("o"));       // Salida: 20
```

**[Ver ejemplo en vivo](https://playcode.io/2445646)**

### `startsWith(prefijo, posicion)`

Determina si una cadena comienza con los caracteres de una cadena especificada, devolviendo `true` o `false`.

```javascript
const url = 'https://www.ejemplo.com/';
console.log(url.startsWith('https')); // Salida: true
console.log(url.startsWith('http')); // Salida: true
console.log(url.startsWith('www', 8)); // Salida: true (comienza a buscar desde el índice 8)
```

**[Ver ejemplo en vivo](https://playcode.io/2445650)**

### `endsWith(sufijo, longitud)`

Determina si una cadena termina con los caracteres de una cadena especificada, devolviendo `true` o `false`.

```javascript
const nombreArchivo = "documento.pdf";
console.log(nombreArchivo.endsWith(".pdf"));   // Salida: true
console.log(nombreArchivo.endsWith(".txt"));   // Salida: false
```

**[Ver ejemplo en vivo](https://playcode.io/2445655)**

### `includes(subcadena, posicion)`

Determina si una cadena contiene los caracteres de una subcadena especificada, devolviendo `true` o `false`. Es sensible a mayúsculas y minúsculas.

```javascript
const frase = "JavaScript es un lenguaje";
console.log(frase.includes("script"));  // Salida: true
console.log(frase.includes("Script"));  // Salida: false (sensible a mayúsculas/minúsculas)
console.log(frase.includes("Java", 1)); // Salida: false (busca desde el índice 1)
```

**[Ver ejemplo en vivo](https://playcode.io/2445658)**

## 3. Reemplazo y División

### `replace(patron, reemplazo)`

Busca un `patron` (una cadena o una expresión regular) en una cadena y lo reemplaza con el `reemplazo` especificado. Solo reemplaza la **primera** ocurrencia si el patrón es una cadena. Para reemplazar todas las ocurrencias, se necesita una expresión regular con la bandera `g` (global).

```javascript
const texto = "El pato pato nada";

console.log(texto.replace("pato", "perro")); // Salida: "El perro pato nada" (solo la primera)

// Con expresión regular para reemplazar todas las ocurrencias
console.log(texto.replace(/pato/g, "gato")); // Salida: "El gato gato nada"
```

**[Ver ejemplo en vivo](https://playcode.io/2445662)**

### `replaceAll(patron, reemplazo)` (ES2021)

Reemplaza todas las ocurrencias de un `patron` (cadena o expresión regular global) con el `reemplazo` especificado.

```javascript
const texto = "El pato pato nada";
console.log(texto.replaceAll("pato", "cisne")); // Salida: "El cisne cisne nada"
```

**[Ver ejemplo en vivo](https://playcode.io/2445663)**

### `split(separador, limite)`

Divide una cadena en un arreglo de subcadenas, utilizando un `separador` especificado. El `limite` es opcional e indica el número máximo de divisiones a realizar.

```javascript
const palabras = "hola,mundo,javascript";
const frase = "El gato saltó.";

console.log(palabras.split(","));        // Salida: ["hola", "mundo", "javascript"]
console.log(frase.split(" "));           // Salida: ["El", "gato", "saltó."]
console.log(frase.split("a"));           // Salida: ["El g", "to s", "ltó."]
console.log(frase.split(" ", 2));        // Salida: ["El", "gato"] (limite de 2)
console.log("ABC".split(""));            // Salida: ["A", "B", "C"] (dividir por cada carácter)
```

**[Ver ejemplo en vivo](https://playcode.io/2445667)**

## 4. Transformación de Mayúsculas/Minúsculas y Espacios

### `toUpperCase()`

Convierte toda la cadena en mayúsculas.

```javascript
const minusculas = "hola mundo";
console.log(minusculas.toUpperCase()); // Salida: "HOLA MUNDO"
```

**[Ver ejemplo en vivo](https://playcode.io/2445670)**

### `toLowerCase()`

Convierte toda la cadena a minúsculas.

```javascript
const mayusculas = "HOLA MUNDO";
console.log(mayusculas.toLowerCase()); // Salida: "hola mundo"
```

**[Ver ejemplo en vivo](https://playcode.io/2445671)**

### `trim()`

Elimina los espacios en blanco (espacios, tabulaciones, nuevas líneas) del principio y del final de una cadena.

```javascript
const textoConEspacios = "   Hola Mundo   ";
console.log(textoConEspacios.trim()); // Salida: "Hola Mundo"
```

## 5. Otros Métodos Útiles

### `padStart(longitudTotal, caracterRelleno)` y `padEnd(longitudTotal, caracterRelleno)` (ES2017)

Rellena la cadena con un carácter especificado (`caracterRelleno`) hasta alcanzar una `longitudTotal` desde el principio (`padStart`) o el final (`padEnd`).

```javascript
const numero = "42";
console.log(numero.padStart(5, "0")); // Salida: "00042"
console.log(numero.padEnd(5, "X"));   // Salida: "42XXX"
```

**[Ver ejemplo en vivo](https://playcode.io/2445677)**

### `repeat(conteo)` (ES6)

Construye y devuelve una nueva cadena que contiene el número especificado de copias de la cadena sobre la cual fue llamado.

```javascript
const eco = "eco ";
console.log(eco.repeat(3)); // Salida: "eco eco eco "
```

**[Ver ejemplo en vivo](https://playcode.io/2445681)**

---

Estos métodos proporcionan las herramientas necesarias para manipular cadenas de texto de manera eficiente y efectiva en JavaScript, desde la extracción de partes hasta la transformación y validación de su contenido.