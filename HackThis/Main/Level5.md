#HackThis - Main -  Level 5

URL:      https://www.hackthis.co.uk/levels/main/5

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
Slightly more complicated JavaScript this time, but just as insecure.

Refresh to try again.
```

## Explicación

Accedemos a la página web y observamos que nos piden que introduzcamos una **Contraseña** en un Pop-Up que nos sale.   

Como no nos dan ninguna pista, empezamos mirando el código fuente de la página web para ver si podemos ver algo ahí.

```html
div class="level-form">
<script language="JavaScript" type="text/javascript">
var pass;
            pass=prompt("Password","");
            if (pass=="9286jas") 
            {
                window.location.href="/levels/main/5?pass=9286jas";
            }
</script>
```

Observando el código, encontramos un script que verifica la contraseña introducida en el campo de texto. 



```html
...
 if (pass=="9286jas") 
...
```

Por lo tanto, ya sabemos con que valor se van a comparar la contraseña que hayamos introducido. 

```html
Pass: 9286jas
```

Los introducimos en el campo de texto y vemos que las credenciales son válida y pasámos el reto :smile:

**FLAG** = {9286jas}
