# SECWEB TP5

Sujet : https://sancy.iut-clermont.uca.fr/~lafourcade/SECWEB/2022-TP5-http-https.pdf  

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

### 3)

## Exercice 2 (Configuration d’apache2 pour activer https)

### 1)

### 2)

### 3)

## Exercice 3 (Rediriger http vers https)

## Exercise 4 (Mettre en place TLS 1.3)

### 1)

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

