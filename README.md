# Lapres_Modul2_JA02
Laporan Praktikum Jaringan Komputer 2019 oleh grup A02.

### Oleh:
- Donny Fitrado (05111740000171)
- Faqih Fathan Irfani (05111740000175)

## Membuat File topologi.sh
Pertama, kita akan membuat file topologi.sh seperti berikut ini:
<img src="images/topologi(dot)sh.png" width="800">

## Menghilangkan (#) dari bagian net.ipv4.ip_forward=1
Kedua, buka file ```sysctl.conf``` pada directory etc di ARTICUNO.
<img src="images/sysctl(conf).png" width="600">
Kemudian, ketikkan ```sysctl -p``` untuk mengaktifkan perubahan.

## Setting IP di Semua UML
Buka file interfaces dengan mengetikkan ```nano /etc/network/interfaces```, lalu isi semua UML dengan IP yang ada di bawah ini:
### Pikachu (Router)
```
auto eth0
iface eth0 inet static
address 10.151.72.18
netmask 255.255.255.252
gateway 10.151.72.17

auto eth1
iface eth1 inet static
address 10.151.73.33
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.168.0.1
netmask 255.255.255.0
```
### Articuno (DNS Server)
```auto eth0
iface eth0 inet static
address 10.151.73.34
netmask 255.255.255.248
gateway 10.151.73.33
```
### Mewtwo (Web Server)
```
auto eth0
iface eth0 inet static
address 10.151.73.35
netmask 255.255.255.248
gateway 10.151.73.33
```
### Moltres (DNS Slave)
```
auto eth0
iface eth0 inet static
address 10.151.73.36
netmask 255.255.255.248
gateway 10.151.73.33
```
### Psyduck (Klien)
```
auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.0
gateway 192.168.0.1
```
### Snorlax (Klien)
```
auto eth0
iface eth0 inet static
address 192.168.0.3
netmask 255.255.255.0
gateway 192.168.0.1
```

Setelah semua UML diberi IP, maka restart network dengan ```service networking restart```

## Membuat file iptables.h
Kita membuat file iptables.h yang berisi ```iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.168.0.0/16```
seperti di bawah ini:
<img src="images/iptables(dot)h.png" width="600">
Pembuatan file ini kita lakukan agar lebih cepat menjalankan iptables(dengan dibash), daripada mengetik satu per satu setiap kita ingin menjalankan iptables.

## Membuat file proxy.sh
Lalu, membuat file proxy.sh yang berisi template proxy (sudah diberikan di soal) namun kita sesuaikan dengan proxy yang kita dapatkan dari OTP integra.
<img src="images/proxy(dot)sh.png" width="600">

## Jalankan iptables dan proxy
```bash iptables.h``` pada PIKACHU, lalu ```source proxy.sh``` pada semua UML.
<img src="images/bash iptables & source proxy.png" width="600">

## Menginstall bind9
Pertama, kita mengupdate package list terlebih dahulu dengan ```apt-get update```
Setelah itu, barulah menginstall bind9 dengan ```apt-get install bind9 -y``` seperti di bawah ini:
<img src="images/install%20bind9.png" width="600">

