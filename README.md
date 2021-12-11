# Jarkom-Modul-5-C03-2021

Repository Praktikum Jaringan Komputer Modul 5 Jaringan Komputer

.  
Junaedi Akbar <br>
(05111940000041)
<br>
Zydhan Linnar Putra
<br>
(05111940000118)
<br>
M.Fajri Davyza Chaniago
<br>
(05111940000180)  
.

# Praktikum Modul 5

### 📅 5 - 7 Desember 2021

### (A) Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Luffy dibawah ini:

![Soal a](img/soal-a.png)

### (B) Konfigurasi IP dengan VLSM (Variable Length Subnet Masking) :

### Tree :

### Pembagian IP :

| Subnet        |   Jumlah IP   |       Netmask |   subnetmask    |      nid      |
| :------------ | :-----------: | ------------: | :-------------: | :-----------: |
| ------------- | ------------- | ------------- |  -------------  | ------------- |
| A1            |       2       |           /30 | 255.255.255.252 |  192.185.0.0  |
| A2            |       2       |           /30 | 255.255.255.252 |  192.185.0.4  |
| A3            |      201      |           /24 |  255.255.255.0  |  192.185.1.0  |
| A4            |      301      |           /23 |  255.255.254.0  |  192.185.2.0  |
| A5            |      101      |           /25 | 255.255.255.128 | 192.185.0.128 |
| A6            |      701      |           /22 |  255.255.252.0  |  192.185.4.0  |
| A7            |       4       |           /29 | 255.255.255.248 | 192.185.0.16  |
| A8            |       4       |           /29 | 255.255.255.248 | 192.185.0.24  |
| Jumlah        |     1316      |           /21 |  255.255.248.0  |       -       |

- SETTING INTERFACE PADA GNS3
  **Foosha**

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
        address 192.185.0.1
        netmask 255.255.255.252

auto eth2
iface eth2 inet static
         address 192.185.0.5
         netmask 255.255.255.252
```

**Water7**

```
auto eth0
iface eth0 inet static
        address 192.185.0.2
        netmask 255.255.255.252
        gateway 192.185.0.1

auto eth1
iface eth1 inet static
        address 192.185.0.17
        netmask 255.255.255.248

auto eth2
iface eth2 inet static
         address 192.185.0.129
         netmask 255.255.255.128

auto eth3
iface eth3 inet static
         address 192.185.4.1
         netmask 255.255.252.0
```

**GUANHAO**

```
auto eth0
iface eth0 inet static
          address 192.185.0.6
          netmask 255.255.255.252
          gateway 192.185.0.5

auto eth1
iface eth1 inet static
          address 192.185.0.25
          netmask 255.255.255.248

auto eth2
iface eth2 inet static
          address 192.185.1.1
          netmask 255.255.255.0

auto eth3
iface eth3 inet static
           address 192.185.2.1
          netmask 255.255.254.0
```

**Blueno**

```
auto eth0
iface eth0 inet static
      address 192.185.0.130
      netmask 255.255.255.128
      gateway 192.185.0.129
```

**Chiper**

```
auto eth0
iface eth0 inet static
       address 192.185.4.2
      netmask 255.255.252.0
       gateway 192.185.4.1
```

**ELENA**

```
auto eth0
iface eth0 inet static
       address 192.185.2.2
       netmask 255.255.254.0
       gateway 192.185.2.1
```

**fukurou**

```
auto eth0
iface eth0 inet static
       address 192.185.1.2
       netmask 255.255.255.0
       gateway 192.185.1.1
```

**MainGate**

```
auto eth0
iface eth0 inet static
       address 192.185.0.27
       netmask 255.255.255.248
       gateway 192.185.0.25
```

**Jorge**

```
auto eth0
iface eth0 inet static
       address 192.185.0.26
       netmask 255.255.255.248
       gateway 192.185.0.25
```

**Doriki**

```
auto eth0
iface eth0 inet static
       address 192.185.0.18
       netmask 255.255.255.248
       gateway 192.185.0.17
```

**Jipangu**

```
auto eth0
iface eth0 inet static
       address 192.185.0.19
       netmask 255.255.255.248
       gateway 192.185.0.17
```

### (C) Routing

**Foosha**

```
route add -net 192.185.1.0 netmask 255.255.255.0 gw 192.185.0.6
route add -net 192.185.2.0 netmask 255.255.254.0 gw 192.185.0.6
route add -net 192.185.0.24 netmask 255.255.255.248 gw 192.185.0.6
route add -net 192.185.4.0 netmask 255.255.252.0 gw 192.185.0.2
route add -net 192.185.0.128 netmask 255.255.255.128 gw 192.185.0.2
route add -net 192.185.0.16 netmask 255.255.255.248 gw 192.185.0.2
```

### (D) Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

cara:

1. Install `apt-get install isc-dhcp-relay -y` pada foosha, water7, dan guanhao, `apt-get install isc-dhcp-server` pada Jipangu

2. Pada Router (foosha, water7 dan guanhao) Edit file `/etc/sysctl.conf` deengan command

```
net.ipv4.ip_forward=1
net.ipv4.conf.all.accept_source_route = 1
```

3. Lakukan sysctl -p
4. Buka file `/etc/default/isc-dhcp-relay` dan edit server dengan mengarahkan dchp-relay menuju Jipangu `192.185.0.19` lalu `service isc-dhcp-relay restart` pada foosha, water7, dan guanhao

```
echo '# What servers should the DHCP relay forward requests to?
SERVERS="192.185.0.19"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES=""

# Additional options that are passed to the DHCP relay daemon?
OPTIONS="" '> /etc/default/isc-dhcp-relay
```

5. Pada Jipangu edit file `/etc/default/isc-dhcp-server` dengan menambahkan:

```
INTERFACES="eth0"
```

6. Pada dhcp-server isikan data pada `/etc/dhcp/dhcpd.conf` di Jipangu, lalu lakukan `service isc-dhcp-server restart`

```
subnet 192.185.1.0 netmask 255.255.255.0 {
    range 192.185.1.2 192.185.1.254;
    option routers 192.185.1.1;
    option broadcast-address 192.185.1.255;
    option domain-name-servers 192.185.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
subnet 192.185.0.128 netmask 255.255.255.128 {
    range 192.185.0.130 192.185.0.254;
    option routers 192.185.0.129;
    option broadcast-address 192.185.0.255;
    option domain-name-servers 192.185.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
subnet 192.185.4.0 netmask 255.255.252.0 {
    range 192.185.4.2 192.185.4.254;
    option routers 192.185.4.1;
    option broadcast-address 192.185.4.255;
    option domain-name-servers 192.185.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
subnet 192.185.2.0 netmask 255.255.254.0 {
    range 192.185.2.2 192.185.2.254;
    option routers 192.185.2.1;
    option broadcast-address 192.185.2.255;
    option domain-name-servers 192.185.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
subnet 192.185.0.16 netmask 255.255.255.248{
}
```

7. Buka file '/etc/network/interfaces`. Command konfigurasi lama (static) dan ubah ip Blueno, Cipher, Fukurou, dan Elena dengan command

```
auto eth0
iface eth0 inet dhcp
```

8. Lakukan restart di node yang dijadikan ip dhcp

### (1) Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.

### (2) Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang memiliki ip DHCP dan DNS Server demi menjaga keamanan.

### (3) Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

### (4) Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut :Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

### (5) Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.Selain itu di reject

### (6) Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate
