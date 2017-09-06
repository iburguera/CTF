## Leviathan Level 1 → Level 2

## Level Goal

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** a la dirección **leviathan.labs.overthewire.org** en el puerto **2223** con los siguientes datos:

```bash
  - User: leviathan1
  - Pass: rioGegei8m
```

Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh leviathan1@leviathan.labs.overthewire.org -p 2223
```

Accedemos sin problemas.

```bash
leviathan1@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan2 leviathan1 7501 Jun 15 11:38 check
```

Parace que hay un executable llamado **check** así que vamos a ejecutarlo.

```bash
leviathan1@leviathan:~$ ./check
password: asdfr
Wrong password, Good Bye ...
```

Observamos que tras introducir una contraseña aleatoria, nos devuelve un mensaje **Wrong Password, Godd Bye**

Parece que compara nuestro input con una la informacion de una variable que tiene en el programa y la compara. 
Probamos sin éxito los comandos **strings**, **file** , **type** , etc. 

Probamos a utilizar la herramienta **ltrace** para saber las llamadas que se hacen a las librerí
Después de probar sin éxito los comandos **strings**, **file** , **type** , etc. 

Probamos a utilizar la herramienta **ltrace** para saber las llamadas que se hacen a las librerías, al fin y al cabo el programa estar haciendo una comparación y est tirando de alguna librería.

```bash
leviathan1@leviathan:~$ ltrace ./check
__libc_start_main(0x804852d, 1, 0xffffd7f4, 0x80485f0 <unfinished ...>
printf("password: ")                                                                                                          = 10
getchar(0x8048680, 47, 0x804a000, 0x8048642password: abce
)                                                                                  = 97
getchar(0x8048680, 47, 0x804a000, 0x8048642)                                                                                  = 98
getchar(0x8048680, 47, 0x804a000, 0x8048642)                                                                                  = 99
strcmp("abc", "sex")                                                                                                          = -1
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
)                                                                                          = 29
+++ exited (status 0) +++
```
¡BIEN! El programa utiliza una llamada la función **strcmp** y lo compara con el string **sex** ¡PERFEKTOA!

Ahora que ya sabemos con que string compara el programa, únicamente tenemos que poner la palabra **sex** para que nos la valide.

Ejecutamos nuevamente el programa y vemos que es lo que pasa.

```bash
leviathan1@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan2 leviathan1 7501 Jun 15 11:38 check
leviathan1@leviathan:~$ ./check
password: sex
$ whoami
leviathan2
$ cd /etc/leviathan_pass
$ ls -l
total 32
-r-------- 1 leviathan0 leviathan0 11 Jun 15 11:37 leviathan0
-r-------- 1 leviathan1 leviathan1 11 Jun 15 11:37 leviathan1
-r-------- 1 leviathan2 leviathan2 11 Jun 15 11:37 leviathan2
-r-------- 1 leviathan3 leviathan3 11 Jun 15 11:37 leviathan3
-r-------- 1 leviathan4 leviathan4 11 Jun 15 11:38 leviathan4
-r-------- 1 leviathan5 leviathan5 11 Jun 15 11:38 leviathan5
-r-------- 1 leviathan6 leviathan6 11 Jun 15 11:38 leviathan6
-r-------- 1 leviathan7 leviathan7 11 Jun 15 11:38 leviathan7
$ cat leviathan2
ougahZi8Ta
```
Hemos accedido al programa y hemos introducido el string correcto **sex** lo que nos ha devuelto una **shell** con el usuario **leviathan2**.

Teniendo esto en cuenta, hemos investigado por el sistema y hemos encontrado un directorio llamado **/etc/leviathan_pass** donde están las contraseñas.

Hacemos un **cat** del fichero **leviathan2** y nos muestra la flag 

:v: :sunglasses: :v:

**FLAG** = {ougahZi8Ta} 
