Una lista enlazada circular es una estructura de datos en la que el último nodo apunta de nuevo al primer nodo, formando un ciclo. Esta estructura permite iterar sobre los elementos de la lista de manera continua sin necesidad de verificar un final explícito.

A continuación, te muestro una implementación básica de una lista enlazada circular en JavaScript. Incluye operaciones para insertar al inicio, insertar al final, eliminar un nodo y mostrar la lista.

### Implementación de una Lista Enlazada Circular en JavaScript

```javascript
class Nodo {
  constructor(valor = null) {
    this.valor = valor;
    this.siguiente = null;
  }
}

class ListaEnlazadaCircular {
  constructor() {
    this.cabeza = null;
  }

  insertarAlInicio(valor) {
    const nuevoNodo = new Nodo(valor);
    
    if (this.cabeza === null) {
      this.cabeza = nuevoNodo;
      nuevoNodo.siguiente = nuevoNodo; // Circular
    
    } else {

      nuevoNodo.siguiente = this.cabeza;
      let nodoActual = this.cabeza;
      while (nodoActual.siguiente !== this.cabeza) {
        nodoActual = nodoActual.siguiente;
    
    }
      nodoActual.siguiente = nuevoNodo;
      this.cabeza = nuevoNodo;
    }
  }

  insertarAlFinal(valor) {
    const nuevoNodo = new Nodo(valor);
    if (this.cabeza === null) {
      this.cabeza = nuevoNodo;
      nuevoNodo.siguiente = nuevoNodo; // Circular
    } else {
      let nodoActual = this.cabeza;
      while (nodoActual.siguiente !== this.cabeza) {
        nodoActual = nodoActual.siguiente;
      }
      nodoActual.siguiente = nuevoNodo;
      nuevoNodo.siguiente = this.cabeza;
    }
  }

  eliminar(valor) {
    if (this.cabeza === null) return;

    let nodoActual = this.cabeza;
    let nodoAnterior = null;

    // Caso especial: eliminar la cabeza
    if (nodoActual.valor === valor) {
      if (nodoActual.siguiente === this.cabeza) {
        this.cabeza = null; // Lista vacía
      } else {
        nodoAnterior = this.cabeza;
        while (nodoAnterior.siguiente !== this.cabeza) {
          nodoAnterior = nodoAnterior.siguiente;
        }
        this.cabeza = nodoActual.siguiente;
        nodoAnterior.siguiente = this.cabeza;
      }
      return;
    }

    // Buscar el nodo a eliminar
    while (nodoActual.siguiente !== this.cabeza && nodoActual.siguiente.valor !== valor) {
      nodoActual = nodoActual.siguiente;
    }

    if (nodoActual.siguiente.valor === valor) {
      nodoActual.siguiente = nodoActual.siguiente.siguiente;
    }
  }

  mostrar() {
    if (this.cabeza === null) {
      console.log("Lista vacía");
      return;
    }

    let nodoActual = this.cabeza;
    let salida = '';
    do {
      salida += nodoActual.valor + ' -> ';
      nodoActual = nodoActual.siguiente;
    } while (nodoActual !== this.cabeza);
    salida += '(ciclo)';
    console.log(salida);
  }
}

// Ejemplo de uso
const listaCircular = new ListaEnlazadaCircular();
listaCircular.insertarAlInicio(3);
listaCircular.insertarAlInicio(2);
listaCircular.insertarAlFinal(4);
listaCircular.insertarAlFinal(5);

console.log("Lista después de inserciones:");
listaCircular.mostrar();

listaCircular.eliminar(3);
console.log("Lista después de eliminar el valor 3:");
listaCircular.mostrar();
```

### Explicación del Código

1. **Clase Nodo**:
   - Define un nodo en la lista enlazada circular. Cada nodo tiene un valor (`valor`) y una referencia al siguiente nodo (`siguiente`).

2. **Clase ListaEnlazadaCircular**:
   - **Método `insertarAlInicio(valor)`**: Inserta un nuevo nodo con el valor dado al inicio de la lista. Si la lista está vacía, el nuevo nodo se convierte en la cabeza y se apunta a sí mismo. De lo contrario, el nuevo nodo se convierte en la nueva cabeza y el último nodo en la lista se ajusta para apuntar al nuevo nodo.
   - **Método `insertarAlFinal(valor)`**: Inserta un nuevo nodo con el valor dado al final de la lista. Si la lista está vacía, el nuevo nodo se convierte en la cabeza y se apunta a sí mismo. De lo contrario, recorre la lista hasta el final y actualiza las referencias para mantener el ciclo.
   - **Método `eliminar(valor)`**: Elimina el primer nodo que tiene el valor dado. Maneja el caso especial en el que el nodo a eliminar es la cabeza y ajusta las referencias de los nodos adyacentes para mantener el ciclo.
   - **Método `mostrar()`**: Recorre la lista desde la cabeza y construye una cadena que muestra los valores de cada nodo, con flechas que indican la conexión entre nodos. Al final, indica que la lista es circular.

### Salida del Ejemplo

Al ejecutar el ejemplo proporcionado, la salida será:

```
Lista después de inserciones:
2 -> 3 -> 4 -> 5 -> (ciclo)
Lista después de eliminar el valor 3:
2 -> 4 -> 5 -> (ciclo)
```

Esta implementación muestra cómo gestionar una lista enlazada circular en JavaScript, permitiendo una navegación continua y facilitando la inserción y eliminación de nodos en cualquier parte de la lista.
