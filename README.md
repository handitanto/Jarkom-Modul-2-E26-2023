# Jarkom-Modul-2-E26-2023
**Praktikum Jaringan Komputer Modul 2 Tahun 2023**

## Author
| Nama | NRP |Github |
|---------------------------|------------|
|Handitanto Herprasetyo | 5025201077 |

## Topologi
![image]()

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
  
- **Prabukusuma**
  ```
  auto eth0
  iface eth0 inet static
  	address 192.219.3.5
  	netmask 255.255.255.0
  	gateway 192.219.3.1
  ```

  
