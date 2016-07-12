#HackThis - Real -  Level 1

URL:      https://www.hackthis.co.uk/levels/real/1

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint
The target is addicted World of Peacecraft and it will really screw him over if you could get access to his account. You have got access to a targets email* account:

email*

## Explicación

Nos indican que tenemos que acceder a la cuenta del juego **World of Peacecraft**  usuario del que nos proporcionan acceso a su correo electrónico

```html
https://www.hackthis.co.uk/levels/extras/real/1/
```

Accedemos a un cliente de correo online en el que podemos ver dos correos

1. Activación de la cuenta
2. Cosas privadas e íntimas del usuario xD :smile:

Hacemos click en el correo de activación de la cuenta y nos lleva a una pantalla donde sólamente aparece un cuadro de texto y un botón de submit.

Parece ser que es ahí donde tenemos que introducir la contraseña  del usuario.

¿Pero donde está la contraseña que necesitamos?

Volvemos a la página principal del cliente de correo online y vemos en el menú de la izquierda otro enlace a los correos que están en la basura.

Accedemos y observamos que el usuario ha eliminado la contraseña moviendola a la papelera pero no ha vaciado la papelera.

Miramod el contenido del correo y nos aparece que la contraseña es 

```html
iamgod
```

Volvemos a la página de activación de la cuenta e introduciendo ese valor, nos indica que hemos pasado el reto :sunglasses:

**FLAG** = {iamgod}

