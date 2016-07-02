#Natas Level 4 → Level 5

Username: natas5

URL:      http://natas5.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas5.natas.labs.overthewire.org** 
- **Usuario    : natas5**
- **Contraseña : iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos sale el siguiente mensaje: 

```html
Access disallowed. You are not logged in
```

De primeras ya nos dice que no podemos acceder al servidor porque no estamos logeados. Miramos el código fuente, directorios de niveles anteriores, modificamos peticiones con **Tamper Data** como prueba pero no conseguimos nada.

Después de pensar un rato en el mensaje que nos manda, **Access disallowed. You are not logged in**, pensamos que le tenemos que estar enviando algo al servidor que le indica que no estamos logeados y pensamos que el reto puede ser referente a las **COOKIES**

Utilizamos la herramienta **EditThisCookie** en el navegador **Chrome** y observamos que existe un campo  de la cookie que dice:

- **Loggedin** con el valor **0** y encima está desbloqueado por lo que podemos modificarlo

Intentamos ponerle el valor de **1** para que la cookie enviada tenga el parametro **loggedin=1** haciendole creer que ya estamos logeados.

Modificamos la cookie con el valor y pulsamos el boton de refrescarla la venta y nos devuelve un mensaje, pero esta vez es distinto ;)

```html
Access granted. The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1
```

**FLAG** = {aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1}




