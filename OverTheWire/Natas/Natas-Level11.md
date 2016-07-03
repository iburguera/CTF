#Natas Level 10 → Level 11

Username: natas11

URL:      http://natas11.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas11.natas.labs.overthewire.org** 
- **Usuario    : natas11**
- **Contraseña : U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK**

La contraseña la hemos sacado del nivel anterior.

Entramos a la prueba y nos muestra un formulario donde nos deja cambiar el color de background de la página web. También nos dicen que las **Cookies** están protegidas con cifrado **XOR**

```html
Cookies are protected with XOR encryption

Background color: 
#cc9900
 Set color
```
Con esta pista, ya sabemos que el reto tiene algo que ver con las **COOKIES**
Vamos a ver que vemos el código fuente:

```php
<?
$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");

function xor_encrypt($in) 
{
    $key = '<censored>';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) 
    {
      $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }
    return $outText;
}

function loadData($def) 
{
    global $_COOKIE;
    $mydata = $def;
    if(array_key_exists("data", $_COOKIE)) 
    {
    $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);
    if(is_array($tempdata) && array_key_exists("showpassword", $tempdata) && array_key_exists("bgcolor", $tempdata)) 
    {
        if (preg_match('/^#(?:[a-f\d]{6})$/i', $tempdata['bgcolor'])) 
        {
          $mydata['showpassword'] = $tempdata['showpassword'];
          $mydata['bgcolor'] = $tempdata['bgcolor'];
        }
    }
    }
    return $mydata;
}

function saveData($d) 
{
    setcookie("data", base64_encode(xor_encrypt(json_encode($d))));
}

$data = loadData($defaultdata);

if(array_key_exists("bgcolor",$_REQUEST)) 
{
    if (preg_match('/^#(?:[a-f\d]{6})$/i', $_REQUEST['bgcolor']))
    {
        $data['bgcolor'] = $_REQUEST['bgcolor'];
    }
}
saveData($data);
?>

<h1>natas11</h1>
<div id="content">
<body style="background: <?=$data['bgcolor']?>;">
Cookies are protected with XOR encryption<br/><br/>

<?
if($data["showpassword"] == "yes") 
{
    print "The password for natas12 is <censored><br>";
}
?>

<form>
Background color: <input name=bgcolor value="<?=$data['bgcolor']?>">
<input type=submit value="Set color">
</form>

<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
```

Bueno parece que tenemos trabajo en esta prueba. 

Primero vemos que tenemos un array llamado **$defaultdata**.

```php
$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");
````

Tiene dos parámetros:

- **bgcolor**: Almacena el valor que tendrá el background 
- **showpassword**: 
 - **no**  -> Si el valor está en **no** no muestra la password.
 - **yes** -> Si el valor está en **yes** si muestra la password.
 
Tenemos que conseguir que **showpassword** de la variable **$data** tenga el valor **yes** para que nos muestre la contraseña. Vamos a ver como lo conseguimos.

```php
if($data["showpassword"] == "yes") 
{
    print "The password for natas12 is <censored><br>";
}
```

NOTA: El valor **$data["showpassword"] == "yes"** tiene que ser de la variable **$data** y no de la variable **$defaultdata** ya que esta última es para inicializar las variables y luego con la función **loadData** cargar estos parámetros en **$data**

```php
$data = loadData($defaultdata);
```

Vamos a leer con detenimiento el código y aclararnos que es lo que hace.
 




