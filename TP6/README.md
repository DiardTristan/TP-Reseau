# TP 6

## DNS

#### 🌞 Compte rendu des 3 cats meow mao meow mao la la la la la

```console
[tristan@dns ~]$ sudo cat /etc/named.conf
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

options {
        listen-on port 53 { 127.0.0.1; any; };
        listen-on-v6 port 53 { ::1; };
        directory       "/var/named";
        dump-file       "/var/named/data/cache_dump.db";
        statistics-file "/var/named/data/named_stats.txt";
        memstatistics-file "/var/named/data/named_mem_stats.txt";
        secroots-file   "/var/named/data/named.secroots";
        recursing-file  "/var/named/data/named.recursing";
        allow-query     { localhost; any; };
        allow-query-cache { localhost; any; };
        /*
         - If you are building an AUTHORITATIVE DNS server, do NOT enable recursion.
         - If you are building a RECURSIVE (caching) DNS server, you need to enable
           recursion.
         - If your recursive DNS server has a public IP address, you MUST enable access
           control to limit queries to your legitimate users. Failing to do so will
           cause your server to become part of large scale DNS amplification
           attacks. Implementing BCP38 within your network would greatly
           reduce such attack surface
        */
        recursion yes;

        dnssec-validation yes;

        managed-keys-directory "/var/named/dynamic";
        geoip-directory "/usr/share/GeoIP";

        pid-file "/run/named/named.pid";
        session-keyfile "/run/named/session.key";

        /* https://fedoraproject.org/wiki/Changes/CryptoPolicy */
        include "/etc/crypto-policies/back-ends/bind.config";
};

logging {
        channel default_debug {
                file "data/named.run";
                severity dynamic;
        };
};

zone "tp6.b1" IN {
     type master;
     file "tp6.b1.db";
     allow-update { none; };
     allow-query {any; };
};

zone "1.4.10.in-addr.arpa" IN {
     type master;
     file "tp6.b1.rev";
     allow-update { none; };
     allow-query { any; };
};

include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";
```

```console
[tristan@dns ~]$ sudo cat /var/named/tp6.b1.rev
$TTL 86400
@ IN SOA dns.tp6.b1. admin.tp6.b1. (
    2019061800 ;Serial
    3600 ;Refresh
    1800 ;Retry
    604800 ;Expire
    86400 ;Minimum TTL
)

@ IN NS dns.tp6.b1.

101 IN PTR dns.tp6.b1.
11 IN PTR john.tp6.b1.
```

```console
[tristan@dns ~]$ sudo cat /var/named/tp6.b1.db
$TTL 86400
@ IN SOA dns.tp6.b1. admin.tp6.b1. (
    2019061800 ;Serial
    3600 ;Refresh
    1800 ;Retry
    604800 ;Expire
    86400 ;Minimum TTL
)

@ IN NS dns.tp6.b1.

dns       IN A 10.6.1.101
john      IN A 10.6.1.11
```

#### Le systemctl status

```console
[tristan@localhost ~]$ systemctl status named
● named.service - Berkeley Internet Name Domain (DNS)
     Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; preset: disabled)
     Active: active (running) since Fri 2023-11-17 10:57:55 CET; 8min ago
   Main PID: 37440 (named)
      Tasks: 5 (limit: 4673)
     Memory: 17.2M
        CPU: 67ms
     CGroup: /system.slice/named.service
             └─37440 /usr/sbin/named -u named -c /etc/named.conf

Nov 17 10:57:55 localhost.localdomain named[37440]: network unreachable resolving './DNSKEY/IN': 2001>
Nov 17 10:57:55 localhost.localdomain named[37440]: network unreachable resolving './NS/IN': 2001:500>
Nov 17 10:57:55 localhost.localdomain named[37440]: zone tp6.b1/IN: loaded serial 2019061800
Nov 17 10:57:55 localhost.localdomain named[37440]: zone localhost.localdomain/IN: loaded serial 0
Nov 17 10:57:55 localhost.localdomain named[37440]: zone localhost/IN: loaded serial 0
Nov 17 10:57:55 localhost.localdomain named[37440]: all zones loaded
Nov 17 10:57:55 localhost.localdomain systemd[1]: Started Berkeley Internet Name Domain (DNS).
Nov 17 10:57:55 localhost.localdomain named[37440]: running
Nov 17 10:57:55 localhost.localdomain named[37440]: managed-keys-zone: Initializing automatic trust a>
Nov 17 10:57:55 localhost.localdomain named[37440]: resolver priming query complete
 ESCOC
S)
service; enabled; preset: disabled)
```

```console
[tristan@dsn ~]$ sudo ss -alnptu
Netid State  Recv-Q Send-Q  Local Address:Port   Peer Address:Port Process
udp   UNCONN 0      0          10.6.1.101:53          0.0.0.0:*     users:(("named",pid=37440,fd=19))
udp   UNCONN 0      0           127.0.0.1:53          0.0.0.0:*     users:(("named",pid=37440,fd=16))
udp   UNCONN 0      0               [::1]:53             [::]:*     users:(("named",pid=37440,fd=22))
tcp   LISTEN 0      4096        127.0.0.1:953         0.0.0.0:*     users:(("named",pid=37440,fd=24))
tcp   LISTEN 0      10          127.0.0.1:53          0.0.0.0:*     users:(("named",pid=37440,fd=17))
tcp   LISTEN 0      128           0.0.0.0:22          0.0.0.0:*     users:(("sshd",pid=16677,fd=3))
tcp   LISTEN 0      10         10.6.1.101:53          0.0.0.0:*     users:(("named",pid=37440,fd=21))
tcp   LISTEN 0      4096            [::1]:953            [::]:*     users:(("named",pid=37440,fd=25))
tcp   LISTEN 0      10              [::1]:53             [::]:*     users:(("named",pid=37440,fd=23))
tcp   LISTEN 0      128              [::]:22             [::]:*     users:(("sshd",pid=16677,fd=4))
```


#### 🌞 Ouvrez le bon port dans le firewall

Le port à ouvrir est le port : 53

```sudo firewall-cmd --add-port=53/udp --permanent```

```sudo firewall-cmd --reload```

### 3. Test

```console
[tristan@john.tp6.b1 network-scripts]$ dig john.tp6.b1

; <<>> DiG 9.16.23-RH <<>> john.tp6.b1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5014
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 0119d82e7eb42ca601000000655749c61dde605a31eef949 (good)
;; QUESTION SECTION:
;john.tp6.b1.                   IN      A

;; ANSWER SECTION:
john.tp6.b1.            86400   IN      A       10.6.1.11

;; Query time: 13 msec
;; SERVER: 10.6.1.101#53(10.6.1.101)
;; WHEN: Fri Nov 17 12:08:54 CET 2023
;; MSG SIZE  rcvd: 84
```


```console
[tristan@john.tp6.b1 network-scripts]$ dig dns.tp6.b1

; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 28027
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: b86df4e9b106d10d0100000065574a89fecad54a9eafabde (good)
;; QUESTION SECTION:
;dns.tp6.b1.                    IN      A

;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.1.101

;; Query time: 16 msec
;; SERVER: 10.6.1.101#53(10.6.1.101)
;; WHEN: Fri Nov 17 12:12:10 CET 2023
;; MSG SIZE  rcvd: 83
```


```console

[tristan@john.tp6.b1 network-scripts]$ dig www.ynov.com

; <<>> DiG 9.16.23-RH <<>> www.ynov.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 341
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: c2f830176f5808d30100000065574ab40241e2b1002c2ff7 (good)
;; QUESTION SECTION:
;www.ynov.com.                  IN      A

;; ANSWER SECTION:
www.ynov.com.           300     IN      A       104.26.10.233
www.ynov.com.           300     IN      A       172.67.74.226
www.ynov.com.           300     IN      A       104.26.11.233

;; Query time: 564 msec
;; SERVER: 10.6.1.101#53(10.6.1.101)
;; WHEN: Fri Nov 17 12:12:53 CET 2023
;; MSG SIZE  rcvd: 117
```


#### Depuis mon PC

```console
PS C:\Users\trist> nslookup john.tp6.b1 10.6.1.101
Serveur :   UnKnown
Address:  10.6.1.101

Nom :    john.tp6.b1
Address:  10.6.1.11
```

##### 🦈 [La question réponse des 12 coups de midi](tp5_3_way.pcapng)