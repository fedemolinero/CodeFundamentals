## I: Interface segregation principle o Principio de segregación de la interfaz
Ninguna clase deberia ser forzada a implementar interfaz o metodos q no va a utilizar.

En este ejemplo vamos a considerar la interfaz Producto y tiene metodos para obtener detalles y mostrar en frontend. 
Por ejemplo producto digital no necesita guardar a db, por lo que romperia la segregacion de la interfaz.


```javascript
class Product {
    getDetails(){
        // code here
    }

    saveToDB(){
        // code here
    }

    displayInFrontend(){
        // code here
    }
}

class DigitalProduct extends Product {
// no need to save on db
}  
```

Deberia entonces crear una clase de producto y extender la interfaz a distintos productos.

```javascript
class Product {
    getDetails(){
        // code here
    }

    displayInFrontend(){
        // code here
    }
}

class PhisicalProduct extends Product {
    savetoDB()
}

class DigitalProduct extends Product {
// no need to save on db
}  
```
