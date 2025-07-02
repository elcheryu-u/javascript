# Métodos Comunes de Arreglos en JavaScript

Los arreglos en JavaScript vienen con una gran cantidad de métodos incorporados que facilitan la manipulación, búsqueda y transformación de sus elementos. Aquí se presentan algunos de los más utilizados, categorizados por su función principal.

## Métodos para Añadir y Eliminar Elementos

### `push()`

Añade uno o más elementos al final de un arreglo y devuelve la nueva longitud del arreglo.

```javascript
const frutas = ["manzana", "banana"];
const nuevaLongitud = frutas.push("cereza", "dátil");

console.log(frutas);         // Salida: ["manzana", "banana", "cereza", "dátil"]
console.log(nuevaLongitud);  // Salida: 4
```

**[Visitar ejemplo en vivo](https://playcode.io/2444016)**

### `pop()`

Elimina el último elemento de un arreglo y lo devuelve.

```javascript
const animales = ["perro", "gato", "pez"];
const ultimoAnimal = animales.pop();

console.log(animales);      // Salida: ["perro", "gato"]
console.log(ultimoAnimal);  // Salida: "pez"
```

**[Visitar ejemplo en vivo](https://playcode.io/2444018)**

### `unshift()`

Añade uno o más elementos al principio de un arreglo y devuelve la nueva longitud del arreglo.

```javascript
const colores = ["verde", "azul"];
const nuevaLongitudColores = colores.unshift("rojo", "amarillo");

console.log(colores);             // Salida: ["rojo", "amarillo", "verde", "azul"]
console.log(nuevaLongitudColores); // Salida: 4
```

**[Visitar ejemplo en vivo](https://playcode.io/2444019)**

### `shift()`

Elimina el primer elemento de un arreglo y lo devuelve.

```javascript
const paises = ["España", "Francia", "Alemania"];
const primerPais = paises.shift();

console.log(paises);     // Salida: ["Francia", "Alemania"]
console.log(primerPais); // Salida: "España"
```

**[Visitar ejemplo en vivo](https://playcode.io/2444020)**

### `splice()`

Cambia el contenido de un arreglo eliminando elementos existentes y/o añadiendo nuevos elementos en su lugar. Es un método muy versátil.

- `array.splice(indiceInicio, cantidadAEliminar, elemento1, ..., elementoN)`

```javascript
const meses = ["Ene", "Feb", "Mar", "Abr", "May"];

// Eliminar 1 elemento desde el índice 2 ("Mar")
meses.splice(2, 1);
console.log(meses); // Salida: ["Ene", "Feb", "Abr", "May"]

// Eliminar 0 elementos desde el índice 1, y añadir "NuevoFeb"
meses.splice(1, 0, "NuevoFeb");
console.log(meses); // Salida: ["Ene", "NuevoFeb", "Feb", "Abr", "May"]

// Eliminar 2 elementos desde el índice 2 ("Feb", "Abr"), y añadir "Jun", "Jul"
meses.splice(2, 2, "Jun", "Jul");
console.log(meses); // Salida: ["Ene", "NuevoFeb", "Jun", "Jul", "May"]
```

**[Ver ejemplo en vivo](https://playcode.io/2444022)**

## Métodos para Iteración y Transformación

### `forEach()`

Ejecuta una función proporcionada una vez para cada elemento del arreglo. No devuelve un nuevo arreglo.

- `array.forEach(callback(elemento, indice, array))`

```javascript
const numeros = [1, 2, 3];
numeros.forEach(function(numero, index) {
    console.log(`El número ${numero} está en el índice ${index}`);
});
// Salida:
// El número 1 está en el índice 0
// El número 2 está en el índice 1
// El número 3 está en el índice 2
```

**[Ver ejemplo en vivo](https://playcode.io/2444027)**

### `map()`

Crea un nuevo arreglo con los resultados de la llamada a la función indicada aplicada a cada uno de sus elementos.

- `array.map(callback(elemento, indice, array))`

```javascript
const numeros = [1, 2, 3];
const duplicados = numeros.map(numero => numero * 2);

console.log(numeros);     // Salida: [1, 2, 3] (el arreglo original no se modifica)
console.log(duplicados);  // Salida: [2, 4, 6]
```

**[Ver ejemplo en vivo](https://playcode.io/2444029)**

### `filter()`

Crea un nuevo arreglo con todos los elementos que pasan la prueba implementada por la función proporcionada.

- `array.filter(callback(elemento, indice, array))`

```javascript
const edades = [12, 18, 25, 6, 30];
const mayoresDeEdad = edades.filter(edad => edad >= 18);

console.log(edades);         // Salida: [12, 18, 25, 6, 30]
console.log(mayoresDeEdad);  // Salida: [18, 25, 30]
```

**[Ver ejemplo en vivo](https://playcode.io/2444031)**

### `reduce()`

Ejecuta una función "reductora" sobre cada elemento de un arreglo, de forma que se obtiene un único valor de retorno.

- `array.reduce(callback(acumulador, elementoActual, indice, array), valorInicial)`

```javascript
const numeros = [1, 2, 3, 4];
const suma = numeros.reduce((acumulador, numero) => acumulador + numero, 0);

console.log(suma); // Salida: 10 (0 + 1 + 2 + 3 + 4)

const palabras = ["Hola", " ", "Mundo", "!"];
const frase = palabras.reduce((acumulador, palabra) => acumulador + palabra, "");

console.log(frase); // Salida: "Hola Mundo!"
```

**[Ver ejemplo en vivo](https://playcode.io/2444034)**

## Métodos para búsqueda

### `indexOf()`

Devuelve el primer índice en el que se puede encontrar un elemento dado en el arreglo, o `-1` si no está presente.

```javascript
const frutas = ["manzana", "banana", "cereza", "manzana"];
console.log(frutas.indexOf("banana"));  // Salida: 1
console.log(frutas.indexOf("manzana")); // Salida: 0 (primera ocurrencia)
console.log(frutas.indexOf("uva"));     // Salida: -1
```

**[Ver ejemplo en vivo](https://playcode.io/2444036)**

### `includes()`

Determina si un arreglo incluye un determinado elemento, devolviendo `true` o `false` según corresponda.

```javascript
const numeros = [1, 5, 10, 15];
console.log(numeros.includes(5));   // Salida: true
console.log(numeros.includes(20));  // Salida: false
```

**[Ver ejemplo en vivo](https://playcode.io/2444040)**

### `find()`

Devuelve el valor del primer elemento del arreglo que cumple la función de prueba proporcionada. Si n ose encuentra ningún elemento, devuelve `undefined`.

- `array.find(callback(elemento, indice, array))`

```javascript
const usuarios = [
    { id: 1, nombre: "Ana" },
    { id: 2, nombre: "Luis" },
    { id: 3, nombre: "Carlos" }
];

const usuarioEncontrado = usuarios.find(usuario => usuario.id === 2);
console.log(usuarioEncontrado); // Salida: { id: 2, nombre: "Luis" }

const usuarioNoEncontrado = usuarios.find(usuario => usuario.id === 4);
console.log(usuarioNoEncontrado); // Salida: undefined
```

**[Visitar ejemplo en vivo](https://playcode.io/2444041)**

### `findIndex()`

Devuelve el índice del primer elemento del arreglo que cumple la función de prueba proporcionada. En caso contrario, devuelve `-1`.

- `array.findIndex(callback(elemento, indice, array))`

```javascript
const productos = [
    { id: "a", nombre: "Laptop" },
    { id: "b", nombre: "Teclado" },
    { id: "c", nombre: "Mouse" }
];

const indiceTeclado = productos.findIndex(producto => producto.nombre === "Teclado");
console.log(indiceTeclado); // Salida: 1

const indiceMonitor = productos.findIndex(producto => producto.nombre === "Monitor");
console.log(indiceMonitor); // Salida: -1
```

**[Visitar ejemplo en vivo](https://playcode.io/2444043)**

## Métodos para combinar y copiar

### `concat()`

Se usa para unir dos o más arreglos. Este método no cambia arreglos existentes, sino que devuelve un nuevo arreglo.

```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];
const arr3 = [5, 6];

const combinado = arr1.concat(arr2, arr3);
console.log(combinado); // Salida: [1, 2, 3, 4, 5, 6]
console.log(arr1);      // Salida: [1, 2] (original no modificado)
```

**[Ver ejemplo en vivo](https://playcode.io/2444045)**

### `slice()`

Devuelve una copia superficial de una porción de un arreglo dentro de un nuevo objeto de arreglo seleccionado desde `inicio` hasta `fin` (fin no incluido). El arreglo original no se modificará.

- `array.slice(inicio, fin)`

```javascript
const animales = ["ant", "bison", "camel", "duck", "elephant"];

console.log(animales.slice(2));     // Salida: ["camel", "duck", "elephant"] (desde el índice 2 hasta el final)
console.log(animales.slice(2, 4));  // Salida: ["camel", "duck"] (desde el índice 2 hasta antes del 4)
console.log(animales.slice(1, 5));  // Salida: ["bison", "camel", "duck", "elephant"]
console.log(animales.slice(-2));    // Salida: ["duck", "elephant"] (los dos últimos elementos)
console.log(animales.slice(2, -1)); // Salida: ["camel", "duck"] (desde el índice 2 hasta el penúltimo)
```

**[Ver ejemplo en vivo](https://playcode.io/2444047)**