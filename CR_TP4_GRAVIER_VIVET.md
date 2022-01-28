# Sécurité Web : TP4

https://sancy.iut-clermont.uca.fr/~lafourcade/SECWEB/2022-TP4-Bof-SQL.pdf

Réalisé par Léo Gravier et Florian VIVET le 21/01/2022

## Exercice 1

### Config : on a lancé les commandes suivantes :

Configurer vdn :  
```
wget https://sancy.iut-clermont.uca.fr/~lafourcade/SECWEB/baseConfigSecure-1.txt
vdn-scripts $PWD/baseConfigSecure-1.txt
vdn-ssh root@debian-1
```
note : vdn-start-secure-1 était déjà disponible sur notre session.  

Lancer le projet avec docker :  
```
https://sancy.iut-clermont.uca.fr/~lafourcade/SECWEB/SQLIA.tar
tar -xvf SQLIA.tar
cd ./SQLIA
docker-compose-up
```
Désactiver le proxy :  
```
unset http_proxy
unset https_poxy
```

### 1) SQL Injection

Mot de passe pas testé
```
mdp"' OR 'x'='x' LIMIT 1;--
```

## Exercice 2

Avec le fichier file.c suivant :
```c
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>
int main(int argc, char **argv)
{
  int modified;
  char buffer[64];
  modified = 0;
  gets(buffer);
  if(modified != 0) 
  {
    printf("you have changed the ’modified’ variable\n");
  } else {
    printf("Try again?\n");
  }
  return 0;
}
```

On cherche à modifier la variable qui contient 0 (modified). Pour cela on va essayer de créer un buffer overflow sur la variable buffer qui a une taille de 64. Il faut donc donner en paramètre de la fonction une valeur qui fait plus de 64 caractères.

## Exercice 3

```
import time

global password

def crack():
    bobo = False
    num = 0
    while (num < 1000000) & (bobo == False):
        x = '{0:06}'.format(num)
        bobo = checkpassword(x)
        if bobo :
            return '{0:06}'.format(num)
        num = num + 1
    return -1

def checkpassword(l):
    for i in range(len(password)):
        #time.sleep(1)
        if password[i]!= l[i]:
            return(False)
    return(True)
    
password=input("L’ordi va deviner votre code PIN de chiffres entre 0 et 9 de longeur 6 : ")
p = str(crack())
print("Le mot de passe est : "+p)
```

import time

global password

def bruteForce():
    bobo = False
    num = 0
    while (num < 1000000) & (bobo == False):
        x = '{0:06}'.format(num)
        bobo = checkpassword(x)
        if bobo :
            return '{0:06}'.format(num)
        num = num + 1
    return -1
    
    
def sideChannel():
    pwd_to_test = "000000"
    
    bobo = False
    while bobo == False :
        start = time.time()
        #checkpassword
        #
        #
        end = time.time()
        r = end - start
        if r != 1 :
            #
    return result

def checkpassword(l):
    for i in range(len(password)):
        time.sleep(1)
        if password[i]!= l[i]:
            return(False)
    return(True)
    
password=input("L’ordi va deviner votre code PIN de chiffres entre 0 et 9 de longeur 6 : ")
#p = str(bruteForce())
p = str(sideChannel())
print("Le mot de passe est : "+p)

## Exercice 4  

2/  
Nous remarquons que la connexion à un même site est plus lente avec Tor qu'avec les autres navigateurs.  
On explique cela car avec Tor, la requête est chiffrée pour les différents serveurs par lesquels elle va passé. Le temps de chiffrement et de déchiffrement est donc assez long et ralenti la requête (mais offre une sécurité importante).  

3/  
Les circuits sont différents pour chaque connexion, il s'agit toujours d'un circuit de trois machines.  

4/  
On remarque que lorsque l'on se rend sur le site https://iplookup.flagfox.net/ avec Firefox, le site est capable de donner le lieu d'où notre connexion est établie.  
Avec Tor, le site indiquera la position du dernier serveur par lequel la requête passera, il ne sera donc pas capable de déterminer notre position.  

7/  
L'extension .onion est conçu pour ne pouvoir se suivre qu'avec Tor.





