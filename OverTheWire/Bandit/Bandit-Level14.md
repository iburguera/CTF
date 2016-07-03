#Bandit Level 14 → Level 15

##Level Goal

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

##Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

##Helpful Reading Material

How the Internet works in 5 minutes (YouTube) (Not completely accurate, but good enough for beginners)
IP Addresses
IP Address on Wikipedia
Localhost on Wikipedia
Ports
Port (computer networking) on Wikipedia

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:


**FLAG** = {4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e}

Utilizamos esta contraseña para acceder al siguiente nivel o ya que hemos entrado en el nivel anterior la mantenemos abierta.

```bash 
$ ssh bandit14@bandit.labs.overthewire.org
```

Nos dicen que podemos sacar la contraseña poniendo el NetCat ```nc``` escuchando en le puerto 30000 utilizando el cat para el fichero bandit14

```bash
bandit14@melinda:/etc/bandit_pass$ cat bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
bandit14@melinda:/etc/bandit_pass$ cat bandit14 | nc localhost 30000
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

Primero probamos un simple cat al fichero bandit14 pero nos saca la password del nivel anterior. Buscamos otra diferente. Hacemos caso a lo que nos dice el enunciado y ponemos a escuchar el ```nc```en el puerto 30000 haciendo un pipe ```|```al ```cat```del fichero

Obtenemos el password de la prueba :)

**FLAG** = {BfMYroe26WYalil77FoDi9qh59eK5xNr}




