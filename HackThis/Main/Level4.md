#HackThis - Main -  Level 4

URL:      https://www.hackthis.co.uk/levels/main/4

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

Accedemos a la página web y observamos que nos piden que introduzcamos un **Usuario** y una **Contraseña**  

##Hint

```html
Sometimes extra hidden fields are added to the form which contains extra information for the login script. Again this is very easy for anyone to gain access to as it is clearly shown in the source code.
Sometimes these fields can contain very important information.
```

## Explicación

Como no nos dan ninguna pista, empezamos mirando el código fuente de la página web para ver si podemos ver algo ahí.

```html
<form method="POST">
    <fieldset>
    <label for="user">Username:</label>
    <input type="Text" name="user" id="user" autocomplete="off"/>
    <br/>
    <label for="user">Password:</label>
    <input type="Password" name="pass" id="pass" autocomplete="off"/>
    <br/>
    <input type="hidden" name="passwordfile" value="../../extras/ssap.xml"/>
    <input type="submit" value="Submit" class="button"/>
    </fieldset>
</form>
```

Nos fijamos en la linea que está oculta, la cual que hace referencia a un fichero de password en un fichero xml.

```html
<input type="hidden" name="passwordfile" value="../../extras/ssap.xml"/>
```

Accedemos a la página xml de donde recoge el usuario y contraseña para realizar la validación.

```html
https://www.hackthis.co.uk/levels/extras/ssap.xml
```

Y nos encontramos con el siguiente contenido:

```xml
<user>
<name>Admin</name>
<username>999</username>
<password>911</password>
</user>
```

Por lo tanto, ya sabemos con que valores se van a comparar el usuario y contraseña que hayamos introducido. 

```html
User: 999
Pass: 911
```

Los introducimos en el campo de texto y vemos que las credenciales son válidad y pasámos el reto :smile:

**FLAG** = {999/911}
