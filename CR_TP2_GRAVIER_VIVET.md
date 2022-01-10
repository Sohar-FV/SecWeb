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

1/ Avec gpg --gen-key, on peut générer une clé. Cependant pour pouvoir gérer des paramètres comme la durée de validité, il faut utiliser la commande suivante :
```gpg --full-generate-key :```

Dans les dialogues proposés lors de la saisie de la commande on indique les éléments suivants :

```
type de clé : (2) DSA et ElGamal
Durée de validité : 10 jours
Identité et phrase de passe.
```
Ceupgpl2tds

2/ Pour afficher la liste des clés on tape ```gpg --list-key```

On obtient l'affichage suivant :
```
gpg: vérification de la base de confiance
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: profondeur : 0  valables :   1  signées :   0
     confiance : 0 i., 0 n.d., 0 j., 0 m., 0 t., 1 u.
gpg: la prochaine vérification de la base de confiance aura lieu le 2022-01-20
/home/IUT/flvivet/.gnupg/pubring.kbx
------------------------------------
pub   dsa2048 2022-01-10 [SC] [expire : 2022-01-20]
      ED11E07580CB167934036CA6AEA54545D4D6DAD2
uid          [  ultime ] VIVET <florian.vivet@etu.uca.fr>
sub   elg2048 2022-01-10 [E] [expire : 2022-01-20]
```

3/

a) Pour récupérer l'empreinte de la clé on tape ```fpr```

On obtient l'empreinte suivante :
```Empreinte clef princip. : ED11 E075 80CB 1679 3403  6CA6 AEA5 4545 D4D6 DAD2```

b) Pour changer la date d'expiration on tape ```expire``` et on indique la nouvelle durée d'expiration.

c) Pour ajouter une photo à notre clé, on tape : ```addphoto``` puis on indique le chemin de la photo à utiliser.

d) Pour ajouter une sous-clé, on tape : ```addkey``` on sélectionne chiffremennt RSA et la validité de 4 jours.
```
type de clé : RSA (Chiffrement seul)
Durée de validité : 4 jours
```

e) Pour modifier les préférences de fonctions de chiffrement symétrique et de hachage, on utilise ```setpref AES192 SHA256```

f) On quitte avec ```save```

4/ On a supprimé notre ancienne clé avec 
```
gpg --delete-secret-keys {key_id}
gpg --delete-keys {key_id}
```
Pour supprimer la clé secrête puis la clé publique.

Puis on a regénéré une clé avec :
```
gpg --gen-key 
```
Et les paramètres correspondant : nom et mail universitaire.

5/
