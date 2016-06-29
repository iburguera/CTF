#Bandit Level 5 → Level 6

##Level Goal

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties: - human-readable - 1033 bytes in size - not executable

##Commands you may need to solve this level

ls, cd, cat, file, du, find

##Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {koReBOKuIDDepwhWk7jZC0RTdopnAYKh}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit5@bandit.labs.overthewire.org
```

Entramos en la consola y nos salen varios ficheros en los que debemos encontrar la contraseña ubicada en un fichero de tamaño de **1033 bytes**

Utilizaremos la herramiento ```find``` para encontrar lo que buscamos. Nos ayudamos del manual **man find** para saber como buscar por tamaño en bytes

```bash man find
 -size n[cwbkMG]
              File uses n units of space.  The following suffixes can be used:

              `b'    for 512-byte blocks (this is the default if no suffix is used)

              `c'    for bytes

              `w'    for two-byte words

              `k'    for Kilobytes (units of 1024 bytes)

              `M'    for Megabytes (units of 1048576 bytes)

              `G'    for Gigabytes (units of 1073741824 bytes)
```

Una vez que sabemso que tenemos que agregarle una **c** al valor 1033 del tamaño del fichero, montamos la consulta

```bash 
find ./ -type f -size 1033c
```

Y nos sale el siguiente resultado:

```bash 
bandit5@melinda:~/inhere$ find ./ -type f -size 1033c
./maybehere07/.file2
bandit5@melinda:~/inhere$ cat ./maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

Ya tenemos la **FLAG** = {DXjZPULLxYr17uwoI01bNLQbtFemEgo7}



