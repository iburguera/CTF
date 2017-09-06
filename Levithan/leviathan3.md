## Leviathan Level 3 → Level 4

## Level Goal

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** a la dirección **leviathan.labs.overthewire.org** en el puerto **2223** con los siguientes datos:

```bash
  - User: leviathan3
  - Pass: Ahdiemoo1j
```

Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh leviathan3@leviathan.labs.overthewire.org -p 2223
```

Accedemos sin problemas y vemos que hay un fichero llamado **level3**

```bash
leviathan3@leviathan:~$ ls -l
total 12
-r-sr-x--- 1 leviathan4 leviathan3 9946 Jun 15 11:38 level3
```

Ejecutamos el programa y nos indica que debemos especificarle una contraseña

```bash
leviathan3@leviathan:~$ ltrace ./level3
__libc_start_main(0x80485fe, 1, 0xffffd7f4, 0x80486d0 <unfinished ...>
strcmp("h0no33", "kakaka")                                                                                                    = -1
printf("Enter the password> ")                                                                                                = 20
fgets(Enter the password> asdfdsaf
"asdfdsaf\n", 256, 0xf7fccc20)                                                                                          = 0xffffd5ec
strcmp("asdfdsaf\n", "snlprintf\n")                                                                                           = -1
puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
)                                                                                                    = 19
+++ exited (status 0) +++
```

Vemos como hay **dos** funciones **strcmp** . Probamos a introducir diferentes strings que aparecen en el programa

- **h0no33**
- **kakaka**
- **snlprintf\n**
- **snlprintf**
- **asdfdsaf\n**
- **asdfdsaf**

```bash
leviathan3@leviathan:~$ whoami
leviathan3
leviathan3@leviathan:~$ ./level3
Enter the password> snlprintf
[You've got shell]!
$ whoami
leviathan4
$ cat /etc/leviathan_pass/leviathan4       
vuH0coox6m
```

Metiendo el string **snlprintf** nos da una **shell**. 

Comprobamos que somos **leviathan4** y podemos acceder al fichero dondo nos mostrará la contraseña para el siguiente nivel.

:v: :sunglasses: :v:

**FLAG** = {vuH0coox6m} 
