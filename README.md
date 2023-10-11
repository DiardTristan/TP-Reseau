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

#### 🌞 Modifiez l'IP des deux machines pour qu'elles soient dans le même réseau

Mon IP : 10.10.10.251
L'IP de l'autre machine : 10.10.10.250

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