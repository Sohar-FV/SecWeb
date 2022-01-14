# Sécurité WEB : TP3

https://sancy.iut-clermont.uca.fr/~lafourcade/WebSec.html 

## Exercice 1

### 1) 
Le Hash nous est indiqué par la valeur entre les deux premiers $, et le salt entre le deuxième et le troisième.
Ainsi , on a Hash : 1 et Salt : AAAA

Avec cette commande :
```
openssl passwd -1 -salt "AAAA" '!!1331xxx'
```
On retrouve le MDP hashé $1$AAAA$H9wXcd/WaaomJUgWKFspy

### 2)

Avec un script Bash
```shell
scheme='$1$BABA$DOzBWHNx08SgVSX/YuYvC/';
scheme2='$1$CACA$XLWo4OqFFCYICqYrZ0y5i/';
for line in $(cat phpbb.txt); 
do
       	code=$(openssl passwd -1 -salt 'BABA' "$line");
	if [[ "$code" == "$scheme" ]]
	then
		echo "1";
		echo "$line";
	fi

	code=$(openssl passwd -1 -salt 'CACA' "$line");
	if [[ "$code" == "$scheme2" ]]
	then
		echo "2";
		echo "$line";
	fi
done

```

On retrouve x mot de passe :
Pour $1$BABA$DOzBWHNx08SgVSX/YuYvC/ :
batman

Pour $1$CACA$XLWo4OqFFCYICqYrZ0y5i/ :
enigma

## Exercice 3

### 1)

mescomptes.mafrenchbank.fr
ebanking.bicec.com
homebank.argenta.be
secure.bankvanbreda.be

### 2)

Dans l'ordre, on obtient ces notes :  
A+  
B  
A+  
A+  

### 3)

Voici notre classement des meilleures banques ever :  
1 - mescomptes.mafrenchbank.fr  
2 - secure.bankvanbreda.be  
3 - homebank.argenta.be  
4 - ebanking.bicec.com  

Le 1 est premier car il a les valeurs de sécurité les plus élevées.  
Le 2 et le 3 ont les mêmes niveaux de sécurité, maiss le 2 est compatible avec TLS 1.3.  
Le 4 à la pire note.  

