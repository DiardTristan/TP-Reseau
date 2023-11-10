# TP 5

## 1. First Steps

#### 🌞 Déterminez, pour ces 5 applications, si c'est du TCP ou de l'UDP

- **Video Youtube "Metal Pipe Falling in 6 different languages**" : 91.68.245.77:443 | port local : 52525 (UDP) 🦈 [Le ptit pote](TP5_service_1.pcapng)

- **Discord appel de gamers 🤓**: 66.22.197.97:50005 | port local: 63868 (UDP) 🦈 [Le ptit pote](TP5_service_2.pcapng) 

- **Téléchargement Steam Among us ඞ🔪** : 185.25.182.7:443 | port local : 53323 (TCP) 🦈 [Le ptit pote](TP5_service_3.pcapng)

- **Site KFC nan c'est trop je pleure sur le poulet carrément 🍗**: 21.1.254.130:443 | port local : 53323 (TCP) 🦈 [Le ptit pote](TP5_service_4.pcapng)

- **sit internette Projet Voltaire poure apprendr franssé** : 104.22.4.149:443 | porc locale : 443 (TCP) 🦈 [Le ptit pote](TP5_service_5.pcapng)

#### 🌞 Demandez l'avis à votre OS (à faire)

## 1. SSH

#### 🌞 Examinez le trafic dans Wireshark

- déterminez si SSH utilise TCP ou UDP
C'est forcément du TCP pour éviter de perdre des paquets.

**Depuis le PC**
  ```TCP    10.5.1.1:58108         10.5.1.11:ssh          ESTABLISHED```


**Depuis la VM**
  ```tcp        ESTAB      0           52                                 10.5.1.11:ssh                   10.5.1.1:58108```

  🦈 [3 Way](tp5_3_way.pcapng)

## 2. Routage

#### 🌞 Prouvez que

```console
  [tristan@localhost ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=112 time=19.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=112 time=24.9 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=112 time=22.3 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=112 time=21.2 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=112 time=24.5 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=112 time=21.9 ms
^C
--- 8.8.8.8 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5016ms
rtt min/avg/max/mdev = 19.831/22.446/24.936/1.775 ms
```

```console
[tristan@localhost ~]$ ping ynov.com
PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=1 ttl=55 time=24.3 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=2 ttl=55 time=27.3 ms
^C64 bytes from 104.26.10.233: icmp_seq=3 ttl=55 time=27.2 ms

--- ynov.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 10160ms
rtt min/avg/max/mdev = 24.257/26.260/27.337/1.417 ms
```