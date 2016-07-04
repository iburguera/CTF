#Natas Level 14 → Level 15

Username: natas15

URL:      http://natas15.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas15.natas.labs.overthewire.org** 
- **Usuario    : natas15**
- **Contraseña : AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos muestra un campo en el que tenemos que meter un **usuario** y el programa comprueba si existe en la base de datos o no.

Probamos a meter el usuario **natas15** y nos indica que **NO** existe.

```html
This user doesn't exist.
```
Probamos a meter el usuario **natas16** y nos indica que **SI** existe.

```html
This user exists.
```

Tenemos que conseguir que nos saque por pantalla la contraseña del usuario **natas16** haciendo **SQL Injection** sobre el parámetro **username**

Para ello vamos a ver el código fuente y ver como podemos solucionar el reto.

Vemos que se crea una tabla llamada **users** con los parámetros **username** y **password** 

```sql
CREATE TABLE `users` ( 
  `username` varchar(64) DEFAULT NULL, 
  `password` varchar(64) DEFAULT NULL 
); 
```

Con el código anterior ya y sabiendo que se conecta a la **BBDD** llamada **natas15**, podemos empezar a trabajar en nuestra **$query**.
```sql
 mysql_select_db('natas15', $link); 
```

```php
if(array_key_exists("username", $_REQUEST)) 
{ 
    $link = mysql_connect('localhost', 'natas15', '<censored>'); 
    mysql_select_db('natas15', $link); 
     
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\""; 
    
    if(array_key_exists("debug", $_GET)) 
    { 
        echo "Executing query: $query<br>"; 
    } 

    $res = mysql_query($query, $link); 
    if($res) 
    { 
        if(mysql_num_rows($res) > 0) 
        { 
            echo "This user exists.<br>"; 
        } 
        else 
        { 
            echo "This user doesn't exist.<br>"; 
        } 
    } 
    else 
    { 
        echo "Error in query.<br>"; 
    } 

    mysql_close($link); 
```

Query ejecutada:

```php
$query = "SELECT * from users where username=\"".$_REQUEST["username"]."\""; 
```

Si metemos el parámetro **" OR "1"="1** nos indica que **This user exists.** la que la consulta es un **True** pero no nos sirve de mucho.

¿Como lo hacemos? 

Esta prueba me suena que puede ser un reto de **BLIND SQL Injection**. 

**Blind SQL injection**, es una técnica de ataque que utiliza la inyección SQL. Su evidencia cuando en una página web, por una falla de seguridad, no se muestran mensajes de error al no producirse resultados correctos ante una consulta a la base de datos, mostrándose siempre el mismo contenido (es decir, solo hay respuesta si el resultado es correcto).

En nuestro caso nos dice si el usuario existe o no existe con mensajes **This User Exists** o **This user doesn't exist**

Como en esta ocasión tenemos un solo campo, tenemos que agregar más código al parámetro **Username** para que nos permita jugar con el parámetro **password**

Para ello tendremos que crear algo así:

```php
natas16" AND password ...
````

La técnica de Blind SQL Injection nos va a permitir recibir mensajes de usuario **correcto** o **incorrecto** dependiento de los argumentos que les pasemos, por lo tanto tenemos que crear una consulta para el parámetro **password** que nos indique si la contraseña esta bien o mal.

Mejor que esté bien o mal, vamos a optar por indicarle si la contraseña **contiene** o **empieza** con algún caracter. 

Para eso utilizaremos la opción de sql **LIKE BINARY** que nos indica si una cadena de caracteres específica coincide con un patrón especificado. En este casi si la contraseña empieza con el valor **a**

```php
natas16" AND password LIKE BINARY "a%" "
```

- Si la respuesta es **This user exists** significa que la contraseña del usuario **natas16** empieza por **a.........**
- Si la respuesta es **This user doesn't exist** significa que la contraseña no empieza por esa letra.

Hacer esto a mano sería una autentica tortura, así que haciendo uso de un script en **python** hacemos un programa que automatice todo este proceso. 

Sabemos que tenemos que conseguir una contraseña de **32 caracteres** de longitud

Lo llamaremos **BlindNatas15Injector.py**

```python
```


```php







natas16" AND password LIKE BINARY "W%" "










