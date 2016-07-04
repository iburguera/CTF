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




 












 




