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

Primero que nada vemos 3 funciones:

- **loadData($def)**
 - Carga los valores del parámetro **data** de la cookie que le enviamos para cifrarla con **XOR** 
 - ```php $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true); ```
- **xor_encrypt($in)**
 - Recibe un valor y cifra ese valor con una **$key** que no nos muestran
 - Devuelve el valor cifrado 
- **saveData($d)**
 - Guarda la información que le pasemos en la variable **$data** para que luego pueda comparar y ver si tiene que mostrar la password o no
 
La primera función que se cargar es **loadData($def)** que básicamente carga el valor en **Base64** de la **Cookie** y la pasa por la función **xor_encrypt($in)** después de hacerlo un **base64_decode**. A continuación **Decodifica ese valor a **JSON**

```php
$tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);
```

Vamos a ver con la herramienta **EditThisCookie** que valor tiene la variable **$_COOKIE["data"]**

```php
ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw
```

Vamos analizar la función **xor_encrypt($in)** pero antes que eso necesitamos saber como funciona un **XOR** y ver como podemos aprovechar para sacar lo que no necesitemos.

```bash 
TEXTO ORIGINAL (XOR) KEY = TEXTO CIFRADO (Valor en Cookie)
````

Para sacar la clave **KEY** necesitamos hacer lo siguiente

```bash 
TEXTO ORIGINAL (XOR) TEXTO CIFRADO (Valor en Cookie) = KEY 
````

En este caso nuestro **TEXTO ORIGINAL** es el asignado a la variable **$defaultdata**

```php
array( "showpassword"=>"no", "bgcolor"=>"#ffffff");
```

El cual tenemos que conseguir que sea:

```php
array( "showpassword"=>"yes", "bgcolor"=>"#ffffff");
```

¡Hora de programa un poco! :smile:

Vamos a programar un código en **PHP** que nos devolverá la **KEY** con la que ha estado codificando el texto en la función **xor_encrypt**

```php
 <?  

 function xor_encrypt($in) 
 {  
   $text = $in;  
   $key = json_encode(array( "showpassword"=>"no", "bgcolor"=>"#ffffff"));      
   $outText = '';  
   
   for($i=0;$i<strlen($text);$i++) 
   {  
   		$outText .= $text[$i] ^ $key[$i % strlen($key)];  
   }  
   return $outText;  
 } 

$texto_original = base64_decode('ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw'); 
$clave 			= xor_encrypt($texto_original);

print "La clave utilizada es: $clave";
?>
```

Nos devuelve el siguiente valor:

```php
 La clave utilizada es: qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq
```

Nos devuelve la **clave** o **key** -> **qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq** .

Vemos que se repite el patrón -> **qw8J** 

De momento lo dejamos así para probar luego más adelante.

Ya tenemos la **key** con la que cifra el texto la función **xor_encrypt** así que ahora sólo nos queda crear el **texto_modificado** pasandole **json_encode** para crear el contenido que **escribiremos** en la **cookie** y después enviaremos para que nos muestre la contraseña:

Tenemos las variables que tenemos necesarias:

```php
$texto_modificado = json_encode(array( "showpassword"=>"yes", "bgcolor"=>"#ffffff"));
$key = "qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq"
//$key = "qw8J"
```

NOTA: Como no se cual de las dos claves puede ser, si la **cadena entera** o **el patrón**, pongo la dos y pruebo el resultado

Tenemos que escribir un código en **PHP** para que nos cree el contenido que escribiremos en la **cookie**

```php
 <?

 function xor_encrypt() 
 {  
   $texto_modificado = json_encode(array( "showpassword"=>"yes", "bgcolor"=>"#ffffff"));
   $key = "qw8J";

   $salidaTexto = '';  
 
   for($i=0;$i<strlen($texto_modificado);$i++) 
   {  
   	$salidaTexto .= $texto_modificado[$i] ^ $key[$i % strlen($key)];  
   }  
   return $salidaTexto;  
 }  

 $valorNuevaCookie = base64_encode(xor_encrypt());

 print "El valor de la nueva cookie tiene que ser: $valorNuevaCookie"; 

 ?>
```

NOTA: Después de pasar la prueba, hemos comprobado que utiliza **EL PATRÓN** y no la cadena de texto entera para realizar el **XOR** y por ese motivo hemos puesto el valor de la **$key = "qw8J"**

Al igual que en anteriores niveles, ejecutamos el código que hemos escrito en alguna página web que nos permita testear código PHP online. En este caso, hemos vuelto a utilizar el **PHP Sandbox**

```html
http://sandbox.onlinephpfunctions.com/
```

Obtenemos la salida de texto: 

```html
El valor de la nueva cookie tiene que ser: ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK
```

Comparamos los valores de la **Nueva Cookie** y la **Antigua Cookie**

- **Antigua Cookie**
 - texto_original = array( "showpassword"=>"no", "bgcolor"=>"#ffffff")
 - valor_Cookie = **ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw**

- **Nueva Cookie** 
 - texto_modificado = array( "showpassword"=>"yes", "bgcolor"=>"#ffffff")
 - valor_Cookie = **ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK**


 












 




