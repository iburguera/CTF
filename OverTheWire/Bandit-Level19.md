#Bandit Level 19 → Level 20

##Level Goal

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used to setuid binary.

##Helpful Reading Material

setuid on Wikipedia

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x}

Utilizamos esta contraseña para acceder al siguiente nivel o ya que hemos entrado en el nivel anterior la mantenemos abierta.

```bash 
$ ssh bandit19@bandit.labs.overthewire.org
```

Nos conectamos y observamos un fichero llamado **bandit20-do** e intentamos ejecutarlo para saber como funciona:

```bash
bandit19@melinda:~$ ls -l
total 8
-rwsr-x--- 1 bandit20 bandit19 7370 Nov 14  2014 bandit20-do
bandit19@melinda:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
bandit19@melinda:~$ 
```
Probamos a ver si acepta comandos como parámetros:

```bash
bandit19@melinda:~$ ./bandit20-do ls                           
bandit20-do
bandit19@melinda:~$ ./bandit20-do ls -l                        
total 8
-rwsr-x--- 1 bandit20 bandit19 7370 Nov 14  2014 bandit20-do
```

LOL!! Acepta ejecutar comandos desde los parámetros introducidos xD

Con esto podemos hacer tranquilamente un ```cat```al fichero que contenga la password. Como no estoy seguro a cual de los dos (bandit19,bandit20) tengo que hacerlo, lo hago a los dos :)

```bash
bandit19@melinda:~$ ./bandit20-do cat /etc/bandit_pass/bandit19
cat: /etc/bandit_pass/bandit19: Permission denied
bandit19@melinda:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

Al final la flag está en el **Bandit20** :)

**FLAG** = {GbKksEFF4yrVs6il55v6gwY5aVje5f0j}

