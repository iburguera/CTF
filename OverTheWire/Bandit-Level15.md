#Bandit Level 15 → Level 16

##Level Goal

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…

##Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

##Helpful Reading Material

Secure Socket Layer/Transport Layer Security on Wikipedia
OpenSSL Cookbook - Testing with OpenSSL

## Write up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {BfMYroe26WYalil77FoDi9qh59eK5xNr}

Utilizamos esta contraseña para acceder al siguiente nivel o ya que hemos entrado en el nivel anterior la mantenemos abierta.

```bash 
$ ssh bandit15@bandit.labs.overthewire.org
```

Según el enunciado, podemos obtener la contraseña para el siguiente nivel enviando la contraseña actual de este nivel15 al puerto 30001 utilizando **SSL Encryption**

```bash
bandit15@melinda:/etc/bandit_pass$ cat bandit15
BfMYroe26WYalil77FoDi9qh59eK5xNr
```
Enviaremos esa contraseña cifrada usando openssl y escucharemos la respuesta en el puerto 30001

Leemos la documentación que nos proporcionan para ver como podríamos hacerlo:

```html 
https://www.feistyduck.com/library/openssl-cookbook/online/ch-testing-with-openssl.html
```

Utilizamos el código de ejemplo para modificarlo a nuestro antojo.

```bash 
Ejemplo: openssl s_client -connect www.feistyduck.com:443
Nuestro: openssl s_client -connect localhost:30001
````
OK! Tenemos nuestro comando preparado y ahora tenemos que leer la contraseña del nivel15 ubicada en **/etc/bandit_pass$ cat bandit15**  que es **BfMYroe26WYalil77FoDi9qh59eK5xNr** y la mandamos cifrada usando **OpenSSL** haciendo un  ``` echo cat```al fichero

Quedando el comando completo de la siguiente manera:

```bash
echo `cat /etc/bandit_pass/bandit15` | openssl s_client -connect localhost:30001    
```

Obtenemos respuesta del servidor, pero no es la contraseña que esperábamos:

```bash
bandit15@melinda:/etc/bandit_pass$ echo `cat /etc/bandit_pass/bandit15` | openssl s_client -connect localhost:30001 
CONNECTED(00000003)
depth=0 CN = li190-250.members.linode.com
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = li190-250.members.linode.com
verify return:1
---
Certificate chain
 0 s:/CN=li190-250.members.linode.com
   i:/CN=li190-250.members.linode.com
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIC3jCCAcagAwIBAgIJAI5QiWZw4YHbMA0GCSqGSIb3DQEBCwUAMCcxJTAjBgNV
BAMTHGxpMTkwLTI1MC5tZW1iZXJzLmxpbm9kZS5jb20wHhcNMTQxMTE0MTAyODA0
WhcNMjQxMTExMTAyODA0WjAnMSUwIwYDVQQDExxsaTE5MC0yNTAubWVtYmVycy5s
aW5vZGUuY29tMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsKmy9o5z
WU+1EH7Z3bB5TGQA+16zXDcEJy6tZWZ8CDrRyQXiahendp45BWUc/ZuLDo0+B3Wt
ZXjofmLw/F4fmR+8X1s1fQZX2dFt920qEm7LxqzWd0c7FdHiBwwRrwhkk+3cQpOB
TTGdLWEgpdmwwNZDTUdsDLzjDczPnju6T6p6ArTECztPbmTjfY4QIRtC6capL1Z+
yPJSQVAuAMEX1wTDWTGdm0VV7oW4F5cGZutf6QAP51jdhSyZuGilIPHbnj0l6Qc7
a7+OtEsEGi31aJ8KpRf7LNZ7DXCuoB3Hf75Pd6VjDgoOIagcH0NYqa75gEjBkGzs
ktLWykT7ag7fKwIDAQABow0wCzAJBgNVHRMEAjAAMA0GCSqGSIb3DQEBCwUAA4IB
AQCaZdUNAj8WDEKWdoU3LNXUBJlTJwiWBrh550PbHSQORcCz2K0kiMei1A4ojK2N
dMHFGAqAeUEaxtz92p2BoFpZasAtdSa3u63tBckFhfUolIS1TC7Cj51y19ysTeep
fGPFpuPCVqVPsruei8Z/iqn3bFIhQQdmumeePZQdPMwZSWHNVYC5XODd7PvNDrDu
5MZJjkz4+6LbwwAvyew62meFN2QEsYbK2Brtbhze+IjE27FGWlSw4K3jlwa409MD
MTf4JU41ELaYY8G/LSNDJsBVhhkHzvXR9iCbXxNz3IL0dQDNj7h4LKhBy0q7hvqg
kDzwlmBO4WKSmCAuky44cXmd
-----END CERTIFICATE-----
subject=/CN=li190-250.members.linode.com
issuer=/CN=li190-250.members.linode.com
---
No client certificate CA names sent
---
SSL handshake has read 1714 bytes and written 637 bytes
---
New, TLSv1/SSLv3, Cipher is DHE-RSA-AES256-SHA
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
SSL-Session:
    Protocol  : SSLv3
    Cipher    : DHE-RSA-AES256-SHA
    Session-ID: 49CF6BC0D30A1BE66496CC582BC2489F71A3DCAC79BF62F0A0AAA0D180EE287B
    Session-ID-ctx: 
    Master-Key: 88D284DA928315622E93AFD099518DA34351E30E34D7B394E227BD7F7231CE261F0E88A3637BA408B30D0105A93BD066
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    Start Time: 1467289449
    Timeout   : 300 (sec)
    Verify return code: 18 (self signed certificate)
---
HEARTBEATING
DONE
```

Umm, volvemos a leer la documentación por que no se nos ocurre nada más :(

Después de Googlear un poco nos recomiendan utilizar la opción **-quiet** como argumento en el comando **openssl** para no mostrar la respuesta del servidor **No server output**

```bash openssl <parameters> -quiet        - No server output ````

Probamos de nuevo a mandar el comando utilizando el comando que nos dicen:

```bash
bandit15@melinda:/etc/bandit_pass$ echo `cat /etc/bandit_pass/bandit15` | openssl s_client -connect localhost:30001 -quiet
```

o sino tambien de esta manera:

```bash
bandit15@melinda:/etc/bandit_pass$ echo 'BfMYroe26WYalil77FoDi9qh59eK5xNr' | openssl s_client -connect localhost:30001 -quiet 
```

Esta vez si que hemos obtenido la flag que esperábamos :) 

```bash
bandit15@melinda:/etc/bandit_pass$ echo `cat /etc/bandit_pass/bandit15` | openssl s_client -connect localhost:30001 -quiet
depth=0 CN = li190-250.members.linode.com
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = li190-250.members.linode.com
verify return:1
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
read:errno=0
```

Este reto me ha llevado más tiempo del que esperaba. He tenido que leer mucho acerca de **OpenSSL** en las páginas que nos hacen referencia pero vamos, así es como se aprende ;)

**FLAG** = {cluFn7wTiGryunymYOu4RcffSxQluehd}
