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


-----BEGIN PGP PUBLIC KEY BLOCK-----

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
mBeuVaW6A12hVyNKBqrgj4ycrNnKOtTp
=Vyjl
-----END PGP PUBLIC KEY BLOCK-----
