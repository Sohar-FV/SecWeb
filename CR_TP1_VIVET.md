# Compte rendu TP1 - Sécurité WEB

https://sancy.iut-clermont.uca.fr/~lafourcade/WebSec.html

Réalisé du 07/01/2022 au 10/01/2022 par Florian VIVET

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

```Le 15 mai 2020 a Aubiere A qui de droit Login identique et mot de passe ASCII pour la prochaine lettre Pascal```

Login : Pascal
Password : ASCII

# Lettre 4


Clé de hachage

Plusieurs lignes ont le même H(password). En regroupant les astuces des lignes avec le même hachage on a :
```
Alice 709 -> Yellow, Pokemon, Nintendo 
		  -> Pikachu

Blaise 637 -> Musique, Flute enchantée, Amadeus, Compositeur 
		   -> Mozart  
		   
Camille 722 -> Cubisme, Demoiselles d'Avignon, Guernica, Peintre, Pablo 
			-> Picasso  
```
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
Secret 1: 1548

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
Avec *N* la valeur que l'on recherche :
<pre>
ASCII(A,B,5,42,<i>N</i>) = H(A) + H(B) + H(5) + H(4) + H(2) + H(<i>N</i>)
                  = 65 + 66 + 53 + 52 + 50 + <i>N</i>
                  = 286
</pre>
On cherche alors N le plus faible possible tel que :

ASCII((286 + ASCII(*N*))) est divible par 3 et par 5.

Pour trouver cet valeur j'ai réalisé le programme suivant :  
```java
public class Main {
    public static void main(String[] args){
        int n;
        int val;
        int val_ascii;
        n = 0;
        val_ascii = 1;

        while ((val_ascii % 3) != 0 || (val_ascii % 5) !=0) {
            val = 286 + ASCII(Integer.toString(n));

            val_ascii = ASCII(Integer.toString(val));
            System.out.println(val_ascii);
            n++;
        }

        System.out.println("Terminé : n = " + (n-1) + " & tot = " + val_ascii);
    }

    // Renvoie le code ASCII de la somme des caractères de la chaîne passée en paramètre
    private static int ASCII(String s) {
        int result = 0;
        for (int i=0; i< s.length(); i++){
            result += s.charAt(i);
        }
        return result;
    }
}
```

On obtient le résultat suivant :
```Terminé : n = 89 & tot = 165```

Secret 2 : 89

Comme vu à la lettre 5 :

Login : Camille  
Password : Picasso

## Lettre 7

Bob doit trouver les 4 chiffres de la combinaison, avec 10 possibilités pour chaque chiffre. On sait qu'un chiffre est correct lorsqu'il est saisi.  
Dans le pire cas, où le code serait 9999 et où Bob testerait des valeurs à partir de 0 jusqu'à 9, on aurait :  
```
étape 1, trouver le premier chiffre : on teste les valeurs de 0 à 9 -> 10 combinaisons
étape 2, trouver le deuxième chiffre : on teste les valeurs de 0 à 9, mais on commence à partir de la 10ème combinaison de l'étape 1 -> 10 - 1 combinaisons
étape 3, trouver le troisième chiffre : idem -> 10 - 1 combinaisons
étape 4, trouver le troisième chiffre : idem -> 10 - 1 combinaisons
```
Au total, on a 37 combinaisons

Login : Pascal
Password : 37

## Lettre 8

Déchiffrement 

On sait qu'un produit est plus énergivore qu'un carré, donc sur le graphique fourni, un grand pic correspond à un produit et un petit pic à un carré.  
De plus on sait qu'un carré seul correspond au bit 0 et qu'un carré suivi d'un produit correspond au bit 1. 

En convertissant les pics de la courbe en binaire on obtient :

```000010110100000```

Comme la clé secrète est codée sur 14 bit, on obtient alors :

```00001011010000 -> 720```

Login : Pascal
Password : 720
