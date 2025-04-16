El patrón **Command** es un patrón de diseño de comportamiento que encapsula una solicitud como un objeto, permitiendo que el parámetro de una solicitud sea tratado como un objeto, lo que permite parametrizar clientes con diferentes solicitudes, colas de solicitudes y operaciones de deshacer. Este patrón es útil para desacoplar el origen de una solicitud de su procesamiento, y para soportar operaciones de deshacer y rehacer.

### Conceptos Clave del Patrón Command

1. **Encapsulación de Solicitudes**: Convierte una solicitud en un objeto, lo que permite parametrizar métodos con diferentes solicitudes, retrasar la ejecución de una solicitud y soportar operaciones de deshacer.

2. **Desacoplamiento**: Desacopla el invocador de la operación que se va a realizar. El invocador no necesita saber qué clase concreta se encargará de la solicitud.

3. **Deshacer/Rehacer**: Permite implementar operaciones de deshacer y rehacer al encapsular la lógica de la solicitud en un objeto que puede ser almacenado y manipulado.

### Componentes del Patrón Command

1. **Command (Comando)**: Define una interfaz para ejecutar una operación. Debe declarar un método `execute` que todas las clases concretas deben implementar.

2. **ConcreteCommand (Comando Concreto)**: Implementa la interfaz `Command` y define la vinculación entre una acción y una operación específica. Debe invocar el método correspondiente en el receptor.

3. **Client (Cliente)**: Crea un objeto `ConcreteCommand` y configura su receptor.

4. **Invoker (Invocador)**: Pide al objeto `Command` que ejecute la solicitud. No sabe qué operación concreta se llevará a cabo.

5. **Receiver (Receptor)**: Sabe cómo realizar la operación asociada con la solicitud. El comando concreto invoca métodos en el receptor para llevar a cabo la solicitud.

### Ejemplo de Implementación en JavaScript

Vamos a implementar un ejemplo simple del patrón Command para un sistema de control remoto que puede encender y apagar luces.

**Definir la Interfaz Command**

```javascript
// Interfaz Command
class Command {
  execute() {
    throw new Error('Este método debe ser sobrescrito!');
  }
}
```

**Definir el Receiver**

```javascript
// Receiver
class Light {
  on() {
    console.log('La luz está encendida.');
  }

  off() {
    console.log('La luz está apagada.');
  }
}
```

**Definir los Comandos Concretos**

```javascript
// Comando Concreto: Encender Luz
class LightOnCommand extends Command {
  constructor(light) {
    super();
    this.light = light;
  }

  execute() {
    this.light.on();
  }
}

// Comando Concreto: Apagar Luz
class LightOffCommand extends Command {
  constructor(light) {
    super();
    this.light = light;
  }

  execute() {
    this.light.off();
  }
}
```

**Definir el Invocador**

```javascript
// Invocador
class RemoteControl {
  setCommand(command) {
    this.command = command;
  }

  pressButton() {
    this.command.execute();
  }
}
```

**Uso del Patrón Command**

```javascript
// Crear el receptor
const livingRoomLight = new Light();

// Crear los comandos concretos
const lightOn = new LightOnCommand(livingRoomLight);
const lightOff = new LightOffCommand(livingRoomLight);

// Crear el invocador
const remote = new RemoteControl();

// Configurar el invocador con el comando de encender la luz
remote.setCommand(lightOn);
remote.pressButton();
// Output: La luz está encendida.

// Configurar el invocador con el comando de apagar la luz
remote.setCommand(lightOff);
remote.pressButton();
// Output: La luz está apagada.
```

### Explicación del Ejemplo

1. **Command**:
   - `Command` define la interfaz con el método `execute`, que debe ser implementado por todos los comandos concretos.

2. **ConcreteCommand**:
   - `LightOnCommand` y `LightOffCommand` implementan `Command` y vinculan la solicitud de encender o apagar la luz con la operación concreta en el `Light` (receptor).

3. **Receiver**:
   - `Light` realiza las operaciones de encender y apagar la luz. Es el objeto sobre el que se ejecuta el comando.

4. **Invoker**:
   - `RemoteControl` mantiene una referencia al comando y lo invoca cuando se presiona el botón. No necesita conocer el receptor ni la lógica específica del comando.

5. **Uso**:
   - Crea instancias de `Light`, `LightOnCommand`, `LightOffCommand`, y `RemoteControl`. Configura el `RemoteControl` con diferentes comandos y ejecuta las solicitudes correspondientes.

### Aplicaciones Comunes

- **Controles Remotos**: Implementar sistemas de control remoto para encender y apagar dispositivos.
- **Operaciones Deshacer/Rehacer**: Implementar operaciones que se puedan deshacer o rehacer, como ediciones en un documento.
- **Sistemas de Menú**: Implementar menús en aplicaciones donde cada opción puede ejecutar una operación específica.

### Ventajas del Patrón Command

1. **Desacoplamiento**: Desacopla el invocador de la operación concreta, permitiendo modificar las solicitudes sin alterar el código del invocador.
2. **Flexibilidad**: Permite parametrizar métodos con diferentes solicitudes, colas de solicitudes y operaciones de deshacer.
3. **Extensibilidad**: Nuevos comandos pueden ser añadidos fácilmente sin modificar el código existente del invocador o del receptor.

### Consideraciones

- **Número de Comandos**: Un gran número de comandos puede llevar a una proliferación de clases, aumentando la complejidad del sistema.
- **Mantenimiento**: Puede ser necesario gestionar la sincronización entre los comandos y su estado si se implementan características como deshacer y rehacer.

En resumen, el patrón Command es útil para encapsular solicitudes en objetos, lo que permite desacoplar el origen de la solicitud de su procesamiento y proporciona flexibilidad para parametrizar, deshacer y rehacer operaciones. Es ideal para sistemas donde las solicitudes y operaciones pueden variar y necesitan ser gestionadas de manera desacoplada.