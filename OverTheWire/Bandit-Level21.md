#Bandit Level 21 → Level 22

##Level Goal

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

##Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr}

Utilizamos esta contraseña para acceder al siguiente nivel.

```bash 
$ ssh bandit21@bandit.labs.overthewire.org
```

Nos conectamos a la prueba y analizamos como se comporta el programa o Job de **Cron**

Accedemos a la carpeta donde está el programa:

```bash
bandit21@melinda:~$ cd /etc/cron.d
bandit21@melinda:/etc/cron.d$ ls -l
total 92
-r--r----- 1 root root  46 Nov 14  2014 behemoth4_cleanup
-rw-r--r-- 1 root root 355 May 25  2013 cron-apt
-rw-r--r-- 1 root root  61 Nov 14  2014 cronjob_bandit22
-rw-r--r-- 1 root root  62 Nov 14  2014 cronjob_bandit23
-rw-r--r-- 1 root root  61 May  3  2015 cronjob_bandit24
-rw-r--r-- 1 root root  62 May  3  2015 cronjob_bandit24_root
-r--r----- 1 root root  47 Nov 14  2014 leviathan5_cleanup
-rw------- 1 root root 233 Nov 14  2014 manpage3_resetpw_job
...
```

Como el siguiente reto es el **22** miramos la tarea que se ejecuta en **cronjob_bandit22**

```bash
bandit21@melinda:/etc/cron.d$ cat cronjob_bandit22
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Parece que ejecuta un script en **/usr/bin/cronjob_bandit22.sh** el cual escribe la password del bandit22 **/etc/bandit_pass/bandit22** en el path **/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv**

Miramos el tipo de fichero que es y hacemos un ``` cat ``` del fichero ubicado en esa ruta y obtenemos la password :)

```bash
bandit21@melinda:/etc/cron.d$ file /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv: ASCII text
bandit21@melinda:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

**FLAG** = {Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI}


