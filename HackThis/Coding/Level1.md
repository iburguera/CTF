#HackThis - Coding -  Level 1

URL:      https://www.hackthis.co.uk/levels/coding/1

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
The words have been jumbled up, your task is to write some code to return them to alphabetical order. Then submit your answer in the same format, for example: ant, badger, cattle, zebra. You have 5 seconds to complete the mission.
```

## Explicación

En este reto de programación, tenemos que ordenar una lista de palabras que nos propocionan en un textarea. 

La lista pone las palabras de forma aleatoria por lo que tendremos que programar un bot para que haha lo siguiente:

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

```python
#---------------------------------------------------------------------------------------
#						HACKTHIS CODING LEVEL 1 PYTHON SCRIPT
#---------------------------------------------------------------------------------------
#
#	|--------------------------------------------------|
#	|[+] HackThis Coding Level1 Python Script Example  |
#	|[+] Written by: Iker Burguera                     |
#	|[+] Version: 1.0                                  |
#	|[+] Email me @: ikerburguera@gmail.com            |
#	|--------------------------------------------------|
# 
#---------------------------------------------------------------------------------------

from selenium import webdriver
import time

baseURL  = "https://www.hackthis.co.uk/"																	# Pagina web Login retos HackThis
levelURL = "https://www.hackthis.co.uk/levels/coding/1"														# Pagina web Nivel Coding 1
username = "delmer"																							# Nuestro usuario
password = "" 																								# Poner la contraseña del reto

xpaths = { 'username' 		: "//*[@id=\"username\"] ",     												# XPath del Campo de Email
           'password' 		: "//*[@id=\"password\"]",	  													# XPath del Campo de Contrasena	
           'submitLogin' 	: "//*[@id=\"login_form\"]/input[3]",       									# XPath del Boton de Submit Login
           'unorderedList'	: "//*[@id=\"main-content\"]/div/div[2]/div[2]/form/fieldset/textarea[1]",      # XPath del textarea con lista DESORDENADA 
           'orderedList'	: "//*[@id=\"main-content\"]/div/div[2]/div[2]/form/fieldset/textarea[2]",      # XPath del textarea con lista ORDENADA
           'submitLevel'    : "//*[@id=\"main-content\"]/div/div[2]/div[2]/form/fieldset/input"				# Xpath del Boton de Submit Nivel
         }

profile = webdriver.FirefoxProfile()												# Creamos el WebDriver con Firebox 
profile.accept_untrusted_certs = True												# Aceptamos certificados desconocidos. Selenium da un error si no lo haces
mydriver = webdriver.Firefox(firefox_profile=profile)								# Cargamos el perfil que hemos creado a nuestro webdriver
mydriver.get(baseURL)																# Asignamos el URL al webDriver para que pueda trabajar con ello
mydriver.maximize_window()															# Ponemos la ventana a maxima resolucion

mydriver.find_element_by_xpath(xpaths['username']).clear()							# Limpiamos el campo de Email si tenemos puesto el Remember me
mydriver.find_element_by_xpath(xpaths['username']).send_keys(username)				# Mandamos el dato Email
mydriver.find_element_by_xpath(xpaths['password']).clear()							# Limpiamos el campo de Password si tenemos puesto el Remember me
mydriver.find_element_by_xpath(xpaths['password']).send_keys(password)				# Mandamos el dato Password
mydriver.find_element_by_xpath(xpaths['submitLogin']).click()						# Hacemos click en el boton

mydriver.get(levelURL)																# Accedemos a la URL del Nivel Coding 1

webElement = mydriver.find_element_by_xpath(xpaths['unorderedList'])				# Obtenemos el WebElement que contiene las palabras
unorderedList = webElement.get_attribute('value')									# Obtenemos los valores de ese Web Element

orderedList = sorted(unorderedList.split(', '))										# Separamos la lista por ESPACIOS y COMAS para luego ordenarla correctamente
orderedList = ", ".join(orderedList)												# Juntamos la lista ordenada en el formato que nos indica el reto con espacio y comas-> "Then submit your answer in the same format, for example: ant, badger, cattle, zebra"

mydriver.find_element_by_xpath(xpaths['orderedList']).send_keys(orderedList)		# Introducimos el valor en el campo de listaOrdenada
mydriver.find_element_by_xpath(xpaths['submitLevel']).click()						# Hacemos click en el boton para enviarlo y pasar la prueba
```

Ejecutamos el código en la consola, nos abre el navegador y vamos viendo como el bot que hemos programado va resolviendo el reto :sunglasses: :beers:
