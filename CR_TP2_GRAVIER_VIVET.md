# TP2

## Exercice 1 :

1/ On a téléchargé deux images de 380x380 pixel.

2/ Suite à l'utilisation de la commande fournie :
```
openssl dgst -sha1 {file}
```

On obtient, pour ces deux images :
```
0b97a402464fe97b46b96ae55173e684eae7357f
8d65712dbcfcf461b10f9558ddd2fc4b0656fc45
```

3/ Avec le site SHA1 collider, on a généré deux pdf ayant le même hashage, mais contenant chacun une image différente.
On a vérifié le hashage avec la commande vue en 2/ :
```
e9c904df912511ca88bb9eb492e2418846ab50e4
e9c904df912511ca88bb9eb492e2418846ab50e4
```
## Exercice 2

1/ Avec gpg --gen-key, on peut générer une clé. Cependant pour pouvoir gérer des paramètres comme la durée de validité, il faut utiliser gpg --full-generate-key :

```
gpg --full-generate-key
type de clé : (2) DSA et ElGamal
Durée de validité : 10 jours
Identité et phrase de passe.
```

Ceupgpl2tds
