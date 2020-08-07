# Introduction aux réseaux locaux

Dans les réseaux locaux actuels la technologie utilisée (la méthode d'accès au réseau) est l'Ethernet. Le réseau Ethernet est composé d'un ensemble de noeuds (ordinateur, montre connecté, imprimante, etc...)

On identifie un noeud sur le réseau à travers deux paramètres :
* Une adresse MAC (adresse matérielle) qui est composé de 6 octets unique dans le monde, elle est associé à une carte réseau et est affecté par le constructeur.
* Une adresse IP composé d'une partie réseau et une partie machine (toute adresse IP doit posséder 2 parties).
  * La partie machine c'est l'adresse IP d'un noeud au sein de l'adresse réseau. Les adresses de classe A par exemple, ont leurs partie réseau défini sur le premier octet (le plus à gauche).
  * 10.0.0.2 -> partie réseau : 10    |    partie machine : 0.0.2

Un octet est composé d'une succession de 8 bits (donc une adresse MAC = 48 bits).

* Une adresse IP (V4) est une adresse logique affectée par l'administrateur réseau au matériel de façon manuelle ou automatique. Cette adresse est composé de 4 octets (32 bits) séparé par des points.
* Il y a 4 classes d'adresses IP.

# Les classes d'adresses IP

## Classe A

* Le premier octet d'une adresse de classe A est définie par une valeur décimale entre 1 et 127.
* La partie réseau d'une adresse de classe A est définie sur le premier octet.
* Les trois octets restants définissent la partie machine.

_Exemple :_
* 10.0.0.2
  * Ici nous reconnaissons que l'adresse est une classe A car le premier octet a pour valeur 10 qui est compris entre 1 < 10 < 127.


## Classe B

* Le premier octet d'une adresse de classe B est définie par une valeur décimale entre 128 et 191.
* La partie réseau d'une adresse de classe B est définie sur les deux premiers octets.
* Les deux octets restants définissent la partie machine.

_Exemple :_
* 182.10.0.2
  * Ici nous reconnaissons que l'adresse est une classe A car le premier octet a pour valeur 182 qui est compris entre 128 < 182 < 191.
  
  
## Classe C

* Le premier octet d'une adresse de classe C est définie par une valeur décimale entre 192 et 223.
* La partie réseau d'une adresse de classe C est définie sur les trois premiers octets.
* Le dernier octet restant défini la partie machine.

_Exemple :_
* 201.17.8.2
  * Ici nous reconnaissons que l'adresse est une classe A car le premier octet a pour valeur 10 qui est compris entre 192 < 201 < 223.
  
  
## Classe D
La classe D est utilisée pour un certain type de protocole bien précis.

* Le premier octet d'une adresse de classe B est définie par une valeur décimale entre 224 et 239.


## Classe E
Les adresses de classe E sont réservées par IANA à un usage non déterminé. Les adresses de classe E commencent toujours par la séquence de bits 1111, ils débutent donc en 240.0.0.0 et se terminent en 255.255.255.255.


# Résumé

Classe | Bits de départ | Début | Fin | Notation CIDR par défaut | Masque de sous-réseau par défaut
---|---|---|---|---|---
Classe A | 0 | 0.0.0.0 | 126.255.255.255 (127 est réservé) | /8 | 255.0.0.0
Classe B | 10 | 128.0.0.0 | 191.255.255.255 | /16 | 255.255.0.0
Classe C | 110 | 192.0.0.0 | 223.255.255.255 | /24 | 255.255.255.0
Classe D (multicast) | 1110 | 224.0.0.0 | 239.255.255.255 |  | 255.255.255.255
Classe E (réservée) | 1111 | 240.0.0.0 | 255.255.255.255 |  | non défini 
