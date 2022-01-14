# Sécurité WEB : TP3

https://sancy.iut-clermont.uca.fr/~lafourcade/WebSec.html

## Exercice 1

1/ Le Hash nous est indiqué par la valeur entre les deux premiers $, et le salt entre le deuxième et le troisième.
Ainsi , on a Hash : 1 et Salt : AAAA

Avec cette commande :
```
openssl passwd -1 -salt "AAAA" '!!1331xxx'
```
On retrouve le MDP hashé $1$AAAA$H9wXcd/WaaomJUgWKFspy

2/
