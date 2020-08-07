# Protocole ARP

## Quel est le rôle du protocole ARP ?

Le protocole ARP (_Address Resolution Protocol_) a pour rôle d'associer une adresse IP et une adresse MAC, il permet de connaître l'adresse physique d'une carte réseau correspondant à une adresse IP.

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
  * Protocol Type : le type de protocole (exemple : IP)
  * Hardware size : le nombre d’octet de l’adresse MAC (6)
  * Protocol size : le nombre d’octet de l’adresse IP (4)
  * Opcode : le type de requête (exemple : request / reply)
  * Sender MAC address : l’adresse Mac de l’envoyeur
  * Sender IP address : l’adresse IP de l’envoyeur
  * Target MAC address : l’adresse MAC de la machine visée
  * Target IP address : l’adresse IP de la machine visée)
* Le CRS (FCS) va contenir un code (binaire) afin de vérifier la non altéation des données.

## Processus d'intersection logique (PIL)

Le protocole ARP ne peut se faire que lorsqu’on se trouve sur le même réseau. Un poste ne
peut pas envoyer un broadcast ARP que s’il s’assure que le destinataire se trouve sur le
même réseau que lui.

Le broadcast envoie une requête à toutes les machines sur le même réseau que lui, pour les
questionner et trouvé la machine qui à l’IP de destination voulue et récupérer son adresse
MAC.

L’unicast est pour « parler » directement à une seule machine.
Il peut savoir qu’il est sur le même réseau que lui, en faisant un et logique entre l’IP de
destination et son masque :

_Exemples :_

* Ip de destination : 10.0.0.2/8
* Masque : 255.0.0.0

-> Le **ET** logique nous donne donc l'adresse réseau de destination : 10.0.0.0/8

* IP de source : 10.0.0.1/8
* Masque : 255.0.0.0

-> Le **ET** logique nous donne donc l'adresse réseau source : 10.0.0.0/8

Les deux adresses de réseau son identique donc le protocole ARP peut s’exécuter.

Il peut donc utiliser le broadcast ARP.

Le PIL est déclenché dès lors qu’il y a une intersection, si les deux adresses réseaux ne sont
pas identiques, il doit voir s’il a une parcelle, si oui, il passe par elle, sinon il ne fais rien.

## Exemple avec deux machines

*Configurations :*
* Les deux machines sont situés sur le même réseau LAN et se nomme WIN1 et WIN2.
* WIN1
  * Adresse IP : 10.0.0.1/8
  * Adresse MAC : 00:0c:29:06:77:d7
* WIN2
  * Adresse IP : 10.0.0.2/8
  * Adresse MAC : 00:0c:29:C6:05:71
 
### Scénario
Faire un ping de la machie WIN1 vers WIN2 : **ping 10.0.0.2**

/!\ Ne pas oublier de vider le contenu des caches ARP des deux machines avec la commande **arp -d** sinon il ne fera pas un broadcast ARP donc on ne verra pas la trame du broadcast ARP.

### Résultat
Captures de trames avec Wireshark

### ARP request
![ARP Request](https://lindwen.fr/img/arp%20request.png)

Que voyons-nous ?
* La machine WIN1 envoie un broadcast avec l'adresse IP de la machine WIN2 pour pouvoir récupérer son adresse MAC.
* La Destination : Broadcast est reçu par tous les nœuds (machines) du même réseau (ici notre réseau est en LAN).
* La source est l’adresse MAC de XP1.
* Le type : ARP nous renseigne sur le type de protocole utilisé.
* Hardware size : 6 octets -> adresse MAC
* Protocole size : 4 octets -> adresse IP
* Opcode : request (1) donc nous savons que nous allons envoyer une requête.
* La Sender MAC address est l’adresse MAC de XP1 (celle qui envoie le broadcast) et Sender IP address son adresse IP.
* La target MAC address est 00:00:00:00:00:00 car nous ne la connaissons pas encore mais nous connaissons l’adresse IP de la cible qui est ici la machine XP2 (Target IP address).

### ARP reply
![ARP Request](https://lindwen.fr/img/arp%20reply.png)

Que voyons-nous ?
* La machine WIN2 répond à la demande de WIN1.
* La destination n’est plus en broadcast mais en unicast vu que la machine XP2 connait maintenant l’adresse MAC de XP1 (qu’elle garde en cache).
* La source est l’adresse MAC de XP2.
* Le type de protocole ne change pas c’est bien ARP.
* padding sert de bourrage pour avoir le nombre minimal d’octet (46).
*  Opcode a changé car maintenant c’est une réponse (reply), la machine XP2 répond à la requête de la XP1.
*  Sender MAC address est l’adresse MAC de l’envoyeur ici XP2, et Sender IP address est son adresse IP.
* Vu que XP1 a fait une requête, XP2 connait maintenant son adresse MAC, qui est la Target MAC address, et son IP Target address IP.
