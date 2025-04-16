
#### ejemplos de uso en javascript de una lista single linked list

class Nodo {
  constructor(valor = null) {
    this.valor = valor;
    this.siguiente = null;
  }
}

class ListaEnlazada {
  constructor() {
    this.cabeza = null;
  }

  insertarAlInicio(valor) {
    const nuevoNodo = new Nodo(valor);
    nuevoNodo.siguiente = this.cabeza;
    this.cabeza = nuevoNodo;
  }

  insertarAlFinal(valor) {
    const nuevoNodo = new Nodo(valor);
    if (this.cabeza === null) {
      this.cabeza = nuevoNodo;
      return;
    }
    let nodoActual = this.cabeza;
    while (nodoActual.siguiente !== null) {
      nodoActual = nodoActual.siguiente;
    }
    nodoActual.siguiente = nuevoNodo;
  }

  eliminar(valor) {
    if (this.cabeza === null) return;

    if (this.cabeza.valor === valor) {
      this.cabeza = this.cabeza.siguiente;
      return;
    }

    let nodoActual = this.cabeza;
    while (nodoActual.siguiente !== null && nodoActual.siguiente.valor !== valor) {
      nodoActual = nodoActual.siguiente;
    }

    if (nodoActual.siguiente !== null) {
      nodoActual.siguiente = nodoActual.siguiente.siguiente;
    }
  }

  mostrar() {
    let nodoActual = this.cabeza;
    let salida = '';
    while (nodoActual !== null) {
      salida += nodoActual.valor + ' -> ';
      nodoActual = nodoActual.siguiente;
    }
    salida += 'null';
    console.log(salida);
  }
}

// Ejemplo de uso
const lista = new ListaEnlazada();
lista.insertarAlInicio(3);
lista.insertarAlInicio(2);
lista.insertarAlFinal(4);
lista.insertarAlFinal(5);

console.log("Lista después de inserciones:");
lista.mostrar();

lista.eliminar(3);
console.log("Lista después de eliminar el valor 3:");
lista.mostrar();

