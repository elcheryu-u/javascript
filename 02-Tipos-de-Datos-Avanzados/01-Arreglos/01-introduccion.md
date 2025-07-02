# Arreglos (Arrays) en JavaScript

Los arreglos en JavaScript son objetos similares a listas que te permiten almacenar colecciones ordenadas de datos. Son fundamentales para manejar grupos de información, ya sean números, cadenas de texto, otros objetos, o incluso funciones.

## Características Clave de los Arreglos

* **Ordenados:** Los elementos en un arreglo mantienen un orden específico, al que se puede acceder mediante un índice numérico (posición). El primer elemento está en el índice `0`, el segundo en el `1`, y así sucesivamente.
* **Basados en Cero:** La indexación de los arreglos en JavaScript comienza en `0`.
* **Heterogéneos:** Un mismo arreglo puede contener elementos de diferentes tipos de datos (números, cadenas, booleanos, objetos, `null`, `undefined`, etc.).
* **Tamaño Dinámico:** Los arreglos en JavaScript no tienen un tamaño fijo; pueden crecer o encogerse según sea necesario.
* **Son Objetos:** Aunque se comportan como listas, los arreglos son un tipo especial de objeto en JavaScript. Esto significa que tienen propiedades y métodos inherentes que facilitan su manipulación.

## Declaración de Arreglos

Hay varias formas de declarar un arreglo en JavaScript:

### 1. Usando Literales de Arreglo (Recomendado)

Esta es la forma más común y concisa de crear un arreglo.

```javascript
// Arreglo de números
const numeros = [1, 2, 3, 4, 5];
console.log(numeros); // Salida: [1, 2, 3, 4, 5]

// Arreglo de cadenas de texto
const frutas = ["manzana", "banana", "cereza"];
console.log(frutas); // Salida: ["manzana", "banana", "cereza"]

// Arreglo mixto (diferentes tipos de datos)
const mixto = ["Hola", 123, true, { nombre: "Juan" }];
console.log(mixto); // Salida: ["Hola", 123, true, { nombre: "Juan" }]

// Arreglo vacío
const arregloVacio = [];
console.log(arregloVacio); // Salida: []
```

**[Visitar ejemplo en vivo](https://playcode.io/2444007)**

### 2. Usando el Constructor `Array()`

Aunque es menos común para la creación básica, el constructor `Array()` también se puede utilizar.

```javascript
// Creando un arreglo vacío
const arr1 = new Array();
console.log(arr1); // Salida: []

// Creando un arreglo con elementos iniciales
const arr2 = new Array(1, 2, 3);
console.log(arr2); // Salida: [1, 2, 3]

// ¡Cuidado! Si se pasa un solo número al constructor,
// se crea un arreglo con esa longitud, pero vacío.
const arr3 = new Array(5);
console.log(arr3); // Salida: [ <5 empty items> ]
console.log(arr3.length); // Salida: 5
```

**[Visitar ejemplo en vivo](https://playcode.io/2444009)**

## Acceso a Elementos del Arreglo

Se accede a los elementos de un arreglo utilizando su índice entre corchetes `[]`.

```javascript
const colores = ["rojo", "verde", "azul"];

console.log(colores[0]); // Salida: "rojo" (el primer elemento)
console.log(colores[1]); // Salida: "verde"
console.log(colores[2]); // Salida: "azul"

// Acceder a un índice que no existe devuelve `undefined`
console.log(colores[3]); // Salida: undefined
```

**[Visitar ejemplo en vivo](https://playcode.io/2444012)**

## Modificación de Elementos del Arreglo

Puedes modificar un elemento existente asignándole un nuevo valor a su índice.

```javascript
const nombres = ["Ana", "Luis", "Carlos"];
console.log(nombres); // Salida: ["Ana", "Luis", "Carlos"]

nombres[1] = "Pedro"; // Modifica el segundo elemento
console.log(nombres); // Salida: ["Ana", "Pedro", "Carlos"]

// Puedes añadir elementos en un índice superior a la longitud actual,
// lo que creará "agujeros" (elementos vacíos) en el arreglo.
nombres[4] = "Sofía";
console.log(nombres); // Salida: ["Ana", "Pedro", "Carlos", <1 empty item | elemento vacío>, "Sofía"]
console.log(nombres[3]); // Salida: undefined
```

**[Visitar ejemplo en vivo](https://playcode.io/2444014)**

## Propiedad `length`

La propiedad `length` de un arreglo devuelve el número de elementos que contiene.

```javascript
const elementos = [10, 20, 30, 40];
console.log(elementos.length); // Salida: 4

elementos.push(50); // Añade un elemento al final
console.log(elementos.length); // Salida: 5

elementos.pop(); // Elimina el último elemento
console.log(elementos.length); // Salida: 4

// Modificar `length` puede truncar o extender el arreglo
let miArray = [1, 2, 3, 4, 5];
miArray.length = 3; // Trunca el array
console.log(miArray); // Salida: [1, 2, 3]

miArray.length = 5; // Extiende el array con elementos vacíos
console.log(miArray); // Salida: [1, 2, 3, <2 empty items>]
```

**[Visitar ejemplo en vivo](https://playcode.io/2444015)**