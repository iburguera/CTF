#Bandit Level 11 → Level 12

##Level Goal

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

##Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

##Helpful Reading Material

Rot13 on Wikipedia

## Write Up Iker


La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit11@bandit.labs.overthewire.org
```
El enunciado nos dice que la contraseña está rotada en las letras mayusculas y minusculas 13 posiciones en el fichero data.txt. 

```bash
bandit11@melinda:~$ ls -l
total 4
-rw-r----- 1 bandit12 bandit11 49 Nov 14  2014 data.txt
bandit11@melinda:~$ cat data.txt 
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
bandit11@melinda:~$ 
````

Vemos como el texto **Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh** podría ser algo así como **The password is ....** 

Lo que tenemos que hacer es modificar/rotar cada letra en 13 posiciones para que nos devuelva la contraseña.

Leemos la documentación de ROT13 que nos proporcionan y sacamos el comando que necesitamos para decodificarlo

```bash
bandit11@melinda:~$ ls -l
total 4
-rw-r----- 1 bandit12 bandit11 49 Nov 14  2014 data.txt
bandit11@melinda:~$ cat data.txt 
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
bandit11@melinda:~$ cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
bandit11@melinda:~$ 
```

**FLAG** = {5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu}


    
