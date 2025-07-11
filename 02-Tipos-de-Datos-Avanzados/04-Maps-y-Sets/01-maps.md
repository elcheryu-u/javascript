# Map en JavaScript (ES6)

`Map` es una colección de pares clave-valor donde las claves pueden ser de cualquier tipo de dato (objetos, funciones, números, etc.), a diferencia de los objetos literales (`{}`), donde las claves siempre se convierten a cadenas (strings). `Map` fue introducido en ECMAScript 2015 (ES6) para ofrecer una alternativa más robusta y flexible a los objetos tradicionales cuando se necesita almacenar datos con claves que no son cadenas.

## Características Clave de `Map`

* **Claves de Cualquier Tipo:** Acepta cualquier tipo de dato como clave (primitivos, objetos, funciones).
* **Orden de Inserción:** Los elementos en un `Map` mantienen el orden en que fueron insertados.
* **Iterable:** Los `Map` son directamente iterables, lo que permite recorrer sus elementos fácilmente.
* **Rendimiento:** Generalmente, los `Map` tienen un mejor rendimiento cuando se añaden y eliminan muchos pares clave-valor con frecuencia.
* **Propiedad `size`:** Permite obtener el número de elementos.

## Creación de un `Map`

Puedes crear un `Map` vacío o inicializarlo con un arreglo de pares `[clave, valor]`.

### 1. `new Map()` (Vacío)

```javascript
const miMapa = new Map();
console.log(miMapa); // Salida: Map(0) {}
```

**[Ver ejemplo en vivo](https://playcode.io/2456264)**

### 2. `new Map(iterable)` (Con Valores Iniciales)

Se le puede pasar un `iterable` (como un arreglo) de arreglos de dos elementos, donde cada arreglo anidado es un par `[clave, valor]`.

```javascript
const mapaInicial = new Map([
    ['nombre', 'Juan'],
    [1, 'Uno'],
    [true, 'Verdadero']
]);
console.log(mapaInicial); // Salida: Map(3) { 'nombre' => 'Juan', 1 => 'Uno', true => 'Verdadero' }
```

**[Ver ejemplo en vivo](https://playcode.io/2456285)**

## Métodos Comunes de `Map`

### `map.set(clave, valor)`

Añade o actualiza un par clave-valor en el `Map`. Si la clave ya existe, su valor se actualiza. Devuelve el propio objeto `Map`, lo que permite el encadenamiento.

```javascript
const usuarios = new Map();

usuarios.set('id1', { nombre: 'Alice', edad: 30 });
usuarios.set('id2', { nombre: 'Bob', edad: 25 });

console.log(usuarios);
// Salida: Map(2) { 'id1' => { nombre: 'Alice', edad: 30 }, 'id2' => { nombre: 'Bob', edad: 25 } }

// Actualizar un valor
usuarios.set('id1', { nombre: 'Alicia', edad: 31 });
console.log(usuarios.get('id1')); // Salida: { nombre: 'Alicia', edad: 31 }

// Usar un objeto como clave
const objClave = { tipo: 'config' };
usuarios.set(objClave, 'Configuración Global');
console.log(usuarios);
// Salida: Map(3) { 'id1' => { nombre: 'Alicia', edad: 31 }, 'id2' => { nombre: 'Bob', edad: 25 }, { tipo: 'config' } => 'Configuración Global' }
```

**[Ver ejemplo en vivo](https://playcode.io/2456290)**

### `map.get(clave)`

Devuelve el valor asociado a la `clave` especificada, o `undefined` si la clave no se encuentra.

```javascript
const datos = new Map([
    ['ciudad', 'París'],
    ['temperatura', 20]
]);

console.log(datos.get('ciudad'));      // Salida: 'París'
console.log(datos.get('humedad'));     // Salida: undefined
```

**[Ver ejemplo en vivo](https://playcode.io/2456295)**

### `map.has(clave)`

Devuelve `true` si un elemento con la `clave` especificada existe en el `Map`, de lo contrario, `false`.

```javascript
const inventario = new Map([
    ['manzana', 10],
    ['banana', 5]
]);

console.log(inventario.has('manzana')); // Salida: true
console.log(inventario.has('uva'));     // Salida: false
```

**[Ver ejemplo en vivo](https://playcode.io/2456298)**

### `map.delete(clave)`

Elimina el elemento asociado a la `clave` especificada. Devuelve `true` si el elemento existía y fue eliminado, o `false` si no existía.

```javascript
const mapaEliminar = new Map([
    ['a', 1],
    ['b', 2]
]);

console.log(mapaEliminar.delete('a'));    // Salida: true
console.log(mapaEliminar);              // Salida: Map(1) { 'b' => 2 }
console.log(mapaEliminar.delete('c'));    // Salida: false (no existía)
```

**[Ver ejemplo en vivo](https://playcode.io/2456306)**

### `map.clear()`

Elimina todos los elementos de un `Map`. No devuelve nada.

```javascript
const colores = new Map([
    ['rojo', '#FF0000'],
    ['azul', '#0000FF']
]);

console.log(colores.size); // Salida: 2
colores.clear();
console.log(colores.size); // Salida: 0
console.log(colores);      // Salida: Map(0) {}
```

**[Ver ejemplo en vivo](https://playcode.io/2456315)**

### `map.size`

Una propiedad (no un método) que devuelve el número de elementos (pares clave-valor) en el `Map`.

```javascript
const productos = new Map([
    ['pan', 1],
    ['leche', 2],
    ['huevos', 12]
]);
console.log(productos.size); // Salida: 3
```

**[Ver ejemplo en vivo](https://playcode.io/2456319)**

## Iteración sobre `Map`

Los `Map` son iterables, lo que significa que puedes usar `for...of` para recorrer sus elementos.

### `map.keys()`

Devuelve un nuevo objeto `MapIterator` que contiene las **claves** de cada elemento en el `Map` en el orden de inserción.

```javascript
const usuarios = new Map([
    ['id1', 'Alice'],
    ['id2', 'Bob']
]);
for (const key of usuarios.keys()) {
    console.log(key);
}
// Salida:
// id1
// id2
```

**[Ver ejemplo en vivo](https://playcode.io/2456321)**

### `map.values()`

Devuelve un nuevo objeto `MapIterator` que contiene los **valores** de cada elemento en el `Map` en el orden de inserción.

```javascript
const usuarios = new Map([
    ['id1', 'Alice'],
    ['id2', 'Bob']
]);

for (const value of usuarios.values()) {
    console.log(value);
}
// Salida:
// Alice
// Bob
```

### `map.entries()`

Devuelve un nuevo objeto `MapIterator` que contiene los pares `[clave, valor]` de cada elemento en el `Map` en el orden de inserción. Es el comportamiento por defecto cuando iteras directamente un `Map` con `for...of`.

```javascript
const usuarios = new Map([
    ['id1', 'Alice'],
    ['id2', 'Bob']
]);

for (const entry of usuarios.entries()) {
    console.log(entry);
}
// Salida:
// ["id1", "Alice"]
// ["id2", "Bob"]

// También puedes desestructurar directamente
for (const [key, value] of usuarios) { // `map.entries()` es el iterador por defecto
    console.log(`Clave: ${key}, Valor: ${value}`);
}
// Salida:
// Clave: id1, Valor: Alice
// Clave: id2, Valor: Bob
```

**[Ver ejemplo en vivo](https://playcode.io/2456330)**

### `map.forEach(callbackFn, thisArg)`

Ejecuta una función proporcionada una vez por cada par clave-valor en el `Map`

```javascript
const ciudades = new Map([
    ['NY', 'Nueva York'],
    ['LDN', 'Londres']
]);

ciudades.forEach((value, key) => { // Nota el orden: (valor, clave)
    console.log(`La clave ${key} corresponde a la ciudad ${value}`);
});
// Salida:
// La clave NY corresponde a la ciudad Nueva York
// La clave LDN corresponde a la ciudad Londres
```

**[Ver ejemplo en vivo](https://playcode.io/2456343)**

## ¿Cuándo usar `Map` en lugar de Objetos (`{}`)?

- Necesitas que las **claves no sean solo cadenas de texto** (por ejemplo, números, booleanos, o incluso otros objetos).
- El **orden de inserción** de los elementos es importante.
- Necesitas **iterar** sobre la colección de manera sencilla.
- Añades o eliminas pares clave-valor con **frecuencia**.
- El tamaño de la colección es **desconocido** o puede volverse **muy grande**.

Los `Map` ofrecen una solución robusta y con mejor rendimiento para escenarios donde los objetos tradicionales pueden tener limitaciones o comportamientos inesperados (como la coerción de claves a cadenas).