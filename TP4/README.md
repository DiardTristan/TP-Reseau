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

   #### 🌞 Preuve de mise en place

   - Depuis dhcp.tp4.b1

```console
[tristan@dhcp ~]$ ping google.com
PING google.com (142.251.37.238) 56(84) bytes of data.
64 bytes from waw02s07-in-f174.1e100.net (172.217.20.174): icmp_seq=1 ttl=114 time=16.3 ms
64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=2 ttl=114 time=17.4 ms
64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=3 ttl=114 time=18.6 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1505ms
   ```

```console
[tristan@node2 ~]$ ping google.com
PING google.com (142.251.37.238) 56(84) bytes of data.
64 bytes from waw02s07-in-f174.1e100.net (172.217.20.174): icmp_seq=1 ttl=114 time=16.5 ms
64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=2 ttl=114 time=17.2 ms
64 bytes from waw02s07-in-f14.1e100.net (172.217.20.174): icmp_seq=3 ttl=114 time=17.9 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1503ms
   ```

```console
[tristan@node2 ~]$ traceroute 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  _gateway (10.4.1.254)  1.221 ms  1.121 ms  1.139 ms
 2  10.0.3.2 (10.0.3.2)  1.126 ms  1.093 ms  1.078 ms^C
 ```

 #### 🌞 Rendu

 ```console
 [tristan@localhost ~]$ systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Wed 2023-11-08 21:35:09 CEST; 5min ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 1884 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 4674)
     Memory: 4.6M
        CPU: 17ms
     CGroup: /system.slice/dhcpd.service
             └─1884 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhcpd --no-pid
```

```console
[tristan@dhcp ~]$sudo dnf -y install dhcp-server
[tristan@dhcp ~]$ sudo nano /etc/dhcp/dhcpd.conf
[tristan@dhcp ~]$ sudo cat /etc/dhcp/dhcpd.conf
option domain-name     "srv.world";
option domain-name-servers     dlp.srv.world;
default-lease-time 600;
max-lease-time 7200;
authoritative;
subnet 10.4.1.0 netmask 255.255.255.0 {
    range dynamic-bootp 10.4.1.137 10.4.1.147;
    option broadcast-address 10.4.1.255;
    option routers 10.4.1.254;
}
 ```

## 5 Client DHCP

#### 🌞 Rendu  bbbb

```console
[tristan@dhcp ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:de:36:da brd ff:ff:ff:ff:ff:ff
    inet 10.4.1.137/24 brd 10.4.1.255 scope global 🌟dynamic noprefixroute enp0s3🌟
       valid_lft 404sec preferred_lft 404sec
    inet6 fe80::a00:27ff:fede:36da/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
       ```

```console
[tristan@dhcp ~]$ nmcli con show enp0s3
```

##### Date exacte du début du bail sombre des crousty caraibes des cocopops : 08/11/2023 21:50:06

##### Date exacte d'expiration : 08/11/2023 22:05:07

##### dhcp_server_identifier = 10.4.1.253
