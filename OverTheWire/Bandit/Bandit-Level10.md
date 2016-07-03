#Bandit Level 10 → Level 11

##Level Goal

The password for the next level is stored in the file data.txt, which contains base64 encoded data

##Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit10@bandit.labs.overthewire.org
```

Entramos en la consola y nos indican que la flag está alojada dentro del fichero **data.txt** codificada en **Base64**

```bash
bandit10@melinda:~$ ls -l
total 4
-rw-r----- 1 bandit11 bandit10 69 Nov 14  2014 data.txt
bandit10@melinda:~$ strings data.txt 
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
bandit10@melinda:~$ 
```

Aquí tenemos dos opciones para resolver el reto:

  - 1 Coger el valor de: **VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==** y subirlo a algun decodificador de Base64 online
    - 1 https://www.base64decode.org/
    - 2 Resultado: The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
  - 2 Utilizamos los comandos que trae la consola
    - ```bash $ base64 -d data.txt
    - ```bash $ The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR  

**FLAG** = {IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR}
    



