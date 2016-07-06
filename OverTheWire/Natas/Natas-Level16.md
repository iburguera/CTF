#Natas Level 15 → Level 16

Username: natas16

URL:      http://natas16.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas16.natas.labs.overthewire.org** 
- **Usuario    : natas16**
- **Contraseña : WaIHEacj63wnNIBROHeqi3p9t0m5nhmh**

La contraseña la hemos sacado del nivel anterior.

Entramos en la página web y nos muestra un mensaje parecido a la prueba anterior indicando que se han filtrado incluso más caracteres que en la prueba anterior.

```html
For security reasons, we now filter even more on certain characters

Find words containing: 
Search

Output:
```

Encontramos un campo de texto donde podemos buscar palabras dentro de un fichero, al igual que hicimos en alguna prueba anterior.

Antes de meternos en harina, vamos a mirar el código fuente y ver que han podido cambiar.

```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) 
{
    $key = $_REQUEST["needle"];
}

if($key != "") 
{
    if(preg_match('/[;|&`\'"]/',$key)) 
    {
        print "Input contains an illegal character!";
    } else 
    {
        passthru("grep -i \"$key\" dictionary.txt");
    }
}
?>
```

Vamos a comparar con la prueba nº 10 de Natas en la que también filtraban los caracteres:

Natas10
```php
if(preg_match('/[;|&]/',$key))
```
Natas16
```php
if(preg_match('/[;|&`\'"]/',$key)) 
```

Al igual que en la prueba Natas10 intentamos poner la mascara Wildcard(.*) y vemos que nos devuelve el contenido de todo el fichero.

Intentamos hacer el mismo truco poniendo el siguiente comando, pero no nos funciona.

```bash
.* /etc/natas_webpass/natas17
```

Tenemos que intentar otra cosa. Vamos a analizar que caracteres filtra y podríamos sacar provecho de lo que no filtra.

Filtra los valores ```bash (;, |, &, `, ', ")``` pero no los valores **$** y **()** entre otros. 

Investigando un poco por internet nos encontramos un comando o truco en bash que nos puede servir de ayuda.

El siguiente comando
```bash 
`cat /etc/natas_webpass/natas17`
```
es lo mismo que 

```bash 
$(cat /etc/natas_webpass/natas17)
```

Nos fijamos que no utilizamos ningún caracter prohibido de la lista que han bloqueado y podemos obtener los mismos resultados. 

Bien, hemos pasado el primer filtro y ahora tenemos que montar la consulta para que nos muestre la contraseña del siguiente nivel.





