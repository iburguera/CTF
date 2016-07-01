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


  
