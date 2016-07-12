#HackThis - Real -  Level 2

URL:      https://www.hackthis.co.uk/levels/real/2

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
One of my school chums has got in a spot of bother with their school library. They borrowed a book a long time back and is getting frequent letters asking for the money that he owes for the overdue book. He is a bit on the poor side and doesn't have the money to pay the library. Here is the link to the librarians site, please help.
```

## Explicación

Nos comentan que un compañero de la escuela ha cogido prestado varios libros de la biblioteca que todavía no ha devuelto. Las bibliotecarias están molestas ya qye el plazo de entrega ha expirado y todavía no ha devuelto lo libros. Esto conlleva a una sanción por cada día que pasa pero como nuestro amigo es un poco pobre no puede pagarlo. Nos dejan un enlace a la URL de los bibliotecarios.

```html
https://www.hackthis.co.uk/levels/extras/real/2/login.html
```

Accedemos a la página y vemos dos campos (Usuario/Contraseña) que probablemente utilizarán para veificar el estado de cada usuario.

Vamos a ver el código fuente del reto a ver si nos muestra algo interesante

```javascript
var req, image, status, imagepath;

function loadimage()
{
	var username= document.getElementById('username').value;
	var password= document.getElementById('password').value;
	URL= "members/" + username + " " + password + ".htm";
	path = URL;
	document.getElementById("status").innerHTML = 'Checking details...';

	req = getreq();
	req.onreadystatechange = exists;
	req.open("get", path, true);
	req.send(null);     
}

function exists() 
{
	if(req.readyState == 4) 
	{
		if(req.status == 200) 
		{
			  document.getElementById("status").innerHTML = 'Correct!';
			  document.location = "/levels/real/2?user=" + document.getElementById('username').value + "&pass=" + document.getElementById('password').value;
	  } 
	  else 
	  {
	      document.getElementById("status").innerHTML = 'Incorrect username/password';
	  }
	}
}

function getreq() 
{
  if(window.XMLHttpRequest)
      return new XMLHttpRequest();
  else if(window.ActiveXObject)
      return new ActiveXObject("Microsoft.XMLHTTP");
}
</script>
```

Vemos un código interesante en la función 

```javascript
URL= "members/" + username + " " + password + ".htm";
```







