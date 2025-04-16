## L: Liskov substitution principle o Principio de sustitución de Liskov
Los objetos de una clase deben poder ser reemplazados por los objetos de una subclase 

Se le pasa como parametro una funcion que contiene los manejadores del error.


```javascript
function makerequest(url, erroHandler){
    fetch(url)
    .then(response => response.json)
    .catch(error => {
        errorHandler.handle(error);
    })
}

const consoleErrorHandler = {
    handle: function(error){
        sendErrorToService(error);
    }
}

const externalErrorHandler = {
    handle: function(error){
        sendErrorToExternal(error);
    }
}

makeRequest('https://.....', consoleErrorHandler)
makeRequest('https://.....', externalErrorHandler)
