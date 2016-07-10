#HackThis - Main -  Level 6

URL:      https://www.hackthis.co.uk/levels/main/6

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
This page is coded to only let in one user (Ronald). But there is no Ronald?! You will need to find a way to add him to the list.
```

## Explicación

Accedemos a la página web y observamos que nos piden que registremos con el usuari **Ronald**.

Observamos en menu despegable que nos proporcionan pero nos damos cuenta de que no exite el usuario Ronald entre ellos


```html
<select id="user" name="user">
    <option>John</option>
    <option>Petter</option>
    <option>David</option>
    <option>Sam</option>
</select>
```

Tenemos que conseguir cambiar el valor de alguno de esos campos al valor de **Ronald**. ¿Pero como?

Por suerte, Google Chrome viene con **Herramientas del desarrollador** instaladas que nos permiten manipulas el contenido de estos campos.

Iniciamos las herramientas del desarrollador y cambiamos cualquier valor por el de **Ronald** 

```html
<select id="user" name="user">
    <option>John</option>
    <option>Petter</option>
    <option>David</option>
    <option>Ronald</option>
</select>
```

Los introducimos en el campo de texto y vemos que las credenciales con el usuarios Ronald es válida y pasámos el reto :smile:

**FLAG** = {Ronald}
