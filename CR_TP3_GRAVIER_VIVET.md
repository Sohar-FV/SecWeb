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

## Exercice 2

### 1)
Mots de passe en clair

Aucune action particulière n'est réalisée, on récupère le login et le mot de passe depuis la page d'authentification avec la méthode POST et on le stocke directement dans la base de données

### 2)

Même chose que la version précédente mais avant de stocker le mot de passe, on lance une fonction de hachage sur ce dernier. De plus pour vérifier la validité d'un mot de passe, on hache le mot de passe saisi et on le compare avec le mot de passe haché stocké dans la base.

```php
$hashed_passwd = hash('sha256', $passwd);
```

### 3)

Même chose que la version 2), mais on ajoute un sel à la fonction de hachage.

```
$options = [
    'salt' => 12,
];
echo password_hash($passwd, PASSWORD_BCRYPT, $options);
```

### 4)

### 5)

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

On a testé les Webmails suivants : Gmail, Free et Orange mail

Pour Gmail on a :
```
D'après la page d'information :
- Chiffrement avec TLS AES128 GCM SHA256, avec des clés de 128 bits + TLS 1.3
- Le site expire le 2 mars 2022

D'après le certificat :
- Site valide entre le 08/12/2021 à 23:51:41 et le 02/03/2022 à 23:51:40
- Clé publique basée sur Elyptic curve de 256bit
- Signature avec SHA-256 with RSA Encryption
```

Pour Free on a :
```
Chiffrement avec TLS ECDHE RSA AES128 GCM SHA256, avec des clés de 128 bits+ TLS 1.3
Le site expire le 16 juillet 2022 

D'après le certificat :
- Site valide entre le 15/07/2021 à 02:00:00 et le 16/07/2022 à 01:59:59
- Clé publique basée sur RSA de 2048bits
- Signature avec SHA-256 with RSA Encryption
```

Pour Orange mail on a :
```
Chiffrement avec TLS ECDHE RSA AES128 GCM SHA256, avec des clés de 128 bits + TLS 1.2
Le site expire le 16 juillet 2022 

D'après le certificat :
- Site valide entre le 29/07/2021 à 02:00:00 et le 30/08/2022 à 01:59:59
- Clé publique basée sur RSA de 4096bits
- Signature avec SHA-256 with RSA Encryption
```

