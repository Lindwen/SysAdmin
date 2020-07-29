# Protocole ARP

## Quel est le rôle du protocole ARP ?

Le protocole ARP (_Address Resolution Protocol_) a pour rôle d'associer une adresse IP et une adresse MAC, il permet de connapitre l'adresse physique d'une carte réseau correspondant à une adresse IP.

## En-tête protocole ARP

Préambule | @ MAC destination | @ MAC source | Type protocole 0806 | Paquet ARP + bourrage | FCS
---|---|---|---|---|---
7+1 octets | 6 octets | 6 octets | 2 octets | 28+18=46 octets | 4 octets
