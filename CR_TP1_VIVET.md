# Compte rendu TP1 - Sécurité WEB

https://sancy.iut-clermont.uca.fr/~lafourcade/WebSec.html

Réalisé le 07/01/2020 par Florian VIVET

## Lettre 0

Comme indiqué, le login, le password et le prénom sont les mêmes :  
```
Login = Password = Prénom = Pascal  
```
Login : Pascal  
Password : Pascal  

## Lettre 1

Cette énigme implique l'utilisation du code de César, avec chaque lettre décalée dans l'alphabet. Le début du message a la même forme que celui de la lettre précédente :   
```
D txl gh gurlw -> A qui de droit  
```
On en déduit le décalage :  
```
ABCDEFGHIJKLMNOPQRSTUVWXYZ  
XYZABCDEFGHIJKLMNOPQRSTUVW  
```
Déchiffrement du message :
```
Ceci est le code de Cesar empreur des romains. Le login de la prochaine lettre est toujours le meme et le mot de passe est le prenom de Cesar
```
Login : Pascal  
Password : Jules  

## Lettre 2

Ici on cherche le nombre de combinaisons différentes qu'un ordinateur peut calculer en 1 vie.
```
3GHz -> 3 000 000 000 Hz  
80 ans -> 2 522 880 000 s  

nb_ope = 2 522 880 000 / (1/3 000 000 000 000) = 7,56865*10¹⁸ opérations en une vie.  
```
105 possibilités par caractère:  On cherche ```105^x > t``` avec x le nombre de caractères
```
105⁹ = 1,55*10¹⁸  
105¹⁰ = 1,63*10²⁰  
```
Il faut donc au moins 10 caractères   

Login : Pascal  
Password : 10  

## Lettre 3

Le texte est composé de nombres avec 2 ou 3 chiffres inférieurs à 117 -> valeurs décimales de la table ASCII :
```
Le 15 mai 2020 a Aubiere A qui de droit Login identique et mot de passe ASCII pour la prochaine lettrePasca
```
Login : Pascal
Password : ASCII

# Lettre 4


Clé de hachage

Plusieurs lignes ont le même H(password). En regroupant les astuces des lignes avec le même hachage on a :

Alice 709 -> Yellow, Pokemon, Nintendo 
		  -> Pikachu

Blaise 637 -> Musique, Flute enchantée, Amadeus, Compositeur 
		   -> Mozart
Camille 722 -> Cubisme, Demoiselles d'Avignon, Guernica, Peintre, Pablo 
			-> Picasso

Login : Alice
Password : Pikachu

## Lettre 5

Chiffrement avec le code de Vigenère
```
HI TWGTAX FKX FEB NAPNA GJFU EARU IYCNEOLI JQMU

Heuyem 
```
On retrouve la signature à la fin et on en déduit la clé:
```
Chiffré : Heuyem
Clair :   Pascal
Clé :     SECWEB
```
En reportant la clé sur le reste du message :
```
Chiffré : HI TWGTAX FKX FEB NAPNA GJFU EARU IYCNEOLI JQMU Heuyem
Clé :     WE BSECWE BSE CWE BSECW EBSE CWEB SECWEBSE CWEB SECWEB
Clair :   LE SECRET EST DIX MILLE CINQ CENT QUARANTE HUIT PASCAL
```
Secret : 1548

Comme vu à la lettre 5 :

Login : Blaise
Password : Mozart

## Lettre 6


Hachage 2

On cherche N avec ASCII(ASCII(X, Y, Montant, BP, N)) divisible par 3 et 5

On a :  
```
X = A  
Y = B  
Montant = 5  
BP = 42  
```
Avec ? la valeur que l'on recherche :
```
ASCII(A,B,5,42,?) = H(A) + H(B) + H(5) + H(4) + H(2) + H(N)
                  = 65 + 66 + 53 + 52 + 50 + ?
                  = 286
```
On cherche alors N tel que :

ASCII((286 + ASCII(N))) est divible par 3 et par 5.

286 + 48 = 334 -> ASCII(334) = 51 + 51 + 52 = 154
286 + 49 = 335 -> ASCII(335) = 51 + 51 + 53 = 155 -> div par 5 mais par 3
286 + 50 = 336 -> ASCII(336) = 51 + 51 + 54 = 156
286 + 51 = 337 -> ASCII(337) = 51 + 51 + 55 = 157
286 + 52 = 338 -> ASCII(338) = 51 + 51 + 56 = 158
286 + 53 = 339 -> ASCII(340) = 51 + 51 + 57 = 159
286 + 54 = 340 -> ASCII(340) = 51 + 52 + 48 = 160 -> div par 5 mais pas 3
286 + 55 = 341 -> ASCII(341) = 51 + 52 + 49 = 169
286 + 56 = 342 -> ASCII(342) = 51 + 52 + 50 = 170 -> div par 5 mais pas 3
286 + 57 = 343 -> ASCII(343) = 51 + 52 + 51 = 171

!!! Le faire dans un programme


Comme vu à la lettre 5 :

Login : Camille
Password : Picasso
