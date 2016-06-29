#[2/6]  Level 2: Persistence is key

##Mission Description

Web applications often keep user data in server-side and, increasingly, client-side databases and later display it to users. No matter where such user-controlled data comes from, it should be handled carefully. 

This level shows how easily XSS bugs can be introduced in complex apps.

##Mission Objective

Inject a script to pop up an alert() in the context of the application. 

Note: the application saves your posts so if you sneak in code to execute the alert, this level will be solved every time you reload it.

#Write Up Iker

Al igual que en el nivel anterior, debemos ejecutar una alerta en la página web. En este caso nos encontramos un foro en el que podemos dejar comentarios.

Comenzamos con el mismo script del **nivel 1** pero **no funciona**:

```javascript
<script>alert('aibalaostiapues!')</script>
```

Podemos intentar que busque una imagen dentro del código que vamos a injectar y que ejecute una alerta si no encuentra la imagen.
En este caso vamos a poner mal el path the la imagen con el objetivo de que salte la alerta.

```javascript
<img src=x onerror="alert('PATXIIIIIIIIII!! Esto FUN-TZI-O-NA!!');"
```

El texto introducido en el textarea del foro se ejecuta como una alerta en el navegador y nos muestra un mensaje diciendo que hemos pasado la prueba. :)

