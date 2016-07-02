##Natas Level 2 → Level 3

Username: natas3

URL:      http://natas3.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas3.natas.labs.overthewire.org** 
- **Usuario    : natas3**
- **Contraseña : sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos sale el siguiente mensaje: 

```html
There is nothing on this page
```

Miramos el código fuente y observamos que nos muestra el mismo mensaje que antes de que no hay nada en esta página

```html
<h1>natas3</h1>
<div id="content">
There is nothing on this page
<!-- No more information leaks!! Not even Google will find it this time... -->
</div>
</body>
```

En esta ocasión no nos proporcionan ninguna información ya que no quieren dar más información debida (No more information leaks!!) sobre donde puede estar la contraseña

Probamos a entrar en el directorio **files** como en el nivel anterior pero no sale un error, no existe pero obtenemos que es un servidor **Apache 2.4.7**

```html
http://natas3.natas.labs.overthewire.org/files/
```

Sabiendo que es un **Apache** miramos si tiene el fichero **robots.txt** y efectivamente lo tiene! :)

```html
http://natas3.natas.labs.overthewire.org/robots.txt
```

El fichero **robots.txt nos permite configurar el servidor Apache para permitir o denegar el mostrar directorios y ficheros en el servidor.

Observamos el contenido del fichero **robots.txt** 

```bash
User-agent: *
Disallow: /s3cr3t/
```

Vaya, parece que alguien ha intentado ocultar el directorio **/s3cr3t/**

Vamos a introducir la URL en el navegador

```html
http://natas3.natas.labs.overthewire.org/s3cr3t
```

Bien! Nos sale un directorio con un fichero llamado **users.txt** al cual accedemos y nos muestra la contraseña del usuario **Natas4** y podemos avanzar al a siguiente nivel

```html
natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
```

**FLAG** = {Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ}



