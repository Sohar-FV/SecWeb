# TP2

https://sancy.iut-clermont.uca.fr/~lafourcade/WebSec.html

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

5/ Pour générer le certificat de révocation, on tape : ```gpg --gen-revoke {key_id}```
Créer un tel certificat permet de révoquer une clé lorsqu'elle est compromise, remplacée ou plus utilisée.

6/ Pour exporter la clé au format binaire, on tape gpg --export. On obtient la clé suivante :

```
��a�Uw
      �A<���s�-_Y�CA��*�
                        w��2�+��uGPr&2/$��/�GG��rr�CS���	�
                                                                 (�����G��^I�Ea�v�3h������iV�JUz{�q�G�pR��#��<}{h�">��L��z�F�!T��\����nDO����Qm{���/o�{��fR�U��j�q��yѾx'�H��}6-P�-0�n��D�����(�DYV����T��A@�t<¢T`^��e(R�|�D�~E/��w4x�$�e�S��9�v��
�O'U�"��X��
           ��{OK��O�D��݅�G�e��R���;�E�;��h>X3� VIVET <florian.vivet@etu.uca.fr>��
>!���̙OV�#8�K���wa�Uw	g
                         	
	
       �
	�K���wE�
                �.m&��)2&#$�E����9=4X�Y*U��ש��7�-�,X�g������-b�M�Y�N�cHT��l7�8�1�<W�g�Q��<��_S��8�Z��6��Xo��
      ��D��P:�L��ƙh�~U�9]z�8�Y7!�z��vf#���O�E�U��`[y�H���Qv��*^e�6�
@��E�=)Tr����q_����E 7��.ߘj/1mB��zO�p��dCmkC�̾��?�]93ٕ�&8�GqV�*�w�
..�
��h���Ө�@�k��w8�7>��Jȥ`�s-/Y�lb!qM��a�Uw��}�=��Z�Wm휷$r�3)
                                        �0Y� I�[�j���e潡��`)�E��87N7C'����F�����a�
                                                                                  ��-[͓��V��W߰�t�w�z�J�&,�Cg�U5�E���7d��:|��NH�׌�(�LFJ�D]�
                          �:������j	
�#a�~5�������ۖF�t���34�OV}�U��Ă��߄��ez{�`�v��G�B�2:e�IJ��u��������A�`�k޷Y��#I���_��lCp�U �lP�t!֌OO��ո�%&�H1<��dT��;���
&!���̙OV�#8�K���wa�Uw
                    	g
	�K���w0�
                ��Ǖ	%���l��Ц2��*��_Y�ᠣ�U[�?���u/�g�De<��7ă��m�GLx�%��
                                                                         u6v�̔��*�A���8�龄�L�.�
                                                                                             ,k_��h�Z��:tIs��8d�x�_"N�=���G~��y�
                                  ��R���X��>*��e�+���Q�z�ʮ`-2��P��N�e"�T5�v?y�0��?�g\��m:����u�,��]�`�ۚ��9�QPl�7���p%�InK�Я
��<ŗMn��+h"�Ž7�x���w���&l�e�ԃ?F�%�E�>�l
                                       !Qju�rK����Iq����6(l9����b�5��
                                                                     ���vܺJ�)p�ϧ��{D�bxB�QJ��AY��

```
Pour exporter la clé au format texte, on tape gpg --export --armor. On obtient la clé suivante :

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
ERHPp/zke0SxYngZQvlRSuWsw0FZyfw=
=i/ZG
-----END PGP PUBLIC KEY BLOCK-----
```

Votre clé publique :
```
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
sg40X3SW1cQ=
=T6+M
-----END PGP PUBLIC KEY BLOCK-----
```
7/
On a importé votre clé publique avec : ```gpg --import keyfile.key```
Puis on a chiffré un ```mail.txt``` avec la commande ```gpg --encrypt --sign --armor -r pascal.lafourcade@uca.fr mail.txt```
Vous avez normalement reçu notre mail avec un fichier chiffré et signé ```mail.txt.asc```

8/
