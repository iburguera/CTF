#Bandit Level 17 → Level 18

##Level Goal

There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

##Commands you may need to solve this level

cat, grep, ls, diff

## Write Up Iker

En el anterior (**nivel16**) hemos conseguido una **Clave Privada** que utilizaremos para conetarnos al **nivel17**

Utilizaremos el siguiente comando para conectarnos al **nivel17** 

```bash
ikerburguera@MacBook-Pro-de-Iker:~/Desktop$ sudo ssh bandit17@bandit.labs.overthewire.org -i  sshkey17.private 
```

Entramos al servidor y observamos que tenemos dos ficheros: **password.old** y **password.new**

```bash
bandit17@melinda:~$ ls -l
total 8
-rw-r----- 1 bandit18 bandit17 3300 Nov 14  2014 passwords.new
-rw-r----- 1 bandit18 bandit17 3300 Nov 14  2014 passwords.old
```

Nos indican que la contraseña está en el fichero **passwords.new** y que es la diferencia entre el contenido del fichero **passwords.old** y el fichero **passwords.new**

El enunciado nos muestra una pista con los comandos que podemos utilizar en la prueba. El comando es ```diff```

Ejecutamos el comando pasándole los dos ficheros:

```bash
bandit17@melinda:~$ diff passwords.old passwords.new 
42c42
< BS8bqB1kqkinKJjuxL6k072Qq9NRwQpR
---
> kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
bandit17@melinda:~$ 
```

En este caso obtenemos el string **kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd** como contraseña ya que nos piden la diferencia en **passwords.new** y lo hemos introducido como segundo parámetro.

**FLAG** = {kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd}

