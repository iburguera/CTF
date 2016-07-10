#HackThis - Main -  Level 2

URL:      https://www.hackthis.co.uk/levels/main/2

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

Accedemos a la página web y observamos que nos piden que introduzcamos un **Usuario** y una **Contraseña**  

##Hint

```html
Just expanding on the idea of Level 1. The best place to start is always the source code.

Or maybe the answer is right under your nose?!
```
```html
Username: 
Password:
Submit
```

## Explicación

Como no nos dan ninguna pista, empezamos mirando el código fuente de la página web para ver si podemos ver algo ahí.

```html
<form method="POST">
  <fieldset>
    <label for="user">Username:</label>
    <span style="color: rgb(0, 0, 0);">resu</span>
    <input type="Text" name="user" id="user" autocomplete="off"/>
    <br/>
    <label for="user">Password:</label>
    <span style="color: rgb(0, 0, 0);">ssap</span>
    <input type="Password" name="pass" id="pass" autocomplete="off"/>
    <br/>
    <input type="submit" value="Submit" class="button"/>
  </fieldset>
</form>
```

Observamos como hay dos campo sospechosos en color **Negro** -> **rgb(0, 0, 0)** en cual muestra un texto en ese color. 

Como el color del background es negro, no podemos verlo, así que apuntamos los dos texto que probablemente sean el usuario y la contraseña del reto


```html
User: resu
Pass: ssap
```

Los introducimos en el campo de texto y vemos que las credenciales son válidad y pasámos el reto :smile:

**FLAG** = {resu/ssap}
