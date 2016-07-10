#HackThis - Main -  Level 8

URL:      https://www.hackthis.co.uk/levels/main/8

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
The coder has made the same mistake as level 4 but this time at least he has tried to protect the password. The password has been encrypted, convert the binary into something that is easier for humans to read (base 16).

If you think you have the right answer but it isn't being accepted, submit your answer in CAPITALS.
```

## Explicación

Accedemos a la página web y observamos que nos piden que introduzcamos un **usuario** y una **Contraseña**.   

Observamos el código fuente de la página y vemos lo siguiente:

```html
<fieldset>
    <label for="user">Username:</label>
    <input type="Text" name="user" id="user" autocomplete="off"/>
    <br/>
    <label for="user">Password:</label>
    <input type="Password" name="pass" id="pass" autocomplete="off"/>
    <br/>
    <input type="hidden" name="passwordfile" value="extras/secret.txt"/>
    <input type="submit" value="Submit" class="button"/>
</fieldset>
```

Vemos que hace referencia a un fichero de texto para realizar la comparación de las contraseñas.

```html
https://www.hackthis.co.uk/levels/extras/secret.txt
```

Accedemos a la página web y vemos que hay una fila de **1** y **0**

```html
1011 0000 0000 1011
1111 1110 1110 1101
```

Parece que tiene la estructura de usuario y contraseña. 

El enunciado nos indica que están codificadas en Base16 por lo que lo único que tenemos que hacer es pasar esos números a **HEX** y obtendremos  el usuario y contraseña

```html
1011 0000 0000 1011
 B    0    0    B
1111 1110 1110 1101
 F    E    E    D
```

NOTA: A la hora de poner la contraseña, hay que tener en cuenta que el nombre de **boob** está representado por **B** y **0** (el número)

```html
User: B00B
Pass: FEED
```
Los introducimos en el campo de texto y vemos que las credenciales son válida y pasámos el reto :smile:

**FLAG** = {B00B/FEED}
