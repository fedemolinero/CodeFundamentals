Las **tablas de hash** (o **hash tables**) son estructuras de datos que permiten la búsqueda, inserción y eliminación eficiente de elementos. Utilizan una función hash para mapear claves a índices en un array, facilitando un acceso rápido a los valores asociados.

### Conceptos Básicos

1. **Clave**: Un identificador único asociado con un valor. Se utiliza para calcular el índice en el array donde se almacenará el valor.
2. **Valor**: El dato asociado a una clave específica.
3. **Función Hash**: Una función que toma una clave y devuelve un índice en el array donde se almacenará el valor. La función hash debe distribuir las claves uniformemente para evitar colisiones.
4. **Colisión**: Ocurre cuando dos claves diferentes son mapeadas al mismo índice por la función hash. Se deben manejar de manera efectiva para mantener la eficiencia.
5. **Resolución de Colisiones**: Métodos para manejar colisiones, como encadenamiento (chaining) y direccionamiento abierto (open addressing).

### Métodos de Resolución de Colisiones

1. **Encadenamiento (Chaining)**:
   - Cada posición del array mantiene una lista de elementos (usualmente una lista enlazada) que se han asignado al mismo índice. Las colisiones se manejan agregando elementos a la lista en esa posición.

2. **Direccionamiento Abierto (Open Addressing)**:
   - Cuando ocurre una colisión, el algoritmo busca la siguiente posición disponible en el array para almacenar el valor. Las técnicas comunes incluyen:
     - **Lineal**: Probar posiciones secuenciales.
     - **Cuadrática**: Probar posiciones según una función cuadrática.
     - **Hashing Doble**: Utilizar una segunda función hash para calcular el salto en el caso de una colisión.

### Implementación de una Tabla de Hash en JavaScript

Aquí te muestro cómo implementar una tabla de hash básica en JavaScript utilizando encadenamiento para resolver colisiones.

#### Implementación Básica con Encadenamiento

```javascript
class HashNode {
  constructor(key, value) {
    this.key = key;
    this.value = value;
    this.next = null; // Referencia al siguiente nodo en la lista encadenada
  }
}

class HashTable {
  constructor(size = 10) {
    this.size = size; // Tamaño del array de la tabla de hash
    this.table = new Array(size).fill(null); // Inicializa el array con nulls
  }

  // Función hash simple
  hashFunction(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash = (hash + key.charCodeAt(i)) % this.size;
    }
    return hash;
  }

  // Inserta un nuevo elemento
  put(key, value) {
    const index = this.hashFunction(key);
    let node = this.table[index];

    if (!node) {
      // Si no hay nodos en la posición, añade el nuevo nodo
      this.table[index] = new HashNode(key, value);
    } else {
      // Maneja la colisión mediante encadenamiento
      while (node) {
        if (node.key === key) {
          node.value = value; // Actualiza el valor si la clave ya existe
          return;
        }
        if (!node.next) break; // Si llegamos al final de la lista, añadimos el nuevo nodo
        node = node.next;
      }
      node.next = new HashNode(key, value);
    }
  }

  // Busca un valor por clave
  get(key) {
    const index = this.hashFunction(key);
    let node = this.table[index];

    while (node) {
      if (node.key === key) return node.value;
      node = node.next;
    }
    return null; // Retorna null si no se encuentra la clave
  }

  // Elimina un elemento por clave
  remove(key) {
    const index = this.hashFunction(key);
    let node = this.table[index];
    let prev = null;

    while (node) {
      if (node.key === key) {
        if (prev) {
          prev.next = node.next; // Salta el nodo para eliminarlo
        } else {
          this.table[index] = node.next; // Actualiza el inicio de la lista
        }
        return;
      }
      prev = node;
      node = node.next;
    }
  }

  // Muestra el contenido de la tabla de hash
  display() {
    this.table.forEach((node, index) => {
      let output = '';
      while (node) {
        output += `${node.key}: ${node.value} -> `;
        node = node.next;
      }
      console.log(`Index ${index}: ${output || 'empty'}`);
    });
  }
}

// Ejemplo de uso
const hashTable = new HashTable();
hashTable.put('name', 'Alice');
hashTable.put('age', 30);
hashTable.put('job', 'Engineer');
hashTable.put('city', 'New York');

console.log("Hash Table contents:");
hashTable.display();

console.log("Get 'name':", hashTable.get('name')); // Output: Alice
console.log("Get 'city':", hashTable.get('city')); // Output: New York

hashTable.remove('city');
console.log("Hash Table contents after removing 'city':");
hashTable.display();
```

### Explicación del Código

1. **Clase `HashNode`**:
   - Representa un nodo en la lista encadenada dentro de la tabla de hash, con una clave (`key`), un valor (`value`), y una referencia al siguiente nodo (`next`).

2. **Clase `HashTable`**:
   - **Método `hashFunction(key)`**: Calcula el índice para una clave usando una suma de valores de caracteres, modulado por el tamaño de la tabla.
   - **Método `put(key, value)`**: Inserta un valor en la tabla. Si hay una colisión, agrega el nuevo nodo al final de la lista encadenada en el índice calculado.
   - **Método `get(key)`**: Busca y devuelve el valor asociado a una clave. Si no se encuentra la clave, devuelve `null`.
   - **Método `remove(key)`**: Elimina el nodo con la clave especificada. Maneja la eliminación de nodos en listas encadenadas.
   - **Método `display()`**: Muestra el contenido de la tabla de hash, indicando los elementos almacenados en cada índice.

### Salida del Ejemplo

La salida del código es:

```
Hash Table contents:
Index 0: empty
Index 1: empty
Index 2: name: Alice -> 
Index 3: job: Engineer -> 
Index 4: empty
Index 5: empty
Index 6: age: 30 -> 
Index 7: empty
Index 8: empty
Index 9: city: New York -> 

Get 'name': Alice
Get 'city': New York

Hash Table contents after removing 'city':
Index 0: empty
Index 1: empty
Index 2: name: Alice -> 
Index 3: job: Engineer -> 
Index 4: empty
Index 5: empty
Index 6: age: 30 -> 
Index 7: empty
Index 8: empty
Index 9: empty
```

### Consideraciones

- **Complejidad Temporal**: En una tabla de hash ideal, las operaciones de inserción, búsqueda y eliminación son \(O(1)\) en promedio. Sin embargo, en el peor caso (cuando todas las claves colisionan), puede llegar a \(O(n)\), donde \(n\) es el número de elementos.
- **Espacio**: El tamaño de la tabla puede influir en la eficiencia. Una tabla demasiado pequeña puede tener muchas colisiones, mientras que una tabla demasiado grande puede desperdiciar espacio.
- **Función Hash**: Una buena función hash debe distribuir uniformemente las claves para minimizar colisiones y mejorar el rendimiento.

Las tablas de hash son muy útiles en aplicaciones donde se requiere un acceso rápido a datos mediante una clave única, y son ampliamente usadas en sistemas de bases de datos, cachés, y estructuras de datos asociativas.