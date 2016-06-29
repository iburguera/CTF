#Bandit Level 8 → Level 9

##Level Goal

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

##Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

##Helpful Reading Material

The unix commandline: pipes and redirects

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {cvX2JJa4CFALtqS87jk27qwqGhBM9plV}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit8@bandit.labs.overthewire.org
```
El enunciado nos indica que la password está alojada en el fichero data.txt y que esta en la única línea de texto que se repite una vez.

Para esta tarea vamos a utilizar las herramientas ```sort```y ``ùniq``` . Utilizamos el manual para saber como se utilizan y una vez aprendido montamos la consulta sobre el fichero.

```bash
bandit8@melinda:~$ man sort
bandit8@melinda:~$ man uniq
bandit8@melinda:~$ sort data.txt | uniq -u 
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

**FLAG** = {UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR}
