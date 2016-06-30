#Bandit Level 13 → Level 14

##Level Goal

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

##Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

##Helpful Reading Material

SSH/OpenSSH/Keys

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:


**FLAG** = {8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit13@bandit.labs.overthewire.org
```

El anunciado nos dice que en esta ocasion no vamos a encontrar la flag en el directorio, sino una clave **SSH PRIVADA** del usuario Bandit14 para acceder al nivel 14.

```bash
bandit13@melinda:~$ ls -l
total 4
-rw-r----- 1 bandit14 bandit13 1679 Nov 14  2014 sshkey.private
bandit13@melinda:~$ 
```

Lo que haremos será copiar esa clave **SSH PRIVADA** a nuestra máquina y utilizarla como parámetro en la conexión a la prueba **Bandit14**

Yo he utilizado el programa **FILEZILLA** para descargarme la clave **SSH**

Ahora tenemos que conectarnos a la prueba **bandit14@bandit.labs.overthewire.org** utilizando la clave **SSH** que nos hemos descargado

Para ello leemos el manual de SSH con el comando ```man ssh```y observamos que con el parámetro ```-i```podemos especificar la clave privada que necesitemos

```bash
$ man ssh
...
 -i identity_file
             Selects a file from which the identity (private key) for public key authentication is read.  The default is ~/.ssh/identity for protocol version 1, and ~/.ssh/id_dsa, ~/.ssh/id_ecdsa,
             ~/.ssh/id_ed25519 and ~/.ssh/id_rsa for protocol version 2.  Identity files may also be specified on a per-host basis in the configuration file.  It is possible to have multiple -i
             options (and multiple identities specified in configuration files).  ssh will also try to load certificate information from the filename obtained by appending -cert.pub to identity
             filenames.
````

Así que nos conectamos utilizando esa clave con el siguiente parámetro.

```bash
ssh bandit14@bandit.labs.overthewire.org -i ~/Almacen/sshkey.private
```

**SALE UN ERROR**

```bash
ikerburguera@MacBook-Pro-de-Iker:~/Almacen$ ssh bandit14@bandit.labs.overthewire.org -i ~/Almacen/sshkey.privatesshkey.private 

This is the OverTheWire game server. More information on http://www.overthewire.org/wargames
Please note that wargame usernames are no longer level<X>, but wargamename<X>
e.g. vortex4, semtex2, ...

Note: at this moment, blacksun is not available.

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '~/Almacen/sshkey.private' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "~/Almacen/sshkey.private": bad permissions
bandit14@bandit.labs.overthewire.org's password: 
Permission denied, please try again.
```

```html
<font color="red">PENDIENTE</font>
```

Mirar permisos de la clave SSH


