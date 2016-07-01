#Bandit Level 22 → Level 23

##Level Goal

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

##Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI}

Utilizamos esta contraseña para acceder al siguiente nivel.

```bash 
$ ssh bandit22@bandit.labs.overthewire.org
```

Nos conectamos a la prueba y analizamos como se comporta el programa o Job de **Cron**

Al igual que la anterior, entramos en la carpeta de Cron para ver la tarea, que en este caso será la **cronjob_bandit23**.

Inspeccionamos el fichero y nos encontramos con un código escrito en **bash**

```bash
bandit22@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

Si analizamos el código, vemos que guarda en la variable **myname** el valor de **whoami** que si lo ejecutamos en el terminal nos sale que somos **bandit22**

```bash
bandit22@melinda:/etc/cron.d$ whoami
bandit22
```

Seguimos ne la siguiente línea y guarda en la variable **mytarget** el texto **I am user $myname (el valor de la variable)** haciendole un **md5sum** y después pasar este resultado al comando **cut -d ' ' -f 1**.

```bash
NAME
       cut - remove sections from each line of files
DESCRIPTION
       Print selected parts of lines from each FILE to standard output.
        -d, --delimiter=DELIM
              use DELIM instead of TAB for field delimiter
        -f, --fields=LIST
              select only these fields;  also print any line that contains no delimiter character, unless the -s option is specified
```

Lo mejor que podemos hacer es ejecutar el script ** ** con el comando **bash <nombre fichero> nosotros mismos la tarea de Cron y ver el resultado en la consola.

El programa ya nos mostraría en consola el resultado con el comando **echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"**

```bash
bandit22@melinda:/etc/cron.d$ bash /usr/bin/cronjob_bandit23.sh
Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3
```

Vemos que ha escrito el valor del password **/etc/bandit_pass/bandit22** en la ruta generada **/tmp/8169b67bd894ddbb4412f91573b38db3**

Vamos a ver que contiene el fichero ;) 

```bash
bandit22@melinda:/etc/cron.d$ cat /tmp/8169b67bd894ddbb4412f91573b38db3
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

**FLAG** = {Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI}


