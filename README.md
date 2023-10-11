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