# Métodos de Fábrica (Factory Methods) en JavaScript

Los Métodos de Fábrica, o "Factory Methods", son un patrón de diseño creacional en el que se utiliza una función (la "función fábrica") para crear y devolver objetos. En lugar de crear objetos directamente con el operador `new` (especialmente antes de ES6 y las clases, o cuando se manejan objetos complejos), las funciones fábrica encapsulan la lógica de creación de objetos, lo que las hace muy útiles para producir múltiples objetos con propiedades y métodos similares de forma consistente.

Este patrón promueve la **reutilización de código** y ayuda a mantener el principio de **separación de preocupaciones**, ya que la lógica de creación de objetos se centraliza en un único lugar.

## ¿Por qué usar Métodos de Fábrica?

1.  **Abstracción de la Creación:** Oculta la complejidad de la creación del objeto. El código que llama a la fábrica no necesita saber cómo se construye el objeto internamente.
2.  **Reutilización:** Permite crear múltiples instancias de objetos con configuraciones o inicializaciones predefinidas sin duplicar código.
3.  **Flexibilidad:** Facilita la creación de diferentes tipos de objetos basados en ciertos parámetros de entrada, sin que el código cliente tenga que cambiar.
4.  **No requiere `new` ni `this` (en su forma más simple):** A diferencia de los constructores (funciones constructoras o clases), las funciones fábrica son simplemente funciones regulares, lo que significa que no se requiere el uso de `new` ni hay que preocuparse por el enlace de `this` (a menos que los métodos internos del objeto creado usen `this`).

## Ejemplo Básico de un Método de Fábrica

Consideremos que queremos crear múltiples objetos `usuario` con propiedades como `nombre`, `edad` y un método `saludar`.

### Sin un Método de Fábrica (Repetitivo)

```javascript
const usuario1 = {
    nombre: "Alice",
    edad: 25,
    saludar: function() {
        console.log(`Hola, soy ${this.nombre} y tengo ${this.edad} años.`);
    }
};

const usuario2 = {
    nombre: "Bob",
    edad: 30,
    saludar: function() {
        console.log(`Hola, soy ${this.nombre} y tengo ${this.edad} años.`);
    }
};

usuario1.saludar(); // Salida: Hola, soy Alice y tengo 25 años.
usuario2.saludar(); // Salida: Hola, soy Bob y tengo 30 años.
```

**[Ver ejemplo en vivo](https://playcode.io/2454892)**

Aquí, la lógica de `saludar` se repite para cada objeto.

### Con un Método de Fábrica

```javascript
function crearUsuario(nombre, edad) {
    return {
        nombre: nombre,
        edad: edad,
        saludar: function() {
            console.log(`Hola, soy ${this.nombre} y tengo ${this.edad} años.`);
        }
    };
}

const usuario3 = crearUsuario("Charlie", 28);
const usuario4 = crearUsuario("Diana", 35);

usuario3.saludar(); // Salida: Hola, soy Charlie y tengo 28 años.
usuario4.saludar(); // Salida: Hola, soy Diana y tengo 35 años.
```

**[Ver ejemplo en vivo](https://playcode.io/2454895)**

En este ejemplo, la función `crearUsuario` es nuestro método de fábrica. Centraliza la creación del objeto `usuario`, haciendo el código más DRY (Don't Repeat Yourself).

## Reutilización de Métodos con Fábricas y Clausuras

Si bien el ejemplo anterior es bueno para la creación, los métodos como `saludar` todavía se recrean en cada objeto. Para optimizar esto y usar el poder de las clausuras (closures) o delegación de prototipos, podemos refactorizar.

### Reutilizando Métodos (sin Prototypes, usando Closure)

```javascript
function crearProducto(nombre, precio) {
    // Definimos el método una sola vez
    const getDetalles = function() {
        return `${nombre} - $${precio}`;
    };

    return {
        nombre: nombre,
        precio: precio,
        getDetalles: getDetalles // Asignamos la referencia al método
    };
}

const productoA = crearProducto("Teléfono", 800);
const productoB = crearProducto("Auriculares", 150);

console.log(productoA.getDetalles()); // Salida: Teléfono - $800
console.log(productoB.getDetalles()); // Salida: Auriculares - $150
```

**[Ver ejemplo en vivo](https://playcode.io/2454898)**

Aquí `getDetalles` se define una vez dentro del ámbito de `crearProducto` y se referencia en el objeto devuelto. Sin embargo, cada objeto `producto` tendrá su _propia copia_ de `getDetalles`, aunque la implementación es la misma.

### Combinando Fábricas con la Cadena de Prototipos (Más Eficiente)

Para evitar la duplicación de métodos en cada objeto creado, las fábricas a menudo combinan la creación del objeto con la delegación prototípica.

```javascript
const usuarioMetodos = {
    saludar() {
        console.log(`Hola, soy ${this.nombre} y tengo ${this.edad} años.`);
    },
    obtenerEdadEnMeses() {
        return this.edad * 12;
    }
};

function crearUsuarioOptimo(nombre, edad) {
    // Object.create() crea un nuevo objeto con el prototipo especificado
    const nuevoUsuario = Object.create(usuarioMetodos);
    nuevoUsuario.nombre = nombre;
    nuevoUsuario.edad = edad;
    return nuevoUsuario;
}

const usuario5 = crearUsuarioOptimo("Eve", 22);
const usuario6 = crearUsuarioOptimo("Frank", 40);

usuario5.saludar();             // Salida: Hola, soy Eve y tengo 22 años.
console.log(usuario6.obtenerEdadEnMeses()); // Salida: 480
// Ambos objetos comparten los métodos del prototipo, ahorrando memoria.
console.log(usuario5.saludar === usuario6.saludar); // Salida: true
```

**[Ver ejemplo en vivo](https://playcode.io/2454904)**

Esta es una forma muy potente de usar métodos de fábrica, combinando la flexibilidad de la creación con la eficiencia de la cadena de prototipos. Es el patrón que `new` y las clases de ES6 abstraen y formalizan.

## Casos de Uso Comunes

- **Creación de objetos con configuraciones especificas:** Una fábrica puede tomar parámetros y devolver un objeto configurado de forma diferente (ej. `crearConexion("mysql")`, `crearConexion("mongodb)`).
- **Encapsulación de lógica compleja:** Si la creación de un objeto implica muchos pasos o dependencias, una fábrica puede manejar esa complejidad.
- **Evitar el uso de `new`:** Cuando se prefiere un estilo de programación más funcional o se quiere evitar el acoplamiento a constructores especificos.
- **Patrones de diseño:** Son la base para otros patrones de diseño como el patrón Singleton o el patrón Abstract Factory.

Los métodos de fábrica son una herramienta flexible y poderosa en el arsenal de JavaScript para la creación de objetos, especialmente valiosa cuando se necesita controlar o simplificar el proceso de instanciación.