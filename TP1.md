I. Basics
--------

☀️ Carte réseau WiFi
Déterminer...
---

l'adresse MAC de votre carte WiFi :

```
PS C:\Users\pc> ipconfig /all
[...]
Adresse physique . . . . . . . . . . . : 28-16-AD-2E-C7-19
```



l'adresse IP de votre carte WiFi :
```
PS C:\Users\pc> ipconfig /all
[...]
Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.10
```

le masque de sous-réseau du réseau LAN auquel vous êtes connectés en WiFi

en notation CIDR, par exemple /16 :

- c'est /28 dcp 

**CALCUL :**

255 = 8

255.255.255 = 8x3 = 24

240 = 4

24+4 = 28

***DAB on them***


ET en notation décimale, par exemple 255.255.0.0 :
```
PS C:\Users\pc> ipconfig /all
[...]
 Masque de sous-réseau. . . . . . . . . : 255.255.255.240
```
☀️ Déso pas déso
---
Pas besoin d'un terminal là, juste une feuille, ou votre tête, ou un tool qui calcule tout hihi. Déterminer...**

l'adresse de réseau du LAN auquel vous êtes connectés en WiFi :

```
PS C:\Users\pc> ipconfig
[...]
Adresse IPv4. . . . . . . . . . . . . .: 10.33.79.75
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254

```
donc adresse reseau = premiere adresse = 10.33.64.0


--------

l'adresse de broadcast
le nombre d'adresses IP disponibles dans ce réseau :

l'adresse broadcast = la derniere adresse = 10.33.79.255


le nombre d'adresses IP disponibles dans ce réseau :

la le masque c'est 255.255.240.0 ca veut dire qu'il y'a 20 bits qui sont pas modifiable en gros donc il en reste 12

**petit calcul**

 2^12 = 4094

on enleve 2 (broadcast + adresse reseau)

= 4091

-------------
☀️ Passerelle du réseau
Déterminer...
----

l'adresse IP de la passerelle du réseau : ipconfig 10.33.79.254

l'adresse MAC de la passerelle du réseau : ipconfig /all =

```
Carte réseau sans fil Wi-Fi :
[...]
   Adresse physique . . . . . . . . . . . : 28-16-AD-2E-C7-19
```

------
☀️ Serveur DHCP et DNS
Déterminer...
---

l'adresse IP du serveur DHCP qui vous a filé une IP : 

pareil  : ipconfig /all  

10.33.79.254 (meme ip que la passerelle)

l'adresse IP du serveur DNS que vous utilisez quand vous allez sur internet :

8.8.8.8

--------


☀️ Table de routage
Déterminer...
---

dans votre table de routage, laquelle est la route par défaut :

```
PS C:\Users\pc> route print -4
[...]
Destination réseau    Masque réseau  Adr. passerelle   Adr. interface Métrique
          0.0.0.0          0.0.0.0     10.33.79.254      10.33.79.75     35
```
---------
☀️ Hosts ?
---

faites en sorte que pour votre PC, le nom b2.hello.vous corresponde à l'IP 1.1.1.1:

```
PS C:\Users\pc> cat C:\Windows\System32\drivers\etc\hosts
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
[...]

1.1.1.1         Truc2ouf
192.168.56.101      mon-super-site.local
```

prouvez avec un ping b2.hello.vous que ça ping bien 1.1.1.1:

```
PS C:\Users\pc> ping Truc2ouf

Envoi d’une requête 'ping' sur Truc2ouf [1.1.1.1] avec 32 octets de données :
Réponse de 1.1.1.1 : octets=32 temps=12 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=15 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=12 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=12 ms TTL=57

Statistiques Ping pour 1.1.1.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 12ms, Maximum = 15ms, Moyenne = 12ms
```


Putain je suis content 

☀️ Go mater une vidéo youtube et déterminer, pendant qu'elle tourne...
---

l'adresse IP du serveur auquel vous êtes connectés pour regarder la vidéo et le port du serveur auquel vous êtes connectés :

j'ouvre wireshark je lance une capture, je lance une video YT, je chope l'adresse ip qui me spam (c'est du QUIC en l'occurence)

ensuite : 
```
PS C:\WINDOWS\system32> netstat -a -n -b  | Select-String 216.58.215.34
```
rien ne se passe wtf

bon dcp j'essaye avec le port :

```
PS C:\WINDOWS\system32> netstat -a -n -b  | Select-String 50239 -Context 0,1

>   UDP    0.0.0.0:50239          *:*
   [msedge.exe]
```

ok enft youtube change le monde, ils redefinissent ce qu'on sait deja, IMPOSSIBLE de se reposer sur ses acquis bordel, ils deviennent obsoletes presque instant.

bref le port destination est 443 j'ai vu sur wireshark

et le port ouvert sur mon pc est 50239

----
☀️ Requêtes DNS
---
Déterminer...

à quelle adresse IP correspond le nom de domaine www.ynov.com

Ca s'appelle faire un "lookup DNS".  :

```
PS C:\WINDOWS\system32> nslookup www.ynov.com
[...]
Nom :    www.ynov.com
Addresses:  2606:4700:20::681a:be9
          2606:4700:20::ac43:4ae2
          2606:4700:20::681a:ae9
          172.67.74.226
          104.26.11.233
          104.26.10.233
```



à quel nom de domaine correspond l'IP 174.43.238.89

Ca s'appelle faire un "reverse lookup DNS".  :

```
PS C:\WINDOWS\system32> nslookup 174.43.238.89
>>
Serveur :   dns.google
Address:  8.8.8.8

Nom :    89.sub-174-43-238.myvzw.com
Address:  174.43.238.89
```
------
☀️ Hop hop hop
Déterminer...
---

par combien de machines vos paquets passent quand vous essayez de joindre www.ynov.com :

```
PS C:\WINDOWS\system32> tracert www.ynov.com

Détermination de l’itinéraire vers www.ynov.com [104.26.11.233]
avec un maximum de 30 sauts :

  1     4 ms     1 ms     1 ms  10.33.79.254
  2     3 ms     2 ms     6 ms  145.117.7.195.rev.sfr.net [195.7.117.145]
  3     2 ms     3 ms     2 ms  237.195.79.86.rev.sfr.net [86.79.195.237]
  4     5 ms     4 ms     3 ms  196.224.65.86.rev.sfr.net [86.65.224.196]
  5    12 ms    12 ms    11 ms  12.148.6.194.rev.sfr.net [194.6.148.12]
  6    11 ms    10 ms    11 ms  12.148.6.194.rev.sfr.net [194.6.148.12]
  7    13 ms    10 ms    12 ms  141.101.67.48
  8    11 ms    12 ms    11 ms  172.71.124.4
  9    11 ms    10 ms    11 ms  104.26.11.233

Itinéraire déterminé.
```

9 machines a priori

--------------

☀️ IP publique
Déterminer...
---

l'adresse IP publique de la passerelle du réseau (le routeur d'YNOV donc si vous êtes dans les locaux d'YNOV quand vous faites le TP) :

WhatIsMyIPAddress :
176.149.203.205

---------



☀️ Scan réseau
Déterminer...

combien il y a de machines dans le LAN auquel vous êtes  :

*bon j'ai telechargé nmap etc mais je sais pas comment l'utiliser, d'apres ce que j'ai compris il faut utiliser la commande : 
nmap -sn 192.168.1.0/24*

*en gros tu donnes l'adresses de ton reseau + le masque et nmap envoi un ping a tte les adresse ip quoi*

*et si ca "pong" c'est que le host is up*

---------


III. Le requin

*Bon Wireshark c'est mon point faible l'année derniere j'ai fait l'impasse sur la plupart des trucs wireshark mais oklm je vais faire au mieux*

☀️ Capture ARP


capturez un échange ARP entre votre PC et la passerelle du réseau :

voila ma [Capture ARP](./captures/ARP_pc-passerelle.pcap ), j'ai utilisé un filtre "ARP"



☀️ Capture DNS


📁 fichier dns.pcap

capturez une requête DNS vers le domaine de votre choix et la réponse
vous effectuerez la requête DNS en ligne de commande :

```
PS C:\Users\pc> nslookup www.notion.so
Serveur :   bbox.lan
Address:  2001:861:82:39a0:ce00:f1ff:fe37:330c

Réponse ne faisant pas autorité :
Nom :    www.notion.so
Addresses:  2606:4700:4400::6812:2766
          2606:4700:4400::ac40:949a
          104.18.39.102
          172.64.148.154
```

*je n'ai pas su l'enregistrer dans un fichier .pcap sans utiliser tcpdump*


Si vous utilisez un filtre Wireshark pour mieux voir ce trafic, précisez-le moi dans le compte-rendu.


☀️ Capture TCP


📁 fichier tcp.pcap

effectuez une connexion qui sollicite le protocole TCP
je veux voir dans la capture :

un 3-way handshake
un peu de trafic
la fin de la connexion TCP




Si vous utilisez un filtre Wireshark pour mieux voir ce trafic, précisez-le moi dans le compte-rendu.







