El patrón **Factory** es un patrón de diseño creacional que proporciona una interfaz para crear objetos en una clase base, pero permite que las subclases alteren el tipo de objetos que se crean. En lugar de instanciar un objeto directamente, se utiliza una fábrica para gestionar la creación de instancias. Esto es útil cuando el tipo exacto del objeto a crear no se conoce hasta el momento de ejecución o cuando la creación de objetos puede ser compleja.

### Características del Patrón Factory

1. **Encapsulación de la Creación**: La lógica de creación de objetos está encapsulada en una fábrica, lo que ayuda a desacoplar el código cliente de las clases concretas de los objetos que necesita.

2. **Flexibilidad**: Permite crear diferentes tipos de objetos a partir de una interfaz común sin conocer la clase concreta de los objetos que se van a crear.

3. **Simplicidad**: Facilita la adición de nuevos tipos de objetos sin modificar el código cliente que usa la fábrica.

### Tipos de Factory

1. **Simple Factory**: Un método que devuelve instancias de diferentes clases basadas en parámetros proporcionados. A veces, se le denomina "Método de Fábrica".

2. **Factory Method**: Un patrón en el que una clase define un método para crear objetos, pero deja a las subclases la implementación del método de creación.

3. **Abstract Factory**: Un patrón que proporciona una interfaz para crear familias de objetos relacionados sin especificar sus clases concretas.

### Ejemplo de Implementación

Vamos a ver un ejemplo de cada tipo de patrón Factory en JavaScript.

#### **1. Simple Factory**

En el Simple Factory, una clase o función se encarga de la creación de instancias.

```javascript
class Car {
  constructor(model) {
    this.model = model;
  }
  drive() {
    console.log(`Driving a ${this.model}`);
  }
}

class Bike {
  constructor(model) {
    this.model = model;
  }
  ride() {
    console.log(`Riding a ${this.model}`);
  }
}

class VehicleFactory {
  static createVehicle(type, model) {
    switch (type) {
      case 'car':
        return new Car(model);
      case 'bike':
        return new Bike(model);
      default:
        throw new Error('Invalid vehicle type');
    }
  }
}

// Uso
const car = VehicleFactory.createVehicle('car', 'Toyota');
car.drive(); // Output: Driving a Toyota

const bike = VehicleFactory.createVehicle('bike', 'Yamaha');
bike.ride(); // Output: Riding a Yamaha
```

#### **2. Factory Method**

En el Factory Method, una clase base define el método de creación, y las subclases lo implementan.

```javascript
// Clase abstracta
class Document {
  create() {
    throw new Error('This method should be overridden!');
  }
}

// Subclases concretas
class PDFDocument extends Document {
  create() {
    console.log('Creating a PDF document');
  }
}

class WordDocument extends Document {
  create() {
    console.log('Creating a Word document');
  }
}

// Fábrica abstracta
class DocumentFactory {
  createDocument(type) {
    throw new Error('This method should be overridden!');
  }
}

// Fábrica concreta
class ConcreteDocumentFactory extends DocumentFactory {
  createDocument(type) {
    switch (type) {
      case 'pdf':
        return new PDFDocument();
      case 'word':
        return new WordDocument();
      default:
        throw new Error('Invalid document type');
    }
  }
}

// Uso
const factory = new ConcreteDocumentFactory();
const pdfDoc = factory.createDocument('pdf');
pdfDoc.create(); // Output: Creating a PDF document

const wordDoc = factory.createDocument('word');
wordDoc.create(); // Output: Creating a Word document
```

#### **3. Abstract Factory**

En el Abstract Factory, se proporciona una interfaz para crear familias de objetos relacionados.

```javascript
// Interfaces de productos
class Chair {
  sit() {
    throw new Error('This method should be overridden!');
  }
}

class Sofa {
  lie() {
    throw new Error('This method should be overridden!');
  }
}

// Implementaciones concretas
class VictorianChair extends Chair {
  sit() {
    console.log('Sitting on a Victorian chair');
  }
}

class ModernChair extends Chair {
  sit() {
    console.log('Sitting on a Modern chair');
  }
}

class VictorianSofa extends Sofa {
  lie() {
    console.log('Lying on a Victorian sofa');
  }
}

class ModernSofa extends Sofa {
  lie() {
    console.log('Lying on a Modern sofa');
  }
}

// Interfaz de la fábrica
class FurnitureFactory {
  createChair() {
    throw new Error('This method should be overridden!');
  }

  createSofa() {
    throw new Error('This method should be overridden!');
  }
}

// Fábricas concretas
class VictorianFurnitureFactory extends FurnitureFactory {
  createChair() {
    return new VictorianChair();
  }

  createSofa() {
    return new VictorianSofa();
  }
}

class ModernFurnitureFactory extends FurnitureFactory {
  createChair() {
    return new ModernChair();
  }

  createSofa() {
    return new ModernSofa();
  }
}

// Uso
function clientCode(factory) {
  const chair = factory.createChair();
  const sofa = factory.createSofa();
  chair.sit();
  sofa.lie();
}

const victorianFactory = new VictorianFurnitureFactory();
clientCode(victorianFactory);
// Output:
// Sitting on a Victorian chair
// Lying on a Victorian sofa

const modernFactory = new ModernFurnitureFactory();
clientCode(modernFactory);
// Output:
// Sitting on a Modern chair
// Lying on a Modern sofa
```

### Aplicaciones Comunes del Patrón Factory

- **Creación de Objetos Complejos**: Cuando la creación de un objeto es compleja y el tipo de objeto no se conoce hasta el momento de ejecución.
- **Sistemas de Plugins**: Para crear objetos de diferentes tipos de plugins o módulos.
- **Interfaz de Usuario**: Para crear diferentes componentes de interfaz de usuario que deben cumplir con una interfaz común pero que pueden tener diferentes implementaciones.

### Conclusión

El patrón Factory es útil para gestionar la creación de objetos y facilitar la adición de nuevos tipos de objetos sin modificar el código que los usa. Facilita el desacoplamiento y la extensibilidad del código. Sin embargo, debe usarse con cuidado para evitar la sobrecomplicación del diseño.
