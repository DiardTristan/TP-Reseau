# TP 5

## 1. First Steps

#### 🌞 Déterminez, pour ces 5 applications, si c'est du TCP ou de l'UDP

- Video Youtube "Metal Pipe Falling in 6 different languages" : 91.68.245.77:443 | port local : 52525 (UDP) 🦈 [Le ptit pote](TP5_service_1.pcapng)

- Discord appel de gamers 🤓 : 66.22.197.97:50005 | port local : 63868 (UDP) 🦈 [Le ptit pote](TP5_service_2.pcapng) 

- Téléchargement Steam Among us ඞ🔪 : 185.25.182.7:443 | port local : 53323 (TCP) 🦈 [Le ptit pote](TP5_service_3.pcapng)

- Site KFC nan c'est trop je pleure sur le poulet carrément 🍗 : 21.1.254.130:443 | port local : 53323 (TCP) 🦈 [Le ptit pote](TP5_service_4.pcapng)

- sit internette Projet Voltaire poure apprendr franssé : 104.22.4.149:443 | porc locale : 443 (TCP) 🦈 [Le ptit pote](TP5_service_5.pcapng)

#### 🌞 Demandez l'avis à votre OS (à faire)

## 1. SSH

#### 🌞 Examinez le trafic dans Wireshark

- déterminez si SSH utilise TCP ou UDP
C'est forcément du TCP pour éviter de perdre des paquets.

**Depuis le PC**
  ```TCP    10.5.1.1:58108         10.5.1.11:ssh          ESTABLISHED```


**Depuis la VM**
  ```tcp        ESTAB      0           52                                 10.5.1.11:ssh                   10.5.1.1:58108```