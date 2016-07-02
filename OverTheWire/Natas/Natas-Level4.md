##Natas Level 3 → Level 4

Username: natas4

URL:      http://natas4.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas4.natas.labs.overthewire.org** 
- **Usuario    : natas4**
- **Contraseña : Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos sale el siguiente mensaje: 

```html
Access disallowed. You are visiting from "" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/" 
```

El mensaje que nos muestra nos indica que tenemos el acceso denegado porque visitamos la página desde:

```html
** "" ** (un campo vacío).
```

Solamente podrán entrar los usuarios que vengan de:

```html
http://natas5.natas.labs.overthewire.org/
```

Parece que le tendremos que pasa esa URL como parámetro. Probamos a modificar la URL poniendole algunos parámetros y nos devuelve el siguiente mensaje.

```html
Access disallowed. 
You are visiting from 
"http://natas4.natas.labs.overthewire.org/?index.php?viewsource=patxiii" 
while authorized users should come only from 
"http://natas5.natas.labs.overthewire.org/"
```

¿Pero como vamos a acceder desde natas5 si todavia no tenemos acceso!? 

Bueno tendremos que **engañarle** haciendo un pequeño **spoofing** a la hora de realizar un **request** a la página haciendonos pasar como que venimos el **nivel 5**

Para ello utilizamos un **plugin** o **herramienta** llamada **Tamper Data** que podemos instalarla en nuestro navegador **Firefox**.

También podemos utilizar la herramienta **Burp** si estamos trabajando en un **Kali Linux** ;)

La instalamos y la ejecutamos al darle **Refresh** en la página. El plugin intercepta la petición y nos muestra una ventana con los parámetros que podemos modificar.

En este caso queremos modificar el parámetro **Referer** el cual contiene el valor de donde venimos. Lo modificamos y enviamos la petición para ver si hemos podido modificar el contenido de la petición

```html
Access disallowed. 
You are visiting from 
"http://natas5.natas.labs.overthewire.org/index.php"
while authorized users should come only from 
"http://natas5.natas.labs.overthewire.org/"
```

Vaya, hemos puesto mal la URL, le hemos añadido el **index.php** al final, pero esto nos sirve para comprobar que efectivamente podemos modificar la petición el servidor.

Ahora nos aseguramos de escribir correctamente la URL y enviamos de nuevo la petición.

Esta vez accedemos y nos muestra un mensaje muy bonito :)

```html
Access granted. The password for natas5 is iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq 
```

**FLAG** = {iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq}

