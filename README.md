# Jarkom-Modul-4-IT23-2024


| Nama | NRP |
| :--: | :--: |
| Daffa Rajendra Priyatama | 5027231009 |
| Nabiel Nizar Anwari | 5027231087 |


Soal Modul 4 : https://avalon-ai.org/m/SoalModul5

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

## Pohon Subnet : 


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

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```

### Ballet Twins
```
post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.193

post-up route add -net 10.75.1.224 netmask 255.255.255.252 gw 10.75.1.193

post-up route add -net 10.75.1.128 netmask 255.255.255.192 gw 10.75.1.193

post-up route add -net 10.75.1.200 netmask 255.255.255.248 gw 10.75.1.193

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```

### Six Street
```
post-up route add -net 10.75.1.224 netmask 255.255.255.252 gw 10.75.1.210

post-up route add -net 10.75.1.128 netmask 255.255.255.192 gw 10.75.1.211

post-up route add -net 10.75.1.192 netmask 255.255.255.248 gw 10.75.1.221
post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.221
post-up route add -net 10.75.1.0 netmask 255.255.255.128 gw 10.75.1.221

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```

### Scout Outpost
```
post-up route add -net 10.75.1.200 netmask 255.255.255.248 gw 10.75.1.209
post-up route add -net 10.75.1.192 netmask 255.255.255.248 gw 10.75.1.209
post-up route add -net 10.75.1.0 netmask 255.255.255.128 gw 10.75.1.209
post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.209

post-up route add -net 10.75.1.128 netmask 255.255.255.192 gw 10.75.1.211

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```

### Outer Ring
```
post-up route add -net 10.75.1.200 netmask 255.255.255.248 gw 10.75.1.209
post-up route add -net 10.75.1.192 netmask 255.255.255.248 gw 10.75.1.209
post-up route add -net 10.75.1.0 netmask 255.255.255.128 gw 10.75.1.209
post-up route add -net 10.75.0.0 netmask 255.255.255.0 gw 10.75.1.209

post-up route add -net 10.75.1.224 netmask 255.255.255.252 gw 10.75.1.210

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```

### Fairy (DHCP Server)
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```

### HDD (DNS Server)
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```

### HIA & HollowZero (Apache Worker)
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```


## Misi 2 (No. 1)

### NewEridu terhubung ke internet menggunakan iptables tanpa MASQUERADE
```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source [IP eth0]
```