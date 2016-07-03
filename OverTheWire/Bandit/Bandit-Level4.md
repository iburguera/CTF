#Bandit Level 4 → Level 5

##Level Goal

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

##Commands you may need to solve this level

ls, cd, cat, file, du, find

## Write up Iker 

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {pIwrPrtPN36QITSp3EQaw936yaFoFgAB} 

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit4@bandit.labs.overthewire.org
```

Entramos en la consola y nos salen varios fichero que de primera no reconocemos 

```bash
bandit4@melinda:~$ ls -l
total 4
drwxr-xr-x 2 root root 4096 Nov 14  2014 inhere
bandit4@melinda:~$ cd inhere/
bandit4@melinda:~/inhere$ ls -l
total 40
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file00
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file01
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file02
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file03
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file04
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file05
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file06
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file07
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file08
-rw-r----- 1 bandit5 bandit4 33 Nov 14  2014 -file09
````

Intentamos ver de que tipo son son el comando  ```file ./*```  y nos sale los siguiente:

```bash
bandit4@melinda:~$ ls -l
total 4
drwxr-xr-x 2 root root 4096 Nov 14  2014 inhere
bandit4@melinda:~$ cd inhere/
bandit4@melinda:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@melinda:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

**FLAG** = {koReBOKuIDDepwhWk7jZC0RTdopnAYKh} 
