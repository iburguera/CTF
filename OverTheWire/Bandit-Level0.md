#Bandit Level 0 → Level 1

##Level Goal

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH to log into that level and continue the game.

##Commands you may need to solve this level

ls, cd, cat, file, du, find

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
