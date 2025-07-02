# Arreglos Multidimensionales en JavaScript

Aunque JavaScript no tiene arreglos multidimensionales "nativos" en el sentido estricto como otros lenguajes (donde se reservan bloques de memoria contiguos para matrices), se pueden simular fácilmente creando **arreglos de arreglos**. Esto permite representar estructuras de datos complejas como matrices, tablas o cuadrículas.

Un arreglo multidimensional es esencialmente un arreglo donde cada elemento es, a su vez, otro arreglo.

## Arreglos Bidimensionales (Matrices)

El caso más común es un arreglo bidimensional, que se puede visualizar como una tabla con filas y columnas.

### Declaración de un Arreglo Bidimensional

Se declara anidando literales de arreglo.

```javascript
// Matriz 3x3 que representa un tablero de juego
const tablero = [
    ['X', 'O', 'X'],
    ['O', 'X', 'O'],
    ['X', 'O', 'X']
];

console.log(tablero);
/* Salida:
[
  [ 'X', 'O', 'X' ],
  [ 'O', 'X', 'O' ],
  [ 'X', 'O', 'X' ]
]
*/

// Matriz de números (2 filas, 3 columnas)
const matrizNumeros = [
    [1, 2, 3],
    [4, 5, 6]
];
console.log(matrizNumeros);
/* Salida:
[
  [ 1, 2, 3 ],
  [ 4, 5, 6 ]
]
*/
```

**[Ver ejemplo en vivo](https://playcode.io/2444048)**

### Acceso a Elementos en Arreglos Bidimensionales

Para acceder a un elemento específico, se utilizan dos índices: el primero para la fila y el segundo para la columna.

- `arreglo[indiceFila][indiceColumna]`

```javascript
const tablero = [
    ['X', 'O', 'X'],
    ['O', 'X', 'O'],
    ['X', 'O', 'X']
];

// Acceder al elemento en la primera fila, segunda columna (índice 0, 1)
console.log(tablero[0][1]); // Salida: 'O'

// Acceder al elemento en la segunda fila, primera columna (índice 1, 0)
console.log(tablero[1][0]); // Salida: 'O'

// Acceder al elemento en la tercera fila, tercera columna (índice 2, 2)
console.log(tablero[2][2]); // Salida: 'X'
```

**[Ver ejemplo en vivo](https://playcode.io/2444050)**

### Modificación de Elementos en Arreglos Bidimensionales

De manera similar, se modifica un elemento asignando un nuevo valor a su posición.

```javascript
const tablero = [
    ['X', 'O', 'X'],
    ['O', 'X', 'O'],
    ['X', 'O', 'X']
];

console.log("Antes de modificar:", tablero[1][1]); // Salida: 'X'

// Cambiar el centro del tablero a ' ' (vacío)
tablero[1][1] = ' ';
console.log("Después de modificar:", tablero[1][1]); // Salida: ' '
console.log(tablero);
/* Salida:
[
  [ 'X', 'O', 'X' ],
  [ 'O', ' ', 'O' ],
  [ 'X', 'O', 'X' ]
]
*/
```

**[Ver ejemplo en vivo](https://playcode.io/2444051)**

### Iteración sobre Arreglos Bidimensionales

Para recorrer todos los elementos de un arreglo bidimensional, generalmente se utilizan bucles `for` aninados.

```javascript
const matriz = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

console.log("Iterando sobre la matriz:");
for (let i = 0; i < matriz.length; i++) { // Itera sobre las filas
    for (let j = 0; j < matriz[i].length; j++) { // Itera sobre las columnas de la fila actual
        console.log(`Elemento en [${i}][${j}]: ${matriz[i][j]}`);
    }
}
/* Salida:
Elemento en [0][0]: 1
Elemento en [0][1]: 2
Elemento en [0][2]: 3
Elemento en [1][0]: 4
...
Elemento en [2][2]: 9
*/

// Usando for...of (más moderno y legible)
console.log("\nIterando con for...of:");
for (const fila of matriz) {
    for (const elemento of fila) {
        console.log(elemento);
    }
}
/* Salida:
1
2
3
4
...
9
*/
```

**[Ver ejemplo en vivo](https://playcode.io/2444053)**

## Arreglos Multidimensionales Irregulares (Jagged Arrays)

Dado que los arreglos en JavaScript son arreglos de referencias a otros arreglos, las "filas" no tienen que tener la misma longitud. Esto crea lo que se conoce como arreglos "irregulares" o "jagged arrays".

```javascript
const matrizIrregular = [
    [1, 2],
    [3, 4, 5],
    [6]
];

console.log(matrizIrregular);
/* Salida:
[
  [ 1, 2 ],
  [ 3, 4, 5 ],
  [ 6 ]
]
*/

console.log(matrizIrregular[0].length); // Salida: 2
console.log(matrizIrregular[1].length); // Salida: 3
```

**[Ver ejemplo en vivo](https://playcode.io/2444057)**

## Arreglos de Mayor Dimensión

Puedes extender este concepto para crear arreglos de tres o más dimensiones (cubos, etc.) anidando más arreglos.

```javascript
// Arreglo tridimensional (3D)
const cubo = [
    [
        [1, 2],
        [3, 4]
    ],
    [
        [5, 6],
        [7, 8]
    ]
];

console.log(cubo[0][1][0]); // Accede al '3'
console.log(cubo[1][0][1]); // Accede al '6'
```

**[Ver ejemplo completo](https://playcode.io/2444058)**

Los arreglos multidimensionales son una herramienta poderosa para organizar datos complejos en JavaScript, especialmente cuando se trabaja con estructuras que tienen una relación jerárquica o espacial.