#Bandit Level 20 → Level 21

##Level Goal

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: To beat this level, you need to login twice: once to run the setuid command, and once to start a network daemon to which the setuid will connect.

NOTE 2: Try connecting to your own network daemon to see if it works as you think

##Commands you may need to solve this level

ssh, nc, cat

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {GbKksEFF4yrVs6il55v6gwY5aVje5f0j}

Utilizamos esta contraseña para acceder al siguiente nivel.

```bash 
$ ssh bandit20@bandit.labs.overthewire.org
```

Nos conectamos a la prueba y analizamos como se comporta el programa

```bash
bandit20@melinda:~$ ls -l
total 8
-rwsr-x--- 1 bandit21 bandit20 8006 Nov 14  2014 suconnect
bandit20@melinda:~$ ./suconnect 
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
bandit20@melinda:~$ 
```

Parece que le tenemos que pasar un **Nº de Puerto** al programa **suconnect** para que se ponga a escuchar en la máquina peticiones de **Password** que le mandemos desde otra máquina.

Si la contraseña que enviemos al puerto donde está escuchando el programa suconnect es correcta nos devuelve la contraseña del siguiente nivel.

Entonces vamos a abrir dos terminales donde en una ejecutaremos el ```nc```y en el otro ejecutaremos el programa ```suconnect````

### Terminal 1

```bash
bandit20@melinda:~$ nc -l 4444
<aqui podemos meter la contraseña del nivel anterior: GbKksEFF4yrVs6il55v6gwY5aVje5f0j > 
```

### Terminal 2

```bash
bandit20@melinda:~$ ./suconnect 4444
```

Vamos al **Terminal 1** y escribimos la contraseña del nivel anterior: **GbKksEFF4yrVs6il55v6gwY5aVje5f0j** y observamos que en el **Terminal2** lee el valor de la contraseña y la valida, devolviéndonos la contraseña del siguiente nivel :) Ou yeah!!

### Terminal 1

```bash
bandit20@melinda:~$ nc -l 4444
GbKksEFF4yrVs6il55v6gwY5aVje5f0j     -> Password Enviado
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr     <- Password Recibido
```

### Terminal 2

```bash
bandit20@melinda:~$ ./suconnect 4444
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```
Nos devuelve la flag: gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr

**FLAG** = {gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr}
