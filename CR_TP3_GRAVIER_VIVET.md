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

## Exercice 4

### 1)

On a testé les Webmails suivants : Gmail, Free et 

Pour Gmail on a :
```
D'après la page d'information :
- Chiffrement avec TLS AES 128 GCM SHA256, avec des clés de 128 bits
- Le site expire le 2 mars 2022

D'après le certificat :
- Site valide entre le 08/12/2021 à 23:51:41 et le 02/03/2022 à 23:51:40
- Clé publique basée sur Elyptic curve de 256bit
- Signature avec SHA-256 with RSA Encryption
```

Pour Free on a :
```
Chiffrement avec TLS ECDHE RSA AES128 GCM SHA256, avec des clés de 128 bits
Le site expire le 16 juillet 2022 

D'après le certificat :
- Site valide entre le 15/07/2021 à 02:00:00 et le 16/07/2022 à 01:59:59
- Clé publique basée sur RSA de 2048bits
- Signature avec SHA-256 with RSA Encryption
```

