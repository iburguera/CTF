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

Nos conectamos a la prueba y analizamos como se comporta el programa

