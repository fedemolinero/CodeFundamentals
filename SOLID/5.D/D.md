## D: Dependency inversion principle o Principio de inversión de dependencia
Que pases toda la configuracion posible por parametro basicamente para no limitar las dependencias

En este ejemplo tenemos una conexion a una base de datos para el password reminder, pero si quisieramos cambiarla en el futuro deberiamos cambiar todas las ocurrencias de esto en varios lugares, lo que sugiere el patron es que en lugar que password Reminder DEPENDA de mysql connection, vamos a crear una nueva instancia de la conexion pasandola por parametro

```javascript
class MySQLConnection {
    connect(){
        //CONNECT CODE
    }
}

class PasswordReminer {
    constructor(){
        this.dbConnection = new MySQLConnection()
    }
}

// ... posible new code
// class PostGreConnection{
    // connect(){
    //CONNECT CODE
    // }
// }
```

Que en lugar de ese codigo donde no tenemos parametros y cada funcion conecta por separado
Seguiriamos teniendo las dos funciones la funcion recibe un parametro de conexion para la instancia de la clase.
Haciendo que la dependencia este en la clase que pasa por parametro.

```javascript
class MySQLConnection {
    connect(){
        //CONNECT CODE
    }
}

class PostGreConnection{
    connect(){
    //CONNECT CODE
    }
}
 

class PasswordReminer {
    constructor(dbConnection){
        this.dbConnection = dbconnection;
    }
}
```