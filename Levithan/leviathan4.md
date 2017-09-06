## Leviathan Level 4 → Level 5

## Level Goal

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** a la dirección **leviathan.labs.overthewire.org** en el puerto **2223** con los siguientes datos:

```bash
  - User: leviathan4
  - Pass: vuH0coox6m
```

Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh leviathan4@leviathan.labs.overthewire.org -p 2223
```

Accedemos sin problemas y vemos que no hay ningun fichero

```bash
leviathan3@leviathan:~$ ls -l
total 0
```
Ejecutamos el fichero para ver si existe algun fichero oculto

```bash
leviathan4@leviathan:~$ ls -a
.  ..  .bash_logout  .bashrc  .cache  .profile  .trash
leviathan4@leviathan:~$ cd .trash
leviathan4@leviathan:~/.trash$ ls -l
total 8
-r-sr-x--- 1 leviathan5 leviathan4 7433 Jun 15 11:38 bin
```
Vemos que hay un directorio interesante llamado **trash** así que vamos a ver que hay en el y ejecutamos el fichero **bin**

Ejecutamos el programa y nos muestra un código binario:

```bash
leviathan4@leviathan:~/.trash$ ./bin
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010 
```

Suponemos que es la contraseña codificada en **Binario**. Tenemos que pasa de **Binario** -> **ASCII**

El resultado es:

```bash
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010 -> Tith4cokei
```
Suponemos que esa es la contraseña

:v: :sunglasses: :v:

**FLAG** = {Tith4cokei} 
