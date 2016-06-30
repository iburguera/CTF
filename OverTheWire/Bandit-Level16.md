#Bandit Level 16 → Level 17

##Level Goal

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

##Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

##Helpful Reading Material

Port scanner on Wikipedia

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {cluFn7wTiGryunymYOu4RcffSxQluehd}

```bash 
$ ssh bandit16@bandit.labs.overthewire.org
```

Nos conectamos a la máquina.

El enunciado no indica que podemos obtener las credenciales del siguiente nivel a algún puerto entre 31000-32000.

- 1 Primero tenemos que encontrar algún puerto que nos responda
  - Utilizaremos la herramienta ```nmap```para saber que puertos tiene abiertos
- 2 De los puertos abiertos que encontremos, **solamente uno** habla **SSL** y es quien nos dará la contraseña del siguiente nivel

Lanzamos el ```nmap```para que escanee los puertos que tiene abierto abiertos.

```bash
bandit16@melinda:~$ nmap -p31000-32000 localhost -v

Starting Nmap 6.40 ( http://nmap.org ) at 2016-06-30 12:57 UTC
Initiating Ping Scan at 12:57
Scanning localhost (127.0.0.1) [2 ports]
Completed Ping Scan at 12:57, 0.00s elapsed (1 total hosts)
Initiating Connect Scan at 12:57
Scanning localhost (127.0.0.1) [1001 ports]
Discovered open port 31790/tcp on 127.0.0.1
Discovered open port 31518/tcp on 127.0.0.1
Discovered open port 31046/tcp on 127.0.0.1
Discovered open port 31960/tcp on 127.0.0.1
Discovered open port 31691/tcp on 127.0.0.1
Completed Connect Scan at 12:57, 0.03s elapsed (1001 total ports)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0011s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds
```

Nos muestra los puertos abiertos que tiene pero no la descripcion del servicio. Hacemos uso del manual de **nmap** y buscamos el comando que nos de la descripción del servicio utilizado

```bash
$ man nmap
...
-sV (Version detection) .
           Enables version detection, as discussed above. Alternatively, you can use -A, which enables version detection among other things.
```

Agregamos el comando al comando anterior y nos muestra el resultado

```bash
bandit16@melinda:~$ nmap -p31000-32000 localhost -sV

Starting Nmap 6.40 ( http://nmap.org ) at 2016-06-30 12:57 UTC
Stats: 0:00:21 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 20.00% done; ETC: 12:59 (0:01:24 remaining)
Stats: 0:01:53 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 50.00% done; ETC: 12:59 (0:00:23 remaining)
Stats: 0:01:56 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 50.00% done; ETC: 13:00 (0:00:26 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00085s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  msdtc       Microsoft Distributed Transaction Coordinator (error)
31691/tcp open  echo          
31790/tcp open  ssl/unknown   <--- (ESTE ES EL QUE NOS INTERESA A NOSOTROS)
31960/tcp open  echo
```

Los demás puertos nos realizan un **echo** a los que mandamos como dice el enunciado. El otro puerto es de Microsoft Distributed Transaction Coordinator (error) al que no prestaremos atención en este caso.

OK! Tenemos la password actual del **nivel16** ubicada en **/etc/bandit_pass/bandit16** que es **cluFn7wTiGryunymYOu4RcffSxQluehd** y tenemos que mandarla usando **OpenSSL** al puerto **localhost:31790** que hemos sacado del **nmap**

Probamos de nuevo a mandar el comando utilizando el comando que nos dicen:

```bash
bandit16@melinda:/etc/bandit_pass$ echo `cat /etc/bandit_pass/bandit16` | openssl s_client -connect localhost:31790 -quiet
```

o sino tambien de esta manera:

```bash
bandit16@melinda:/etc/bandit_pass$ echo 'cluFn7wTiGryunymYOu4RcffSxQluehd' | openssl s_client -connect localhost:31790 -quiet 
```

BIEN! No obtenemos la password pero obtenemos la **CLAVE PRIVADA** que nos puede proporcionar el acceso al **nivel17**

```bash
bandit16@melinda:/etc/bandit_pass$ echo 'cluFn7wTiGryunymYOu4RcffSxQluehd' | openssl s_client -connect localhost:31790 -quiet 
depth=0 CN = li190-250.members.linode.com
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = li190-250.members.linode.com
verify return:1
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

read:errno=0

```

Utilizaremos el siguiente comando para conectarnos al **nivel17** :)

```bash
ikerburguera@MacBook-Pro-de-Iker:~/Desktop$ sudo ssh bandit17@bandit.labs.overthewire.org -i  sshkey17.private 
````


