Un **heap** (o **montículo**) es una estructura de datos de árbol que satisface la propiedad de heap, que asegura que el valor en cada nodo cumple con un orden específico con respecto a sus hijos. Los heaps se utilizan comúnmente en algoritmos de prioridad, como los heaps de prioridad y los algoritmos de ordenamiento, como el **heapsort**.

### Tipos de Heaps

1. **Heap Máximo (Max-Heap)**:
   - En un max-heap, el valor en cada nodo es mayor o igual que los valores de sus hijos. Por lo tanto, el nodo raíz contiene el valor máximo.

2. **Heap Mínimo (Min-Heap)**:
   - En un min-heap, el valor en cada nodo es menor o igual que los valores de sus hijos. Por lo tanto, el nodo raíz contiene el valor mínimo.

### Propiedades de un Heap

1. **Propiedad de Heap**:
   - **Heap Máximo**: Para cada nodo \(i\), el valor de \(i\) es mayor o igual que el valor de sus hijos.
   - **Heap Mínimo**: Para cada nodo \(i\), el valor de \(i\) es menor o igual que el valor de sus hijos.

2. **Propiedad de Completo**:
   - Un heap es un árbol binario completo, lo que significa que todos los niveles del árbol están completamente llenos, excepto posiblemente el último nivel, que está lleno de izquierda a derecha.

### Operaciones en un Heap

1. **Inserción**:
   - Se añade un nuevo elemento al final del árbol (al final del último nivel). Luego, se realiza una operación de "heapify up" para asegurar que la propiedad de heap se mantenga.

2. **Extracción del Máximo/Mínimo**:
   - En un max-heap, se elimina el nodo raíz, que contiene el valor máximo. Se reemplaza con el último elemento del árbol y se realiza una operación de "heapify down" para restaurar la propiedad de heap.
   - En un min-heap, se elimina el nodo raíz, que contiene el valor mínimo, y se realiza una operación similar.

3. **Heapify**:
   - **Heapify Up (o Bubble Up)**: Usado después de la inserción para mantener la propiedad de heap.
   - **Heapify Down (o Bubble Down)**: Usado después de la extracción para mantener la propiedad de heap.

### Implementación de un Heap en JavaScript

Aquí te muestro cómo implementar un heap mínimo en JavaScript. La implementación incluye operaciones básicas como inserción, extracción del mínimo y heapify.

#### Implementación de un Min-Heap

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  // Método para obtener el índice del padre
  getParentIndex(index) {
    return Math.floor((index - 1) / 2);
  }

  // Método para obtener el índice del hijo izquierdo
  getLeftChildIndex(index) {
    return 2 * index + 1;
  }

  // Método para obtener el índice del hijo derecho
  getRightChildIndex(index) {
    return 2 * index + 2;
  }

  // Método para intercambiar dos elementos en el heap
  swap(index1, index2) {
    const temp = this.heap[index1];
    this.heap[index1] = this.heap[index2];
    this.heap[index2] = temp;
  }

  // Método para "heapificar" hacia arriba
  heapifyUp(index) {
    const parentIndex = this.getParentIndex(index);
    if (index > 0 && this.heap[index] < this.heap[parentIndex]) {
      this.swap(index, parentIndex);
      this.heapifyUp(parentIndex);
    }
  }

  // Método para "heapificar" hacia abajo
  heapifyDown(index) {
    const leftChildIndex = this.getLeftChildIndex(index);
    const rightChildIndex = this.getRightChildIndex(index);
    let smallest = index;

    if (leftChildIndex < this.heap.length && this.heap[leftChildIndex] < this.heap[smallest]) {
      smallest = leftChildIndex;
    }

    if (rightChildIndex < this.heap.length && this.heap[rightChildIndex] < this.heap[smallest]) {
      smallest = rightChildIndex;
    }

    if (smallest !== index) {
      this.swap(index, smallest);
      this.heapifyDown(smallest);
    }
  }

  // Método para insertar un nuevo elemento en el heap
  insert(value) {
    this.heap.push(value);
    this.heapifyUp(this.heap.length - 1);
  }

  // Método para extraer el mínimo valor del heap
  extractMin() {
    if (this.heap.length === 0) {
      throw new Error("Heap is empty");
    }
    const min = this.heap[0];
    const end = this.heap.pop();
    if (this.heap.length > 0) {
      this.heap[0] = end;
      this.heapifyDown(0);
    }
    return min;
  }

  // Método para ver el mínimo valor del heap sin extraerlo
  peek() {
    if (this.heap.length === 0) {
      throw new Error("Heap is empty");
    }
    return this.heap[0];
  }

  // Método para mostrar el contenido del heap
  display() {
    console.log(this.heap);
  }
}

// Ejemplo de uso
const minHeap = new MinHeap();
minHeap.insert(10);
minHeap.insert(5);
minHeap.insert(20);
minHeap.insert(1);

console.log("Heap contents:");
minHeap.display();

console.log("Extracted min:", minHeap.extractMin());
console.log("Heap contents after extraction:");
minHeap.display();
```

### Explicación del Código

1. **Clase `MinHeap`**:
   - **Métodos `getParentIndex(index)`, `getLeftChildIndex(index)`, `getRightChildIndex(index)`**: Calculan los índices del padre y los hijos en el heap.
   - **Método `swap(index1, index2)`**: Intercambia dos elementos en el heap.
   - **Método `heapifyUp(index)`**: Mantiene la propiedad del heap después de una inserción.
   - **Método `heapifyDown(index)`**: Mantiene la propiedad del heap después de una extracción.
   - **Método `insert(value)`**: Inserta un nuevo valor en el heap y lo ajusta para mantener la propiedad.
   - **Método `extractMin()`**: Extrae el valor mínimo del heap, reemplaza la raíz con el último valor y ajusta el heap.
   - **Método `peek()`**: Devuelve el valor mínimo sin extraerlo.
   - **Método `display()`**: Muestra el contenido del heap.

### Salida del Ejemplo

La salida del código es:

```
Heap contents:
[1, 5, 20, 10]
Extracted min: 1
Heap contents after extraction:
[5, 10, 20]
```

### Aplicaciones de los Heaps

1. **Heapsort**: Un algoritmo de ordenamiento basado en heaps que convierte un array en un heap y luego extrae los elementos del heap para ordenarlos.
2. **Algoritmo de Dijkstra**: Utiliza un heap de prioridad para encontrar el camino más corto en un grafo ponderado.
3. **Colas de Prioridad**: Los heaps se utilizan para implementar colas de prioridad eficientes, donde los elementos se pueden insertar y extraer de acuerdo con su prioridad.

Los heaps son una herramienta esencial en la programación y la teoría de algoritmos, proporcionando una forma eficiente de gestionar y acceder a datos en muchas aplicaciones.
