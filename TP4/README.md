# TP 4

## DHCP Client

#### 🌞 Déterminer  

##### IP du serveur DNS :

```console
PS C:\Users\trist> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6 AX201 160MHz
   Adresse physique . . . . . . . . . . . : DC-46-28-B5-66-57
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::f9ad:14b2:37b4:90c2%20(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.70.207(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Bail obtenu. . . . . . . . . . . . . . : 🌟vendredi 27 octobre 2023 08:52:08🌟
   Bail expirant. . . . . . . . . . . . . : 🌟samedi 28 octobre 2023 08:52:02🌟
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveur DHCP . . . . . . . . . . . . . : 🌟10.33.79.254🌟
   IAID DHCPv6 . . . . . . . . . . . : 165430824
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2C-0C-01-3A-04-7C-16-AC-F9-CA
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
   ```

   #### 🌞 Capturer un échange DHCP

   [Les 4 Trames DHCP](tp4_dhcp_client.pcapng)

   #### 🌞 Analyser la capture Wireshark

   ##### C'est la seconde trame (Offer) qui contient les informations proposées au client.

   ## II. Serveur DHCP