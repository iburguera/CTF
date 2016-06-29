#[5/6]  Level 5: Breaking protocol

##Mission Description

Cross-site scripting isn't just about correctly escaping data. Sometimes, attackers can do bad things even without injecting new elements into the DOM.

##Mission Objective

Inject a script to pop up an alert() in the context of the application.

## Write Up Iker 

En esta ocasion tenemos que registrarnos con nuestro correo y hacer salta la alerta con algún parámetro injectable en el código.
Vamos a ver que nos muestra el código **welcome.html*

```html 
 <a href="/level5/frame/signup?next=confirm">Sign up</a> 
```

Que nos lleva a la siguiente dirección:

```html
https://xss-game.appspot.com/level5/frame/signup?next=confirm 
```

Observando el código de ```confirm.html```, ```signup.html```y ```level.py``` vemos que el código **window.location** se basa en el parámetro **next**
```html
<a href="{{ next }}">Next >></a>
```

```python
# Route the request to the appropriate template
    if "signup" in self.request.path:
      self.render_template('signup.html', 
        {'next': self.request.get('next')})
    elif "confirm" in self.request.path:
      self.render_template('confirm.html', 
        {'next': self.request.get('next', 'welcome')})
    else:
      self.render_template('welcome.html', {})
```
```javascript
<script>
      setTimeout(function() { window.location = '{{ next }}'; }, 5000);
    </script>
```

Tras investigar un poco en Google hemos llegado a la conclusión de que puede ser un ataque **DOM Based XSS** 
-https://www.owasp.org/index.php/DOM_Based_XSS

Como ya sabemos que el código **window.location** ejecutará el código que pongamos en la variable **next**, podemos hacer que la variable next ejecute directamente la alerta con el siguiente código:

```javascript
javascript:alert('CARACOL FUNTZIONA!')
```
Quedando como resultado final la siguiente URL:

```html
https://xss-game.appspot.com/level5/frame/signup?next=javascript:alert('CARACOL FUNTZIONA!')
````

La URL modificada nos lleva al a página para rellenar el formulario con nuestro correo en el campo **enter email** y pulsamos en **Next**.
Observamos como se ejecuta la alerta que hemos introducido al campo **Next** :) 

Iker Burguera

```
