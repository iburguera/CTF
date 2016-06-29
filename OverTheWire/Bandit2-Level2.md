#Bandit Level 1 → Level 2

##Level Goal

The password for the next level is stored in a file called - located in the home directory

Commands you may need to solve this level

ls, cd, cat, file, du, find

Helpful Reading Material

Google Search for “dashed filename”
Advanced Bash-scripting Guide - Chapter 3 - Special Characters

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9}

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh badit2@bandit.labs.overthewire.org
```

Observamos que hay un fichero que contiene espacios. Intentamos hacer un cat al fichero y nos devuelve la flag. 

```bash 
bandit2@melinda:~$ ls -l
total 4
-rw-r----- 1 bandit3 bandit2 33 Nov 14  2014 spaces in this filename
bandit2@melinda:~$ cat spaces\ in\ this\ filename 
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
bandit2@melinda:~$ 
```

**FLAG** = {UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK}
