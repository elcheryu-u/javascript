# Cadena de Métodos (Method Chaining) en JavaScript

La Cadena de Métodos, o "Method Chaining", es un patrón de programación que permite invocar múltiples métodos sobre un objeto en una única expresión (o línea de código), sin necesidad de almacenar el resultado intermedio de cada llamada a método en una variable separada. Esto se logra cuando cada método en la cadena devuelve el propio objeto (o una referencia a él), permitiendo que el siguiente método sea invocado inmediatamente.

Este patrón mejora la **legibilidad** y la **concisión** del código, haciendo que las secuencias de operaciones sean más fluidas y expresivas.

## ¿Cómo Funciona la Cadena de Métodos?

Para que la cadena de métodos funcione, cada método que forma parte de la cadena debe devolver `this` (una referencia al objeto actual) al finalizar su operación, o en algunos casos, un nuevo objeto sobre el que se pueda seguir encadenando.

### Ejemplo Básico con un Objeto Simple

Vamos a crear un objeto `Calculadora` que permita encadenar operaciones.

```javascript
const calculadora = {
    valor: 0, // Propiedad interna para almacenar el resultado

    sumar(num) {
        this.valor += num;
        return this; // Devuelve el propio objeto para permitir el encadenamiento
    },

    restar(num) {
        this.valor -= num;
        return this; // Devuelve el propio objeto
    },

    multiplicar(num) {
        this.valor *= num;
        return this; // Devuelve el propio objeto
    },

    obtenerResultado() {
        return this.valor; // Este método no devuelve `this` porque es el final de la cadena
    },

    limpiar() {
        this.valor = 0;
        return this; // Para poder encadenar un reset
    }
};

// Encadenamiento de métodos
const resultadoFinal = calculadora
    .limpiar()         // Reinicia el valor a 0
    .sumar(10)         // valor = 10
    .multiplicar(2)    // valor = 20
    .restar(5)         // valor = 15
    .obtenerResultado(); // Obtiene el valor final

console.log(resultadoFinal); // Salida: 15

// Otro ejemplo
const resultado2 = calculadora.limpiar().sumar(100).restar(50).obtenerResultado();
console.log(resultado2); // Salida: 50
```

**[Ver ejemplo en vivo](https://playcode.io/2456201)**

En este ejemplo, los métodos `sumar`, `restar`, `multiplicar` y `limpiar` devuelven `this`, lo que permite que el siguiente método se ejecute sobre el mismo objeto `calculadora`. El método `obtenerResultado` no devuelve `this` porque su propósito es finalizar la cadena y proporcionar el resultado.

## Cadena de Métodos con Arreglos (Transformaciones)

Los métodos de arreglo en JavaScript son un excelente ejemplo de cade de métodos, aunque no siempre devuelven el _mismo_ arreglo, sino _nuevos arreglos_ sobre los cuales se puede seguir encadenando operaciones.

```javascript
const numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const numerosParesDuplicados = numeros
    .filter(num => num % 2 === 0) // Filtra solo los pares: [2, 4, 6, 8, 10]
    .map(num => num * 2)         // Duplica cada par: [4, 8, 12, 16, 20]
    .reduce((sum, num) => sum + num, 0); // Suma los duplicados: 60

console.log(numerosParesDuplicados); // Salida: 60

// Otro ejemplo: obtener nombres en mayúsculas de usuarios mayores de 20
const usuarios = [
    { nombre: "Ana", edad: 22 },
    { nombre: "Luis", edad: 18 },
    { nombre: "Marta", edad: 25 },
    { nombre: "Pedro", edad: 19 }
];

const nombresMayores = usuarios
    .filter(usuario => usuario.edad > 20) // [{ nombre: "Ana", edad: 22 }, { nombre: "Marta", edad: 25 }]
    .map(usuario => usuario.nombre.toUpperCase()); // ["ANA", "MARTA"]

console.log(nombresMayores); // Salida: ["ANA", "MARTA"]
```

**[Ver ejemplo en vivo](https://playcode.io/2456209)**

Aquí, `filter` devuelve un nuevo arreglo, sobre el cual `map` puede operar y devolver otro nuevo arreglo. Este es un tipo de encadenamiento común en la programación funcional.

## Beneficios del Method Chaining

- **Legibilidad:** El flujo de operaciones es lineal y fácil de seguir.
- **Concisión:** Reduce la necesidad de variables temporales.
- **Expresividad:** Permite escribir código que se lee casi como una descripción de los pasos.

## Cuando considerar el Method Chaining

- Cuando tienes una secuencia de operaciones que se aplican al mismo objeto (o a resultados intermedios lógicamente relacionados).
- En APIs fluidas donde el diseño de la librería está pensado para ello (ej. librerías de DOM, manipulación de colecciones).
- Cuando la legibilidad de la secuencia de pasos es más importante que la depuración paso a paso de cada resultado intermedio individual (aunque las herramientas de depuración)

## Desventajas Potenciales

- **Depuración:** Puede ser ligeramente más dificil depurar una cadena larga si no se usan puntos de interrupción estratégicos, ya que los resultados intermedios no están en variables nombradas.
- **Errores:** Un error en cualquier parte de la cadena puede romper toda la secuencia.
- **Complejidad:** Un encadenamiento excesivo o mal diseñado puede hacer que el código sea difícil de leer y mantener si la lógica de cada método no es clara.

La cadena de métodos es una técnica poderosa para escribir código JavaScript más limpio y expresivo, siempre y cuando se utilice con sensatez para mejorar la legibilidad y no para oscurecer la lógica.