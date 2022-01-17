# Sécurité WEB : TP2

TP réalisé par Léo GRAVIER et Florian VIVET du 10/01/22 au 17/01/22

Sujet du TP : https://sancy.iut-clermont.uca.fr/~lafourcade/SECWEB/2022-TP2-Crypto-web.pdf

## Exercice 1 :

### 1) 
On a téléchargé deux images de 380x380 pixel.

### 2)
Suite à l'utilisation de la commande fournie :
```
openssl dgst -sha1 {file}
```

On obtient respectivement, pour ces deux images :
```
0b97a402464fe97b46b96ae55173e684eae7357f
8d65712dbcfcf461b10f9558ddd2fc4b0656fc45
```

### 3)
Avec le site SHA1 collider, on a généré deux pdf ayant le même hashage, mais contenant chacun une image différente.
On a vérifié le hashage avec la commande vue en 2/ :
```
e9c904df912511ca88bb9eb492e2418846ab50e4
e9c904df912511ca88bb9eb492e2418846ab50e4
```
## Exercice 2

### 1)
Avec gpg --gen-key, on peut générer une clé. Cependant pour pouvoir gérer des paramètres comme la durée de validité, il faut utiliser la commande suivante :
```gpg --full-generate-key :```

Dans les dialogues proposés lors de la saisie de la commande on indique les éléments suivants :

```
type de clé : (2) DSA et ElGamal
Durée de validité : 10 jours
Identité et phrase de passe.
```

### 2)
Pour afficher la liste des clés on tape ```gpg --list-key```

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

### 3)

Depuis le menu obtenu en tapant ```gpg --edit-key```, on effectue les opérations suivantes

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

### 4)
On a supprimé notre ancienne clé avec les commandes suivantes pour supprimer la clé secrète puis la clé publique
```
gpg --delete-secret-keys {key_id}
gpg --delete-keys {key_id}
```

Puis on a regénéré une clé avec :
```
gpg --gen-key 
```
Et les paramètres correspondant : nom et mail universitaire.

5/ Pour générer le certificat de révocation, on tape : ```gpg --gen-revoke {key_id}```
Créer un tel certificat permet de révoquer une clé lorsqu'elle est compromise, remplacée ou n'est plus utilisée.

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

mQGNBGHcVXcBDAC8QR48qsvhc4UtX1nVQ0Hlf8YqBOkLd7fipzLoK6+6dUdQciYy
LyTw2C/TR0e2AfFycsGCCB5DU+Ww/cwJmgsoFP+Kn6vHRx32/F5JkEVh23bQM2jW
3Bq6nK5pVqcJSlV6e4Rxv0eecFIUpOwjs8M8fXto8QQiGT7RwEyA9RF6jkbzIVSm
mlylpBKl0m5ET+XA6tdRbXuLEd7WL2+Ue5CYZlKDVajIapZxnc95HNG+eCfGSMLm
G+t9Ni1QyC0wD/pug7RE5Byqp+Ua5IbeObTLzjoHpjerSocAQ05ggju3nuj2eWOV
A2JRRh0uHWTe9N8sqIatHnc0eK4k6RvIZa1TBw4DGuE5f6R2h5sNnq+hcpYR5a8a
k948nA3pKAD9RFlW9JkbG/r3glSPvkFAsXQ8wqJUYAdewsllKBFShnzPRJIDfkUv
2wr4TydV7iLu7wVY+J0L+7F7T0uwF4ZP4b0cRPnT3YXhFUfrZavuUpCZ8aQ7nQFF
sTsCtBYS+Wg+WDMAEQEAAbQgVklWRVQgPGZsb3JpYW4udml2ZXRAZXR1LnVjYS5m
cj6JAdMEEwEKAD4WIQSB/4DMmU9WpCM4AQezS6+d+BUQdwUCYdxVdwIbAwUJA8Jn
AAULCQgHAgYVCgkICwIEFgIDAQIeAQIXgAAKCRCzS6+d+BUQd0WNC/YubSbl6Cky
JiMk4EXd+zAI7tc5PTRYEIxZKlXBsdepvrE3ky0GFvYGLBxYzWcB3fuuzcnCLWKq
TfJZuU6lY0hU9pJsN604HMkxxDxXkmfnUecUjTwQrYhfUxpW//mnkhPbNpi0WG+S
9Q2l8zh/9gVa4ZgMFxbJ2UT971A67EzJGcQXxplopX5VwjldeoE4s1k3If16puG4
dmYj1szITx6URRfIVZbjYFsDeYlIrqiOUXax8ipeZfKkHTapCkCt5kXuPSlUchSl
3fX3cV+MD9TU8UUgN6/HLt+Yag8vMW1Cq/KfehVPpXCe92RDbWtDv8y+FKUAkj/c
XTkz2ZWSJjiuR3EcVs8qyXf8Ci4HLu8Kt0aL2YTuqiO/+EvAp81RL0/VA0i0wU9b
52KPBXE6I4K/SRY09Qh7wmjarNQlpx0sXtLQfbY98MVayVdt7Zy3JHIGizMpDdbB
aMbw79Oo+kDNa8TxHnc4yjc+uoUeSsilH2Ducy0vWRfpbGIhF3EVTbkBjQRh3FV3
AQwAwDBZ9yBJp1ukaqHd4Y9l5r2hgrRgKdNF/wUQmTg3TgA3Qyf0squrRqaxArCD
0WHQDNfNLVvNk7nOVvTLAVffsBexdOaRyVqXEhKRlt9v9h3n9XvTp/X5Y4BHDgYh
N6CCIvtrg0biN81IZcVYO9hGSoREXawNQwBrTxTDS8JoZP4Iv6gFScQqF156ersY
p+i9883u/JbSU+joTkjS14yWKM9MDet3Dh0H/nrXStUBJiy3Q2faVTUU10Wk6rjz
N2Sp4zp8CxPOOvvgzBanttRqCQzhO0pAqyH93tcF7vZg8m+MzTF89gmDI1usyC0J
vBHBxxXwYUFDFkGDM+0N1CNhxn41lfyGpI2Z69uWRu50Feb1izM0nU9WfcZV9YnE
gvai34S9+mV6EHv+YNt2FJKlR6hCxDI6ZdBJSqyudaLorwabs528xOVB9IKzYIFr
3rdZ/uEjSdHvqN9fFvrebENwzlUg8GxQ03Qh1oxPT4Xt1bjzJSb6SDE8+cUSZFSu
izvTABEBAAGJAbwEGAEKACYWIQSB/4DMmU9WpCM4AQezS6+d+BUQdwUCYdxVdwIb
DAUJA8JnAAAKCRCzS6+d+BUQdzCfDACh8ceVCSWK2cRsogKu0KYyxfQqj8xfWa3h
oKOtVVuNP+oY+Y51L7RniERlPBP3ogE3xIMSHoGNbZlHTHjsJaLzC3U2dhXKzJTI
HBoq2kH31vs4FMTpvoTHAEyaLokLLEOlAVrSfow4evxSCX8Na1/I7miIWpzvBTp0
0QgESXO4Ets4ZI94zl8iTuw9haGVR36C6HnyjAAL+oZSBcvawliy8D4qlBCsZY4r
ovEUz1HimXrvyq5gLTL775BQn55OG2+mZSKcA1Q1kHY/eaYwopc/mGdcFJ/sbTqe
CI+Zf4vNGyTorXXpLLcF0l2NYJ7bmqHfOZZRUGykN8HK0HAlE+BJbhdLntCvCpiC
EDzFlwMGTW7t4ytoFSLKxb03i3ifncR38tzNJmyBZb/UgwU/RuSoJZFFlT6ZbAsh
UWp1tXJLm/aW1hhJcdIYnYWcG842KGw5vKfpxGLMBDX9gAyyuct5CHbcukqUKXDV
ERHPp/zke0SxYngZQvlRSuWsw0FZyfw=
=i/ZG
-----END PGP PUBLIC KEY BLOCK-----
```


### 7)
On a importé votre clé publique avec : ```gpg --import keyfile.key``` avec keyfile.key un fichier contenant la clé suivante :   

Votre clé publique :  
```
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
sg40X3SW1cQ=
=T6+M
-----END PGP PUBLIC KEY BLOCK-----
```

Puis on a chiffré un ```mail.txt``` avec la commande ```gpg --encrypt --sign --armor -r pascal.lafourcade@uca.fr mail.txt```
Vous avez normalement reçu notre mail avec un fichier chiffré et signé ```mail.txt.asc```

### 8)
Le fichier txt chiffré est deux fois moins volumineux que l'original. ```325942 -> 169850```  
Le fichier MP3 chiffré est plus lourd que l'original. ```6195911 -> 8342426```  

### 9)
Les fichiers chiffrés par le binôme pour l'un pour l'autre font la même taille après chiffrement. => 740 octets  
Les fichiers chiffrés avec AES256 font également la même taille, cependant ils sont beaucoup moins volumineux. => 48 octets.   
Dans ce cas on utilisé la commande suivante :    
```
openssl enc -e -aes-256-cbc -in fichier -out fichier_secret
```

## Exercice 3:

### 1)
On observe que l'on voit en clair le login et le mot de passe.

## Exercice 4:

### 1)
Avec la commande donnée, on a généré une clé rsa :
```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvQZBvYGM9UEmTv3keriYA9DhDWNbqOMQ3ld9hhW+SsX7ZaHA
0tXX/Qk83WCOGbNKC8taDYWEyTW8sdjWRAaAhYKp+yDfuxf6crdZhYkRVtqZqE1g
hKfQnO2jnvkU+6nAWHWNld4C3l2+YsaiLlN23+bYfya1xx+LnPKYR7Ez4BcdfOrE
CnzTHWSfr6aNUHpQvx6OlxZ9cdGX1BskdU4SvWmoh8KT0hGg+5GZQUhVlSFvewEp
bz5Y5O0DmmcidFcqU/WnaLHeeIanI/RPar/5Bt6PrBeseI73sDcSqvZjvCsawWAj
IM/yXmcjNpXIfSEmbRV1fJtz5bgEhhERw/V7FQIDAQABAoIBACFKNs2/QSn4XVzQ
Dism027onJoVA5GM2+2sjujMb4UPtSTDBgibrLxdoiCC3sPb9ZB6MdPrzeT518+i
lqnIU14wEuutcHms0WjerZ988lbPjPw9FGCIhY79szFOQMnJrZxmp5bbULoE3IDc
5rct7+Oi7kIGeUEmZxovB26o4K/4VIRB6vy5KujyY5HqQIn/50gXOkUVmjWJMZV3
Enfi7RkyefyYHTdx4A23PppRpqZeJdbm9pitZU6pqfo30cmetXxgpR2MqHBdXBdu
vU7XF16ZIfiAQybIEwJitxZN1fs1xLrNDztyGvrb/dbH7gsZKil2gA0/Va7KBFti
Q8yFN0ECgYEA7FfAFd/U4Ur9YfANjyhkTNyeORUfkEz2Li67fh5hmOpRv6TOyx+X
X+heZk4BKF2clYBwbkuwYMUXky028LBhf9CSOJnfJbWYL5eG/dGtbRAEc31x4TQz
MFj1GqCT3DyLnvcQJmh0TVhuy2RbZ8r0r6eZUejej6fYrqxv5hPDr2kCgYEAzL7/
IsYthRf5ko63l0fh0djdK8Icjx7WYAy3ndh3swBk5FaNLyIyDDUP4bFl8NfF4NTM
I8qdDUhbZC+TvM0hjsOpqmDy+LSbl8fOZ+A3cwp+AbUkI2L74Kj5c9NycrcIqWx/
DVgF+f7DI+c3HwVSRlxtJ/lsiRRnGFYiL9c1ZM0CgYBbztKNLL/TLIA1NTzvKW+c
8+56mhwCwAK5eenXWhHrhspuuaSi/wicdvWEpDSK66JR6OzDy58eWDGKOHwpDzsw
nWLPneYzDdGqWyBTJMpLnXc9LbO5Gb/wvf2odEw7t0E9ZRfe86CKExom5DslnI9k
VKSYTu91umvPnqhxJahUUQKBgGVyXUgFmZhQgMA1JpI2c5VeNnfv/eaMCPweUPxM
vUJb96GLoPixoMqbn/rbwv7KaqkzxtIVGivyphXF3RW3LeFm4TIiR0Eje9SAk6y0
U8UUdcqyze0apmJyVuck5ZghSJFpyKn76zorGNU5Qv6DzHhAY3VjCHwDN/G++8Fo
iHQhAoGAJ5VnQiIG8ZfrCDYBPIg1Sz8W3PhO77jyoJ6x3Gesp7YRiGgJcrqDo1cs
1wiKPNQyU0/MUeLCj1sBkufp8VAJAi7UiB1Qn4tTr1XC+8jkcLkTN6F8VS/nCDRd
TDAaAM1cEkVgn3kYqS3WtOZT9Qe896Iy2+bSdcKaJq6xJHSPOZA=
-----END RSA PRIVATE KEY-----
```

### 2)
Certificat du serveur :
```
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            3d:ac:59:77:f8:e3:20:a5:fc:32:c5:7a:08:ba:b1:db:17:02:08:ab
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = fr, ST = france, L = clermont, O = Internet Widgits Pty Ltd
        Validity
            Not Before: Jan 14 10:13:31 2022 GMT
            Not After : Feb 13 10:13:31 2022 GMT
        Subject: C = fr, ST = france, L = clermont, O = Internet Widgits Pty Ltd
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                RSA Public-Key: (2048 bit)
                Modulus:
                    00:f2:a7:33:cd:eb:d0:77:25:fe:ae:1d:f6:12:52:
                    53:d6:99:e9:97:8b:31:1e:e5:fa:50:4d:b6:a5:e6:
                    a4:b4:15:47:f4:15:88:31:69:f9:c9:55:35:b5:65:
                    7a:8c:d5:06:14:81:bc:3b:de:8e:af:7a:1a:3c:b8:
                    b4:cc:87:6a:53:ae:5b:58:61:75:07:1c:96:25:92:
                    ed:24:53:e5:5b:ab:78:a2:83:09:13:fd:51:92:f8:
                    59:d1:4b:cc:d9:14:47:5d:e4:60:72:f2:32:b3:ce:
                    b6:79:20:db:de:21:8f:bd:c9:54:41:d4:cc:3b:21:
                    17:4e:77:52:17:4a:9f:5a:2c:91:1a:49:42:eb:ad:
                    03:49:13:20:81:bd:d4:1e:8c:f6:18:58:9e:a9:2c:
                    0d:ed:9d:18:02:97:e4:96:8f:d2:e6:27:8f:f5:28:
                    94:74:c8:15:bb:fb:e9:31:46:ed:ec:b7:6c:25:a3:
                    3c:a6:4a:34:b1:ff:01:00:07:bc:14:be:8b:4f:98:
                    25:02:c3:3d:60:ce:97:c6:28:59:df:ad:97:f0:c8:
                    2c:15:79:1d:c0:83:05:7b:85:3e:b5:79:33:27:1d:
                    00:32:2a:91:cb:7e:42:f8:77:db:b4:e5:6f:97:76:
                    c3:13:be:9e:01:37:fd:5f:3a:5e:cb:f0:b6:fa:10:
                    8f:45
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Subject Key Identifier: 
                8F:4B:D0:D5:23:CA:E1:3E:07:BF:D2:18:FA:F5:01:1B:CA:93:CC:0A
            X509v3 Authority Key Identifier: 
                keyid:8F:4B:D0:D5:23:CA:E1:3E:07:BF:D2:18:FA:F5:01:1B:CA:93:CC:0A

            X509v3 Basic Constraints: critical
                CA:TRUE
    Signature Algorithm: sha256WithRSAEncryption
         bb:dc:0e:d4:94:a6:e8:d1:14:c6:3c:a4:bc:b7:f4:d5:0f:e9:
         7e:0e:1f:a1:fe:7d:bc:ae:e4:b0:33:db:e0:07:06:8c:91:70:
         58:25:18:6b:7f:3a:44:91:b9:c8:2c:2b:60:73:94:6a:e6:34:
         5f:5f:97:09:95:16:4b:3b:cd:b4:ff:8a:e3:cc:27:b1:26:ea:
         79:c4:56:68:9e:b1:a8:77:ca:66:4a:ac:d2:ea:11:a8:ec:42:
         d3:72:af:4b:99:82:0e:b2:00:99:8a:24:69:d6:a4:b1:80:f7:
         06:2c:3a:aa:51:aa:28:1c:7e:da:41:bf:5d:c4:76:aa:44:8a:
         60:93:26:1b:8d:05:e4:2d:3c:86:d0:5d:e7:aa:20:09:31:b5:
         bd:49:f6:7d:0f:39:1d:a0:66:bc:f4:8f:41:17:84:e2:44:71:
         2e:c2:8b:e2:a4:05:e5:6c:e0:42:9c:b7:c6:4a:d9:d9:6b:22:
         98:8f:b2:0e:cd:3a:98:31:f2:44:49:0e:26:4c:4f:dc:2c:5e:
         29:5a:9b:f0:53:fa:36:31:b6:b4:f1:9b:f7:24:e8:03:2f:45:
         34:6d:0c:bb:f1:6f:ec:d6:c3:32:60:e9:f9:b4:a8:0e:12:f0:
         e8:0e:4a:ba:a9:bb:c9:77:6c:6f:f1:01:f2:93:3d:95:37:9b:
         7a:76:94:5c
```

### 3)
On a établie la connection entre avec le serveur :
1er terminal :
```
 Start Time: 1642155326
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
cc
ca fonctionne
la connection est vraiment etablie hein
```

terminal serveur :
```
ACCEPT
-----BEGIN SSL SESSION PARAMETERS-----
MH4CAQECAgMEBAITAgQg8ruvgGMbZ9mdI+YVzYUAS5dQtRYWJfVbWlvGYHsHENIE
MOqYjM0dJTm/kTN6iEBfAT9pOebvVeZdmWGzZDiLPOdPoXZ6x+ZtWt9vn7SEDfy3
8aEGAgRh4U0+ogQCAhwgpAYEBAEAAACuBwIFAMddKoM=
-----END SSL SESSION PARAMETERS-----
Shared ciphers:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256:TLS_AES_128_GCM_SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:DHE-RSA-AES256-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
Signature Algorithms: ECDSA+SHA256:ECDSA+SHA384:ECDSA+SHA512:Ed25519:Ed448:RSA-PSS+SHA256:RSA-PSS+SHA384:RSA-PSS+SHA512:RSA-PSS+SHA256:RSA-PSS+SHA384:RSA-PSS+SHA512:RSA+SHA256:RSA+SHA384:RSA+SHA512:ECDSA+SHA224:RSA+SHA224:DSA+SHA224:DSA+SHA256:DSA+SHA384:DSA+SHA512
Shared Signature Algorithms: ECDSA+SHA256:ECDSA+SHA384:ECDSA+SHA512:Ed25519:Ed448:RSA-PSS+SHA256:RSA-PSS+SHA384:RSA-PSS+SHA512:RSA-PSS+SHA256:RSA-PSS+SHA384:RSA-PSS+SHA512:RSA+SHA256:RSA+SHA384:RSA+SHA512:ECDSA+SHA224:RSA+SHA224
Supported Elliptic Groups: X25519:P-256:X448:P-521:P-384
Shared Elliptic groups: X25519:P-256:X448:P-521:P-384
CIPHER is TLS_AES_256_GCM_SHA384
Secure Renegotiation IS supported
cc
ca fonctionne
la connection est vraiment etablie hein
```

