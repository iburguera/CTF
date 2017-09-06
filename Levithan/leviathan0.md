#Leviathan Level 0 → Level 1

##Level Goal

Leviathan Level 0 → Level 1

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** al a dirección **bandit.labs.overthewire.org** con los siguientes datos:
  - **User**: bandit0
  - **Pass**: bandit0
  
Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh bandit0@bandit.labs.overthewire.org
```

Accedemos sin problemas y observamos que hay un fichero que se llama **README** con el contenido de la flag:

```bash
$ ls -l
-rw-r----- 1 bandit1 bandit0 33 Nov 14  2014 readme
$ bandit0@melinda:~$ cat readme 
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

**FLAG** = {boJ9jbbUNNfktd78OOpsqOltutMc3MY1} 
