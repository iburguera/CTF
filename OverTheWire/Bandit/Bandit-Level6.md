
#Bandit Level 6 → Level 7

##Level Goal

The password for the next level is stored somewhere on the server and has all of the following properties: - owned by user bandit7 - owned by group bandit6 - 33 bytes in size

##Commands you may need to solve this level

ls, cd, cat, file, du, find, grep

## Write up Iker 

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {DXjZPULLxYr17uwoI01bNLQbtFemEgo7} 

Utilizamos esta contraseña para acceder al siguiente nivel 

```bash 
$ ssh bandit6@bandit.labs.overthewire.org
```

Nos indican que el fichero se encuentra en algun lugar del sistema y que tiene estas propiedades:
  - owned by user bandit7 
  - owned by group bandit6 
  - 33 bytes in size
  
Una vez más utilizaremos el comando ```find```para buscarlo 

```bash
find ./ -type f -user bandit7 -group bandit6 -size 33c
```

Nos devuelve muchos resultados con el mensaje **Permission Denied** menos uno: **/var/lib/dpkg/info/bandit7.password**.

```bash
...
find: `/var/lib/php5': Permission denied
find: `/var/lib/cron-apt/_-_etc_-_cron-apt_-_config': Permission denied
find: `/var/lib/mysql': Permission denied
/var/lib/dpkg/info/bandit7.password
find: `/var/cache/ldconfig': Permission denied
find: `/var/log': Permission denied
find: `/var/lock': Permission denied
...
```
Tiene que estar ahí nuestra Flag

```bash
bandit6@melinda:/home$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
````

**FLAG** = {HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs}
