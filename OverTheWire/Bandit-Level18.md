#Bandit Level 18 → Level 19

##Level Goal

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

##Commands you may need to solve this level

ssh, ls, cat

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd}

Utilizamos esta contraseña para acceder al siguiente nivel o ya que hemos entrado en el nivel anterior la mantenemos abierta.

```bash 
$ ssh bandit18@bandit.labs.overthewire.org
```

Nos conectamos pero nos desconecta de inmediato :(

```bash
ikerburguera@MacBook-Pro-de-Iker:~/Desktop$ sudo ssh bandit18@bandit.labs.overthewire.org 
...
This is the OverTheWire game server. More information on http://www.overthewire.org/wargames
Please note that wargame usernames are no longer level<X>, but wargamename<X>
e.g. vortex4, semtex2, ...
Note: at this moment, blacksun is not available.
bandit18@bandit.labs.overthewire.org's password: 
...
Byebye !
Connection to bandit.labs.overthewire.org closed.
```

El enunciado nos dice que alguien ha cambiado el fichero **.bashrc** para que nos "Deslogeemos" (menudo palabro que acabo de inventar :) ) al conectarnos al servidor.

Tenemos que buscar la forma de **modificar el fichero** o mejor aún hacer que se **ejecutar** una **shell** con **/bin/sh**. Optamos por la segunda opción ya que la primera es más complicada :)

Googleamos un poco y damos con un comando en **SSH** que nos permite pasarle el parámetro **/bin/sh** y así poder obtener una **shell**.

- http://serverfault.com/questions/94503/login-without-running-bash-profile-or-bashrc

```bash
ikerburguera@MacBook-Pro-de-Iker:~/Desktop$ ssh  -t bandit18@bandit.labs.overthewire.org /bin/sh 
````

Lo probamos:

```bash
ikerburguera@MacBook-Pro-de-Iker:~/Desktop$ ssh  -t bandit18@bandit.labs.overthewire.org /bin/sh 

This is the OverTheWire game server. More information on http://www.overthewire.org/wargames
Please note that wargame usernames are no longer level<X>, but wargamename<X>
e.g. vortex4, semtex2, ...
Note: at this moment, blacksun is not available.
bandit18@bandit.labs.overthewire.org's password:  
$ 
$ ls -l
total 4
-rw-r----- 1 bandit19 bandit18 33 Nov 14  2014 readme
$ cat readme    
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

Obtenemos la flag para el nivel18 :)

**FLAG** = {IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x}

