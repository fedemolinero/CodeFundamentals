El patrón **Decorator** es un patrón de diseño estructural que permite agregar funcionalidades adicionales a un objeto de manera dinámica sin alterar su estructura. Es útil para extender el comportamiento de los objetos en tiempo de ejecución, ofreciendo una forma flexible y extensible de agregar nuevas responsabilidades.



### Conceptos Clave del Patrón Decorator

1. **Extensión Dinámica**: Permite añadir nuevas funcionalidades a un objeto sin modificar su código, a diferencia de la herencia, que requiere cambiar el código de la clase base.

2. **Composición**: Utiliza la composición para añadir funcionalidades en lugar de herencia. Se compone de un objeto base y uno o más decoradores que añaden comportamiento adicional.

3. **Transparencia**: Los decoradores pueden ser aplicados y eliminados en tiempo de ejecución sin que el cliente necesite saber cómo están implementados.




### Componentes del Patrón Decorator

1. **Componente**: Define la interfaz que puede ser extendida por los decoradores. Esta es la interfaz común para los objetos que se pueden decorar.

2. **ConcreteComponent**: Implementa la interfaz del Componente y representa el objeto al que se le pueden añadir funcionalidades.

3. **Decorator**: Implementa la interfaz del Componente y tiene una referencia a un objeto de tipo Componente. Los decoradores usan esta referencia para delegar el trabajo al objeto base.

4. **ConcreteDecorator**: Extiende el Decorator para añadir funcionalidades adicionales a la interfaz del Componente.

### Ejemplo de Implementación en JavaScript

Vamos a ver un ejemplo simple del patrón Decorator usando una clase `Coffee` que puede ser decorada con diferentes tipos de complementos.

**Definir la Interfaz Común**

```javascript
// Componente
class Coffee {
  cost() {
    return 5; // Precio base del café
  }
}
```

**Definir los Decoradores**

```javascript
// Decorador Base
class CoffeeDecorator {
  constructor(coffee) {
    this.coffee = coffee;
  }

  cost() {
    return this.coffee.cost(); // Delegar al objeto base
  }
}

// Decorador Concreto 1
class MilkDecorator extends CoffeeDecorator {
  cost() {
    return this.coffee.cost() + 2; // Añadir costo de la leche
  }
}

// Decorador Concreto 2
class SugarDecorator extends CoffeeDecorator {
  cost() {
    return this.coffee.cost() + 1; // Añadir costo del azúcar
  }
}
```

**Uso del Patrón Decorator**

```javascript
// Crear un café básico
const myCoffee = new Coffee();

// Decorar el café con leche y azúcar
const milkCoffee = new MilkDecorator(myCoffee);
const sweetMilkCoffee = new SugarDecorator(milkCoffee);

console.log(sweetMilkCoffee.cost()); // Output: 8 (5 + 2 + 1)
```

### Explicación del Ejemplo

1. **Componente**:
   - `Coffee` es la clase base que define el costo básico del café.

2. **Decorator**:
   - `CoffeeDecorator` es la clase base para todos los decoradores. Implementa la misma interfaz que `Coffee` y tiene una referencia a un objeto de tipo `Coffee`.

3. **ConcreteDecorator**:
   - `MilkDecorator` y `SugarDecorator` extienden `CoffeeDecorator` para añadir el costo de la leche y el azúcar, respectivamente.

4. **Uso**:
   - Crea un café básico y luego decóralo con leche y azúcar usando los decoradores. Cada decorador añade su costo al costo base del café.

### Aplicaciones Comunes

- **Interfaces de Usuario**: Añadir características a componentes de interfaz de usuario (como bordes, colores o comportamientos adicionales) sin modificar la clase base.
- **Sistemas de Logging**: Añadir funcionalidades adicionales a los sistemas de logging (como enviar logs a diferentes destinos) de manera dinámica.
- **Procesamiento de Datos**: Aplicar diferentes transformaciones o filtros a datos de manera flexible y extensible.

### Ventajas del Patrón Decorator

1. **Extensibilidad**: Permite añadir nuevas funcionalidades sin alterar el código existente.
2. **Flexibilidad**: Los decoradores se pueden aplicar y eliminar de manera dinámica, lo que permite una gran flexibilidad en la configuración del objeto.
3. **Desacoplamiento**: Separa las responsabilidades en diferentes clases decoradoras, promoviendo una mayor modularidad y reutilización.

### Consideraciones

- **Complejidad**: El uso de múltiples decoradores puede aumentar la complejidad del sistema, haciendo que sea más difícil entender cómo se construye el objeto final.
- **Rendimiento**: Aunque el impacto es generalmente mínimo, cada decorador añade una capa adicional de llamada de método, lo que puede afectar el rendimiento en sistemas con muchos decoradores.

En resumen, el patrón Decorator es útil para añadir funcionalidades a un objeto de manera dinámica y flexible sin modificar el código de la clase base, proporcionando una forma modular y extensible de extender el comportamiento de los objetos.