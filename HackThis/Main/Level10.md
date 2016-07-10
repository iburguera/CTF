#HackThis - Main -  Level 10

URL:      https://www.hackthis.co.uk/levels/main/10

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
Encrypted passwords can be quite difficult to decode, but when you use a common method there is usually a way to get around it. Especially when the encrypted information are simple common words.
```

## Explicación

Accedemos a la página web y observamos que nos piden que introduzcamos un **usuario** y una **Contraseña**.

El enunciado nos indica que las contraseñas cifradas suelen ser dificiles de descifrar.

Accedemos al código y vemos que se sirve de un fichero llamada **level10pass.txt** para comparar la contraseña

```html
<form method="POST">
<fieldset>
<label for="user">Username:</label>
<input type="Text" name="user" id="user" autocomplete="off"/>
<br/>
<label for="user">Password:</label>
<input type="Password" name="pass" id="pass" autocomplete="off"/>
<br/>
<input type="hidden" name="passwordfile" value="level10pass.txt"/>
<input type="submit" value="Submit" class="button"/>
</fieldset>
</form>
```

La URL es la siguiente:

```html
www.hackthis.co.uk/levels/extras/level10pass.txt
```

Nos encontramos con el siguiente texto dentro del fichero **level10pass.txt**

```html
69bfe1e6e44821df7f8a0927bd7e61ef208fdb25deaa4353450bc3fb904abd52:f1abe1b083d12d181ae136cfc75b8d18a8ecb43ac4e9d1a36d6a9c75b6016b61
```

Por la longitud podríamos suponer que es un **SHA256 Hash** por lo que podemos ver si alguien ya a encontrado el texto para esa Hash

Podemos acceder a la siguiente página para verlo:

```html
https://md5hashing.net/hash/sha256/
```

Encontramos el texto que necesitamos que nos dan el usuario y la contraseña del reto

```html
69bfe1e6e44821df7f8a0927bd7e61ef208fdb25deaa4353450bc3fb904abd52  : carl
f1abe1b083d12d181ae136cfc75b8d18a8ecb43ac4e9d1a36d6a9c75b6016b61  : guess
```

Los introducimos en el campo de texto y vemos que las credenciales son válida y pasámos el reto :smile:

**FLAG** = {carl/guess}
