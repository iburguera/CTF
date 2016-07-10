#HackThis - Main -  Level 3

URL:      https://www.hackthis.co.uk/levels/main/3

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

Accedemos a la página web y observamos que nos piden que introduzcamos un **Usuario** y una **Contraseña**  

##Hint

```html
Using JavaScript as the only method to secure your site is a bad idea, but this has obviously been over looked while coding this page.
```


## Explicación

Como no nos dan ninguna pista, empezamos mirando el código fuente de la página web para ver si podemos ver algo ahí.

```javascript
$(function()
{ 
    $('.level-form').submit(function(e)
        { 
          if(document.getElementById('user').value == 'heaven' && document.getElementById('pass').value == 'hell') 
          { 
          } else { e.preventDefault(); alert('Incorrect login') 
          } 
        })})
```

Observamos como hay un script en el código escrito en **JavaScript** que hace una validación del usuario y contraseña.

Analizando el código, podemos sacar facilmente el usuario y la contraseña de la prieba

```html
User: heaven
Pass: hell
```

Los introducimos en el campo de texto y vemos que las credenciales son válida y pasámos el reto :smile:

**FLAG** = {heaven/hell}

