# Jarkom-Modul-2-E26-2023
**Praktikum Jaringan Komputer Modul 2 Tahun 2023**

## Author
| Nama | NRP |
|---------------------------|------------|
|Handitanto Herprasetyo | 5025201077 |

## Topologi
![image](https://github.com/handitanto/Jarkom-Modul-2-E26-2023/blob/main/img/topologi.png)

## Config 
- **Pandudewanata**
  ```
  auto eth0
  iface eth0 inet dhcp
  
  auto eth1
  iface eth1 inet static
  	address 192.219.1.1
  	netmask 255.255.255.0
  
  auto eth2
  iface eth2 inet static
  	address 192.219.2.1
  	netmask 255.255.255.0
  
  auto eth3
  iface eth3 inet static
  	address 192.219.3.1
  	netmask 255.255.255.0

  ```

- **Nakula**
  ```
   auto eth0
  iface eth0 inet static
  	address 192.219.1.2
  	netmask 255.255.255.0
  	gateway 192.219.1.1
  ```
- **Sadewa**
  ```
   auto eth0
  iface eth0 inet static
  	address 192.219.1.3
  	netmask 255.255.255.0
  	gateway 192.219.1.1
  ```
  
  - **Yudhistira**
  ```
  auto eth0
  iface eth0 inet static
  	address 192.219.2.2
  	netmask 255.255.255.0
  	gateway 192.219.2.1
  ```
  
- **Werkudara**
  ```
  auto eth0
  iface eth0 inet static
  	address 192.219.2.3
  	netmask 255.255.255.0
  	gateway 192.219.2.1
  ```
- **Arjuna**
  ```
  auto eth0
  iface eth0 inet static
  	address 192.219.3.2
  	netmask 255.255.255.0
  	gateway 192.219.3.1
  ```
 
  - **Wisanggeni**
  ```
  auto eth0
  iface eth0 inet static
  	address 192.219.3.3
  	netmask 255.255.255.0
  	gateway 192.219.3.1
  ```

- **Abimanyu**
  ```
  auto eth0
  iface eth0 inet static
  	address 192.219.3.4
  	netmask 255.255.255.0
  	gateway 192.219.3.1
  ```

  ### Setup Master, Slave, Client
- **Prabukusuma**
  ```
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.219.0.0/16
  cat /etc/resolv.conf
  ```

## Soal 1
> Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive

- Lakukan tes ping google pada client. `Nakula dan Sadewa`
```
ping google.com -c 5
```
![image](https://github.com/handitanto/Jarkom-Modul-2-E26-2023/blob/main/img/no1.1.png)
![image](https://github.com/handitanto/Jarkom-Modul-2-E26-2023/blob/main/img/no1.2.png)

## Soal 2 
> Buatlah website utama dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.

- Ketik command `nano /root/no2.sh` di Yudhistira untuk membuat folder yang bernama no2 pada root.
- Isi folder tersebut dengan
```
echo 'zone "arjuna.e26.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.e26.com";
        allow-transfer { 192.219.3.2; }; // IP Arjuna
};' > /etc/bind9/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/arjuna.e26.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     arjuna.e26.com. root.arjuna.e26.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.e26.com.
@       IN      A       192.219.2.2     ; IP Yudhistira
www     IN      CNAME   arjuna.e26.com.' > /etc/bind/jarkom/arjuna.e26.com

service bind9 restart
```
- Simpan dan kemudian jalankan dengan command `bash /root/no2.sh`
- Tes script tersebut pada client dengan command `ping arjuna.e26.com -c 5`
![image](https://github.com/handitanto/Jarkom-Modul-2-E26-2023/blob/main/img/no2.png)

## Soal 3
> Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

- Ketik command `nano /root/no3.sh` di Yudhistira untuk membuat folder yang bernama no3 pada root.
- Isi folder tersebut dengan
```
echo 'zone "arjuna.e26.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.e26.com";
};

zone "abimanyu.e26.com" {
        type master;
        file "/etc/bind/jarkom/abimanyu.e26.com";
};' > /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/abimanyu.e26.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.e26.com. root.abimanyu.e26.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.e26.com.
@       IN      A       192.219.2.2     ; IP Yudhistira
www     IN      CNAME   abimanyu.e26.com.' > /etc/bind/jarkom/abimanyu.e26.com

service bind9 restart
```
- Simpan dan kemudian jalankan dengan command `bash /root/no3.sh`
- Tes script tersebut pada client dengan command `ping abimanyu.e26.com -c 5`
![image](https://github.com/handitanto/Jarkom-Modul-2-E26-2023/blob/main/img/no3.png)

## Soal 4
> Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

- Ketik command `nano /root/no4.sh` di Yudhistira untuk membuat folder yang bernama no4 pada root.
- Isi folder tersebut dengan
```
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.e26.com. root.abimanyu.e26.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.e26.com.
@       IN      A       192.219.2.2     ; IP Yudhistira
www     IN      CNAME   abimanyu.e26.com.
parikesit IN    A       192.219.3.4     ; IP Abimanyu' > /etc/bind/jarkom/abimanyu.e26.com

service bind9 restart
```
- Simpan dan kemudian jalankan dengan command `bash /root/no4.sh`
- Tes script tersebut pada client dengan command `ping parikesit.abimanyu.e26.com -c 5`
![image](https://github.com/handitanto/Jarkom-Modul-2-E26-2023/blob/main/img/no4.png)

## Soal 5
> Buat juga reverse domain untuk domain utama.

- Ketik command `nano /root/no5.sh` di Yudhistira untuk membuat folder yang bernama no5 pada root.
- Isi folder tersebut dengan
```
  echo 'zone "3.219.192.in-addr.arpa" {
        type master;
        file "/etc/bind/jarkom/3.219.192.in-addr.arpa";
  };' > /etc/bind/named.conf.local
  
  cp /etc/bind/db.local /etc/bind/jarkom/3.219.192.in-addr.arpa
  
  echo '
  ;
  ; BIND data file for local loopback interface
  ;
  $TTL    604800
  @       IN      SOA     abimanyu.e26.com. root.abimanyu.e26.com. (
                          2003101001      ; Serial
                           604800         ; Refresh
                            86400         ; Retry
                          2419200         ; Expire
                           604800 )       ; Negative Cache TTL
  ;
  3.219.192.in-addr.arpa. IN      NS      abimanyu.e26.com.
  4                       IN      PTR     abimanyu.e26.com.
  2                       IN      PTR     arjuna.e26.com.' > /etc/bind/jarkom/3.219.192.in-addr.arpa
  
  service bind9 restart
```
- Simpan dan kemudian jalankan dengan command `bash /root/no5.sh`
- Tes script tersebut pada client dengan command `host -t PTR 192.219.3.4`
![image](
