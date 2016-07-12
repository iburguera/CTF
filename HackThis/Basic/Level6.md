#HackThis - Basic -  Level 6

URL:      https://www.hackthis.co.uk/levels/basic+/6

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

## Hint
This isn't the page I was looking for...

## Explicación

Accedemos a la página web y nos indican que tenemos que introducir los siguientes campos:

1. What is the IP of the server hosting this page: 
2. What company hosts our server: 
3. X-B6-Key header:

Vamos a empezar en orden

Tenemos que averiguar la dirección IP del servidor de hosting de la web **www.hackthis.co.uk**

Para ellos podemos ir a la página de [Ip Address Lookup](http://ip-lookup.net/domain.php) y ver la **IP** del servidor

##What is the IP of the server hosting this page: 

**85.159.213.101**

##What company hosts our server: 

Para saber quien es el **hosting** de esa dirección IP podemos hacer un **WHOIS** en la página [WHOIS](http://ping.eu/ns-whois/)

```html
inetnum	85.159.208.0 - 85.159.215.255
netname	EU-LINODE-20050406
country	GB
org	ORG-LL72-RIPE
admin-c	TA2589-RIPE
tech-c	TA2589-RIPE
status	ALLOCATED PA
remarks	This block is used for static customer allocations
remarks	Please send abuse reports to abuse@linode.com
mnt-by	RIPE-NCC-HM-MNT
mnt-lower	Linode-mnt
mnt-routes	Linode-mnt
created	2005-04-06T12:12:19Z
mnt-domains	Linode-mnt
last-modified	2016-04-14T07:47:42Z
source	RIPE # Filtered

% Information related to '85.159.208.0/21AS15830'

route	85.159.208.0/21
descr	Linode
origin	AS15830
mnt-by	Linode-mnt
created	2013-06-28T15:53:24Z
last-modified	2013-06-28T15:53:24Z
source	RIPE

```
Sacamos la conclusión que el hosting es [linode](https://www.linode.com/)

**linode**

```html
inetnum	85.159.208.0 - 85.159.215.255
netname	EU-LINODE-20050406
country	GB
org	ORG-LL72-RIPE
admin-c	TA2589-RIPE
tech-c	TA2589-RIPE
status	ALLOCATED PA
remarks	This block is used for static customer allocations
remarks	Please send abuse reports to abuse@linode.com
mnt-by	RIPE-NCC-HM-MNT
mnt-lower	Linode-mnt
mnt-routes	Linode-mnt
created	2005-04-06T12:12:19Z
mnt-domains	Linode-mnt
last-modified	2016-04-14T07:47:42Z
source	RIPE # Filtered
```

##X-B6-Key header:

Este es quizás el apartado más confuso de todos. 

El X-B6 Header es una cabecera de correo, por lo tanto tenemos que buscar un correo de **Hackthis** y pasarlo por la herramienta [MXToolBox Email Header](http://mxtoolbox.com/Public/Tools/EmailHeaders.aspx) y sacar la cabecera.

Para ello, vamos a ir a nuestro cliente de correo electrónico, como por ejemplo **GMAIL**, y vamos a escoger un correo que nos han mandado desde **Hackthis.co.uk**

Vamos a mostrar el contenido original del correo y copiamos ese contenido en la dirección:

```html
http://mxtoolbox.com/Public/Tools/EmailHeaders.aspx
```

Buscamos el término **X-B6** en el resultado y nos da el siguiente texto:

```html
Lajklsb#!"3jlak
```

Por lo tanto, ya tenemos toda la información que necesitamos para pasar el reto:

```html
85.159.213.101
linode
Lajklsb#!"3jlak
```

Introducimos los términos en la correspondientes campo y pasamos el reto :beers:

**FLAG** = {85.159.213.101/linode/Lajklsb#!"3jlak}






