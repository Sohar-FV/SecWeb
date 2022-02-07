# SECWEB TP5

Sujet : https://sancy.iut-clermont.uca.fr/~lafourcade/SECWEB/2022-TP5-http-https.pdf  

Réalisé par Léo GRAVIER et Florian VIVET

## Exercice 1 (Création des certificats auto-signés)

### 1)

Pour récupérer les informations du certificat, on a tapé la commande suivante :  
```
openssl x509 -text -in  /etc/ssl/certs/ssl-cert-snakeoil.pem
```

On peut voir que ce certificat est valable jusqu'au 05/02/2030.  
D'autres caractéristiques sont visible :

```
Certificate:  
    Data:  
        Version: 3 (0x2)  
        Serial Number:  
            20:4e:9e:9c:dd:2c:4e:71:cf:f1:44:a9:7e:bd:79:51:e1:97:a4:0d  
        Signature Algorithm: sha256WithRSAEncryption  
        Issuer: CN = debian  
        Validity  
            Not Before: Feb  8 14:26:24 2020 GMT  
            Not After : Feb  5 14:26:24 2030 GMT   
        Subject: CN = debian  
```

Il y a également la clé publique RSA, le certificat, et l'algorithme de signature.  

### 2)  

Ancien certificat et ancienne clé :  

```
Public Key Algorithm: rsaEncryption
                RSA Public-Key: (2048 bit)
                Modulus:
                    00:ad:28:d2:b5:12:c2:c8:32:6d:36:d1:0e:6c:aa:
                    c3:7e:5d:1e:40:45:fe:01:1e:9d:8a:b3:3b:57:69:
                    f0:f9:24:06:60:94:ce:f6:a7:ed:a3:9d:c5:86:dd:
                    29:00:89:a7:c6:7b:c5:11:fc:be:09:f3:21:74:a8:
                    07:61:e4:48:62:89:bb:dc:5a:d4:d2:c1:ae:59:67:
                    31:ad:dd:3c:e4:92:fc:7f:a9:d6:0c:aa:69:bc:d4:
                    1d:0d:ab:c6:b8:c8:52:0e:4e:8a:e8:6c:3c:0b:70:
                    d5:43:3e:42:7d:d2:e3:f5:d5:f7:e8:a0:30:66:ee:
                    85:3a:91:49:d8:d3:e6:85:a3:31:2a:33:ee:56:d3:
                    ab:83:1a:c5:17:cf:31:7c:85:0f:46:14:87:e0:42:
                    24:c3:b7:f7:e8:19:22:dc:ce:06:19:8f:94:ed:a7:
                    b3:88:24:1f:79:2c:0c:43:72:f7:6d:22:9b:2c:31:
                    a1:cb:c8:94:74:cc:9f:ed:66:84:fd:38:87:6e:53:
                    c9:85:a9:ab:83:56:6c:93:82:79:f5:4f:77:c1:40:
                    ba:4e:aa:d5:0f:23:8a:ee:fc:ab:76:ab:15:00:2c:
                    99:ca:3a:ca:55:5c:ba:80:1c:9d:e6:af:d1:1c:93:
                    13:8a:25:da:ec:3a:bf:93:b8:70:50:e9:cb:78:04:
                    b0:9b
                Exponent: 65537 (0x10001)


-----BEGIN CERTIFICATE-----
MIIC0DCCAbigAwIBAgIUIE6enN0sTnHP8USpfr15UeGXpA0wDQYJKoZIhvcNAQEL
BQAwETEPMA0GA1UEAwwGZGViaWFuMB4XDTIwMDIwODE0MjYyNFoXDTMwMDIwNTE0
MjYyNFowETEPMA0GA1UEAwwGZGViaWFuMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
MIIBCgKCAQEArSjStRLCyDJtNtEObKrDfl0eQEX+AR6dirM7V2nw+SQGYJTO9qft
o53Fht0pAImnxnvFEfy+CfMhdKgHYeRIYom73FrU0sGuWWcxrd085JL8f6nWDKpp
vNQdDavGuMhSDk6K6Gw8C3DVQz5CfdLj9dX36KAwZu6FOpFJ2NPmhaMxKjPuVtOr
gxrFF88xfIUPRhSH4EIkw7f36Bki3M4GGY+U7aeziCQfeSwMQ3L3bSKbLDGhy8iU
dMyf7WaE/TiHblPJhamrg1Zsk4J59U93wUC6TqrVDyOK7vyrdqsVACyZyjrKVVy6
gByd5q/RHJMTiiXa7Dq/k7hwUOnLeASwmwIDAQABoyAwHjAJBgNVHRMEAjAAMBEG
A1UdEQQKMAiCBmRlYmlhbjANBgkqhkiG9w0BAQsFAAOCAQEAEpA1Lm+2zfMY5MrW
sWp5Gzx6qatjhgHMwP5nc04NBgA+HDEYjqWW4hCNSePNkSFhmIf53Gn61ltBpCc6
OL3XLo/RXMNRqVk9e+tUuvhgyKXGk3OwQjOcP8XMno2qYmrF996MUdA2cdfdoqZR
y178DV/dqpEDhVke9FNhYJvNl6XWL+YGQ89EoeBYU3RmDE/GqvtuvoJ1rVLYV3S+
ekSQWZNXcmDwRsymZ4W6II6TDozB5GmaWZGi+81931BxbOMQOQu0UjA39rKD/5Xq
9/4/aKGWs37cbuC3thaYu0BOJlWtc0Hm1655JoGBkiSkJSraH2hLmjvV+3Ooq2qZ
lPAChg==
-----END CERTIFICATE-----
```

Le nouveau certificat expire le 05/02/2032  
Nouveau certificat et nouvelle clé :  

```
Public Key Algorithm: rsaEncryption
                RSA Public-Key: (2048 bit)
                Modulus:
                    00:b6:45:82:15:7c:f8:01:0f:1a:6e:ef:9f:cd:9b:
                    a2:7d:7e:5d:ae:2c:c0:9b:67:b6:15:cd:0a:2e:ab:
                    5c:19:15:f5:e7:ac:5d:31:26:58:b5:07:34:be:f8:
                    dd:26:e9:d6:a8:82:16:99:c0:c5:e4:10:e4:f3:bb:
                    c1:81:56:af:66:bd:f1:84:19:7e:30:06:0b:20:0b:
                    42:a9:a2:8b:6c:f9:3f:d3:94:34:2a:fa:0e:18:9f:
                    58:d4:c7:9b:c7:ef:11:98:60:e1:f2:7b:1f:00:73:
                    76:29:e1:28:91:4b:b3:e4:86:43:d8:3f:25:ba:9c:
                    a4:2f:63:42:51:4c:ce:85:76:73:af:27:04:97:3f:
                    0b:d4:61:57:27:d4:6e:66:4b:4f:9a:19:d6:4f:22:
                    b1:cb:1b:c5:21:cc:18:21:72:c1:a7:c9:0d:7f:ee:
                    d1:d8:05:48:2e:a5:7f:a6:22:99:da:3d:8c:d5:5b:
                    6d:79:6b:10:d1:2d:a2:cf:8c:74:9d:2c:db:84:1a:
                    7e:ba:f3:5d:68:99:0d:04:08:4f:ca:b5:01:c6:8e:
                    7f:4e:4d:35:0e:23:47:1d:09:47:2c:3e:f6:12:4e:
                    9f:84:67:1d:23:8d:14:97:a7:fa:92:c4:b4:e4:75:
                    b0:f4:2a:72:c4:44:46:c9:2b:cb:a3:1b:4f:c8:d4:
                    50:57
                Exponent: 65537 (0x10001)
                
   
   -----BEGIN CERTIFICATE-----
MIIC1jCCAb6gAwIBAgIUf+nMJK7eqhKr7grh46l5AD8FdC4wDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIZGViaWFuLTEwHhcNMjIwMjA3MTA0MzI5WhcNMzIwMjA1
MTA0MzI5WjATMREwDwYDVQQDDAhkZWJpYW4tMTCCASIwDQYJKoZIhvcNAQEBBQAD
ggEPADCCAQoCggEBALZFghV8+AEPGm7vn82bon1+Xa4swJtnthXNCi6rXBkV9ees
XTEmWLUHNL743Sbp1qiCFpnAxeQQ5PO7wYFWr2a98YQZfjAGCyALQqmii2z5P9OU
NCr6DhifWNTHm8fvEZhg4fJ7HwBzdinhKJFLs+SGQ9g/JbqcpC9jQlFMzoV2c68n
BJc/C9RhVyfUbmZLT5oZ1k8iscsbxSHMGCFywafJDX/u0dgFSC6lf6Yimdo9jNVb
bXlrENEtos+MdJ0s24QafrrzXWiZDQQIT8q1AcaOf05NNQ4jRx0JRyw+9hJOn4Rn
HSONFJen+pLEtOR1sPQqcsRERskry6MbT8jUUFcCAwEAAaMiMCAwCQYDVR0TBAIw
ADATBgNVHREEDDAKgghkZWJpYW4tMTANBgkqhkiG9w0BAQsFAAOCAQEAUyiZEiDL
qNawAI9NL3O+CygwDx1z/jjVhzp4p8oDT7Y/u65SAb7juugR+FOrr7BBAp8DD9FJ
pwn5tZ09c/9RVubASVzpNbdYaZtRYPEItH6HQ9lIuIbADrPfG069JoYo6aF0RXOS
aPdYSbmhk7HPvQPY6F64C4xsg0KCQnLJcT/FzqWdcBjCIXWARwKSfFK0Sl7Fe7BQ
IG2YKpOjvf2Cm2ommnrNrNKQITgF4av3LAT1VzyEjkY13wLGcmL0Bon6ZFN9LcR1
+oLpm/C1l34ZuxnOeE4RiTzb8FwquKbc8mr695P6uiyl/BSh5Wg5WviYRmSaiK1r
lmbodGbLk5bsbg==
-----END CERTIFICATE-----

                
```


### 3)

Afin de changer la durée de validité des certificats générés, on a modifié les lignes suivantes du fichier ```/usr/sbin/make-ssl-cert```
```
if [ "$1" != "generate-default-snakeoil" ]; then
    if ! openssl req -config $TMPFILE -new -x509 -days 10 -nodes -sha256 \
```
La valeur suivant l'option ```-days``` est passée de 3650 (10ans) à 10 jours.  

## Exercice 2 (Configuration d’apache2 pour activer https)

### 1) 

La requête vers http://0.0.0.0:443 donne une erreur ```Bad request```, le serveur demandant une requête HTTPS

### 2) 

En se connectant en https, le site fonctionne.

### 3) 

Pour tester les protocoles autorisés, on lance la commande suivante :```./testssl.sh/testssl.sh https://0.0.0.0:443```

```
 SSLv2      not offered (OK)
 SSLv3      not offered (OK)
 TLS 1      offered (deprecated)
 TLS 1.1    offered (deprecated)
 TLS 1.2    offered (OK)
 TLS 1.3    offered (OK): final
 NPN/SPDY   not offered
 ALPN/HTTP2 http/1.1 (offered)
```

## Exercice 3 (Rediriger http vers https)

```
<Directory "/html">
        RewriteEngine On
                RewriteBase "/html/"
                RewriteCond %{HTTPS} off
                RewriteRule ^(.*)$ https://0.0.0.0:443 [L,R=301]
</Directory>
```

## Exercise 4 (Mettre en place TLS 1.3)

### 1)

On vérifie si les sites suivants sont en TLS 1.2 ou 1.3 :

```
openssl s_client -proxy 193.49.118.36:8080 -connect www.google.com -tls1_2
openssl s_client -proxy 193.49.118.36:8080 -connect www.google.com -tls1_3
openssl s_client -proxy 193.49.118.36:8080 -connect ayesh.me:443 -tls1_3
```
On voit que www.google.com supporte TLS 1.2 mais pas TLS 1.3. ayesh.me quant à lui supporte TLS 1.3.

### 2)

### 3)

### 4)

### 5)

## Exercise 5 (https en gérant la cryptographie avec openssl)

### 1)

### 2)

### 3)

### 4)

### 5)

### 6)

