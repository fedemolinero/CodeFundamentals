Las **pilas** (o **stacks** en inglés) son una estructura de datos que sigue el principio LIFO (Last In, First Out), es decir, el último elemento en entrar es el primero en salir. Esta estructura es útil en situaciones donde se necesita mantener un seguimiento del último elemento añadido o para realizar operaciones que requieren "deshacer" acciones en orden inverso a cómo fueron realizadas.

### Operaciones Básicas en una Pila

1. **Push**: Añadir un elemento al tope de la pila.
2. **Pop**: Eliminar y devolver el elemento del tope de la pila.
3. **Peek**: Ver el elemento en el tope de la pila sin eliminarlo.
4. **IsEmpty**: Comprobar si la pila está vacía.

### Implementación de una Pila en JavaScript

Aquí te muestro una implementación básica de una pila utilizando un array y una implementación utilizando una lista enlazada.

#### Implementación de una Pila usando un Array

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(element) {
    this.items.push(element);
  }

  pop() {
    if (this.isEmpty()) {
      throw new Error('Stack is empty');
    }
    return this.items.pop(); // Elimina el último elemento
  }

  peek() {
    if (this.isEmpty()) {
      throw new Error('Stack is empty');
    }
    return this.items[this.items.length - 1]; // Devuelve el último elemento
  }

  isEmpty() {
    return this.items.length === 0;
  }

  getSize() {
    return this.items.length;
  }

  display() {
    console.log(this.items.join(' <- '));
  }
}

// Ejemplo de uso
const stack = new Stack();
stack.push(1);
stack.push(2);
stack.push(3);

console.log("Stack contents:");
stack.display(); // Output: 1 <- 2 <- 3

console.log("Top element:", stack.peek()); // Output: 3

console.log("Popped element:", stack.pop()); // Output: 3
console.log("Stack contents after pop:");
stack.display(); // Output: 1 <- 2

console.log("Is the stack empty?", stack.isEmpty()); // Output: false
console.log("Stack size:", stack.getSize()); // Output: 2
```

#### Implementación de una Pila usando una Lista Enlazada

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.top = null; // El nodo en el tope de la pila
    this.size = 0;
  }

  push(value) {
    const newNode = new Node(value);
    newNode.next = this.top;
    this.top = newNode;
    this.size++;
  }

  pop() {
    if (this.isEmpty()) {
      throw new Error('Stack is empty');
    }
    const value = this.top.value;
    this.top = this.top.next;
    this.size--;
    return value;
  }

  peek() {
    if (this.isEmpty()) {
      throw new Error('Stack is empty');
    }
    return this.top.value;
  }

  isEmpty() {
    return this.top === null;
  }

  getSize() {
    return this.size;
  }

  display() {
    let current = this.top;
    let output = '';
    while (current !== null) {
      output += current.value + ' -> ';
      current = current.next;
    }
    output += 'null';
    console.log(output);
  }
}

// Ejemplo de uso
const stack = new Stack();
stack.push(1);
stack.push(2);
stack.push(3);

console.log("Stack contents:");
stack.display(); // Output: 3 -> 2 -> 1 -> null

console.log("Top element:", stack.peek()); // Output: 3

console.log("Popped element:", stack.pop()); // Output: 3
console.log("Stack contents after pop:");
stack.display(); // Output: 2 -> 1 -> null

console.log("Is the stack empty?", stack.isEmpty()); // Output: false
console.log("Stack size:", stack.getSize()); // Output: 2
```

### Explicación del Código

1. **Clase `Node`** (para la implementación con lista enlazada):
   - Define un nodo para la lista enlazada, con un valor (`value`) y una referencia al siguiente nodo (`next`).

2. **Clase `Stack`**:
   - **Método `push(value)`**: Añade un nuevo nodo al tope de la pila. En la implementación con un array, utiliza `push` del array. En la implementación con lista enlazada, el nuevo nodo apunta al nodo actual en el tope.
   - **Método `pop()`**: Elimina y devuelve el valor del nodo en el tope de la pila. En la implementación con un array, utiliza `pop` del array. En la implementación con lista enlazada, actualiza el tope a lo que estaba justo debajo del tope actual.
   - **Método `peek()`**: Devuelve el valor del nodo en el tope de la pila sin eliminarlo. En la implementación con un array, accede al último elemento. En la implementación con lista enlazada, accede al valor del nodo en el tope.
   - **Método `isEmpty()`**: Comprueba si la pila está vacía. En la implementación con un array, verifica la longitud del array. En la implementación con lista enlazada, verifica si el tope es `null`.
   - **Método `getSize()`**: Devuelve el número de elementos en la pila. En la implementación con un array, es la longitud del array. En la implementación con lista enlazada, es un contador de tamaño.
   - **Método `display()`**: Muestra el contenido de la pila en la consola. En la implementación con un array, utiliza `join` para construir una cadena. En la implementación con lista enlazada, recorre la lista y construye una cadena.

### Salida de los Ejemplos

Para ambas implementaciones, la salida de ejemplo será similar:

```
Stack contents:
1 <- 2 <- 3
Top element: 3
Popped element: 3
Stack contents after pop:
1 <- 2
Is the stack empty? false
Stack size: 2
```

y para la implementación con lista enlazada:

```
Stack contents:
3 -> 2 -> 1 -> null
Top element: 3
Popped element: 3
Stack contents after pop:
2 -> 1 -> null
Is the stack empty? false
Stack size: 2
```

Estas implementaciones demuestran cómo gestionar una pila en JavaScript, utilizando tanto un array como una lista enlazada para representar la estructura de datos de manera eficaz.
