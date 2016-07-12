
#HackThis - Intermediate -  Level 1

URL:      https://www.hackthis.co.uk/levels/intermediate/1

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint
Use the GET method to send the password 'flubergump' to this page

When submitting a form, data is passed to another page. There are a few ways this could be done. In this example there is no form, but you can still easily send the data.

## Explicación

Entramos en la página y nos indican que le tenemos que pasar el campo password al a URL con el método GET

También nos dan la contraseña que tenemos que poner :smile:

```html
flubergump
```

Pasarle la password al campo **password** mediante la URL es muy sencillo si sabemos como funcionan las URL y como se envían los datos en la web.

Por lo tanto montamos la URL con la contraseña y validamos

```html
https://www.hackthis.co.uk/levels/intermediate/1?password=flubergump
```

**FLAG** = {https://www.hackthis.co.uk/levels/intermediate/1?password=flubergump}
