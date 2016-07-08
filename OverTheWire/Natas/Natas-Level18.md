#Natas Level 17 → Level 18

Username: natas17

URL:      http://natas17.natas.labs.overthewire.org

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

Así que vamos a seguir mirando el código fuente para ver como podemos hacerle creer que somos los usuarios **admin**

Vamos a ver si podemos hacer algo con las **COOKIES** 

Vemos que el valor de la **COOKIE** para el campo **PHPSESSID** es **93**

```php
PHPSESSID = 93
```




