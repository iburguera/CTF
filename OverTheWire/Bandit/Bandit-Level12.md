#Bandit Level 12 → Level 13

##Level Goal

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

##Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv

##Helpful Reading Material

Hex dump on Wikipedia

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit12@bandit.labs.overthewire.org
```

El enunciado nos indica que la flag está ubicada en el fichero data.txt que es un fichero **HEXDUMP** que está comprimido. Nos indican que podemos crear un directorio en **tmp** usando ```mkdir```
y renombrandolo con ```mv````

```bash
bandit12@melinda:~$ ls -l
total 4
-rw-r----- 1 bandit13 bandit12 2546 Nov 14  2014 data.txt
bandit12@melinda:~$ mkdir /tmp/iker  
bandit12@melinda:~$ cp data.txt /tmp/iker
bandit12@melinda:~$ cd /tmp/iker
bandit12@melinda:/tmp/iker$ ls -l
total 4
-rw-r----- 1 bandit12 bandit12 2546 Jun 30 07:35 data.txt
```

Ya tenemos el fichero en la carpeta temp. Ahora tenemos que convertir el fichero **HEXDUMP** a una **BINARIO** con el comando ```xxd -r```

Vemos que data out tiene dentro el fichero **data2.bin** comprimido con **GZIP**

```bash
$ xxd -r data.txt data.out
```

Nos sale lo siguiente y comprobamos que **data.out** es un fichero comprimido. Por lo que tenemos que cambiar el nombre con ```mv```y descomprimirlo con ```gzip```

```bash
bandit12@melinda:/tmp/iker$ xxd -r data.txt data.out
bandit12@melinda:/tmp/iker$ ls -l
total 8
-rw-rw-r-- 1 bandit12 bandit12  608 Jun 30 07:43 data.out
-rw-r----- 1 bandit12 bandit12 2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ strings data.out
data2.bin
BZh91AY&SY
6m9q
(lUu
L79,
sEDO
`gyT
bandit12@melinda:/tmp/iker$ file data.out
data.out: gzip compressed data, was "data2.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
bandit12@melinda:/tmp/iker$ ls -l
total 8
-rw-rw-r-- 1 bandit12 bandit12  608 Jun 30 07:43 data.gz
-rw-r----- 1 bandit12 bandit12 2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ gzip -d data.gz 
bandit12@melinda:/tmp/iker$ ls -l
total 8
-rw-rw-r-- 1 bandit12 bandit12  575 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12 2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ file data
data: bzip2 compressed data, block size = 900k
```
Despues de descomprimirlo volvemos a ver que el fichero comprimido tenía otro fichero comprimido con **BZIP** así que lo descomprimimos.

```bash
bandit12@melinda:/tmp/iker$ bzip2 -d data
bzip2: Can't guess original name for data -- using data.out
bandit12@melinda:/tmp/iker$ ls -l
total 8
-rw-rw-r-- 1 bandit12 bandit12  436 Jun 30 07:43 data.out
-rw-r----- 1 bandit12 bandit12 2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ file data.out 
data.out: gzip compressed data, was "data4.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
```

Volvemos a encontrarnos con otro **GZIP** pero en este caso contiene **data4.bin**. Cambiamos de nombre de *.out a *.gz y lo volvemos a descomprimir

```bash
bandit12@melinda:/tmp/iker$ ls -l    
total 8
-rw-rw-r-- 1 bandit12 bandit12  436 Jun 30 07:43 data.out
-rw-r----- 1 bandit12 bandit12 2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ mv data.out data.gz
bandit12@melinda:/tmp/iker$ ls -l
total 8
-rw-rw-r-- 1 bandit12 bandit12  436 Jun 30 07:43 data.gz
-rw-r----- 1 bandit12 bandit12 2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ gzip -d data.gz 
bandit12@melinda:/tmp/iker$ ls -l
total 24
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ file data
data: POSIX tar archive (GNU)
```

Después de descomprimirlo vemos que tiene un fichero **TAR**, WTF!! ¿Esto no se termina? En fin seguimos adelante...

```bash
bandit12@melinda:/tmp/iker$ ls -l
total 8
-rw-rw-r-- 1 bandit12 bandit12  436 Jun 30 07:43 data.gz
-rw-r----- 1 bandit12 bandit12 2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ gzip -d data.gz 
bandit12@melinda:/tmp/iker$ ls -l
total 24
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ file data
data: POSIX tar archive (GNU)
bandit12@melinda:/tmp/iker$ ls -l
total 24
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
bandit12@melinda:/tmp/iker$ tar -xf data
bandit12@melinda:/tmp/iker$ ls -l
total 36
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data5.bin
bandit12@melinda:/tmp/iker$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@melinda:/tmp/iker$ tar -xf data5.bin 
bandit12@melinda:/tmp/iker$ ls -l
total 40
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data5.bin
-rw-r--r-- 1 bandit12 bandit12   224 Nov 14  2014 data6.bin
bandit12@melinda:/tmp/iker$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@melinda:/tmp/iker$ bzip2 -d data6.bin
bzip2: Can't guess original name for data6.bin -- using data6.bin.out
bandit12@melinda:/tmp/iker$ ls -l
total 48
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data5.bin
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data6.bin.out
bandit12@melinda:/tmp/iker$ file data6.bin.out
data6.bin.out: POSIX tar archive (GNU)
bandit12@melinda:/tmp/iker$ tar -xf data6.bin.out
bandit12@melinda:/tmp/iker$ ls -l
total 52
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data5.bin
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data6.bin.out
-rw-r--r-- 1 bandit12 bandit12    79 Nov 14  2014 data8.bin
bandit12@melinda:/tmp/iker$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
bandit12@melinda:/tmp/iker$ mv data8.bin data8.gz
bandit12@melinda:/tmp/iker$ ls -l
total 52
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data5.bin
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data6.bin.out
-rw-r--r-- 1 bandit12 bandit12    79 Nov 14  2014 data8.gz
bandit12@melinda:/tmp/iker$ gzip -d data8.gz
bandit12@melinda:/tmp/iker$ ls -l
total 52
-rw-rw-r-- 1 bandit12 bandit12 20480 Jun 30 07:43 data
-rw-r----- 1 bandit12 bandit12  2546 Jun 30 07:43 data.txt
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data5.bin
-rw-r--r-- 1 bandit12 bandit12 10240 Nov 14  2014 data6.bin.out
-rw-r--r-- 1 bandit12 bandit12    49 Nov 14  2014 data8
bandit12@melinda:/tmp/iker$ file data8
data8: ASCII text
bandit12@melinda:/tmp/iker$ cat data8
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
bandit12@melinda:/tmp/iker$ 
```

Después de mucho tiempo cmabiando nombres, extrayendo con **GZIP**, **TAR** y **BZIP2** llegamos a un fichero de texto que contiene la password.

Supongo que el objetivo de esta prueba era aprender a manejar las herramientas de extracción de ficheros comprimidos **GZIP**, **TAR** y **BZIP2** al igual que utilizar los comandos ```file```y ```mv``` 

Resumiendo estos son los comandos que hemos utilizado:
```bash

[$]-> mkdir /tmp/iker
[$]-> cp data.txt /tmp/iker/data.txt
[$]-> cd /tmp/iker
[$]-> xxd -r data.txt data.out
[$]-> file data.out
[$]-> mv data.out data.gz
[$]-> gzip -d data.gz
[$]-> file data
[$]-> bzip2 -d data
[$]-> file data.out
[$]-> mv data.out data.gz
[$]-> gzip -d data.gz
[$]-> file data
[$]-> tar -xf data
[$]-> file data5.bin
[$]-> tar -xf data5.bin
[$]-> file data6.bin
[$]-> bzip2 -d data6.bin
[$]-> file data6.bin.out
[$]-> tar -xf data6.bin.out
[$]-> file data8.bin
[$]-> mv data8.bin data8.gz
[$]-> gzip -d data8.gz
[$]-> cat data8

bandit12@melinda:/tmp/iker$ cat data8
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

La prueba un poco tediosa pero sirve para aprender "a la fuerza" a utilizar esas herramientas :D




