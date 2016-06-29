#Bandit Level 3 → Level 4

##Level Goal

The password for the next level is stored in a hidden file in the inhere directory.

##Commands you may need to solve this level

ls, cd, cat, file, du, find

## Write Up Iker

Utilizamos esta contraseña para acceder al siguiente nivel 

**FLAG** = {UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK}

```bash 
$ ssh bandit3@bandit.labs.overthewire.org
```

Tenemos que buscar la flag en un fichero que está oculto en el sistema. Seguimos los siguientes pasos

```bash 
bandit3@melinda:~$ ls -l
total 4
drwxr-xr-x 2 root root 4096 Nov 14  2014 inhere
bandit3@melinda:~$ cd inhere/
bandit3@melinda:~/inhere$ ls -l
total 0
bandit3@melinda:~/inhere$ ls -asl
total 12
4 drwxr-xr-x 2 root    root    4096 Nov 14  2014 .
4 drwxr-xr-x 3 root    root    4096 Nov 14  2014 ..
4 -rw-r----- 1 bandit4 bandit3   33 Nov 14  2014 .hidden
bandit3@melinda:~/inhere$ cat .hidden 
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
bandit3@melinda:~/inhere$ 
```

**FLAG** = {pIwrPrtPN36QITSp3EQaw936yaFoFgAB}
