# Protocole ARP

## Quel est le rôle du protocole ARP ?

Le protocole ARP (_Address Resolution Protocol_) a pour rôle d'associer une adresse IP et une adresse MAC, il permet de connapitre l'adresse physique d'une carte réseau correspondant à une adresse IP.

## En-têtes protocole ARP

Préambule | @ MAC destination | @ MAC source | Type protocole 0806 | Paquet ARP + bourrage | FCS
---|---|---|---|---|---
7+1 octets | 6 octets | 6 octets | 2 octets | 28+18=46 octets | 4 octets

* La MAC destination est l’adresse MAC de la machine a qui on veut « parler ».
* La MAC source est l’adresse MAC de la machine qui envoie.
* Le type protocole ou Ether type (U.L.P Uper Layer Protocol) est une valeur en hexadécimale
qui va annoncer le protocole de niveau supérieur.
  * Ether type = (0800)16 -> Protocole IP niveau 3
  * Ether type = (0806)16 -> ARP
* Paquet ARP :
  * Hardware Type : ici Ethernet II
  * Protocol Type : le type de protocole (exemple : IP
  * Hardware size : le nombre d’octet de l’adresse MAC (6)
  * Protocol size : le nombre d’octet de l’adresse IP (4)
  * Opcode : le type de requête (exemple : request / reply)
  * Sender MAC address : l’adresse Mac de l’envoyeur
  * Sender IP address : l’adresse IP de l’envoyeur
  * Target MAC address : l’adresse MAC de la machine visée
  * Target IP address : l’adresse IP de la machine visée)
* Le CRS (FCS) va contenir un code (binaire) afin de vérifier la non altéation des données.
