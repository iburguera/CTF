#HackThis - JavaScript -  Level 2

URL:      https://www.hackthis.co.uk/levels/javascript/2

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Explicación

Al igual que en la prueba anterior, accedemos a la página web y vemos un campo de texto donde nos indican que tenemos que introducir una contraseña para pasar el reto.

Como no nos dan ninguna pista más, vamos a ver si el código fuente de la página nos da alguna pista.

Encontramos un script muy interesante debajo del formulario.

```javascript
var length = 5;
var x = 3;
var y = 2;
y = Math.sin(118.13);
y = -y;
x = Math.ceil(y);
y++;
y = y+x+x;
y *= (y/2);
y++;
y++;
length = Math.floor(y);
```

Vemos que el script ejecuta un código y almacena el resultado en la variable **length**

Vamos a ejecutar el código y ver que resultado nos devuelve la variable. 

Para mostrar el resultado, vamos a utilizar el comando **alert(lenth)**

```javascript
var length = 5;
var x = 3;
var y = 2;
y = Math.sin(118.13);
y = -y;
x = Math.ceil(y);
y++;
y = y+x+x;
y *= (y/2);
y++;
y++;
length = Math.floor(y);
alert(length);
```

Lo introducimos en la siguiente dirección por ejemplo [https://jsfiddle.net/](https://jsfiddle.net/)

```html
https://jsfiddle.net/
```

Y nos devuelve el valor **9**

Introducimos el valor **9** como contraseña pero no nos la admite. 

Volvemos a mirar el código y nos indica que la **longitud** es de **9** por lo que vamos a intentar meter cualquier contraseña que tenga una longitud de 9 digitos o letras

```html
123456789
```

Nos la acepta y pasamos el reto :beers:

**FLAG** = {123456789}
