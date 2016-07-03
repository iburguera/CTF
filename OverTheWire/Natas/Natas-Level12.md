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



 












 




