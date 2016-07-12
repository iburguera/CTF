#HackThis - Intermediate -  Level 2

URL:      https://www.hackthis.co.uk/levels/intermediate/2

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint
Use the POST method to send the password 'flubergump' to this page

When submitting a form, data is passed to another page. There are a few ways this could be done. In this example there is no form, but you can still easily send the data.

## Explicación

Entramos en la página y nos indican que le tenemos que pasar el campo password al a URL con el método POST

También nos dan la contraseña que tenemos que poner :smile:

Al igual que en la prueba anterior probamos a poner la contraseña directamente ne la URL para ver si nos la acepta pero no lo hace.

```html
https://www.hackthis.co.uk/levels/intermediate/2?password=flubergump
```

Sabemos que tenemos que enviar la contraseña con el método **POST** por lo que escribimos un **HTML** con un formulario que envíe la contraseña con el método POST a la URL del reto

Escribimos el fichero **intermediate-Level2.html**

```html
<form method="post" action="https://www.hackthis.co.uk/levels/intermediate/2">
  Password: <input type="text" name="password" value="flubergump"><br>
  <input type="submit" value="Submit">
</form>
```

Abrimos el fichero en un navegador, le damos a enviar y pasamos el reto :sunglasses:

