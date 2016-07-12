#HackThis - Intermediate -  Level 4

URL:      https://www.hackthis.co.uk/levels/intermediate/4

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint

Bypass the filter and execute exactly this code:

<script>alert('HackThis!!');</script>

## Explicación

Entramos en la página y nos indican que tenemos hacer mostrar el mensaje de arriba haciendo un bypass en el campo de texto que tenemos más abajo.

Primero que nada vamos a mirar que tipo de filtro se le está aplicando al campo de texto donde vamos a poner el mensaje de alerta.

Para ello vamos a ver el código fuente de la página pero no encontramos nada.

Suponemos que es un reto de **XSS** por lo que vamos a utilizar un clásico, poner el **scrscriptipt**

Los filtro de seguridad básicos, eliminan la palabra script dejando el resto como esta. En este caso si escribimos el script de arriba con lo que hemos comantado, eliminará la palabra script de ambos lados, juntará el resto y lo dejará pasar. 

Por lo tanto vamos a utilizar el siguiente código para hacer le **Bypass**:

```html
<scr<script>ipt>alert('HackThis!!');</scr</script>ipt>
```

Lo metemos y nos deja pasar el reto :smile: :beers:


