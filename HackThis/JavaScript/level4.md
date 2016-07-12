#HackThis - JavaScript -  Level 4

URL:      https://www.hackthis.co.uk/levels/javascript/4

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint
This isn't the page I was looking for...

## Explicación

Al igual que en la prueba anterior, accedemos a la página web y vemos un campo de texto donde nos indican que tenemos que introducir una contraseña para pasar el reto.

Nos dicen que esta no es la página que estamos buscando. ¿Entonces cual es?

Como no nos dan ninguna pista más, vamos a ver si el código fuente de la página nos da alguna pista.

Tampoco vemos nada raro. Lo único raro que nos encontramos es en la URL que parece que es diferente a las anteriores pruebas


```html
https://www.hackthis.co.uk/levels/javascript/4?input
```

Vemos como tiene un parámetro **input** ¿Raro verdad? Quizás sea esto una pista de lo que estamos buscando

Como prueba, vamosa introducir el término **output** a ver que nos aparece en el código fuente

```html
https://www.hackthis.co.uk/levels/javascript/4?output
```

Nada, nos devuelve a la página principal.

Volvemos a mirar el código fuente de la página principal y vemos un código relacionado con el input

```html
view-source:https://www.hackthis.co.uk/levels/javascript/4?input
```

```html
<form action='/search.php' method='get'>
  <input autocomplete="off" placeholder='Search: topic, user, article..' name='q'/>
  <i class='icon-search'></i>
</form>
```

Parece que hace referencia a un parámetro con nombre **q**

Vamos a probar a a ver el código fuente de ese parámetro

```html
view-source:https://www.hackthis.co.uk/levels/javascript/4?q
```

¡BINGO! Encontramos la contraseña en su código fuente :smile: :sunglasses: :beers:

```html
<div class='level-form'>
<script> document.location = '?input'; </script>
  <div class='center'>The password is: smellthecheese</div>
</div>
```

**FLAG** = {smellthecheese}


