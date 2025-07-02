# Casos de Uso Comunes de Arreglos en JavaScript

Los arreglos son una de las estructuras de datos más fundamentales y versátiles en JavaScript, utilizadas para una amplia variedad de tareas en el desarrollo web y de aplicaciones. Aquí exploraremos algunos de los casos de uso más comunes y efectivos para los arreglos.

## 1. Almacenar Colecciones de Elementos Similares

Este es el uso más básico y directo de un arreglo: mantener una lista de elementos que comparten una característica o propósito.

**Ejemplos:**
* Una lista de usuarios registrados.
* Una colección de productos en un carrito de compras.
* Una serie de números o resultados de mediciones.
* Una lista de tareas pendientes (To-Do List).

```javascript
// Lista de usuarios
const usuarios = ["Alice", "Bob", "Charlie", "David"];

// Productos en un carrito de compras (podrían ser objetos más complejos)
const carrito = [
    { id: 1, nombre: "Laptop", precio: 1200 },
    { id: 2, nombre: "Mouse", precio: 25 },
    { id: 1, nombre: "Laptop", precio: 1200 } // Pueden haber duplicados
];

// Días de la semana
const diasSemana = ["Lunes", "Martes", "Miércoles", "Jueves", "Viernes", "Sábado", "Domingo"];

console.log(usuarios);
console.log(carrito);
console.log(diasSemana[0]); // Acceder al primer día
```

**[Ver ejemplo en vivo](https://playcode.io/2444061)**

## 2. Implementar Listas de Características o Etiquetas (Tags)

Los arreglos son excelentes para almacenar conjuntos de atributos o categorías asociadas a un elemento.

**Ejemplos:**

- Las etiquetas (`tags`) de una publicación de blog.
- Las características de un producto (ej. "Wi-Fi", "Bluetooth", "USB-C").
- Los permisos que tiene un usuario.

```javascript
const post = {
    titulo: "Mi Primer Blog Post",
    contenido: "...",
    tags: ["JavaScript", "Programación", "Web Development"]
};

console.log(`Etiquetas del post: ${post.tags.join(", ")}`);

if (post.tags.includes("JavaScript")) {
    console.log("Este post trata sobre JavaScript.");
}

const producto = {
    nombre: "Smart TV 55",
    caracteristicas: ["4K", "HDR", "Smart", "Wi-Fi", "HDMI x3"]
};
```

**[Ver ejemplo en vivo](https://playcode.io/2444062)**

## 3. Manejar Series de Tiempo o Datos Secuenciales

Cuando el orden de los datos es importante, los arreglos son la elección natural.

**Ejemplos:**

- Datos de sensores a lo largo del tiempo.
- Movimientos de un juego (ej. Ajedrez).
- Pasos de una receta o un flujo de trabajo.

```javascript
// Temperaturas registradas cada hora
const temperaturasDiarias = [20, 22, 21, 23, 25, 24]; // Temperatura por hora del día

// Secuencia de movimientos en un juego
const movimientosJuego = ["e2-e4", "c7-c5", "g1-f3", "d7-d6"];

console.log(`Temperatura máxima: ${Math.max(...temperaturasDiarias)}°C`);
console.log(`Primer movimiento: ${movimientosJuego[0]}`);
```

**[Ver ejemplo en vivo](https://playcode.io/2444063)**

## 4. Crear Matrices y Cuadrículas (Arreglos Multidimensionales)

Como vimos anteriormente, los arreglos de arreglos son ideales para representar estructuras bidimensionales o de mayor dimensión.

[Ver Arreglos Multidimensionales](./arreglos-multidimensionales.md)

**Ejemplos:**

- Tableros de juegos (Tic-Tac-Toe, Sudoku).
- Mapas de celdas en un videojuego.
- Representación de matrices matemáticas.

```javascript
// Tablero de Tic-Tac-Toe
const ticTacToe = [
    ['X', 'O', ' '],
    [' ', 'X', 'O'],
    ['O', ' ', 'X']
];

console.log("Elemento central:", ticTacToe[1][1]); // Salida: 'X'

// Simulación de un mapa con diferentes tipos de terreno
const mapaJuego = [
    ["agua", "tierra", "agua"],
    ["tierra", "montaña", "tierra"],
    ["agua", "tierra", "bosque"]
];
```

## 5. Implementar Pilas (Stacks) y Colas (Queues)

Los arreglos pueden simular el comportamiento de estructuras de datos abstractas como pilas (LIFO - Last In, First Out) y colas (FIFO - First In, First Out) utilizando sus métodos [`push()`](./metodos-comunes.md#pop), [`pop()`](./metodos-comunes.md#pop), [`unshift()`](./metodos-comunes.md#unshift) y [`shift()`](./metodos-comunes.md#shift)

### Pila (Stack) - LIFO

- `push()` para añadir elementos al "tope" (final).
- `pop()` para eliminar y obtener el elemento del "tope" (final).

```javascript
const pilaLibros = [];

pilaLibros.push("Libro A"); // Añade A
pilaLibros.push("Libro B"); // Añade B
pilaLibros.push("Libro C"); // Añade C
console.log("Pila después de push:", pilaLibros); // Salida: ["Libro A", "Libro B", "Libro C"]

const ultimoLeido = pilaLibros.pop(); // Elimina C
console.log("Último libro leído:", ultimoLeido); // Salida: "Libro C"
console.log("Pila después de pop:", pilaLibros);  // Salida: ["Libro A", "Libro B"]
```

**[Ver ejemplo en vivo](https://playcode.io/2444069)**

### Cola (Queue) - FIFO

- `push()` para añadir elementos al "final" de la cola.
- `shift()` para eliminar y obtener el elemento del "frente" de la cola.

```javascript
const colaImpresion = [];

colaImpresion.push("Documento 1"); // Añade D1
colaImpresion.push("Documento 2"); // Añade D2
colaImpresion.push("Documento 3"); // Alade D3
console.log("Cola después de push:", colaImpresion); // Salida: ["Documento 1", "Documento 2"]

const documentoImpreso = colaImpresion.shift(); // Elimina D1
console.log("Documento impreso:", documentoImpreso); // Salida: "Documento 1"
console.log("Cola después de shift:", colaImpresion);  // Salida: ["Documento 2"]
```

**[Ver ejemplo en vivo](https://playcode.io/2444071)**

## 6. Procesamiento de Datos y Transformaciones

Los métodos de iteración como [`map()`](./metodos-comunes.md#map), [`filter()`](./metodos-comunes.md#filter), y [`reduce()`](./metodos-comunes.md#reduce) hacen que los arreglos sean increíblemente potentes para transformar y analizar colecciones de datos.

**Ejemplos:**

- Filtrar elementos que cumplen una condición.
- Mapear un arreglo de objetos a un arreglo de valores específicos.
- Calcular la suma, promedio o cualquier agregración de valores.

```javascript
const productos = [
    { nombre: "Leche", precio: 1.5, disponible: true },
    { nombre: "Pan", precio: 2.0, disponible: false },
    { nombre: "Huevos", precio: 3.0, disponible: true }
];

// Filtrar productos disponibles
const productosDisponibles = productos.filter(producto => producto.disponible);
console.log("Disponibles:", productosDisponibles);
// Salida: [ { nombre: 'Leche', precio: 1.5, disponible: true }, { nombre: 'Huevos', precio: 3, disponible: true } ]

// Obtener solo los nombres de los productos
const nombresProductos = productos.map(producto => producto.nombre);
console.log("Nombres:", nombresProductos); // Salida: ["Leche", "Pan", "Huevos"]

// Calcular el precio total de los productos disponibles
const precioTotalDisponibles = productosDisponibles.reduce((sum, p) => sum + p.precio, 0);
console.log("Precio total disponibles:", precioTotalDisponibles); // Salida: 4.5 (1.5 + 3.0)
```

**[Ver ejemplo en vivo](https://playcode.io/2444073)**