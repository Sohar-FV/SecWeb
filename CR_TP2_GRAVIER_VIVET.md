# TP2

Exercice 1 :

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
