#Bandit Level 25 → Level 26

##Level Goal

Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

##Commands you may need to solve this level

ssh, cat, more, vi, ls, id, pwd

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG}

Utilizamos esta contraseña para acceder al siguiente nivel.

```bash 
$ ssh bandit25@bandit.labs.overthewire.org
```

Entramos al servidor y vemos que hay una clave privada en el directorio. 

```bash
bandit25@melinda:~$ ls -l
total 4
-r-------- 1 bandit25 bandit25 1679 Nov 16  2014 bandit26.sshkey
```

Que contiene lo siguiente

```bash
-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEApis2AuoooEqeYWamtwX2k5z9uU1Afl2F8VyXQqbv/LTrIwdW
pTfaeRHXzr0Y0a5Oe3GB/+W2+PReif+bPZlzTY1XFwpk+DiHk1kmL0moEW8HJuT9
/5XbnpjSzn0eEAfFax2OcopjrzVqdBJQerkj0puv3UXY07AskgkyD5XepwGAlJOG
xZsMq1oZqQ0W29aBtfykuGie2bxroRjuAPrYM4o3MMmtlNE5fC4G9Ihq0eq73MDi
1ze6d2jIGce873qxn308BA2qhRPJNEbnPev5gI+5tU+UxebW8KLbk0EhoXB953Ix
3lgOIrT9Y6skRjsMSFmC6WN/O7ovu8QzGqxdywIDAQABAoIBAAaXoETtVT9GtpHW
qLaKHgYtLEO1tOFOhInWyolyZgL4inuRRva3CIvVEWK6TcnDyIlNL4MfcerehwGi
il4fQFvLR7E6UFcopvhJiSJHIcvPQ9FfNFR3dYcNOQ/IFvE73bEqMwSISPwiel6w
e1DjF3C7jHaS1s9PJfWFN982aublL/yLbJP+ou3ifdljS7QzjWZA8NRiMwmBGPIh
Yq8weR3jIVQl3ndEYxO7Cr/wXXebZwlP6CPZb67rBy0jg+366mxQbDZIwZYEaUME
zY5izFclr/kKj4s7NTRkC76Yx+rTNP5+BX+JT+rgz5aoQq8ghMw43NYwxjXym/MX
c8X8g0ECgYEA1crBUAR1gSkM+5mGjjoFLJKrFP+IhUHFh25qGI4Dcxxh1f3M53le
wF1rkp5SJnHRFm9IW3gM1JoF0PQxI5aXHRGHphwPeKnsQ/xQBRWCeYpqTme9amJV
tD3aDHkpIhYxkNxqol5gDCAt6tdFSxqPaNfdfsfaAOXiKGrQESUjIBcCgYEAxvmI
2ROJsBXaiM4Iyg9hUpjZIn8TW2UlH76pojFG6/KBd1NcnW3fu0ZUU790wAu7QbbU
i7pieeqCqSYcZsmkhnOvbdx54A6NNCR2btc+si6pDOe1jdsGdXISDRHFb9QxjZCj
6xzWMNvb5n1yUb9w9nfN1PZzATfUsOV+Fy8CbG0CgYEAifkTLwfhqZyLk2huTSWm
pzB0ltWfDpj22MNqVzR3h3d+sHLeJVjPzIe9396rF8KGdNsWsGlWpnJMZKDjgZsz
JQBmMc6UMYRARVP1dIKANN4eY0FSHfEebHcqXLho0mXOUTXe37DWfZza5V9Oify3
JquBd8uUptW1Ue41H4t/ErsCgYEArc5FYtF1QXIlfcDz3oUGz16itUZpgzlb71nd
1cbTm8EupCwWR5I1j+IEQU+JTUQyI1nwWcnKwZI+5kBbKNJUu/mLsRyY/UXYxEZh
ibrNklm94373kV1US/0DlZUDcQba7jz9Yp/C3dT/RlwoIw5mP3UxQCizFspNKOSe
euPeaxUCgYEAntklXwBbokgdDup/u/3ms5Lb/bm22zDOCg2HrlWQCqKEkWkAO6R5
/Wwyqhp/wTl8VXjxWo+W+DmewGdPHGQQ5fFdqgpuQpGUq24YZS8m66v5ANBwd76t
IZdtF5HXs2S5CADTwniUS5mX1HO9l5gUkk+h0cH5JnPtsMCnAUM+BRY=
-----END RSA PRIVATE KEY-----
```

Al igual que en alguna prueba anterior tendremos que utilizar esta clave para acceder al siguiente nivel.

```bash
ikerburguera@MacBook-Pro-de-Iker:~/Desktop$ ssh  bandit26@bandit.labs.overthewire.org -i bandit26.sshkey  

This is the OverTheWire game server. More information on http://www.overthewire.org/wargames
Please note that wargame usernames are no longer level<X>, but wargamename<X>
e.g. vortex4, semtex2, ...
Note: at this moment, blacksun is not available.
...
  _                     _ _ _   ___   __  
 | |                   | (_) | |__ \ / /  
 | |__   __ _ _ __   __| |_| |_   ) / /_  
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
Connection to bandit.labs.overthewire.org closed.
```

Vaya...Nos cierra la conexión. ¿Puede que alguien haya modificado el **.bashrc** para que nos desconecte al entrar?

En alguna prueba anterior hemos llegado a conectarnos a la shell del servidor usando como parámetro **/bin/bash** pero en este caso nos dice el enunciado que el **/bin/bash** es diferente para el usuario **bandit26**

Probamos el comando por si acaso y despejar dudas 

```bash
ikerburguera@MacBook-Pro-de-Iker:~/Desktop$ ssh  bandit26@bandit.labs.overthewire.org -i bandit26.sshkey  -t /bin/bash
...
Connection to bandit.labs.overthewire.org closed.
```

Nos vuelve a desconectar :(

Algo que me parece extraño es que ha salido un banner con el mensaje **Bandit26** al cargarse en la consola. Entiendo que ese banner lo cargará al entrar en el consola desde un fichero de texto y lo muestra en pantalla.

Después de mucho pensar y agotar algunas otra alternativas, se me ocurre que estaría bien que al cargar el banner además del texto **Bandit26** nos apareciese la password del usuario **Bandit26** que probablemente esté ubicada en **/etc/bandit_pass/bandit26**

Miramos el fichero **/etc/passwd** para ver la shell que ejecuta el usuario **bandit26**

```bash
bandit25@melinda:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@melinda:~$ cat /etc/passwd | grep bandit25
bandit25:x:11025:11025:bandit level 25:/home/bandit25:/bin/bash
bandit25@melinda:~$ cat /etc/passwd | grep bandit24
bandit24:x:11024:11024:bandit level 24:/home/bandit24:/bin/bash
```

Tal y como nos decía el enunciado, el usuario **bandit26** utiliza otra **shell** diferente a los demás usuarios **/usr/bin/showtext**

Vamos a ver que contiene el fichero

```bash
bandit25@melinda:~$ file /usr/bin/showtext
/usr/bin/showtext: POSIX shell script, ASCII text executable
bandit25@melinda:~$ cat /usr/bin/showtext
#!/bin/sh

more ~/text.txt
exit 0
```

Básicamente lee el fichero **text.txt** y lo muestra en pantalla con el comando **more**.

Preguntamos en el foro IRC ya que no sabemos como avanzar :`(. 

Nos indican que hay un pequeño truco con el editor **vi** que se encarga de mostrar el texto del fichero que permitiría que ejecutásemos **comandos** de **vi** mientra se cargar el banner.

El truco consiste en hacer la ventana de la consola muy pequeña para que salte el mensaje del programa **more** para que siga cargando el contenido del fichero **text.txt**

En vez de darle a la barra espaciadora para avanzar leyendo el contenido del fichero **text.txt**, pulsamos **v** para entrar en edición de **vi** del fichero y desde ahí ejecutamos el comando de lectura de **vi** que es **:r <nombreFichero>**

```bash
:r /etc/bandit_pass/bandit26
```
Guardamos/Salimos de vi y a nosotros nos aparecen unos errores pero que luego desaparecen.

Volvemos a la pantalla anterior donde se estaba cargando la imagen del banner pero esta vez nos encontramos con un código:

```bash
~                                                                                                                                          
  _                     _ _ _   ___   __
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
~                                                                                                                                          
~                                        
```

Ahí está la password :D

**FLAG** = {5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z}

