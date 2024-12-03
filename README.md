# Jarkom-Modul-5-IT23-2024


| Nama | NRP |
| :--: | :--: |
| Daffa Rajendra Priyatama | 5027231009 |
| Nabiel Nizar Anwari | 5027231087 |


Soal Modul 5 : https://avalon-ai.org/m/SoalModul5

[Spreadsheets Pembagian Rute dan IP](https://intip.in/SPSIT23Modul5) 


## Misi 1: Memetakan Kota New Eridu

```
Keterangan:
    HDD: Berfungsi sebagai DNS Server.
    Fairy: Berfungsi sebagai DHCP Server.
    Web Servers: HIA, HollowZero.
Client:
    Burnice: Memiliki 5 host.
    Lycaon: Memiliki 20 host.
    Policeboo: Memiliki 30 host.
    Caesar: Memiliki 50 host
    Ellen: Memiliki 100 host.
    Jane: Memiliki 200 host.
```

### Topologi : 
![github-small](https://github.com/bielnzar/Jarkom-Modul-5-IT23-2024/blob/main/assets/images/topologi-fiks.png)

### NewEridu
```
## NAT
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.75.1.217
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.75.1.221
	netmask 255.255.255.252

## Otomasi iptables awal
# IP_ETH0=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $IP_ETH0
```

### LuminaSquare
```
auto eth0
iface eth0 inet static
	address 10.75.1.218
	netmask 255.255.255.252
    gateway 10.75.1.216

auto eth1
iface eth1 inet static
	address 10.75.0.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.75.1.193
	netmask 255.255.255.248
```

### BalletTwins
```
auto eth0
iface eth0 inet static
	address 10.75.1.194
	netmask 255.255.255.248
    gateway 10.75.1.193

auto eth1
iface eth1 inet static
	address 10.75.1.1
	netmask 255.255.255.128
```

### HIA (Apache Worker)
```
auto eth0
iface eth0 inet static
    address 10.75.1.195
    netmask 255.255.255.248
    gateway 10.75.1.193
```

### SixStreet
```
auto eth0
iface eth0 inet static
	address 10.75.1.222
	netmask 255.255.255.252
    gateway 10.75.1.221

auto eth1
iface eth1 inet static
	address 10.75.1.201
	netmask 255.255.255.248

auto eth2
iface eth2 inet static
	address 10.75.1.209
	netmask 255.255.255.248
```

### Fairy (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 10.75.1.203
	netmask 255.255.255.248
    gateway 10.75.1.201
```

### HDD (DNS Server)
```
auto eth0
iface eth0 inet static
	address 10.75.1.203
	netmask 255.255.255.248
    gateway 10.75.1.201
```

### OuterRing
```
auto eth0
iface eth0 inet static
	address 10.75.1.211
	netmask 255.255.255.248
    gateway 10.75.1.209

auto eth1
iface eth1 inet static
	address 10.75.1.129
	netmask 255.255.255.192
```

### ScootOutpost
```
auto eth0
iface eth0 inet static
	address 10.75.1.210
	netmask 255.255.255.248
    gateway 10.75.1.209

auto eth1
iface eth1 inet static
	address 10.75.1.225
	netmask 255.255.255.252
```

### HollowZero (Apache Worker)
```
auto eth0
iface eth0 inet static
	address 10.75.1.226
	netmask 255.255.255.252
    gateway 10.75.1.225
```

##  Misi 1 (No. 2)

### VLSM - Tree : 
![github-small](https://github.com/bielnzar/Jarkom-Modul-5-IT23-2024/blob/main/assets/images/VLSM-Tree.png)


## Misi 1 (No. 3)

### New Eridu
```
post-up route add -net 10.75.1.200 netmask 255.255.255.248 gw 10.75.1.222
post-up route add -net 10.75.1.208 netmask 255.255.255.248 gw 10.75.1.222
post-up route add -net 10.75.1.128 netmask 255.255.255.192 gw 10.75.1.222
post-up route add -net 10.75.1.224 netmask 255.255.255.252 gw 10.75.1.222

post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.218
post-up route add -net 10.75.1.192 netmask 255.255.255.248 gw 10.75.1.218
post-up route add -net 10.75.1.0 netmask 255.255.255.128 gw 10.75.1.218
```

### LuminaSquare
```
post-up route add -net 10.75.1.0 netmask 255.255.255.128 gw 10.75.1.194

post-up route add -net 10.75.1.224 netmask 255.255.255.252 gw 10.75.1.217

post-up route add -net 10.75.1.128 netmask 255.255.255.192 gw 10.75.1.217

post-up route add -net 10.75.1.200 netmask 255.255.255.248 gw 10.75.1.217

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Ballet Twins
```
post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.193

post-up route add -net 10.75.1.224 netmask 255.255.255.252 gw 10.75.1.193

post-up route add -net 10.75.1.128 netmask 255.255.255.192 gw 10.75.1.193

post-up route add -net 10.75.1.200 netmask 255.255.255.248 gw 10.75.1.193

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Six Street
```
post-up route add -net 10.75.1.224 netmask 255.255.255.252 gw 10.75.1.210

post-up route add -net 10.75.1.128 netmask 255.255.255.192 gw 10.75.1.211

post-up route add -net 10.75.1.192 netmask 255.255.255.248 gw 10.75.1.221
post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.221
post-up route add -net 10.75.1.0 netmask 255.255.255.128 gw 10.75.1.221

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Scout Outpost
```
post-up route add -net 10.75.1.200 netmask 255.255.255.248 gw 10.75.1.209
post-up route add -net 10.75.1.192 netmask 255.255.255.248 gw 10.75.1.209
post-up route add -net 10.75.1.0 netmask 255.255.255.128 gw 10.75.1.209
post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.209

post-up route add -net 10.75.1.128 netmask 255.255.255.192 gw 10.75.1.211

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Outer Ring
```
post-up route add -net 10.75.1.200 netmask 255.255.255.248 gw 10.75.1.209
post-up route add -net 10.75.1.192 netmask 255.255.255.248 gw 10.75.1.209
post-up route add -net 10.75.1.0 netmask 255.255.255.128 gw 10.75.1.209
post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.209

post-up route add -net 10.75.1.224 netmask 255.255.255.252 gw 10.75.1.210

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Fairy (DHCP Server)
```
up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### HDD (DNS Server)
```
up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### HIA & HollowZero (Apache Worker)
```
up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

> Semua node sudah terhubung satu sama lain, bisa melakukan ping untuk mengetes antar koneksi node.

![github-small](https://github.com/bielnzar/Jarkom-Modul-5-IT23-2024/blob/main/assets/images/m1-s2_1.png)

![github-small](https://github.com/bielnzar/Jarkom-Modul-5-IT23-2024/blob/main/assets/images/m1-s2_2.png)

### NewEridu terhubung ke internet menggunakan iptables tanpa MASQUERADE
```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source [IP eth0]
```

> NewEridu sudah terhubung ke internet, begitu juga subnet yg terhubung dengannya.

![github-small](https://github.com/bielnzar/Jarkom-Modul-5-IT23-2024/blob/main/assets/images/m2-s1_1.png)

![github-small](https://github.com/bielnzar/Jarkom-Modul-5-IT23-2024/blob/main/assets/images/m2-s1_2.png)

## DHCP Stuff

### DHCP Server Stuff
```
apt-get update
apt-get install isc-dhcp-server
```
DHCPserver.sh
```
echo '
INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server

echo '
subnet 10.75.0.0 netmask 255.255.255.0 {
  range 10.75.0.2 10.75.0.254;
  option routers 10.75.0.1;
  option broadcast-address 10.75.0.255;
  option domain-name-servers 10.75.1.203;
}

subnet 10.75.1.0 netmask 255.255.255.128 {
  range 10.75.1.2 10.75.1.126;
  option routers 10.75.1.1;
  option broadcast-address 10.75.1.127;
  option domain-name-servers 10.75.1.203;
}

subnet 10.75.1.128 netmask 255.255.255.192 {
  range 10.75.1.130 10.75.1.190;
  option routers 10.75.1.129;
  option broadcast-address 10.75.1.191;
  option domain-name-servers 10.75.1.203;
}
subnet 10.75.1.200 netmask 255.255.255.248{
  range 10.75.1.202 10.75.1.206;
  option routers 10.75.1.201;
  option broadcast-address 10.75.1.207;
  option domain-name-servers 10.75.1.203;
}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

### DHCP relay stuff
```
apt
```
DHCPrelay.sh
```
echo '
SERVERS="10.75.1.202"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1
' > /etc/sysctl.conf

service isc-dhcp-relay restart
```
### DNS stuff
```
apt
```
DNS.sh
```
echo 'options {
    directory "/var/cache/bind";

    forwarders {
        192.168.122.1;
    };

    // dnssec-validation auto;

    allow-query { any; };
    auth-nxdomain no;    # conform to RFC1035
    listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```

## Misi 2 (No. 2)
```sh
iptables -A INPUT -p icmp --icmp-type echo-request -j REJECT
iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT
```

## Misi 2 (No. 3)
```sh
iptables -A INPUT -j REJECT
iptables -A INPUT -s <ipfairy> -j ACCEPT
```

## Misi 2 (No. 4)
Hollow
```sh
iptables -A INPUT -j REJECT
iptables -A INPUT -s <ipburnice> -m time --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s <ipcaesar> -m time --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s <ipjane> -m time --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s <ippoliceboo> -m time --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
```

## Misi 2 (No. 5)
HIA
```sh
iptables -A INPUT -p tcp -s <IP Ellen> --dport 80 -m time --timestart 01:00 --timestop 14:00 -j ACCEPT
iptables -A INPUT -p tcp -s <IP Lycaon> --dport 80 -m time --timestart 01:00 --timestop 14:00 -j ACCEPT

iptables -A INPUT -p tcp -s <IP Jane> --dport 80 -m time --timestart 20:00 --timestop 16:00  -j ACCEPT
iptables -A INPUT -p tcp -s <IP Policeboo> --dport 80 -m time --timestart 20:00 --timestop 16:00 -j ACCEPT

iptables -A INPUT -p tcp --dport 80 -j REJECT # reject other requests
```

## Misi 2 (No. 6)
```sh
# Create a chain for handling detected scans
iptables -N PORTSCAN

# Rate-limit all new connections: Allow max 25 connections in 10 seconds
iptables -A INPUT -m conntrack --ctstate NEW \
  -m recent --set --name portscan
iptables -A INPUT -m conntrack --ctstate NEW \
  -m recent --update --seconds 10 --hitcount 25 --name portscan -j PORTSCAN

# Handle scanning activity
iptables -A PORTSCAN -m recent --set --name blacklist
iptables -A PORTSCAN -j LOG --log-prefix 'PORT SCAN DETECTED ' --log-level 4
iptables -A PORTSCAN -j DROP

# Block all traffic from blacklisted IPs
iptables -A INPUT -m recent --name blacklist --rcheck -j DROP
iptables -A OUTPUT -m recent --name blacklist --rcheck -j DROP
```

![github-small](https://github.com/bielnzar/Jarkom-Modul-5-IT23-2024/blob/main/assets/images/port-scan.jpg)

## Misi 2 (No. 7)
```
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -m recent --set
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -m recent --update --seconds 1 --hitcount 3 -j REJECT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

## Misi 2 (No. 8)
```
iptables -t nat -A PREROUTING -p tcp -j DNAT --to-destination 10.75.1.226 --dport 8080
iptables -A FORWARD -p tcp -d 10.75.1.226 -j ACCEPT
```

## Misi 3 (No. 1)
```
iptables --policy INPUT DROP
iptables --policy OUTPUT DROP
iptables --policy FORWARD DROP
```
