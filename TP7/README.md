# TP 7

## SSH

#### 🌞 Effectuez une connexion SSH en vérifiant le fingerprint

``` ssh tristan@10.7.1.11```


```console
The authenticity of host '10.7.1.11 (10.7.1.11)' can't be established.
ED25519 key fingerprint is SHA256:CoMGKXc0JWXwmMEiVCxxJ7SifJW18MfCLGMJKJMNO9A.
This host key is known by the following other names/addresses:
    C:\Users\trist/.ssh/known_hosts:11: 10.6.1.254
    C:\Users\trist/.ssh/known_hosts:14: 10.6.1.11
    C:\Users\trist/.ssh/known_hosts:15: 10.6.1.101
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

```console
[tristan@localhost ~]$ sudo ssh-keygen -l -f /etc/ssh/ssh_host_ed25519_key
[sudo] password for tristan:
256 SHA256:CoMGKXc0JWXwmMEiVCxxJ7SifJW18MfCLGMJKJMNO9A /etc/ssh/ssh_host_ed25519_key.pub (ED25519)
```

### 2. Conf serveur SSH

#### 🌞 Consulter l'état actuel

```console
sudo ss -alnptu
Netid  State   Recv-Q  Send-Q   Local Address:Port   Peer Address:Port Process
tcp    LISTEN  0       128            0.0.0.0:22          0.0.0.0:*     users:(("sshd",pid=689,fd=3))
tcp    LISTEN  0       128               [::]:22             [::]:*     users:(("sshd",pid=689,fd=4))
```
#### 🌞 Modifier la configuration du serveur SSH

```sudo nano /etc/ssh/sshd_config```

```console
Port 25555
#AddressFamily any
ListenAddress 10.7.1.254
#ListenAddress ::
```


#### 🌞 Prouvez que le changement a pris effet

```sudo ss -alnptu```

```console
Netid      State       Recv-Q      Send-Q           Local Address:Port              Peer Address:Port      Process
tcp        LISTEN      0           128                 10.7.1.254:25555                  0.0.0.0:*          users:(("sshd",pid=1381,fd=3))
```

#### 🌞 N'oubliez pas d'ouvrir ce nouveau port dans le firewall

```sudo firewall-cmd --add-port=25555/tcp --permanent```

#### 🌞 Effectuer une connexion SSH sur le nouveau port
```console
PS C:\Users\trist> ssh tristan@10.7.1.254 -p 25555
tristan@10.7.1.254's password:
Last login: Fri Nov 24 10:37:47 2023
```

### 3. Connexion par clés


#### 🌞 Générer une paire de clés
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDTcaTZyJG0yi8pzopasDftrGq6UtR+LEGzpOm4cFNKMMIUDZW1Yjot98ojoZcRQFYYdS3Lln+FOgRA3rCkJ3ihAnfNyQnxlKpxy3C4Yv1ZzXgO0D5ZUbEOKnGvvlcu+c/DIx4+saQdCinxUj8PBwR+wGNyfHlGzSfByBZDtZoxWgVeLUNdaiZWVEh3YpjvrFSOECvjIq7h2gYnIv+xkk3eGb5LH8LVKHHPAJE6aHMKCbpgjUjZcU/fn5KyhIk2AFt7FNJFd8Tu2pFyf9jqan0scF//XLZY8VvLPLTbn9sTwm9ew00fnC6Ny5xGWGtnAo7NfN257KnfdD5h7OTydN9QHe7nhlkHPHcFxH82ADk4PiExMx5Y6icJFHAG5/8HLZ38j5pAV7wm7IvJ+yX3WBr+k3jHR1FR7uAZbTjjZN3Z8kEFo0U1QFmvgQAK6F65U9TPWJkODH6JnL17YRQglRxjmS7SrV/NjPeeWqvZIkOK5q+SD3NQ2eoIAXo1n2MgP+ubPwhjQtBwKnx3NSiqrl8wXe/7MV/mJb40vkPCeODrQDlPrFiH1Ao9pKmKscfchNlhtKl7L7aKCtijmGYaTMt8QCObpqFK56n3/UavWCVFVSbpLQEhw2E3JMJT8dO+1xaTfweO+KiZKWDfaCwgYLZ2Pv9JlrfAeQo+YtoFK6PkLw== trist@MSI
```


#### 🌞 Déposer la clé publique sur une VM
```console
trist@MSI MINGW64 ~ (master)
$ ssh-copy-id -p 25555 tristan@10.7.1.254
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/c/Users/trist/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
tristan@10.7.1.254's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh -p 25555 'tristan@10.7.1.254'"
and check to make sure that only the key(s) you wanted were added.
```

#### 🌞 Connectez-vous en SSH à la machine
```console
$ ssh -p 25555 tristan@10.7.1.254
Last login: Fri Nov 24 11:05:45 2023 from 10.7.1.1
[tristan@routeurtp7 ~]$
```


#### 🌞 Supprimer les clés sur la machine router.tp7.b1

```sudo rm /etc//ssh/ssh_host_*```

```console
[tristan@routeurtp7 ~]$ sudo ssh-keygen -A
ssh-keygen: generating new host keys: RSA DSA ECDSA ED25519
```

```sudo systemctl restart sshd```


#### 🌞 Tentez une nouvelle connexion au serveur
```console
PS C:\Users\trist> ssh tristan@10.7.1.11
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:vx/Zj0/Rb2ajAuM/R6M//bgG5hfRznceJ1ZFuBEnLj8.
Please contact your system administrator.
Add correct host key in C:\\Users\\trist/.ssh/known_hosts to get rid of this message.
Offending ED25519 key in C:\\Users\\trist/.ssh/known_hosts:17
Host key for 10.7.1.11 has changed and you have requested strict checking.
Host key verification failed.
```


#### Pour résoudre le problème il suffit de supprimer la ligne dans ```C:\Users\trist\.ssh\known_hosts```

```
10.7.1.11 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINUbbTUR8SqkLdNNrLGEUSTPjjy237qaRxkwWBrO57WX
```

## Web

#### 🌞 Montrer sur quel port est disponible le serveur web


```
[tristan@web ~]$ ss -atnl
State   Recv-Q  Send-Q   Local Address:Port     Peer Address:Port  Process
LISTEN  0       511            0.0.0.0:80            0.0.0.0:*
LISTEN  0       128            0.0.0.0:22            0.0.0.0:*
LISTEN  0       511               [::]:80               [::]:*
LISTEN  0       128               [::]:22               [::]:*
```

```console
[tristan@web ~]$ sudo openssl req -new -newkey rsa:2048 -days 365 -nodes -
    x509 -keyout server.key -out server.crt
Ignoring -days without -x509; not generating a certificate
........+..+.........+.+.....+...+....+..+.+...+.........+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.+............+..+...+............+.+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*......+......+......+....+.....+......+.............+..+..........+......+...............+...+..+.............+..............+.+..+...+.+.....+.+...+.....+.+...........+............+...+....+...+...+.....+.......+..+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
..+...+........+...+......+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*..........+......+..+..........+..+.+......+...+..+......+....+........+.+...............+......+.....+......+...+.+.....+...+...+.........+.+...............+..+............+...+......+....+...+...+.....+......+...+.............+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.....+.+..............+.......+...+.........+......+............+...+.....+....+..+....+.....+.+...........+....+.....+......+....+...+......+..+...+....+..+....+...........+......+...+.........+......+...............+.+........+.+..+..........+........+.......+.....+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:
State or Province Name (full name) []:
Locality Name (eg, city) [Default City]:
Organization Name (eg, company) [Default Company Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:
Email Address []:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
-----BEGIN CERTIFICATE REQUEST-----
MIIChzCCAW8CAQAwQjELMAkGA1UEBhMCWFgxFTATBgNVBAcMDERlZmF1bHQgQ2l0
eTEcMBoGA1UECgwTRGVmYXVsdCBDb21wYW55IEx0ZDCCASIwDQYJKoZIhvcNAQEB
BQADggEPADCCAQoCggEBAKPEyFylcQBMakD6SYMbk/kLEukWczhHH/AbvSQTF2E2
VIMKa0GQvH8NHEWAmH16Yrh+1TfZLEhr9zzRmwYEn6xh3/lJghAG8hPnd9qZrDSZ
u8YVy2V+hMctMkapXi0NIShV8HLlQQljizDO8Sjt+hHqlc3AG3w2jo26hM+1k+eQ
SAi8gs/BQm1yI54tDsFm2WMqatkIkcEZnqZK/fYUizdRbuVCwN4AZnOrzay8vqOa
Sg70Jnq5nDCv6rKj4lKHJUinyPMkxSiMqcOxCUyA4l/eXqexRLjzhQNOpi7RH9Oh
jbdTzqcyc9FrQuv3vjkNDB9CDP3Bdzcxw40Us1MugGcCAwEAAaAAMA0GCSqGSIb3
DQEBCwUAA4IBAQCid903IdG1pnCRw6i19HJ9l5e8R31nV+3ABfQL6JScaCvI88O3
/+22bWyMRqspbK+XFsh+PerH4XU8MlYPVMP+oWRbouaALZmt1l3oXQBatvXBQgRf
EFig8uC+jUss8rwB3mKhCuv94FE7D59TYMON8H6LGDD1yjo/w8Bucvi5lEjQeHw5
m7Rj7LL8g6K2Y2FT9hCUzexgSF2J/wMHYYlbFj3Q39cd7cmptFIKtPDEZTTW77aQ
xWGaWKULwqqnC2Vnj5MvdOlHAGo2poaec9cnVyxZ1bh4k/7pOdZ/7OP9ZvcfSgfg
dHLiTgZZqx3ipTVQQqyJEi6mtkrbSwSsnEyQ
-----END CERTIFICATE REQUEST-----
-bash: x509: command not found
```


#### 🌞 Modification de la conf de NGINX
```console
[tristan@web ~]$ sudo cat /etc/nginx/conf.d/site_web_nul.conf
server {
    listen 10.7.1.12:443 ssl;

    ssl_certificate /etc/pki/tls/certs/web.tp7.b1.crt;
    ssl_certificate_key /etc/pki/tls/private/web.tp7.b1.key;

    server_name www.site_web_nul.b1;
    root /var/www/site_web_nul;
}
```


#### 🌞 Conf firewall

```[tristan@web ~]$ sudo firewall-cmd --add-port=443/tcp --permanent
success
```

#### 🌞 Prouvez que NGINX écoute sur le port 443/tcp

[tristan@web ~]$ ss -atnl
State   Recv-Q  Send-Q   Local Address:Port     Peer Address:Port  Process
LISTEN  0       511          10.7.1.12:443           0.0.0.0:*
LISTEN  0       511            0.0.0.0:80            0.0.0.0:*
LISTEN  0       128            0.0.0.0:22            0.0.0.0:*
LISTEN  0       511               [::]:80               [::]:*
LISTEN  0       128               [::]:22               [::]:*