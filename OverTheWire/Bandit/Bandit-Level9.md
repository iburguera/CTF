#Bandit Level 9 → Level 10

##Level Goal

The password for the next level is stored in the file data.txt in one of the few human-readable strings, beginning with several ‘=’ characters.

##Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit9@bandit.labs.overthewire.org
```

Accedemos a la consola e intentamos abrir el fichero pero no se puede leer nada. Utilizamos una de las herramientas que nos recomiendan en el enunciado ```strings ``` para ver si contiene algun string.

```bash
bandit9@melinda:~$ strings data.txt
````

Nos devuelve los string del fichero incluyendo la flag **The** ... **Password** ... **is** ... **========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk**

**FLAG** = {truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk}
