#Natas Level 1 → Level 2

Username: natas2

URL:      http://natas2.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas2.natas.labs.overthewire.org** 
- **Usuario    : natas2**
- **Contraseña : ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos sale el siguiente mensaje: 

```html
There is nothing on this page 
```

Miramos el código fuente y observamos que carga imagen de un pixel desde el directorio **/files**

```html
<body>
<h1>natas2</h1>
<div id="content">
There is nothing on this page
<img src="files/pixel.png">
</div>
</body>
```

Modificamos la URL para ver si nos devuelve el contenido no solo del fichero **pixel.png** sino de todo el directorio **/files/**

```html
http://natas2.natas.labs.overthewire.org/files/
```

Accedemos y vemos que nos muestra dos ficheros: 

- **pixel.png**
- **users.txt**

Pulsamos sobre el fichero de texto de los usuarios y miramos su contenido:

```bash
# username:password
alice:BYNdCesZqW
bob:jw2ueICLvT
charlie:G5vCxkVV3m
natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
eve:zo4mJWyNj2
mallory:9urtcpzBmH
```

Observamos que el password para el usuario **natas3** es **sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14**

**FLAG** = {sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14}

