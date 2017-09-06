## Leviathan Level 7 → Level 8

## Level Goal

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** a la dirección **leviathan.labs.overthewire.org** en el puerto **2223** con los siguientes datos:

```bash
  - User: leviathan7
  - Pass: ahy7MaeBo9
```

Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh leviathan7@leviathan.labs.overthewire.org -p 2223
```

Accedemos sin problemas y vemos que hay un fichero llamado **CONGRATULATIONS**

```bash
ikerburguera@MacBook-Pro-de-Iker:~$ ssh leviathan7@leviathan.labs.overthewire.org -p 2223
 _            _       _   _                 
| | _____   _(_) __ _| |_| |__   __ _ _ __  
| |/ _ \ \ / / |/ _` | __| '_ \ / _` | '_ \ 
| |  __/\ V /| | (_| | |_| | | | (_| | | | |
|_|\___| \_/ |_|\__,_|\__|_| |_|\__,_|_| |_|
                                            
a http://www.overthewire.org wargame.

leviathan7@leviathan.labs.overthewire.org's password: 
Welcome to Ubuntu 14.04 LTS (GNU/Linux 4.4.0-71-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

leviathan7@leviathan:~$ ls -l
total 4
-r--r----- 1 leviathan7 leviathan7 178 Jun 15 11:38 CONGRATULATIONS
leviathan7@leviathan:~$ cat CONGRATULATIONS
Well Done, you seem to have used a *nix system before.
leviathan7@leviathan:~$ 
```

:beers: ¡Terminamos el CTF! :beers: 

:v: :sunglasses: :v:

**FLAG** = {ahy7MaeBo9} 
