## Leviathan Level 6 → Level 7

## Level Goal

There is no information for this level, intentionally.

## Write Up Iker 

Fácil. Tenemos que conectarnos por **SSH** a la dirección **leviathan.labs.overthewire.org** en el puerto **2223** con los siguientes datos:

```bash
  - User: leviathan6
  - Pass: UgaoFee4li
```

Escribimos el siguiente comando en la consola:
  
```bash 
$ ssh leviathan6@leviathan.labs.overthewire.org -p 2223
```

Accedemos sin problemas y vemos que no hay ningun fichero

```bash
leviathan5@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan6 leviathan5 7642 Jun 15 11:38 leviathan6
```
Ejecutamos el fichero.

```bash
leviathan6@leviathan:~$ ls -l
total 8
-r-sr-x--- 1 leviathan7 leviathan6 7492 Jun 15 11:38 leviathan6
leviathan6@leviathan:~$ ./leviathan6 
usage: ./leviathan6 <4 digit code>
leviathan6@leviathan:~$ ./leviathan6 1234
Wrong +++
```
Parece que tenemos introducir un **código** de 4 **dígitos**

```bash
[0000-9999]
```
Haremos un script que vaya probando números 

```python
import os

for i in range(0,10000):
	comando = "~/leviathan6 %04d" % i
	print comando
	os.system(comando)
```
Ejecutamos el comando y nos salta en el **7123** y comprobamos quienes somos para después mirar el fichero definitivo.

```bash
~/leviathan6 7123
$ whoami    
leviathan7
$ cat /etc/leviathan_pass/leviathan7
ahy7MaeBo9
```
El código que debemos meter al programa es el **7123** y nos dará la shell con el usuario **leviathas7**

```bash
$ ./leviathan6 7123
```

:v: :sunglasses: :v:

**FLAG** = {ahy7MaeBo9} 
