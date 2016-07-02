#Natas Level 0

Username: natas0

Password: natas0

URL:      http://natas0.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas0.natas.labs.overthewire.org** 
- **Usuario    : natas0**
- **Contraseña : natas0**

Accedemos y nos sale un mensaje indicando que podemos encontrar la contraseña para el siguiente nivel en la misma página:

```html
You can find the password for the next level on this page.
```

Miramos el código fuente de la página y observamos que tiene un campo oculto  en el cual aparece nuestra contraseña :)

```html

<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas0", "pass": "natas0" };</script></head>
<body>
<h1>natas0</h1>
<div id="content">
You can find the password for the next level on this page.

<!--The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto -->
</div>
</body>
</html>
```

**FLAG** = {gtVrDuiDfck831PqWsLEZy5gyDz1clto}
