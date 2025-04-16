# S: Single responsibility principle o Principio de responsabilidad única
Una clase debe tener una sola tarea o responsabilidad, o una unica razon para cambiar.
Evitamos tener codigo muy complejo dentro de la misma clase.

En este ejemplo la funcion calculate salary calcula el salario y genera un reporte en la misma funcion.
Lo que nos obligaria a cambiar esta funcion cada vez que querramos generar un reporte, o calcular el salario. Si creamos dos funciones con responsabilidades distintas es mas sencillo expandir las funciones cuando se necesite.


<!-- PROBLEMA QUE SOLUCIONA -->
```javascript
function CalculateSalary(empleado) {  
    const salario = empleado.horas * empleado.valorhora;
    const report = {
        nombre: empleado.nombre,
        valorhora:empleado.valorhora, 
        horas: empleado.horas
    } 
    createReport(report){
            console.log(report); //simulates the generation in this example        
    }
return salary;
}
```

<!-- SOLUCION -->
```javascript
function CalculateSalary(empleado) {  
    const salario = empleado.horas * empleado.valorhora;
    return salary;
}

function createReport(report){
        const report = {
        nombre: empleado.nombre,
        valorhora:empleado.valorhora, 
        horas: empleado.horas
    } 
      return console.log(report); //simulates the generation in this example
    }
```