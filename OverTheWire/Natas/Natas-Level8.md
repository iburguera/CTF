#Natas Level 7 → Level 8

Username: natas8

URL:      http://natas8.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas8.natas.labs.overthewire.org** 
- **Usuario    : natas8**
- **Contraseña : DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe**

La contraseña la hemos sacado del nivel anterior.

Entramos a la página web y observamos que tenemos un **input** al igual que en un nivel anterior en el que tenemos que introductor un texto **secreto** y nos devolverá la contraseña para el siguiente nivel.

Primero que nada, miramos el código fuente de la página:

```html
<body>
<h1>natas8</h1>
<div id="content">

<?

$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
    print "Access granted. The password for natas9 is <censored>";
    } else {
    print "Wrong secret";
    }
}
?>

<form method=post>
Input secret: <input name=secret><br>
<input type=submit name=submit>
</form>

<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
```

Bien, parece que utiliza el texto almacenado en la variable **$encodedSecret = "3d3d516343746d4d6d6c315669563362";** como valor a comparar y validar la contraseña.

Vemos que la página recoge el texto que hemos metido en la página anterior y lo pasa por la función **encodeSecret** y la compara con el valor que está en la variable **encodedSecret**

```php
 if(encodeSecret($_POST['secret']) == $encodedSecret) 
```

Vamos a analizar que es lo que hace la función de codificar la clave:

```php
function encodeSecret($secret) 
{
    return bin2hex(strrev(base64_encode($secret)));
}
```

NOTA: Son comandos **PHP**

Analizamos los pasos:

- 1 Recibe el valor de la variable **$secret**
- 2 **Codifica** ese valor en **Base64**
- 3 El comando **strrev**, **invierte** el valor obtenido del paso 2
- 4 El texto invertido en el paso 3, se pasa por el comando **bin2hex** convierte datos binarios en su representación hexadecimal
- 5 Devuelve el texto

Tenemos la variable **$encodedSecret = "3d3d516343746d4d6d6c315669563362";** con el valor en **Hexadecimal** que previamente habrá creado el administrador y con el que se compara nuestro texto introducido.

Teniendo esto en cuenta, tenemos que hacer el proceso **inverso**, es decir, **Decodificar** la contraseña **$encodedSecret = "3d3d516343746d4d6d6c315669563362";**

Vamos a ver que pasos tenemos que seguir para **decodificar** la contraseña:

- 1 Obtenemos el valor de la variable **$encodedSecret = "3d3d516343746d4d6d6c315669563362";**
- 2 Decodificamos ese valor **Hexadecimal** a **Binario** con el comando **hex2bin**
- 3 **Invertimos** el valor obtenido con **strrev**, que será un valor **Base64 invertido** en el paso 2 para que vuelva a ponerse en su forma no invertida
- 4 Cogemos el valor obtenido en el paso 3 y lo **decodificamos** con el comando **base64_decode**
- 5 Devolvemos el texto con la contraseña

Sabiendo lo pasos, vamos a **programar** el código **PHP** con la función **decodeSecret()** que nos proporcionará la contraseña decodificada.

```php
<?

$encodedSecret = "3d3d516343746d4d6d6c315669563362";
$decodedSecret = "";

function decodeSecret($encodedSecretPass) 
{
    return base64_decode(strrev(hex2bin($encodedSecretPass)));
}

$decodedSecret = decodeSecret($encodedSecret); 

print "La contraseña es: $decodedSecret" 

?>
```

Ya tenemos el decodificador programado y ahora lo tenemos que ejecutar para que nos devuelve el valor correspondiente.

No es necesario montar un **LAMP** en alguna máquina virtual o servidor, ya que hay múltiples herramientas que te permiten testear el código php online.

Yo por ejemplo he utilizado la siguiente:

```html
http://sandbox.onlinephpfunctions.com/
```

Ponemos el código que acabamos de programar y nos muestra la **Contraseña decodificada** que tenemos que meter para nos devuelva la flag del siguiente nivel.

```php
La contraseña es: oubWYf2kBq
```

Vamos a la página anterior e introducimos esa contraseña y obtenemos la contraseña del siguiente nivel :)

```html
Access granted. The password for natas9 is W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl
```

**FLAG** = {W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl}
