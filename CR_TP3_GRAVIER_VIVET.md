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

### 1) Mots de passe en clair

Aucune action particulière n'est réalisée, on récupère le login et le mot de passe depuis la page d'authentification avec la méthode POST et on le stocke directement dans la base de données

### 2) Mots de passe hashés

Même chose que la version précédente mais avant de stocker le mot de passe, on lance une fonction de hachage sur ce dernier. De plus pour vérifier la validité d'un mot de passe, on hache le mot de passe saisi et on le compare avec le mot de passe haché stocké dans la base.

```php
$hashed_passwd = hash('sha256', $passwd);
```

### 3) Mots de passe hachés et salés

Même chose que la version 2), mais on ajoute un sel à la fonction de hachage.

```php
$options = [
    'salt' => 12,
];
echo password_hash($passwd, PASSWORD_BCRYPT, $options);
```

### 4) Mots de passe hachés et salés

Même chose que le point précédent mais on ajoute un élément propre à l'utilisateur dans le sel :  

```php
$options = [
    'salt' => 12.$login,
];
echo password_hash($passwd, PASSWORD_BCRYPT, $options);
```

### 5) Mots de passe chiffré avec chiffrement symétrique puis hachés et salés

Avant d'effectuer le hachage et l'ajout du sel comme les points précédents, on applique un algorithme de chiffrement symétrique sur le mot de passe.
Ici on a utilisé AES-256-CTR avec la fonction suivante

```php
function encrypt($password) 
    {
        $output = false;
        $encrypt_method = "AES-256-CTR";
        $secret_key = 'xxxxxxxxxxxxxxxxxxxxxxxx'; // cle sur 256 bits
        $secret_iv = 'xxxxxxxxxxxxxxxxxxxxxxxxx'; // cle sur 128 bits
         // hash
        $key = hash('sha256', $secret_key);    
        // iv - encrypt method AES-256-CBC expects 16 bytes 
        $iv = substr(hash('sha256', $secret_iv), 0, 16);
        $output = openssl_encrypt($string, $encrypt_method, $key, 0, $iv);
        $output = base64_encode($output);
        return $output;
    }
```

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

### 2)

Après avoir modifié la variable $path dans mon ```.bashrc```  
Je me suis connecté à mon vdn avec ```vdn-ssh root@debian-1```  
On a ensuite essayé le déplacer des fichiers avec ```scp legravier@10.0.2.2:file.txt```  
puis dans l'autre sens avec ```vdn-scp file.txt root@debian-1```

### 3)

Après avoir suivi les préliminaires, le script testssl.sh reste introuvable sur vdn.  
Donc impossible de répondre à cette question. 
```
root@debian-1:~# ./testssl.sh -x ECDH proxy.iut-clermont.uca.fr
-bash: ./testssl.sh: Aucun fichier ou dossier de ce type
```
Commande rentrée après avoir effectué le vdn-start-secure-1 récupéré lors des préliminaires.

### 4)
Le résultat de la commande : ```openssl s_client -proxy 193.49.118.36:8080 -connect uca.fr:443```  
```
CONNECTED(00000003)
Can't use SSL_get_servername
depth=2 C = US, ST = New Jersey, L = Jersey City, O = The USERTRUST Network, CN = USERTrust RSA Certification Authority
verify return:1
depth=1 C = NL, O = GEANT Vereniging, CN = GEANT OV RSA CA 4
verify return:1
depth=0 C = FR, L = Clermont-Ferrand, O = Universit\C3\A9 Clermont Auvergne, CN = *.ed.uca.fr
verify return:1
---
Certificate chain
 0 s:C = FR, L = Clermont-Ferrand, O = Universit\C3\A9 Clermont Auvergne, CN = *.ed.uca.fr
   i:C = NL, O = GEANT Vereniging, CN = GEANT OV RSA CA 4
 1 s:C = NL, O = GEANT Vereniging, CN = GEANT OV RSA CA 4
   i:C = US, ST = New Jersey, L = Jersey City, O = The USERTRUST Network, CN = USERTrust RSA Certification Authority
 2 s:C = US, ST = New Jersey, L = Jersey City, O = The USERTRUST Network, CN = USERTrust RSA Certification Authority
   i:C = GB, ST = Greater Manchester, L = Salford, O = Comodo CA Limited, CN = AAA Certificate Services
 3 s:C = GB, ST = Greater Manchester, L = Salford, O = Comodo CA Limited, CN = AAA Certificate Services
   i:C = GB, ST = Greater Manchester, L = Salford, O = Comodo CA Limited, CN = AAA Certificate Services
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIHXzCCBUegAwIBAgIRALDT5DNsnqIQDpGCzfy0JoYwDQYJKoZIhvcNAQEMBQAw
RDELMAkGA1UEBhMCTkwxGTAXBgNVBAoTEEdFQU5UIFZlcmVuaWdpbmcxGjAYBgNV
BAMTEUdFQU5UIE9WIFJTQSBDQSA0MB4XDTIxMDUyNzAwMDAwMFoXDTIyMDUyNzIz
NTk1OVowZjELMAkGA1UEBhMCRlIxGTAXBgNVBAcTEENsZXJtb250LUZlcnJhbmQx
JjAkBgNVBAoMHVVuaXZlcnNpdMOpIENsZXJtb250IEF1dmVyZ25lMRQwEgYDVQQD
DAsqLmVkLnVjYS5mcjCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBANsC
b9z0ozyQDYSdL0CaBj2aiKI5S4InQbtzOmk7klZoLBCqdd3XeQ80zda4Yxsw8sDV
mFdNKyizrbSrEpKTuJ3viUEu7/OWFCCx8Ag6b5kEe7EyTPOppRidaKNjnGBHaqJT
zGpLLKGjUxWyLY8wsQ2tEotd7XroGBRkTLOtygJ0QxzWtSQHrahK3JV361zxSK8n
xWkiAYQwZ6dCOGoQwDT3x4GS7BDFC7dQ/oP+hkEuE0q/sisrCvPxnYOMfBQL1MY8
9eTL2oongXs9WGosuLEgT9BDrtTNY3Gd5a82XrrbJmnHa3KNKVTovfXqCexlC6s7
Fy9mGyXyVPVxfh7q9u8CAwEAAaOCAygwggMkMB8GA1UdIwQYMBaAFG8dNUkQbDL6
WaCevIroH5W+cXoMMB0GA1UdDgQWBBQsYpe2fp+nMcrClwx3LpDaTweofzAOBgNV
HQ8BAf8EBAMCBaAwDAYDVR0TAQH/BAIwADAdBgNVHSUEFjAUBggrBgEFBQcDAQYI
KwYBBQUHAwIwSQYDVR0gBEIwQDA0BgsrBgEEAbIxAQICTzAlMCMGCCsGAQUFBwIB
FhdodHRwczovL3NlY3RpZ28uY29tL0NQUzAIBgZngQwBAgIwPwYDVR0fBDgwNjA0
oDKgMIYuaHR0cDovL0dFQU5ULmNybC5zZWN0aWdvLmNvbS9HRUFOVE9WUlNBQ0E0
LmNybDB1BggrBgEFBQcBAQRpMGcwOgYIKwYBBQUHMAKGLmh0dHA6Ly9HRUFOVC5j
cnQuc2VjdGlnby5jb20vR0VBTlRPVlJTQUNBNC5jcnQwKQYIKwYBBQUHMAGGHWh0
dHA6Ly9HRUFOVC5vY3NwLnNlY3RpZ28uY29tMCEGA1UdEQQaMBiCCyouZWQudWNh
LmZyggllZC51Y2EuZnIwggF9BgorBgEEAdZ5AgQCBIIBbQSCAWkBZwB1AEalVet1
+pEgMLWiiWn0830RLEF0vv1JuIWr8vxw/m1HAAABea0r5t8AAAQDAEYwRAIgTVe1
tyTISmrreB54+kRTJLo/yuj5Mrvwb+eubu1veV4CIEf2C84TNzOF4SYprC6RrISD
tDLO7JxL/jX8JqznXLAMAHYAQcjKsd8iRkoQxqE6CUKHXk4xixsD6+tLx2jwkGKW
BvYAAAF5rSvmxQAABAMARzBFAiAFEOE5wppm9n3HbPqZeJkPEV8OGUYeRVDoY4ii
lDQzSwIhAP7dZUZnlQE7bpMr1D61Hwfxk3pwJbWk2bq6NMsCRR62AHYAKXm+8J45
OSHwVnOfY6V35b5XfZxgCvj5TV0mXCVdx4QAAAF5rSvmmAAABAMARzBFAiAP5kbY
q94Mm9Nrvr8hvof9+lOXmIydZGEbgdt+MoPPbAIhANFzbXW7mbIiidMP3mtXqvje
yaEJOxjoTpLXoy4rj9O1MA0GCSqGSIb3DQEBDAUAA4ICAQAoTlJE7bZKZ6NQPASG
THOXKWFMI+gv5zaADOCwNhRFnf/2e+RhgnFB0n2nOk5Fff82sJ3x5ErUGoaMNZI8
teVmxDH9Vgn+S6bPxj5fzsltPhIxYUWr9/R4ONEAd66HtvNKhy1qYU/hhxM0o/Gj
TKo8JJs/sMUTAl0MQoI6VSgHFVIYHTagsDFmllG95wLbxT43Fl3MPjNHcdAj24hm
mzHgRWvAwot96iVhDsmnspgQPm4wrzCzSJdrxKXJy8FiKrG2mq2tDnMcECt+56mD
++YwhjGUZZ6kQI6D8zzVp+q7HTLAgQtDsVmevlypuwwRcHFYBk4hcBqdUPdqG5Xw
BYIlhyTTgbsGJMQ7vN3IAzgJNgLuicMZQu6msTePJ+e5dvKImkllBfwq61+U2DAr
ZXQWbPkcFc3TSgvL3ZKAf0x4TJH1/80pBgaBaZPthuC8bqA/BTHLjqh36cmDVssC
QWli2/ra8GB6oXuPRvRq7RKFvyYlZSLdsO1bSIuP+TKei2Bsa1SggtEg2Hlipf34
CoewbHM/EmbpeAjNAf1ev7UYo/mTfhyCjg2udgVnZr/9+qYbgGzvZAp+ajWoD1w9
igXT8irobljdtNFf6HOZl1sXjHKUFBhdgkTH7kOkPPCKVA40c5CMUMi8rUc1Ukkq
IXOQgx7MHLKLzePqW75wv06VgQ==
-----END CERTIFICATE-----
subject=C = FR, L = Clermont-Ferrand, O = Universit\C3\A9 Clermont Auvergne, CN = *.ed.uca.fr

issuer=C = NL, O = GEANT Vereniging, CN = GEANT OV RSA CA 4

---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 6761 bytes and written 394 bytes
Verification: OK
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 0 (ok)
---

---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 59B113A05E61911BA2BA090D4C91F6C04AC5958C877796735FAE732A69FC898E
    Session-ID-ctx: 
    Resumption PSK: 55B13116B73CAEB77D8C3121F31AF2F5C5EE5E3B1B7FBCFC60A39DE6F776C2E8E65632F250EC4EB4556266520F9C3701
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 54 b4 d0 63 6c 3f df e1-3d 53 75 aa 6e fa a4 ae   T..cl?..=Su.n...
    0010 - 56 93 81 d4 29 30 39 4e-c2 09 06 1c 8d 36 5e d4   V...)09N.....6^.
    0020 - eb 97 5c 53 96 db ad 17-9d f6 3c f6 54 a8 40 1e   ..\S......<.T.@.
    0030 - db 5b 46 9f f2 f4 8e f7-ec fc 18 96 70 ba 67 01   .[F.........p.g.
    0040 - f7 6e 92 df 6d 96 2b fe-98 1f 43 1e 14 c6 22 b3   .n..m.+...C...".
    0050 - 58 e4 7c 53 1a 0a 46 c2-88 50 c2 2b 66 3b 9e e1   X.|S..F..P.+f;..
    0060 - 4a 18 8d ed d2 5c e4 d1-d0 0e b2 58 cc ca ae 4b   J....\.....X...K
    0070 - ff c7 e0 1b cb ab af 92-63 3e a8 02 16 29 3e 8d   ........c>...)>.
    0080 - 19 b8 08 ba 60 c3 fb 14-56 34 9e 7c fd db 77 85   ....`...V4.|..w.
    0090 - a4 b1 4f e2 a9 b7 4c 8d-24 4e de 0e 71 71 2c e7   ..O...L.$N..qq,.
    00a0 - 78 12 96 6d e1 c8 89 3b-f6 6a 30 f8 0b 9f 7c 4f   x..m...;.j0...|O
    00b0 - 40 9e 02 bb c4 88 23 b8-4e 2f 48 ae d7 a3 62 c3   @.....#.N/H...b.
    00c0 - 6e cb ca dc 59 76 28 ea-8c e5 bc e6 e8 c3 a2 c0   n...Yv(.........
    00d0 - a6 09 ab fb 7c 00 d3 17-5d d0 72 1d e9 06 f1 a6   ....|...].r.....

    Start Time: 1642607765
    Timeout   : 7200 (sec)
    Verify return code: 0 (ok)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 99184A99AFAC06F1634A9C8F4F0F64DBE6D3C209907187149C4C07348A710414
    Session-ID-ctx: 
    Resumption PSK: EB7A23233DB109768F16482AA57F7D05D41912BFCDA5A5BD4DC6D776CDA8B064E3DB9B673A104DC9B70DC1D217D21408
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 54 b4 d0 63 6c 3f df e1-3d 53 75 aa 6e fa a4 ae   T..cl?..=Su.n...
    0010 - f7 42 e5 26 6b d4 37 08-f8 6d 5f 82 eb 8d 7a 44   .B.&k.7..m_...zD
    0020 - b7 d0 a2 2d 5a e4 f1 42-ad 71 95 d5 43 57 a1 0f   ...-Z..B.q..CW..
    0030 - a2 b3 60 54 a5 e0 e9 83-2d a9 76 7e ec cc 64 1a   ..`T....-.v~..d.
    0040 - de d0 f1 3f ca 35 9e f5-e9 a8 ad 88 eb 3d a0 b8   ...?.5.......=..
    0050 - 09 a0 16 35 7b 49 d7 f0-78 02 07 1c b3 83 9f f8   ...5{I..x.......
    0060 - 3a 0e 88 c0 73 99 07 1f-1b 8b 03 c4 43 76 70 8f   :...s.......Cvp.
    0070 - c2 87 ec b2 86 64 fc f8-56 6a 96 e5 13 df 6d d7   .....d..Vj....m.
    0080 - 7b eb 5e d1 2c 9a 77 04-4f 6c 2a 9a 8a 0a 78 cb   {.^.,.w.Ol*...x.
    0090 - 77 5d 0e b6 1f 8b 4a 5e-e5 dd 2c 21 57 fc 49 a3   w]....J^..,!W.I.
    00a0 - a8 07 c4 91 9f 05 95 f4-f0 a6 07 39 67 5b a3 cc   ...........9g[..
    00b0 - f3 ed 93 07 ad 8a 46 ea-33 ff 63 7a 4c 85 0d 4b   ......F.3.czL..K
    00c0 - 15 a5 e1 b4 a5 54 07 ff-52 84 3d 39 e8 e9 5b 7e   .....T..R.=9..[~
    00d0 - 22 9d bb 1b 79 f6 43 dc-a5 53 81 6a aa 95 0d 93   "...y.C..S.j....

    Start Time: 1642607765
    Timeout   : 7200 (sec)
    Verify return code: 0 (ok)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
closed
```

Le résultat de la commande : ```openssl s_client -proxy 193.49.118.36:8080 -connect limos.fr:443```  
```
CONNECTED(00000003)
Can't use SSL_get_servername
depth=2 C = US, ST = New Jersey, L = Jersey City, O = The USERTRUST Network, CN = USERTrust RSA Certification Authority
verify return:1
depth=1 C = NL, O = GEANT Vereniging, CN = GEANT OV RSA CA 4
verify return:1
depth=0 C = FR, L = Clermont-Ferrand, O = Universit\C3\A9 Clermont Auvergne, OU = ISIMA, CN = app.activmap.limos.fr
verify return:1
---
Certificate chain
 0 s:C = FR, L = Clermont-Ferrand, O = Universit\C3\A9 Clermont Auvergne, OU = ISIMA, CN = app.activmap.limos.fr
   i:C = NL, O = GEANT Vereniging, CN = GEANT OV RSA CA 4
 1 s:C = NL, O = GEANT Vereniging, CN = GEANT OV RSA CA 4
   i:C = US, ST = New Jersey, L = Jersey City, O = The USERTRUST Network, CN = USERTrust RSA Certification Authority
 2 s:C = US, ST = New Jersey, L = Jersey City, O = The USERTRUST Network, CN = USERTrust RSA Certification Authority
   i:C = GB, ST = Greater Manchester, L = Salford, O = Comodo CA Limited, CN = AAA Certificate Services
 3 s:C = GB, ST = Greater Manchester, L = Salford, O = Comodo CA Limited, CN = AAA Certificate Services
   i:C = GB, ST = Greater Manchester, L = Salford, O = Comodo CA Limited, CN = AAA Certificate Services
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIHlDCCBXygAwIBAgIQf+/ykADeyg+tcMI6z+amFzANBgkqhkiG9w0BAQwFADBE
MQswCQYDVQQGEwJOTDEZMBcGA1UEChMQR0VBTlQgVmVyZW5pZ2luZzEaMBgGA1UE
AxMRR0VBTlQgT1YgUlNBIENBIDQwHhcNMjEwNjIzMDAwMDAwWhcNMjIwNjIzMjM1
OTU5WjCBgDELMAkGA1UEBhMCRlIxGTAXBgNVBAcTEENsZXJtb250LUZlcnJhbmQx
JjAkBgNVBAoMHVVuaXZlcnNpdMOpIENsZXJtb250IEF1dmVyZ25lMQ4wDAYDVQQL
EwVJU0lNQTEeMBwGA1UEAxMVYXBwLmFjdGl2bWFwLmxpbW9zLmZyMIIBIjANBgkq
hkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAvQgExti6GeCUg5dXvC+YqOOyCdukeJzo
tkQSVp6kCx+MIqg4QSQR+lWSFozzlBuKa6udZXkHejIyGrChZ3l9TxUnJ3qSInUa
hWPV4/DtNiX80hInWIi2W06UMqfJLv++5L1HPu7r3sOVTtR/F0MqXHzm3ET4MyCY
mzdKLZ4Z1yF6i+tmN6xbda8x0085EiDU2JWRIPmW78ZaoGuNOfrQqZ/iJA54iKud
YgPfskfHtvsHP4JIgdui2/BspdW3WeRYSZJGE75hrEBpjx/s//qI1jzea5s1lCVO
u29fvLftnyxE8j26q3jhy/M6gKO2b8sVy8LEAOK3J+s+mw9v7SdBMQIDAQABo4ID
QzCCAz8wHwYDVR0jBBgwFoAUbx01SRBsMvpZoJ68iugflb5xegwwHQYDVR0OBBYE
FNGN1lFgYxNsAjUg8h4MnHMlzV2IMA4GA1UdDwEB/wQEAwIFoDAMBgNVHRMBAf8E
AjAAMB0GA1UdJQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjBJBgNVHSAEQjBAMDQG
CysGAQQBsjEBAgJPMCUwIwYIKwYBBQUHAgEWF2h0dHBzOi8vc2VjdGlnby5jb20v
Q1BTMAgGBmeBDAECAjA/BgNVHR8EODA2MDSgMqAwhi5odHRwOi8vR0VBTlQuY3Js
LnNlY3RpZ28uY29tL0dFQU5UT1ZSU0FDQTQuY3JsMHUGCCsGAQUFBwEBBGkwZzA6
BggrBgEFBQcwAoYuaHR0cDovL0dFQU5ULmNydC5zZWN0aWdvLmNvbS9HRUFOVE9W
UlNBQ0E0LmNydDApBggrBgEFBQcwAYYdaHR0cDovL0dFQU5ULm9jc3Auc2VjdGln
by5jb20wOwYDVR0RBDQwMoIVYXBwLmFjdGl2bWFwLmxpbW9zLmZyghl3d3cuYXBw
LmFjdGl2bWFwLmxpbW9zLmZyMIIBfgYKKwYBBAHWeQIEAgSCAW4EggFqAWgAdgBG
pVXrdfqRIDC1oolp9PN9ESxBdL79SbiFq/L8cP5tRwAAAXo6X4WPAAAEAwBHMEUC
ICuY701qs8whb4YOa6yOHpanxRXrjAbLoSnW6F2biVl1AiEAp+BiV/oqN8UUSH3r
YzVCvGupglkZb/AF4nLOi6GIc9kAdQBByMqx3yJGShDGoToJQodeTjGLGwPr60vH
aPCQYpYG9gAAAXo6X4VFAAAEAwBGMEQCICXezg6QnbM+rnZAKiqV/X4clyJijGNG
sjGpA+n8iTdfAiB8kIrIeeXTbBWTy8lbSLjHoZ8dBNFwWVLJH3VZWeyQ5wB3ACl5
vvCeOTkh8FZzn2Old+W+V32cYAr4+U1dJlwlXceEAAABejpfhSAAAAQDAEgwRgIh
AKfy1m1yA9fR9cVlyQiMDLBGvkhNKGrsylD5/UyyAJ7MAiEAwij1T7AeKn7ME46q
3wd1MA68QbnbWe4F8k0h9l8gmhswDQYJKoZIhvcNAQEMBQADggIBAFA220Z8Zrpt
lrwo2bEXYafrAxp3aKRjOeTDgJSmo1wLxKgLqa5LfN+5qk5b0Ad67aMyePS0aqoI
lJYL8l8KwT2iHDXERAYDVQAuC+y4J+1lJo7WEro30IF1fg/I1RPH9TF0YBpMtfrT
Z2Dd3SKOVuXiqQVkbLaXq+z3Q20YUfdBHTPirkald55WsDonFthWFzRhyPCPdgZ/
mh+Z8+XhOn2y7DW4g2icGiHpKWdXEaFjhGjf5ht4BbC0pFcA/RcU8OW+s1gemX4V
ZnhGsq1l3lEPU8suF4xyM+F9kh+621ItkTBzC9MKxJpInkNdqrskug0CJXA1OrZb
H4lw/PvGHZY22UaUoWPOQN4Qs0NggD5ftagtEFEG/qmIf4AU4VveoNX5k80Y+tVn
xFBl8Y8d1LVyodwz+t9fLTepCdvSHeLUThCQKY3vZ9Yp9lwYF63fMd3PRHHb/+Bz
W+lQfgYHw+WD9LS3mB/I/lPo5zq2MLyTl6KXRmJKTdj1y2mEihARgpmbyIzLJfr0
+IkxutXq6xP8JyEvYVo2Q8avHeCbsh+vIcZPs3BcWTZ/eggk0MwwyWsIKyefqQCB
fUuQ58ztHuOap57FkSazoANJRrHNt0jHZ9e+zX60WsjeYky/unleDi29JD0/S3UB
7ufaoDYlafWZmhmAOpCx45dkIDFLrWim
-----END CERTIFICATE-----
subject=C = FR, L = Clermont-Ferrand, O = Universit\C3\A9 Clermont Auvergne, OU = ISIMA, CN = app.activmap.limos.fr

issuer=C = NL, O = GEANT Vereniging, CN = GEANT OV RSA CA 4

---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 6893 bytes and written 409 bytes
Verification: OK
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: D808EF6AA0BF3353AD0446CE4FE8FD304253FB2963A01D718CF692B17B627784
    Session-ID-ctx: 
    Master-Key: 2A2C02F3658BE55AE0A2A8EE615AC98397F2A34ACB80DE5D63A6875C1B570A61D49CD3D50854029981229DF7D9FE372F
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 44 00 60 60 54 a4 9c cf-ab 22 cb 43 b0 2f 53 ce   D.``T....".C./S.
    0010 - f2 93 96 7e b6 30 94 d5-ea da cc cb 9f 40 9a 63   ...~.0.......@.c
    0020 - 17 b0 90 3d c3 3c d2 7f-a9 f2 25 4f 46 0c eb 82   ...=.<....%OF...
    0030 - b5 57 3a 86 67 92 f5 d4-a4 40 5c 67 54 58 b3 98   .W:.g....@\gTX..
    0040 - ca 1f 01 0b f1 02 6c 29-bb 30 cc d6 5a 83 06 42   ......l).0..Z..B
    0050 - f2 3f 27 cb c4 ef cf 2e-72 e9 cd 23 07 d9 3c 8d   .?'.....r..#..<.
    0060 - d3 32 57 2a c1 87 ee 29-c9 8b 9e 7e 94 5f c6 e6   .2W*...)...~._..
    0070 - 6d d1 a7 e3 b5 73 2e f4-a4 99 c0 41 02 d3 e0 7c   m....s.....A...|
    0080 - bf 75 b7 6c 22 19 74 29-fe 4c 43 45 6d f7 47 8a   .u.l".t).LCEm.G.
    0090 - 85 ab a4 ec bd 0b fa 0d-2c fb 25 5b 52 f7 26 ed   ........,.%[R.&.
    00a0 - ad 93 90 4b ad 96 85 2a-ed c5 4b 51 d8 cd 32 54   ...K...*..KQ..2T

    Start Time: 1642608537
    Timeout   : 7200 (sec)
    Verify return code: 0 (ok)
    Extended master secret: yes
---

closed
```
