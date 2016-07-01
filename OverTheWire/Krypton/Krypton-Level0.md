#Krypton Level 0

##Level Info

Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:

S1JZUFRPTklTR1JFQVQ=

Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH. You can find the files for other levels in /krypton/

## Write Up Iker

La primera prueba es muy sencilla y nos dan una clave codificada en **Base64** con valor **S1JZUFRPTklTR1JFQVQ=**

Podemos utilizar alguna herramienta online o utilizar la herramienta de Linux que nos proporciona el servidor.

Nos conectamos a alguna máquina del juego anterior Bandit y utilizamos este comando:

```bash
bandit12@melinda:~$ echo 'S1JZUFRPTklTR1JFQVQ=' | base64 -d
KRYPTONISGREAT
```

**FLAG** = {KRYPTONISGREAT}
