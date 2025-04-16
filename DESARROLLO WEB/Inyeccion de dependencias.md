# Inyección de dependencias

La **inyección de dependencias** es un patrón de diseño utilizado en programación para mejorar la modularidad y facilitar la prueba de unidades en el código. 

Su propósito es desacoplar los componentes de una aplicación, permitiendo que dependan de interfaces o contratos en lugar de implementaciones concretas. Aquí te explico en detalle qué es la inyección de dependencias y cómo funciona:

## ¿Qué es la Inyección de Dependencias?

La inyección de dependencias (DI, por sus siglas en inglés) es una técnica para proporcionar a un objeto sus dependencias desde el exterior en lugar de que el objeto las cree o las busque por sí mismo. Esto facilita el intercambio de implementaciones y mejora la capacidad de prueba y mantenimiento del código.

### Conceptos Clave

1. **Dependencia**: Un componente o servicio del sistema que un objeto necesita para funcionar. Por ejemplo, una clase `UsuarioService` podría depender de un repositorio de usuarios para acceder a datos.

2. **Inyección**: El proceso de proporcionar las dependencias a un objeto en lugar de que el objeto las cree. Esto se puede hacer de varias maneras: mediante constructor, propiedades, o métodos.

3. **Contenedor de Dependencias**: Un contenedor o framework que gestiona la creación y la inyección de dependencias. Ejemplos en JavaScript incluyen `InversifyJS` y `Awilix`.

### Tipos de Inyección de Dependencias

1. **Inyección por Constructor**:
   Las dependencias se proporcionan al objeto a través de su constructor. Este es el método más común y suele ser el más fácil de implementar.

   **Ejemplo en JavaScript:**
   ```javascript
   class Logger {
     log(message) {
       console.log(message);
     }
   }

   class UserService {
     constructor(logger) {
       this.logger = logger;
     }

     createUser(user) {
       // Utiliza el logger proporcionado
       this.logger.log(`Usuario creado: ${user.name}`);
     }
   }

   const logger = new Logger();
   const userService = new UserService(logger);
   userService.createUser({ name: 'Juan' }); // Usuario creado: Juan
   ```

2. **Inyección por Propiedad**:
   Las dependencias se inyectan estableciendo propiedades del objeto después de su creación. Esto permite configurar el objeto en múltiples pasos.

   **Ejemplo en JavaScript:**
   ```javascript
   class UserService {
     setLogger(logger) {
       this.logger = logger;
     }

     createUser(user) {
       this.logger.log(`Usuario creado: ${user.name}`);
     }
   }

   const logger = new Logger();
   const userService = new UserService();
   userService.setLogger(logger);
   userService.createUser({ name: 'Juan' }); // Usuario creado: Juan
   ```

3. **Inyección por Método**:
   Las dependencias se inyectan llamando a métodos del objeto después de su creación. Este enfoque es útil si la dependencia solo es necesaria en un contexto específico.

   **Ejemplo en JavaScript:**
   ```javascript
   class UserService {
     createUser(user, logger) {
       logger.log(`Usuario creado: ${user.name}`);
     }
   }

   const logger = new Logger();
   const userService = new UserService();
   userService.createUser({ name: 'Juan' }, logger); // Usuario creado: Juan
   ```

### Ventajas de la Inyección de Dependencias

1. **Desacoplamiento**:
   Al no tener dependencias codificadas directamente en una clase, puedes cambiar la implementación de una dependencia sin afectar al código que la utiliza.

2. **Facilidad de Pruebas**:
   Puedes inyectar objetos simulados (mocks) o objetos de prueba en lugar de las implementaciones reales, facilitando la prueba de unidades.

   **Ejemplo de prueba:**
   ```javascript
   class MockLogger {
     log(message) {
       // Simula el comportamiento del logger
     }
   }

   const mockLogger = new MockLogger();
   const userService = new UserService(mockLogger);
   // Realiza pruebas sobre userService sin depender de una implementación real de Logger
   ```

3. **Flexibilidad**:
   Permite la configuración dinámica de las dependencias y su reemplazo en tiempo de ejecución.

### Contenedores de Dependencias

Los contenedores de dependencias son herramientas que gestionan la creación y la inyección de dependencias automáticamente, simplificando la configuración y el manejo de objetos complejos. Estos contenedores mantienen un registro de las dependencias y cómo deben ser inyectadas.

**Ejemplo usando `InversifyJS` en JavaScript:**

```javascript
const { Container, inject, injectable } = require('inversify');

// Definición de interfaces y clases
const TYPES = {
  Logger: Symbol.for('Logger'),
  UserService: Symbol.for('UserService')
};

@injectable()
class Logger {
  log(message) {
    console.log(message);
  }
}

@injectable()
class UserService {
  constructor(@inject(TYPES.Logger) logger) {
    this.logger = logger;
  }

  createUser(user) {
    this.logger.log(`Usuario creado: ${user.name}`);
  }
}

// Configuración del contenedor
const container = new Container();
container.bind(TYPES.Logger).to(Logger);
container.bind(TYPES.UserService).to(UserService);

// Resolución de dependencias
const userService = container.get(TYPES.UserService);
userService.createUser({ name: 'Juan' }); // Usuario creado: Juan
```

### Resumen

- **Inyección de Dependencias**: Técnica para proporcionar a un objeto sus dependencias desde el exterior en lugar de crearlas dentro del objeto.
- **Tipos**: Constructor, Propiedad, y Método.
- **Ventajas**: Desacoplamiento, facilidad de pruebas, y flexibilidad.
- **Contenedores**: Herramientas que gestionan automáticamente la creación e inyección de dependencias.

Este patrón es esencial para crear aplicaciones bien estructuradas, mantenibles y fáciles de probar, especialmente en sistemas complejos.