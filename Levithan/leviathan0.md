## Leviathan Level 0 → Level 1

## Level Goal

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** a la dirección **leviathan.labs.overthewire.org** en el puerto **2223** con los siguientes datos:

```bash
  - User: leviathan0
  - Pass: leviathan0
```

Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh leviathan0@leviathan.labs.overthewire.org -p 2223
```

Accedemos sin problemas y vemos que no hay nada en el directorio

```bash
$leviathan0@leviathan:~$ ls -l
total 0
```

PArece que no hay nada en el direcotrio pero ejecutamos el comando **ls -a** para ver si existe algún fichero oculto y encontramos lo siguiente:

```bash
leviathan0@leviathan:~$ ls -a
.  ..  .backup  .bash_logout  .bashrc  .cache  .profile
```
¡Bien! hay un directorio oculto bastante apetecible con del nombre **.backup** así que accedemos a el y vemos que hay en el interior.

```bash
leviathan0@leviathan:~/.backup$ ls -l
total 132
-rw-r----- 1 leviathan1 leviathan0 133259 Jun 15 11:38 bookmarks.html
```
Abrimos el fichero **bookmarks.html** pero es muy grande así que decidimos hacre un **grep** en busca de palabras como **Flag** o **password**

```bash
leviathan0@leviathan:~/.backup$ cat bookmarks.html | grep "pass"
<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```
Observamos como nos suelta la password para acceder al siguiente nivel  :v: :sunglasses: :v:

**FLAG** = {rioGegei8m} 
