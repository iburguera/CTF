#Bandit Level 7 → Level 8

##Level Goal

The password for the next level is stored in the file data.txt next to the word millionth

##Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Write up Iker 

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit7@bandit.labs.overthewire.org
```

Nos dicen que tenemos que encontrar la password junto a la palabra **millionth**

Para ello utilizamos un comando muy util llamado **grep**

```bash
bandit7@melinda:~$ ls -l
total 4088
-rw-r----- 1 bandit8 bandit7 4184396 Nov 14  2014 data.txt
bandit7@melinda:~$ cat data.txt | grep millionth
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
````

Y obtenemos la flag

**FLAG** = {cvX2JJa4CFALtqS87jk27qwqGhBM9plV}


