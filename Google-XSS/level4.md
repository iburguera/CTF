#[4/6]  Level 4: Context matters

##Mission Description

Every bit of user-supplied data must be correctly escaped for the context of the page in which it will appear. This level shows why.

##Mission Objective

Inject a script to pop up a JavaScript alert() in the application.

## Write Up Iker 

Esta prueba se complica un poco más que la anterior. Tenemos un **timer** el cual nos indica que saltará una alerta de Time-up una vez que pasen los segundos que hayamos puesto en el campo de texto.
Esto no puede dar una pista que podemos utilizarlo a nuestro favor. Nos dice que saltará una alerta cuando se termine el tiempo, por lo tanto tenemos que encontrar el código que hace saltar la alerta.
Encontramos el siguiente código en timer.html

```html
 <script>
      function startTimer(seconds) {
        seconds = parseInt(seconds) || 3;
        setTimeout(function() { 
          window.confirm("Time is up!");
          window.history.back();
        }, seconds * 1000);
      }
    </script>
  </head>
  <body id="level4">
    <img src="/static/logos/level4.png" />
    <br>
    <img src="/static/loading.gif" onload="startTimer('{{ timer }}');" />
    <br>
    <div id="message">Your timer will execute in {{ timer }} seconds.</div>
  </body>
```

Nos fijamos en la parte donde dice ```html <img src="/static/loading.gif" onload="startTimer('{{ timer }}');" /> ``` el cual ejecuta el script que está más arriba pasándole como parámetro el número de segundos que hemos introducido para realizar la cuenta atrás.
Teniendo esto en cuenta, podemos jugar con el vamos que introducimos al campo **timer** para que ejecute lo que queremos.

Tenemos que hacer que el valor de timer esto: 
```html 
onload="startTimer('{{ timer }}');"
``` 
sea igual a esto esto:
```html 
');alert('Está PATXIIIIIIII?!');var temp=('
``` 
para que al final quede todo como esta consulta:

```html 
onload="startTimer('');alert('Está PATXIIIIIIII?!');var temp=('');"
``` 
Utilizamos la variable var temp para cerrar el último paréntesis del comando ```html onload="startTimer('{{ timer }}');"``` y no de ningún error.

Probamos a introducir el código ```html ');alert('Está PATXIIIIIIII?!');var temp=('```en el campo timer para ejecutar la consulta quedando de la siguiente manera:
Pero nos salta un error de sintaxis con los **;**. Probamos a cambiar caracter **;** por su valor en html **%3B** y modificamos la consulta:

Probamos de nuevo introduciendolo en el campo de timer y ejecutamos:

```html
https://xss-game.appspot.com/level4/frame?timer=')%3Balert('Esta patxiiiiiii?')%3Bvar temp=('
```

Nos carga el timer y nos muestra el mensaje de alerta que nos pasa al siguiente nivel :)

Iker Burguera






