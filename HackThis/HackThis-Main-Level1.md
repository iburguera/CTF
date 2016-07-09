#HackThis - Main -  Level 1

URL:      https://www.hackthis.co.uk/levels/main/1

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

Accedemos a la página web y observamos que nos piden que introduzcamos un **Usuario** y una **Contraseña**  

```html
Do NOT enter your credentials below, these levels are here to test you. Find the correct details and proceed to the next level.

If you get stuck check out the hint, forum posts and articles shown in the help section on the left.
```
```html
Username: 
Password:
Submit
```

Como no nos dan ninguna pista, empezamos mirando el código fuente de la página web para ver si podemos ver algo ahí.

```html
<head>
...
<!-- username: in, password: out -->
...
</head>
```

Observamos como en la etiqueta **HEAD** del código **HTML** se nos muestra el usuario y la contraseña de la prueba.

```html
User: in
Pass: out
```

Los introducimos en el campo de texto y vemos que las credenciales son válidad y pasámos el reto :smile:

**FLAG** = {in/out}
