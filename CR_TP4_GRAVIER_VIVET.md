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






