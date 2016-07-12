
#HackThis - Intermediate -  Level 3

URL:      https://www.hackthis.co.uk/levels/intermediate/3

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint
Restricted Area

ENTER SITE

## Explicación

Entramos en la página y nos indican que tenemos el acceso restringido. 

Si pulsamos el enlace **Enter Site** nos indica que hemos introducido los datos inválidos.

Con la herramienta **EditThisCookie** nos encontramos con un valor que dice lo siguiente

```html
restricted_access = false
```

Parece ser que es esto lo que no nos está permitiendo pasar el reto.

Vamos a editar la Cookie y a ponerle un valor **True**

```html
restricted_access = true
```

La editamos, y volvemos a cargar la página web. 

En esta ocasión nos deja pasar el reto :smile:
