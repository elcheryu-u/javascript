# Objetos en JavaScript: Introducción y Fundamentos

En JavaScript, los objetos son colecciones de propiedades, donde cada propiedad tiene un nombre (clave) y un valor. Son uno de los pilares fundamentales del lenguaje, sirviendo como la estructura de datos más versátil para representar entidades del mundo real, configuraciones o conjuntos de datos complejos. Prácticamente todo en JavaScript es un objeto o se comporta como tal (excepto los valores primitivos).

## Características Clave de los Objetos

* **Colección de Propiedades:** Un objeto es un contenedor de pares clave-valor. La clave (también llamada nombre de propiedad) es siempre una cadena de texto (o un Símbolo), y el valor puede ser cualquier tipo de dato en JavaScript (primitivo, otro objeto, función, etc.).
* **No Ordenados:** A diferencia de los arreglos, las propiedades de un objeto no tienen un orden inherente por índice numérico. El orden de iteración puede variar en versiones antiguas de JavaScript, pero en ES2015+ se garantiza el orden de inserción para propiedades no numéricas.
* **Dinámicos:** Las propiedades pueden añadirse, modificarse o eliminarse en tiempo de ejecución.
* **Referencia:** Los objetos son pasados por referencia, no por valor. Esto significa que cuando asignas un objeto a una nueva variable, ambas variables apuntan a la misma ubicación en memoria.

## Declaración de Objetos

La forma más común y recomendada de crear un objeto es utilizando la sintaxis de literales de objeto (`{}`).

### 1. Usando Literales de Objeto (Recomendado)

```javascript
// Objeto vacío
const miObjetoVacio = {};
console.log(miObjetoVacio); // Salida: {}

// Objeto con propiedades iniciales
const persona = {
    nombre: "Juan",      // Propiedad 'nombre' con valor 'Juan'
    edad: 30,            // Propiedad 'edad' con valor 30
    esEstudiante: false, // Propiedad 'esEstudiante' con valor false
    saludar: function() { // Propiedad 'saludar' con un valor de función (método)
        console.log("Hola, soy " + this.nombre);
    },
    "ciudad de residencia": "Bogotá" // Las claves con espacios o caracteres especiales requieren comillas
};

console.log(persona);
/* Salida:
{
  nombre: 'Juan',
  edad: 30,
  esEstudiante: false,
  saludar: [Function: saludar],
  'ciudad de residencia': 'Bogotá'
}
*/
```

**[Ver ejemplo en vivo](https://playcode.io/2454816)**

### 2. Usando el Constructor `Object()` (Menoss común para objetos simples)

```javascript
const coche = new Object();
coche.marca = "Toyota";
coche.modelo = "Corolla";
coche.anio = 2020;

console.log(coche); // Salida: { marca: 'Toyota', modelo: 'Corolla', anio: 2020 }
```

**[Ver ejemplo en vivo](https://playcode.io/2454818)**

## Acceso a Propiedades

Hay dos formas principales de acceder a las propiedades de un objeto:

### 1. Notación de Punto (`.`) - Recomendada para nombres de propiedad válidos

Es la forma más común y legible. Funciona cuando el nombre de la propiedad es un identificador JavaScript válido **(no contiene espacios, guiones, etc., y no comienza con un número)**.

```javascript
const usuario = {
    nombre: "Ana",
    email: "ana@example.com"
};

console.log(usuario.nombre);  // Salida: "Ana"
console.log(usuario.email);   // Salida: "ana@example.com"
```

**[Ver ejemplo en vivo](https://playcode.io/2454825)**

### 2. Notación de Corchetes (`[]`)

Se usa cuando el nombre de la propiedad es una cadena que contiene caracteres especiales (espacio, guiones, etc.) o cuando el nombre de la propiedad se almacena en una variable.

```javascript
const producto = {
    "nombre-producto": "Camiseta",
    "precio base": 25,
    1: "Primer Item" // Las claves numéricas se acceden como cadenas
};

console.log(producto["nombre-producto"]); // Salida: "Camiseta"
console.log(producto["precio base"]);     // Salida: 25
console.log(producto[1]);                 // Salida: "Primer Item"

const claveDinamica = "nombre-producto";
console.log(producto[claveDinamica]);     // Salida: "Camiseta" (Acceso dinámico)
```

**[Ver ejemplo en vivo](https://playcode.io/2454827)**

## Modificación de Propiedades

Puedes modificar el valor de una propiedad existente o añadir nuevas propiedades a un objeto simplemente asignando un valor.

```javascript
const libro = {
    titulo: "El Quijote",
    autor: "Miguel de Cervantes"
};

console.log(libro); // Salida: { titulo: 'El Quijote', autor: 'Miguel de Cervantes' }

// Modificar una propiedad existente
libro.titulo = "Don Quijote de la Mancha";
console.log(libro.titulo); // Salida: "Don Quijote de la Mancha"

// Añadir una nueva propiedad
libro.anioPublicacion = 1605;
console.log(libro.anioPublicacion); // Salida: 1605

// Añadir una nueva propiedad usando notación de corchetes
libro["editorial"] = "Planeta";
console.log(libro.editorial); // Salida: "Planeta"
```

**[Ver ejemplo en vivo](https://playcode.io/2454828)**

## Eliminación de Propiedades

Usa el operador `delete` para eliminar una propiedad de un objeto.

```javascript
const configuracion = {
    tema: "oscuro",
    idioma: "es",
    notificaciones: true
};

console.log(configuracion); // Salida: { tema: 'oscuro', idioma: 'es', notificaciones: true }

delete configuracion.notificaciones;
console.log(configuracion); // Salida: { tema: 'oscuro', idioma: 'es' }

delete configuracion["idioma"];
console.log(configuracion); // Salida: { tema: 'oscuro' }
```

**[Ver ejemplo en vivo](https://playcode.io/2454830)**

## Objetos como Tipos de Referencia

Cuando se asigna un objeto a una nueva variable, ambas variables apuntan a la misma ubicación en memoria. Esto significa que un cambio a través de una variable reflejará en la otra.

```javascript
const obj1 = { valor: 10 };
const obj2 = obj1; // obj2 ahora apunta al mismo objeto que obj1

obj2.valor = 20;

console.log(obj1.valor); // Salida: 20 (cambió porque obj2 es una referencia a obj1)
console.log(obj2.valor); // Salida: 20
```

**[Ver ejemplo en vivo](https://playcode.io/2454834)**

Para copiar un objeto de forma independiente (copia superficial), se pueden usar métodos como `Object.assign()` o el operador de propagación (spread operator) `{...}`.

```javascript
const original = { a: 1, b: 2 };
const copia = { ...original }; // Copia superficial

copia.a = 10;

console.log(original.a); // Salida: 1 (el original no ha cambiado)
console.log(copia.a);    // Salida: 10
```

**[Ver ejemplo en vivo](https://playcode.io/2454837)**

Los objetos son la columna vertebral de la mayoria de las aplicaciones JavaScript, permitiendo modelar datos de forma estructurada y lógica. Comprender su comportamiento es esencial para escribir código eficiente y libre de errores.