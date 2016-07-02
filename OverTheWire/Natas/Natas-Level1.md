Natas Level 0 → Level 1

Username: natas1
URL:      http://natas1.natas.labs.overthewire.org

##Write Up Iker

Abrimos un navegador y nos conectamos a la página: 

- **URL        : http://natas1.natas.labs.overthewire.org** 
- **Usuario    : natas1**
- **Contraseña : gtVrDuiDfck831PqWsLEZy5gyDz1clto**

La contraseña la hemos sacado del nivel anterior.

Accedemos a la página y nos sale el siguiente mensaje: 

```html
You can find the password for the next level on this page, but rightclicking has been blocked!
```

Nos dice que podemos encontrar la contraseña del siguiente nivel en esta página pero diciendonos que esta vez no podemos utilizar el botón derecho del ratón para ver el ódigo fuente de la página ya que está bloqueado.

Como tenemos el plugin **FIREBUG** en nuestro navegador instalado, lo activamos y vamos a ver el código fuente de la página y obtenemos la password que está oculta. 

```html
<!--The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi -->
```

**FLAG** = {ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi}
