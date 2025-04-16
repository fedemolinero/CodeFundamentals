## O: Open/closed principle o Principio de abierto/cerrado
Las entidades, clases, modulos, funciones deben estar cerradas para su modificacion pero abiertas para su extension.

```javascript
function ProcessPayment(price, cardDetails){
    // gets price 
    return 'se pago todo con tarjeta de credito';
}
```

Supongamos que ahora quisieramos pagar con paypal, entramos en processPayment a meter ifs para cambiar de logica, estaria modificando el codigo en lugar de extenderlo, lo que se busca es:

```javascript
function ProcessPaymentwCard(price, paypalDetails){
    return 'se pago todo con tarjeta de credito';
}
function ProcessPaymentWPaypal(price, cardDetails){
    return 'se pago todo con tarjeta paypal';
}
```