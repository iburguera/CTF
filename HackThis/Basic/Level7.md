#HackThis - Basic -  Level 7

URL:      https://www.hackthis.co.uk/levels/basic+/7

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint
We are running a suspicious looking service. Maybe it will give you the answer.

## Explicación

Accedemos a la página web y el enunciado nos indica que tienen corriendo un servicio sospechoso en los servidores. 

¿Pero cual?

Para ellos vamos a utilizar la herramienta **NMAP** para hacer un scaneo de puertos al servidor y ver que puestos tiene abiertos y que son sospechosos

```nmap
nmap  -A -v www.hackthis.co.uk -p 1-65335
```

y este es el resultado:

```nmap
ikerburguera@MacBook-Pro-de-Iker:~$ nmap  -A -v www.hackthis.co.uk -p 1-65335

Starting Nmap 6.47 ( http://nmap.org ) at 2016-07-12 14:02 CEST
NSE: Loaded 118 scripts for scanning.
NSE: Script Pre-scanning.
Initiating Ping Scan at 14:02
Scanning www.hackthis.co.uk (85.159.213.101) [2 ports]
Completed Ping Scan at 14:02, 0.08s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 14:02
Completed Parallel DNS resolution of 1 host. at 14:02, 0.18s elapsed
Initiating Connect Scan at 14:02
Scanning www.hackthis.co.uk (85.159.213.101) [65335 ports]

Discovered open port 22/tcp on 85.159.213.101
Discovered open port 8080/tcp on 85.159.213.101
Discovered open port 80/tcp on 85.159.213.101
Discovered open port 443/tcp on 85.159.213.101
Discovered open port 6776/tcp on 85.159.213.101
Discovered open port 9051/tcp on 85.159.213.101

NSE: Script scanning 85.159.213.101.
Initiating NSE at 14:12
Completed NSE at 14:12, 20.52s elapsed
Nmap scan report for www.hackthis.co.uk (85.159.213.101)
Host is up (0.071s latency).
Not shown: 65328 filtered ports
PORT     STATE  SERVICE          VERSION
22/tcp   open   ssh              OpenSSH 6.0p1 Debian 4+deb7u3 (protocol 2.0)
| ssh-hostkey: 
|   1024 e6:0c:a8:3a:a7:8d:87:fd:ea:39:4b:db:42:5f:1b:95 (DSA)
|   2048 3d:01:d9:e6:b5:ef:c5:65:56:f9:06:89:78:69:32:a6 (RSA)
|_  256 3a:d9:13:c2:1d:15:34:53:fd:9f:e3:82:14:07:a6:96 (ECDSA)
80/tcp   open   http             nginx
|_http-generator: ERROR: Script execution failed (use -d to debug)
|_http-methods: No Allow or Public header in OPTIONS response (status code 301)
|_http-title: Did not follow redirect to https://hackthis.co.uk/
139/tcp  closed netbios-ssn
443/tcp  open   http             nginx
|_http-methods: No Allow or Public header in OPTIONS response (status code 400)
|_http-title: 400 The plain HTTP request was sent to HTTPS port
| ssl-cert: Subject: commonName=www.hackthis.co.uk
| Issuer: commonName=RapidSSL SHA256 CA - G3/organizationName=GeoTrust Inc./countryName=US
| Public Key type: rsa
| Public Key bits: 2048
| Not valid before: 2015-09-21T10:33:50+00:00
| Not valid after:  2017-12-23T06:35:30+00:00
| MD5:   7ba0 1141 38df cd6f 3d51 9c43 82fb cde8
|_SHA-1: a452 8695 9606 efda ff8e ebd0 8cfe 8a40 8a6e b536
|_ssl-date: 2016-07-12T12:12:10+00:00; 0s from local time.
| tls-nextprotoneg: 
|_  http/1.1
6776/tcp open unknown
8080/tcp open   ssl/http-proxy
|_http-favicon: Unknown favicon MD5: D41D8CD98F00B204E9800998ECF8427E
|_http-methods: No Allow or Public header in OPTIONS response (status code 200)
| http-server-header: Software version grabbed from Server header.
| Consider submitting a service fingerprint.
|_Run with --script-args http-server-header.skip
|_http-title: Site doesn't have a title.
| ssl-cert: Subject: commonName=www.hackthis.co.uk
| Issuer: commonName=RapidSSL SHA256 CA - G3/organizationName=GeoTrust Inc./countryName=US
| Public Key type: rsa
| Public Key bits: 2048
| Not valid before: 2015-09-21T10:33:50+00:00
| Not valid after:  2017-12-23T06:35:30+00:00
| MD5:   7ba0 1141 38df cd6f 3d51 9c43 82fb cde8
|_SHA-1: a452 8695 9606 efda ff8e ebd0 8cfe 8a40 8a6e b536
| sslv2: 
|   SSLv2 supported
|_  ciphers: none
9051/tcp open   ssl/tor-control?
| ssl-cert: Subject: commonName=www.fxnz34zcksaytd4dfz.net
| Issuer: commonName=www.7455fufc.com
| Public Key type: rsa
| Public Key bits: 1024
| Not valid before: 2016-04-12T23:00:00+00:00
| Not valid after:  2016-07-15T23:00:00+00:00
| MD5:   cc18 bc9a 3891 55cb 097e c24e 4f5d 5309
|_SHA-1: 91d9 dd00 0c93 0c45 cb26 505b f29e dae9 0af4 337c
|_ssl-date: 2016-07-12T12:12:10+00:00; 0s from local time.
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
Initiating NSE at 14:12
Completed NSE at 14:12, 0.00s elapsed
Read data files from: /usr/local/bin/../share/nmap
Service detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 591.71 seconds
ikerburguera@MacBook-Pro-de-Iker:~$ 
```

De todos los puertos que nos salen, el más sospechoso es el **6776** así que nos conectamos por telnet a ver que nos devuelve 

```bash
telnet 85.159.213.101 6776
```

```bash
ikerburguera@:~$ telnet 85.159.213.101 6776

Trying 85.159.213.101...
Connected to www.hackthis.co.uk.
Escape character is '^]'.

Welcome weary traveller. I believe you are looking for this: mapthat

Connection closed by foreign host.
```

¡BINGO! Nos devuelve la contraseña :smile:

**FLAG** = {mapthat}



