# Literales de Plantilla (Template Literals) en JavaScript

Los Literales de Plantilla, introducidos en ECMAScript 2015 (ES6), son una forma moderna y flexible de trabajar con cadenas de texto en JavaScript. Permiten la interpolación de expresiones, cadenas multilínea y "tagged templates" (plantillas con etiquetas), lo que mejora significativamente la legibilidad y la funcionalidad del código en comparación con las concatenaciones tradicionales.

Se definen utilizando las **comillas invertidas** (backticks): `` ` ``.

## 1. Cadenas Multilínea

Antes de los literales de plantilla, crear cadenas que abarcaban varias líneas requería el uso de caracteres de nueva línea (`\n`) o concatenaciones tediosas. Con los literales de plantilla, simplemente escribes el texto tal cual.

```javascript
// Antes de ES6
const mensajeAntiguo = "Hola,\n" +
                       "este es un mensaje\n" +
                       "multilínea.";
console.log(mensajeAntiguo);
/* Salida:
Hola,
este es un mensaje
multilínea.
*/

// Con Literales de Plantilla (ES6+)
const mensajeNuevo = `
Hola,
este es un mensaje
multilínea con literales de plantilla.
`;
console.log(mensajeNuevo);
/* Salida:

Hola,
este es un mensaje
multilínea con literales de plantilla.
*/
// Nota: Observa que la salida incluye las nuevas líneas iniciales y finales si las pones en el literal.
// Puedes ajustar el formato para evitar el salto de línea inicial si lo deseas:
const mensajeSinSaltoInicial = `Hola,
este es un mensaje
multilínea sin salto inicial.`;
console.log(mensajeSinSaltoInicial);
```

**[Ver ejemplo en vivo](https://playcode.io/2444430)**

## 2. Interpolación de Expresiones

Esta es una de las características más potentes de los literales de plantilla. Permite incrustar cualquier expresión de JavaScript directamente dentro de la cadena, usando la sintaxis `${expresion}`. La expresión será evaluada y su resultado se convertirá a cadena.

```javascript
const nombre = "Carlos";
const edad = 30;
const ciudad = "Madrid";

// Interpolación de variables
const saludo = `Hola, mi nombre es ${nombre} y tengo ${edad} años.`;
console.log(saludo); // Salida: Hola, mi nombre es Carlos y tengo 30 años.

// Interpolación de expresiones matemáticas
const precioUnitario = 15;
const cantidad = 3;
const total = `El total de la compra es: $${precioUnitario * cantidad}.`;
console.log(total); // Salida: El total de la compra es: $45.

// Interpolación de llamadas a funciones
function obtenerSaludo() {
    return "¡Saludos desde ";
}
const mensajeCompleto = `${obtenerSaludo()}${ciudad}!`;
console.log(mensajeCompleto); // Salida: ¡Saludos desde Madrid!

// Interpolación de propiedades de objetos
const usuario = {
    primerNombre: "Ana",
    apellido: "García"
};
const nombreCompletoUsuario = `El nombre completo es: ${usuario.primerNombre} ${usuario.apellido}.`;
console.log(nombreCompletoUsuario); // Salida: El nombre completo es: Ana García.
```

**[Ver ejemplo en vivo](https://playcode.io/2444436)**

## 3. Literales de Plantilla Anidados

Puedes anidar literales de plantilla para crear estructuras de cadena más complejas.

```javascript
const productos = [
    { nombre: "Laptop", precio: 1200 },
    { nombre: "Teclado", precio: 75 }
];

const listaHTML = `
<ul>
    ${productos.map(producto => `
    <li>
        <strong>${producto.nombre}</strong>: $${producto.precio}
    </li>
    `).join('')}
</ul>
`;
console.log(listaHTML);
/* Salida:
<ul>

    <li>
        <strong>Laptop</strong>: $1200
    </li>

    <li>
        <strong>Teclado</strong>: $75
    </li>

</ul>
*/
// Nota: El .join('') es crucial para eliminar la coma por defecto que map() añade al convertir un arreglo a cadena.
```

**[Ver ejemplo en vivo](https://playcode.io/2444437)**

## 4. (Avanzado) Tagged Templates (Plantillas con Etiquetas)

Las plantillas con etiquetas son una característica avanzada que permite procesar literales de plantilla con una función. La función "tag" recibe el literal de plantilla desglosado (las cadenas estáticas y los valores interpolados) y puede manipularlos o transformarlos antes de devolver la cadena final.

```javascript
function highlight(strings, ...values) {
    let str = '';
    strings.forEach((string, i) => {
        str += string;
        if (i < values.length) {
            str += `<mark>${values[i]}</mark>`; // Envuelve el valor interpolado en una etiqueta <mark>
        }
    });
    return str;
}

const nombre = "Juan";
const edad = 25;

const mensajeResaltado = highlight`Hola, ${nombre} tiene ${edad} años.`;
console.log(mensajeResaltado);
// Salida: "Hola, <mark>Juan</mark> tiene <mark>25</mark> años."
```

**[Ver ejemplo en vivo](https://playcode.io/2444439)**

Este concepto es más avanzado y se usa para casos como:

- **Sanitización de HTML:** Para prevenir ataques XSS.
- **Internacionalización (i18n):** Para manejar plurales o formatos específicos de idioma.
- **CSS-in-JS:** Para escribir estilos CSS directamente en JavaScript.

Los literales de plantilla son una adición poderosa a JavaScript que simplifica la manipulación de cadenas y las hace más legibles, especialmente en escenarios donde se necesita combinar texto estático con datos dinámicos.