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

Le premier octet d'une adresse de classe A est définie par une valeur décimale entre 1 et 127.
La partie réseau d'une adresse de classe A est définie sur le premier octet.

_Exemple :_
* 10.0.0.2
  * Ici nous reconnaissons que l'adresse est une classe A car le premier octet a pour valeur 10 qui est compris entre 1 < 10 < 127.

