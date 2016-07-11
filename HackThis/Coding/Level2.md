#HackThis - Coding -  Level 2

URL:      https://www.hackthis.co.uk/levels/coding/2

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
A string has been encoded using a very simple custom encryption method, [explained here](https://www.hackthis.co.uk/levels/extras/p2.txt), decrypt the message. You have a 5 second time limit for each attempt.
```

## Explicación

En este reto de programación, tenemos que sacar los número de una lista de números previamente cifrados que nos propocionan en un textarea y seguir los pasos que nos indican en el siguiente texto para sacar la contraseña

```html
            ___  ____  _  _  ____  ____    _  _   __  
           / __)(  _ \( \/ )(  _ \(_  _)  / )( \ /  \ 
          ( (__  )   / )  /  ) __/  )(    \ \/ /(_/ /           
           \___)(__\_)(__/  (__)   (__)    \__/  (__) 

X-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-X

 Another file from:                               the.almighty

 Set out below is a guide on to how to 100% securely encrypt
 your data, this is just an idea and no working program has
 been create as of yet.


 1.  Re-number all visible ascii characters, so ! will now be
     1 instead of 33 and " will be 2 instead of 34 and so on

 2.  Get each letter of your string and do the following:
         a: Get its new ascii code value
         b: Take this value, and subtract it from the total
            number of visible ASCII characters
         c: Get the character at this position
         d: Get this characters original ascii value
 
 3.  Put all these values in a csv e.g. 61,72,71

 Extras
     All non-visible characters just appear as they are
     e.g. space will just be blank 61, ,72,71


             As this is stil in early development
        we can not be held responsible for any errors.
             For more info visit www.almighty.com

                 "Play hard, and hack harder"
  
X-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-X
```



La lista pone las palabras de forma aleatoria por lo que tendremos que programar un bot para que haga lo siguiente:

1. Hacer Login a la página del Reto
2. Acceder a la URL del Nivel 1 de Coding
3. Conseguir la lista de palabras desordenadas que nos muestran
4. Ordenar la lista de palabras
5. Enviar el contenido para pasar el reto

Como de costumbre vamosa utilizar **Python** para programar un **BOT** y **Firefox** como navegador predeterminado

Tenemos que tener instalado el paquete **Selenium** que podemos encontrarlo su Web: [Selenium](https://pypi.python.org/pypi/selenium)

Podemos instalarlo desde la consola utilizando el siguiente comando

```bash
pip install -U selenium
```

El siguiente código está comentado por lo que será más fácil entenderlo. 

NOTA: Utilizar [este enlace](http://www.abodeqa.com/2012/10/07/using-firebug-in-selenium-webdriver-to-find-xpath-and-css-selector/) si no sabéis como sacar los **XPATH** de los elementos 
