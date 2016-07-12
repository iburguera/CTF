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


```javascript

```

view-source:https://www.hackthis.co.uk/levels/javascript/4?input

<form action='/search.php' method='get'>
                                    <input autocomplete="off" placeholder='Search: topic, user, article..' name='q'/>
                                    <i class='icon-search'></i>
                                </form>


view-source:https://www.hackthis.co.uk/levels/javascript/4?q


<div class='level-form'>

                <script> document.location = '?input'; </script>
                <div class='center'>The password is: smellthecheese</div>

            </div>
            
            
**FLAG** = {smellthecheese}


