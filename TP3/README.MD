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

```console
[tristan@localhost ~]$ ip neigh show
10.3.1.1 dev enp0s3 lladdr 0a:00:27:00:00:3d DELAY
10.3.1.11 dev enp0s3 lladdr 08:00:27:05:10:e2 STALE```