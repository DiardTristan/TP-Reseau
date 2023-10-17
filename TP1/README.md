# TP-Reseau

## 1. Affichage d'informations sur la pile TCP/IP locale

#### 🌞 Affichez les infos des cartes réseau de votre PC

```ipconfig /all```

Carte réseau sans fil Wi-Fi :

    Nom : Intel(R) Wi-Fi 6 AX201 160MHz

    Adresse MAC : DC-46-28-B5-66-57

    Adresse IPv4 : 10.33.48.118

Carte Ethernet : 

    Nom : Realtek PCIe GbE Family Controller

    Adresse MAC : 04-7C-16-AC-F9-CA

    Adresse IPV4 : Aucune

#### 🌞 Affichez votre gateway

```ipconfig /all```

IP gateway : 10.33.51.254

#### 🌞 Déterminer la MAC de la passerelle

```arp -a```

Adresse MAC de la passerelle : 7c-5a-1c-cb-fd-a4

#### 🌞 Trouvez comment afficher les informations sur une carte IP (change selon l'OS)

##### trouvez l'IP, la MAC et la gateway pour l'interface WiFi de votre PC

IP : 10.33.48.118
MAC : DC-46-28-B5-66-57

## 2. Modifications des informations

#### 🌞 Utilisez l'interface graphique de votre OS pour changer d'adresse IP :

```Paramètres > Réseau et Internet > WiFi > Propriétés du matériel> Attribution de l'adresse IP > Modifier > Manuel```

#### 🌞 Il est possible que vous perdiez l'accès internet

Dans le cas où on perd internet, c'est parce qu'il y'a déjà une machine qui utilise cette IP 

## 3. Modification l'adresse IP

#### 🌞 Modifiez l'IP des deux machines pour qu'elles soient dans le même réseau

Mon IP : 10.10.10.251/24
L'IP de l'autre machine : 10.10.10.250/24

#### 🌞 Vérifier à l'aide d'une commande que votre IP a bien été changée

```ìpconfig```

    Carte Ethernet Ethernet :

    Suffixe DNS propre à la connexion. . . :
    Adresse IPv6 de liaison locale. . . . .: fe80::eece:216c:93d6:d1d1%17
    Adresse IPv4. . . . . . . . . . . . . .: 10.10.10.251
    Masque de sous-réseau. . . . . . . . . : 255.255.255.0
    Passerelle par défaut. . . . . . . . . :

#### 🌞 Vérifier que les deux machines se joignent

```ping 10.10.10.250```

    Réponse de 10.10.10.250 : octets=32 temps<1ms TTL=128
    Réponse de 10.10.10.250 : octets=32 temps<1ms TTL=128
    Réponse de 10.10.10.250 : octets=32 temps=1 ms TTL=128
    Réponse de 10.10.10.250 : octets=32 temps=4 ms TTL=128

    Statistiques Ping pour 10.10.10.250:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
    Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 4ms, Moyenne = 1ms```

 #### 🌞 Déterminer l'adresse MAC de votre correspondant

 ```ARP -a```

    Interface : 10.10.10.251 --- 0x11
    Adresse Internet      Adresse physique      Type
    10.10.10.250          08-8f-c3-4a-e9-64     dynamique
    10.10.10.255          ff-ff-ff-ff-ff-ff     statique
    224.0.0.22            01-00-5e-00-00-16     statique
    224.0.0.251           01-00-5e-00-00-fb     statique
    224.0.0.252           01-00-5e-00-00-fc     statique
    239.255.255.250       01-00-5e-7f-ff-fa     statique

## 4. El pequino Gato privado (Le petit chat privée)

(On n'a pas réussi à le faire fonctionner sur les 2 PC)

# III Manipulations d'autres outils/protocoles côté client

## 1. DHCP

#### 🌞Exploration du DHCP, depuis votre PC

```ipconfig /all```

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6 AX201 160MHz
   Adresse physique . . . . . . . . . . . : DC-46-28-B5-66-57
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::f9ad:14b2:37b4:90c2%20(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.48.118(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.252.0
   Bail obtenu. . . . . . . . . . . . . . : lundi 16 octobre 2023 09:06:28
   Bail expirant. . . . . . . . . . . . . : mardi 17 octobre 2023 09:06:28
   Passerelle par défaut. . . . . . . . . : 10.33.51.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.51.254
   IAID DHCPv6 . . . . . . . . . . . : 165430824
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2C-0C-01-3A-04-7C-16-AC-F9-CA
   Serveurs DNS. . .  . . . . . . . . . . : 10.33.10.2
                                       8.8.8.8

#### 🌞** Trouver l'adresse IP du serveur DNS que connaît votre ordinateur**

```ipconfig /all```

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6 AX201 160MHz
   Adresse physique . . . . . . . . . . . : DC-46-28-B5-66-57
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::f9ad:14b2:37b4:90c2%20(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.48.118(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.252.0
   Bail obtenu. . . . . . . . . . . . . . : lundi 16 octobre 2023 09:06:28
   Bail expirant. . . . . . . . . . . . . : mardi 17 octobre 2023 09:06:28
   Passerelle par défaut. . . . . . . . . : 10.33.51.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.51.254
   IAID DHCPv6 . . . . . . . . . . . : 165430824
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2C-0C-01-3A-04-7C-16-AC-F9-CA
   Serveurs DNS. . .  . . . . . . . . . . : 10.33.10.2
                                       8.8.8.8

#### 🌞 Utiliser, en ligne de commande l'outil nslookup (Windows, MacOS) ou dig (GNU/Linux, MacOS) pour faire des requêtes DNS à la main

```nslookup google.com 8.8.8.8```

    Réponse ne faisant pas autorité :
    Nom :    google.com
    Addresses:  2a00:1450:4007:818::200e
          142.250.179.110

```nslookup ynov.com 8.8.8.8```

    Serveur :   dns.google
    Address:  8.8.8.8

    Réponse ne faisant pas autorité :
    Nom :    ynov.com
    Addresses:  2606:4700:20::681a:be9
          2606:4700:20::681a:ae9
          2606:4700:20::ac43:4ae2
          104.26.11.233
          104.26.10.233
          172.67.74.226

```nslookup 231.34.113.12 8.8.8.8```

    DNS request timed out.
        timeout was 2 seconds.
    Serveur :   UnKnown
    Address:  10.33.10.2
    
```nslookup 78.34.2.17 8.8.8.8```

    Serveur :   dns.google
    Address:  8.8.8.8

    Nom :    cable-78-34-2-17.nc.de
    Address:  78.34.2.17