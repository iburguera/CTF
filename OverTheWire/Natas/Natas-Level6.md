#Natas Level 5 → Level 6

Username: natas6

URL:      http://natas6.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas6.natas.labs.overthewire.org** 
- **Usuario    : natas6**
- **Contraseña : aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos sale un campo de texto y un formulario indicando que tenemos que poner un **secreto**

```html
Input secret: <textarea>

Enviar <submit button>
```

También nos deja ver el código fuente con un enlace y empezamos a analizarlo.

```html
<body>
<h1>natas6</h1>
<div id="content">

<?

include "includes/secret.inc";

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
?>

<form method=post>
Input secret: <input name=secret><br>
<input type=submit name=submit>
</form>

<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
```

Parece que tenemos que enviar un texto y la página va a compararlo con el contenido de la variable **$secret**  importada desde en el directorio **include "includes/secret.inc**

Podemos hacer dos cosas:

  - 1 Fuerza Bruta sobre el input (Nos llevaría mucho tiempo)
  - 2 Mirar el contenido del fichero **includes/secret.inc** 
  
Obviamente elegimos la segunda opción ;)

Montamos la URL quedando la siguiente:

```html
http://natas6.natas.labs.overthewire.org/includes/secret.inc
```

y vemos que el contenido del fichero es muy interesante :)

```php
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```
Pero **OJO!** Esta no es la **FLAG** sino el texto que tenemos que poner en el **input** para que nos devuelva la contraseña del siguiente nivel :)

La ponemos y nos devuelve la contrase del usuario **nata7**

```html
Access granted. The password for natas7 is 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9
```
**FLAG** = {7z3hEENjQtflzgnT29q7wAvMNfZdh0i9}
