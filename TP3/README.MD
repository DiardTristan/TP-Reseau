# TP 3

## ARP

#### 🌞Générer des requêtes ARP

##### effectuer un ping d'une machine à l'autre

``` console
[tristan@localhost network-scripts]$ ping 10.3.1.12
PING 10.3.1.12 (10.3.1.12) 56(84) bytes of data.
64 bytes from 10.3.1.12: icmp_seq=1 ttl=64 time=3.08 ms
64 bytes from 10.3.1.12: icmp_seq=2 ttl=64 time=7.29 ms
64 bytes from 10.3.1.12: icmp_seq=3 ttl=64 time=2.96 ms
```

#### observer les tables ARP des deux machines

##### Mac de John depuis Marcel

``` console
[tristan@localhost ~]$ ip neigh show
10.3.1.1 dev enp0s3 lladdr 0a:00:27:00:00:3d DELAY
10.3.1.11 dev enp0s3 lladdr 🌟08:00:27:05:10:e2🌟 STALE
```


##### Mac de Marcel depuis John

``` console
[tristan@localhost ~]$ ip neigh show
10.3.1.12 dev enp0s3 lladdr 🌟08:00:27:d1:a0:9a REACHABLE🌟
10.3.1.1 dev enp0s3 lladdr 0a:00:27:00:00:3d REACHABLE
```

#### Verification des Adresses MAC :

##### MAC De Marcel

``` console
[tristan@localhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:d1:a0:9a brd ff:ff:ff:ff:ff:ff
    inet 10.3.1.12/24 brd 10.3.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fed1:a09a/64 scope link
       valid_lft forever preferred_lft forever
```

##### MAC de John

``` console 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:05:10:e2 brd ff:ff:ff:ff:ff:ff
    inet 10.3.1.11/24 brd 10.3.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe05:10e2/64 scope link
       valid_lft forever preferred_lft forever
```

### 2. Analyse des trames

##### Commande pour reset la table ARP :

```sudo ip neigh flush all```

##### Pour récuperer la tram :

```[tristan@localhost ~]$ sudo tcpdump -i enp0s3 -c 50 -w test.pcapng
dropped privs to tcpdump
tcpdump: listening on enp0s3, link-type EN10MB (Ethernet), snapshot length 262144 bytes
^C33 packets captured
36 packets received by filter
0 packets dropped by kernel
```

##### Pour récupérer la tram sur le PC :

```PS C:\Users\trist> scp tristan@10.3.1.11:/home/tristan/tp3.pcapng .
tristan@10.3.1.11's password:
tp3.pcapng                                                          100% 4954   919.9KB/s   00:00```