<!-- Una lista enlazada doble (doubly linked list) es una estructura de datos donde cada nodo tiene dos referencias: una al nodo siguiente y otra al nodo anterior. Esto permite una navegación bidireccional a través de la lista, facilitando operaciones de inserción y eliminación en ambos extremos de la lista. -->

<!-- A continuación, te muestro una implementación básica de una lista enlazada doble en JavaScript, incluyendo operaciones para insertar al inicio, insertar al final, eliminar un nodo y mostrar la lista. -->

### Implementación de una Lista Enlazada Doble en JavaScript

```javascript
class Nodo {
  constructor(valor = null) {
    this.valor = valor;
    this.siguiente = null;
    this.anterior = null;
  }
}

class ListaEnlazadaDoble {
  constructor() {
    this.cabeza = null;
    this.cola = null;
  }

  insertarAlInicio(valor) {
    const nuevoNodo = new Nodo(valor);
    if (this.cabeza === null) {
      this.cabeza = nuevoNodo;
      this.cola = nuevoNodo;
    } else {
      nuevoNodo.siguiente = this.cabeza;
      this.cabeza.anterior = nuevoNodo;
      this.cabeza = nuevoNodo;
    }
  }

  insertarAlFinal(valor) {
    const nuevoNodo = new Nodo(valor);
    if (this.cola === null) {
      this.cabeza = nuevoNodo;
      this.cola = nuevoNodo;
    } else {
      nuevoNodo.anterior = this.cola;
      this.cola.siguiente = nuevoNodo;
      this.cola = nuevoNodo;
    }
  }

  eliminar(valor) {
    if (this.cabeza === null) return;

    // Si el nodo a eliminar es la cabeza
    if (this.cabeza.valor === valor) {
      this.cabeza = this.cabeza.siguiente;
      if (this.cabeza !== null) {
        this.cabeza.anterior = null;
      } else {
        this.cola = null;
      }
      return;
    }

    let nodoActual = this.cabeza;
    while (nodoActual !== null && nodoActual.valor !== valor) {
      nodoActual = nodoActual.siguiente;
    }

    if (nodoActual === null) return;

    if (nodoActual.siguiente !== null) {
      nodoActual.siguiente.anterior = nodoActual.anterior;
    } else {
      this.cola = nodoActual.anterior;
    }

    if (nodoActual.anterior !== null) {
      nodoActual.anterior.siguiente = nodoActual.siguiente;
    }
  }

  mostrar() {
    let nodoActual = this.cabeza;
    let salida = '';
    while (nodoActual !== null) {
      salida += nodoActual.valor + ' <-> ';
      nodoActual = nodoActual.siguiente;
    }
    salida += 'null';
    console.log(salida);
  }
}

// Ejemplo de uso
const listaDoble = new ListaEnlazadaDoble();
listaDoble.insertarAlInicio(3);
listaDoble.insertarAlInicio(2);
listaDoble.insertarAlFinal(4);
listaDoble.insertarAlFinal(5);

console.log("Lista después de inserciones:");
listaDoble.mostrar();

listaDoble.eliminar(3);
console.log("Lista después de eliminar el valor 3:");
listaDoble.mostrar();
```

### Explicación del Código

1. **Clase Nodo**:
   - Define un nodo en la lista enlazada doble. Cada nodo tiene un valor (`valor`), una referencia al siguiente nodo (`siguiente`), y una referencia al nodo anterior (`anterior`).

2. **Clase ListaEnlazadaDoble**:
   - **Método `insertarAlInicio(valor)`**: Inserta un nuevo nodo con el valor dado al inicio de la lista. Actualiza las referencias para asegurarse de que el nuevo nodo se convierte en la nueva cabeza de la lista.
   - **Método `insertarAlFinal(valor)`**: Inserta un nuevo nodo con el valor dado al final de la lista. Actualiza las referencias para asegurarse de que el nuevo nodo se convierte en la nueva cola de la lista.
   - **Método `eliminar(valor)`**: Elimina el primer nodo que tiene el valor dado. Actualiza las referencias de los nodos adyacentes para mantener la integridad de la lista.
   - **Método `mostrar()`**: Recorre la lista desde la cabeza y construye una cadena que muestra los valores de cada nodo, con flechas que indican la conexión entre nodos. Al final, agrega "null" para indicar el final de la lista.

### Salida del Ejemplo

Al ejecutar el ejemplo proporcionado, la salida será:

```
Lista después de inserciones:
2 <-> 3 <-> 4 <-> 5 <-> null
Lista después de eliminar el valor 3:
2 <-> 4 <-> 5 <-> null
```

Esta implementación en JavaScript demuestra cómo gestionar una lista enlazada doble, permitiendo una navegación bidireccional y facilitando la inserción y eliminación de nodos en ambas direcciones.
