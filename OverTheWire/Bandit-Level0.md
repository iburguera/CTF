#Bandit Level 0

##Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

##Commands you may need to solve this level

ssh

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** al a dirección **bandit.labs.overthewire.org** con los siguientes datos:
  - **User**: bandit0
  - **Pass**: bandit0
  
Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh badit0@bandit.labs.overthewire.org
```

Accedemos sin problemas y observamos que hay un fichero que se llama **README** con el contenido de la flag:

```bash
$ ls -l
-rw-r----- 1 bandit1 bandit0 33 Nov 14  2014 readme
$ bandit0@melinda:~$ cat readme 
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

**FLAG** = {boJ9jbbUNNfktd78OOpsqOltutMc3MY1} 
