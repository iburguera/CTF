#HackThis - JavaScript -  Level 3

URL:      https://www.hackthis.co.uk/levels/javascript/3

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Explicación

Al igual que en la prueba anterior, accedemos a la página web y vemos un campo de texto donde nos indican que tenemos que introducir una contraseña para pasar el reto.

Como no nos dan ninguna pista más, vamos a ver si el código fuente de la página nos da alguna pista.

Encontramos un script muy interesante debajo del formulario.

```javascript
var thecode = 'code123'; $(function(){ $('.level-form').submit(function(e){ e.preventDefault(); if ($('.level-form #pass')[0].value == thecode) { document.location = "?pass=" + thecode; } else { alert('Incorrect Password'); } }); });
```

Al parecer tenemos la variable **thecode='code123'** con el que se compara la contraseña. La introducimos pero no nos la acepta

Gracias a las herramientas del desarrollador que trae Chrome, podemos interactuar con la consola y poner un alert en la propia página para ver el valor de la variable **thecode**

Introducimos el siguiente comando en la consola de las herramientas del desarrollador web y vemos que nos muestra un mensaje diferente:

```javascript
alert(thecode);
```

```html
www.hackthis.co.uk dice:
getinthere
```

Al parecer la variable **thecode** no es la que nos imaginabamos. 

Probamos a poner la contraseña **getinthere** y nos la admite :smile:

**FLAG** = {getinthere}
