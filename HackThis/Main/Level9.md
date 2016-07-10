#HackThis - Main -  Level 9

URL:      https://www.hackthis.co.uk/levels/main/9

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
The developer has now added a feature that allows him to get a password reminder. Can you exploit it to send you the login details instead?
```

## Explicación

Accedemos a la página web y observamos que nos piden que introduzcamos un **usuario** y una **Contraseña** además de un campo en el que podemos recuperar la contraseña llamada **Request details**   

Esto nos lleva a un apartado donde podemos meter un correo electrónico para poder recuperar la contraseña

```html
<form method="POST">
    <fieldset>
    <label for="email1">Email:</label>
    <input type="text" name="email1" id="email1" autocomplete="off"/>
    <br/>
    <input type="hidden" name="email2" id="email2" value="admin@hackthis.co.uk" autocomplete="off"/>
    <input type="submit" value="Submit" class="button"/>
    </fieldset>
</form>
```

Además tiene un campo de texto que también está oculto.

Al igual que en alguna prueba anterior, vamos a utilizar la herramienta del desarrollador para cambiar los parámetros de **hidden** y el valor del correo electrónico.

Cambiamos el campo:

```html
 <input type="hidden"   por   <input type="text"
```

Al poner lo anterior, vemos que nos aparecen dos **TextField** en el que podemos poner nuestros correos de recuperación.

En este caso vamos a poner en los **dos campos** el **mismo correo** pero tiene que ser diferente a **admin@hackthis.co.uk** para que podamos pasar la prueba.

Los introducimos en el campo de texto y vemos que las credenciales son válida y pasámos el reto :smile:

**FLAG** = {-}
