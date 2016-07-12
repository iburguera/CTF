#HackThis - JavaScript -  Level 1

URL:      https://www.hackthis.co.uk/levels/javascript/1

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Explicación

Accedemos a la página web y vemos un campo de texto donde nos indican que tenemos que introducir una contraseña para pasar el reto.

Como no nos dan ninguna pista más, vamos a ver si el código fuente de la página nos da alguna pista.

Encontramos un script muy interesante en la cabecera **HEAD** del **HTML** y otro java script debajo del formulario.

```javascript
$(function()
{ $('.level-form').submit(function(e)
  { e.preventDefault(); if(document.getElementById('pass').value == correct) 
  { document.location = '?pass=' + correct; 
  } else { alert('Incorrect password') 
} })})
```
 
 y

```javascript
var correct = 'jrules'
```

Si sabemos interpretar el código, podemos concluir que **jrules** es el string con el que se va a comparar la contraseña que introduzcamos en la campo de texto, por lo que vamos introducirlo.

Efectivamente, nos valida la contraseña y pasamos a l siguiente reto :smile:

**FLAG** = {jrules}
