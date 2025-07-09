# Métodos Integrados de Objetos en JavaScript

Más allá de la manipulación directa de propiedades, JavaScript proporciona una serie de métodos estáticos en el constructor global `Object` que permiten realizar operaciones avanzadas sobre los objetos, como la enumeración de propiedades, la copia, la fusión y la configuración de atributos de las propiedades.

## 1. Métodos para Enumerar Propiedades

Estos métodos permiten obtener las claves (nombres de propiedad), los valores o los pares clave-valor de un objeto.

### `Object.keys(obj)`

Devuelve un arreglo de las propiedades enumerables (que pueden ser recorridas con `for...in`) de un objeto dado. El orden de las propiedades es el mismo que el orden de iteración proporcionado por un bucle `for...in`.

```javascript
const persona = {
    nombre: "Ana",
    edad: 28,
    ciudad: "Barcelona"
};

const claves = Object.keys(persona);
console.log(claves); // Salida: ["nombre", "edad", "ciudad"]

const arr = ["a", "b", "c"];
console.log(Object.keys(arr)); // Salida: ["0", "1", "2"] (las claves son los índices)
```

**[Ver ejemplo en vivo](https://playcode.io/2454841)**

### `Object.values(obj)` (ES2017)

Devuelve un arreglo de los valores de las propiedades enumerables de un objeto dado, en el mismo orden que `Object.keys()`.

```javascript
const producto = {
    item: "Laptop",
    precio: 1200,
    enStock: true
};

const valores = Object.values(producto);
console.log(valores); // Salida: ["Laptop", 1200, true]
```

**[Ver ejemplo en vivo](https://playcode.io/2454843)**

### `Object.entries(obj)` (ES2017)

Devuelve un arreglo de arreglos, donde cada arreglo anidado representa un par `[clave, valor]` de las propiedades enumerables de un objeto dado.

```javascript
const configuracion = {
    tema: "oscuro",
    idioma: "es",
    version: "1.0"
};

const entradas = Object.entries(configuracion);
console.log(entradas);
/* Salida:
[
  ["tema", "oscuro"],
  ["idioma", "es"],
  ["version", "1.0"]
]
*/

// Útil para iterar sobre objetos
for (const [clave, valor] of Object.entries(configuracion)) {
    console.log(`${clave}: ${valor}`);
}
/* Salida:
tema: oscuro
idioma: es
version: 1.0
*/
```

**[Ver ejemplo en vivo](https://playcode.io/2454845)**

## 2. Métodos para Copiar y Fusionar Objetos

### `Object.assign(objetoDestino, ...objetosFuente)`

Copia los valores de todas las propiedades enumerables propias de uno o más objetos fuente a un objeto destino. Este método devuelve el objeto destino. Realiza una **copia superficial**.

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };
const obj3 = { d: 5 };

const resultado = Object.assign({}, obj1, obj2, obj3); // El primer argumento es un objeto vacío para no modificar obj1
console.log(resultado); // Salida: { a: 1, b: 3, c: 4, d: 5 }
// Si hay claves duplicadas, las propiedades de los objetos posteriores sobrescriben a las anteriores.

// Copia superficial: si una propiedad es un objeto anidado, se copiará la referencia
const original = { a: 1, b: { c: 2 } };
const copia = Object.assign({}, original);

copia.b.c = 10; // Modifica el objeto anidado
console.log(original.b.c); // Salida: 10 (el original también se modifica)
```

**[Ver ejemplo en vivo](https://playcode.io/2454847)**

## 3. Métodos para Controlar la Extensibilidad y Configuración

Estos métodos permiten controlar cómo se pueden modificar los objetos.

### `Object.freeze(obj)`

Congela un objeto, lo que significa que ya no se pueden añadir nuevas propiedades, ni modificar o eliminar las propiedades existentes. Hace que el objeto sea inmutable. Realiza un congelamiento **superficial**.

```javascript
const punto = { x: 10, y: 20 };
Object.freeze(punto);

punto.x = 30; // No tendrá efecto
punto.z = 50; // No se añadirá
delete punto.y; // No se eliminará

console.log(punto); // Salida: { x: 10, y: 20 }

// Para comprobar si un objeto está congelado
console.log(Object.isFrozen(punto)); // Salida: true
```

**[Ver ejemplo en vivo](https://playcode.io/2454853)**

### `Object.seal(obj)`

Sella un objeto. Esto evita que se añadan o eliminen propiedades, pero permite modificar los valores de las propiedades existentes.

```javascript
const configuracion = { tema: "claro", idioma: "en" };
Object.seal(configuracion);

configuracion.tema = "oscuro"; // Permitido
configuracion.version = "1.0"; // No se añadirá
delete configuracion.idioma;   // No se eliminará

console.log(configuracion); // Salida: { tema: 'oscuro', idioma: 'en' }

// Para comprobar si un objeto está sellado
console.log(Object.isSealed(configuracion)); // Salida: true
```

**[Ver ejemplo en vivo](https://playcode.io/2454855)**

### `Object.preventExtensions(obj)`

Evita que se añadan nuevas propiedades a un objeto. Las propiedades existentes se pueden modificar o eliminar.

```javascript
const usuario = { id: 1, activo: true };
Object.preventExtensions(usuario);

usuario.nombre = "Pedro"; // No se añadirá
usuario.activo = false;   // Permitido

console.log(usuario); // Salida: { id: 1, activo: false }

// Para comprobar si se pueden añadir extensiones
console.log(Object.isExtensible(usuario)); // Salida: false
```

**[Ver ejemplo en vivo](https://playcode.io/2454857)**

## 4. Métodos para Comparación y Prototipos

### `Oject.is(valor1, valor2)` (ES6)

Determina si dos valores son el mismo valor. Es más robusto que el operador de igualdad estricta `===` en ciertos casos (manejo de `NaN` y `-0`).

```javascript
console.log(Object.is(25, 25));         // Salida: true
console.log(Object.is("foo", "foo"));   // Salida: true
console.log(Object.is(NaN, NaN));       // Salida: true (a diferencia de NaN === NaN, que es false)
console.log(Object.is(-0, 0));          // Salida: false (a diferencia de -0 === 0, que es true)
console.log(Object.is([], []));         // Salida: false (diferentes referencias)
```

**[Ver ejemplo en vivo](https://playcode.io/2454861)**

### `Object.getPrototypeOf(obj)`

Devuelve el prototipo (es decir, el valor de una propiedad interna `[[Prototype]]`) del objeto especificado.

```javascript
const protoBase = {
    saludar() {
        return "Hola";
    }
};
const obj = Object.create(protoBase); // Crea un objeto cuyo prototipo es protoBase

console.log(Object.getPrototypeOf(obj)); // Salida: { saludar: [Function: saludar] }
console.log(obj.saludar());              // Salida: "Hola"
```

**[Ver ejemplo en vivo](https://playcode.io/2454862)**

### `Object.setPrototypeOf(obj, prototype)` (ES6)

Establece el prototipo (es decir, la propiedad interna `[[Prototype]]`) de un objeto especificado a otro objeto o a `null`.

```javascript
const nuevoProto = {
    hablar() {
        return "Estoy hablando";
    }
};
const miObjeto = {};

Object.setPrototypeOf(miObjeto, nuevoProto);

console.log(Object.getPrototypeOf(miObjeto)); // Salida: { hablar: [Function: hablar] }
console.log(miObjeto.hablar());              // Salida: "Estoy hablando"
```

**[Ver ejemplo en vivo](https://playcode.io/2454869)**

Los métodos estáticos del objeto `Object` son herramientas esenciales para la manipulación avanzada y el control de los objetos en JavaScript, permitiendo desde la inspección de su estructura hasta la gestión de su mutabilidad.