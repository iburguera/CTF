#HackThis - JavaScript -  Level 5

URL:      https://www.hackthis.co.uk/levels/javascript/5

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint
This isn't the page I was looking for...

## Explicación

Al igual que en la prueba anterior, accedemos a la página web y vemos un campo de texto donde nos indican que tenemos que introducir una contraseña para pasar el reto.

Metemos una contraseña aleatoria, nos da error y nos devuelve a la página donde están todos los niveles.

Como no nos dan ninguna pista más, vamos a ver si el código fuente de la página nos da alguna pista.

Nos vemos ningún indicio de la contraseña y ningún prompt en el que sale la contraseña. 

Sólamente dos referencias ha dos JavasScripts

```html
view-source:https://www.hackthis.co.uk/levels/javascript/5

<script type='text/javascript' src='https://hackthis-10af.kxcdn.com/files/js/min/main.js?1446747682'></script>
<script type='text/javascript' src='https://hackthis-10af.kxcdn.com/files/js/min/extra_48d468a93b.js?1429997775'></script>
```

Entramos a los dos y buscamos la palabra **password**

En el primer JavaScript no encontramos nada pero en el segundo encontramos un código que es interesante y se comporta al igual que hemos experimentando anteriormente al introducir la contraseña (nos retorna a la página de los niveles)

```html
https://hackthis-10af.kxcdn.com/files/js/min/extra_48d468a93b.js?1429997775
```

```javascript
a=window.location.host+"";
b=a.length;
c=4+((5*10)*2);
d=String.fromCharCode(c,-(41-Math.floor(1806/13)),Math.sqrt(b-2)*29,(b*8)-29);
p=prompt("Password:","");
if(p==d)
{
	window.location="?pass="+p;
}
else
{
	window.location="/levels/";
}
```

Vemos que si la contraseña que introducimos en la variable **p** es igual a la variable **d** generada en ese script, nos deja parar la prueba.

Si la contraseña no es correcta, nos devuelve a la página de los niveles como hemos comprobado! ¡Este es nuestro código! :beers:

Al igual que en alguna prueba anterior, vamos a poner una alerta que nos proporcione el valor de la variable **p**

Utilizando la consola del desarrollador Web que trae Chrome, vamos a poner esta alerta en la consola:

```javascript
alert(d);
```

NOTA: tenemos que tener cargadas las herramientas del desarrollador al cargar la págona y poner la alerta antes de introducir la contraseña.

Introducimos una contraseña aleatoria y a continuación se ejecuta la alerta que teníamos puesta en nuestra consola del desarrollador.

Nos devuelve la contraseña :smile:

```html
hats
```

La introducimos y pasamos la prueba :sunglasses:

**FLAG** = {hats}

