# JAVASCRIPT

JavaScript es un lenguaje de programación fundamental para el desarrollo web, que permite añadir interactividad y dinamismo a las páginas web. Algunos aspectos clave de JavaScript, incluyendo manipulación del DOM, gestión de eventos y solicitudes asíncronas.

## 1. **Manipulación del DOM (Document Object Model)**

El DOM es una representación estructural del contenido de una página web. JavaScript permite acceder y manipular estos elementos dinámicamente.

- **Seleccionar Elementos**:
  - `document.getElementById(id)`: Selecciona un elemento por su ID.
  - `document.getElementsByClassName(className)`: Selecciona elementos por su nombre de clase.
  - `document.getElementsByTagName(tagName)`: Selecciona elementos por su nombre de etiqueta.
  - `document.querySelector(selector)`: Selecciona el primer elemento que coincide con el selector CSS.
  - `document.querySelectorAll(selector)`: Selecciona todos los elementos que coinciden con el selector CSS.

  **Ejemplo**:

  ```javascript
  const element = document.querySelector('.my-class');
  ```

- **Modificar Elementos**:
  - `element.textContent`: Cambia el texto de un elemento.
  - `element.innerHTML`: Cambia el contenido HTML de un elemento.
  - `element.style.property`: Modifica el estilo en línea de un elemento.

  **Ejemplo**:
  
  ```javascript
  const element = document.querySelector('#my-element');
  element.textContent = 'Nuevo texto';
  element.style.color = 'blue';
  ```

- **Crear y Eliminar Elementos**:
  - `document.createElement(tagName)`: Crea un nuevo elemento.
  - `parentElement.appendChild(childElement)`: Añade un nuevo hijo a un elemento.
  - `parentElement.removeChild(childElement)`: Elimina un hijo de un elemento.

  **Ejemplo**:
  
  ```javascript
  const newElement = document.createElement('div');
  newElement.textContent = 'Hola, Mundo!';
  document.body.appendChild(newElement);
  ```

## 2. **Gestión de Eventos**

JavaScript permite responder a acciones del usuario, como clics, movimientos del ratón, y teclas presionadas, a través de eventos.

- **Añadir Event Listeners**:
  - `element.addEventListener(event, callback)`: Asocia un evento con una función que se ejecuta cuando el evento ocurre.

  **Ejemplo**:

 ```javascript
  const button = document.querySelector('#my-button');
  button.addEventListener('click', function() {
    alert('¡Botón clickeado!');
  });
  ```

- **Eventos Comunes**:
  - `click`: Se dispara cuando un elemento es clickeado.
  - `submit`: Se dispara cuando se envía un formulario.
  - `mouseover`: Se dispara cuando el ratón pasa sobre un elemento.
  - `keydown`: Se dispara cuando se presiona una tecla.

## 3. **Solicitudes Asíncronas (AJAX)**

AJAX (Asynchronous JavaScript and XML) permite realizar solicitudes al servidor y actualizar partes de la página web sin necesidad de recargarla.

- **`XMLHttpRequest`**:
  - Se usa para hacer solicitudes HTTP asíncronas. Aunque es más antiguo y está siendo reemplazado por `fetch`, sigue siendo relevante.

  **Ejemplo**:

  ```javascript
  const xhr = new XMLHttpRequest();
  xhr.open('GET', 'https://api.example.com/data', true);
  xhr.onload = function() {
    if (xhr.status >= 200 && xhr.status < 300) {
      console.log(xhr.responseText);
    }
  };
  xhr.send();
  ```

- **`fetch` API**:
  - Ofrece una interfaz más moderna y basada en promesas para realizar solicitudes HTTP.

  **Ejemplo**:

  ```javascript
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  ```

## 4. **Funciones y Objetos**

- **Funciones**:
  - JavaScript utiliza funciones para agrupar código y realizar tareas específicas.
  Las funciones pueden ser declaradas de manera tradicional o como funciones de flecha.

  **Ejemplo**:

  ```javascript
  function greet(name) {
    return `Hola, ${name}!`;
  }

  const greet = (name) => `Hola, ${name}!`;
  ```

- **Objetos**:
  - Los objetos en JavaScript permiten agrupar datos y funciones en una sola estructura.

  **Ejemplo**:

  ```javascript
  const person = {
    name: 'Juan',
    age: 30,
    greet() {
      return `Hola, mi nombre es ${this.name}`;
    }
  };
  ```

## 5. **Programación Asíncrona**

- **Promesas**:
  - Las promesas representan el resultado eventual de una operación asíncrona. Permiten manejar el resultado cuando se resuelve o se rechaza.

  **Ejemplo**:

  ```javascript
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('¡Éxito!');
    }, 1000);
  });

  promise.then(result => console.log(result));
  ```

- **`async` y `await`**:
  - Permiten escribir código asíncrono de manera más sencilla, haciendo que las promesas se comporten como si fueran operaciones síncronas.

  **Ejemplo**:

  ```javascript
  async function fetchData() {
    try {
      const response = await fetch('https://api.example.com/data');
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error('Error:', error);
    }
  }

  fetchData();
  ```

### 6. **Manipulación de Datos y Funciones Avanzadas**

- **Array Methods**: JavaScript ofrece métodos avanzados para trabajar con arrays, como `map`, `filter`, `reduce`, entre otros.

  **Ejemplo**:

  ```javascript
  const numbers = [1, 2, 3, 4];
  const doubled = numbers.map(n => n * 2);
  ```

- **Desestructuración**: Permite extraer valores de arrays y objetos en variables individuales.

  **Ejemplo**:

  ```javascript
  const [first, second] = [1, 2];
  const {name, age} = {name: 'Ana', age: 25};
  ```

### 7. **DOM Virtual y Renderizado**

- **DOM Virtual**:
  - Utilizado en bibliotecas y frameworks como React para optimizar el proceso de renderizado. En lugar de manipular directamente el DOM, se crea un DOM virtual para calcular las diferencias y actualizar el DOM real de manera eficiente.

### 8. **Herramientas y Frameworks**

- **Frameworks y Bibliotecas**: JavaScript cuenta con diversas bibliotecas y frameworks como React, Angular, y Vue.js, que facilitan el desarrollo de aplicaciones web modernas y complejas.

  - **React**: Biblioteca para construir interfaces de usuario basadas en componentes.
  - **Angular**: Framework completo para el desarrollo de aplicaciones web.
  - **Vue.js**: Framework progresivo que es fácil de integrar y usar para construir interfaces interactivas.

En resumen, JavaScript es una herramienta poderosa y versátil que añade interactividad y dinamismo a las páginas web. Permite manipular el DOM, gestionar eventos, realizar solicitudes asíncronas y mucho más, facilitando la creación de experiencias web ricas y dinámicas.