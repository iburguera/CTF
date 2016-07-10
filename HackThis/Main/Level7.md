#HackThis - Main -  Level 7

URL:      https://www.hackthis.co.uk/levels/main/7

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
The password is again stored in a txt file. This time however it is not as straight forward as viewing the source.

You wouldn't even find the page by using a search engine as search bots have been excluded.
```

## Explicación

Accedemos a la página web y observamos que nos piden que introduzcamos un **usuario** y una **Contraseña**.   

Nos dicen que la contraseña está oculta en un fichero **TXT** pero que no es tan sencillo como mirarlo en el código fuente de la web.

Sabemos que el fichero **Robots.txt** pueden ser de gran ayuda para ver información adicional a la página web y mostrar directorios que no quieren que veamos ;)

Accedemos y vemos lo siguiente

```html
User-agent: *
Allow: /
Disallow: /contact.php
Disallow: /inbox/
Disallow: /levels/
Disallow: /levels/extras/userpass.txt
Disallow: /users/
Disallow: /ctf/8/php/*

User-agent: Mediapartners-Google
Disallow:

Sitemap: https://www.hackthis.co.uk/sitemap.xml
```

Observando el código, encontramos un campo muy interesante

```html
Disallow: /levels/extras/userpass.txt
```

Como nos ha dicho que tenemos el fichero guardad en un fichero de texto, probablemente esté en ese fichero.

Accedemos a la página web y nos muestra el usuario y la contraseña del reto

```html
https://www.hackthis.co.uk/levels/extras/userpass.txt
```


```html
User: 48w3756
Pass: u3qh458
```
Los introducimos en el campo de texto y vemos que las credenciales son válida y pasámos el reto :smile:

**FLAG** = {48w3756/u3qh458}
