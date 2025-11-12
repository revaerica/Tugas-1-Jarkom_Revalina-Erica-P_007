# Tugas-1-Jarkom_Revalina-Erica-P_007

## Visualisasi
<img width="957" height="584" alt="image" src="https://github.com/user-attachments/assets/a8a3a9b5-355a-4142-8cf0-d8e8ec0dce78" />

## Kofigurasi Router
**R1**
```
! Masuk ke mode konfigurasi
enable
configure terminal
hostname Router1

! Aktifkan interface fisik utama
interface FastEthernet0/0
 no ip address
 no shutdown
exit

interface FastEthernet0/1
 no shutdown
exit

! Buat Subinterface untuk VLAN & subnet di Pusat (HQ)
! VLAN 10 - Sekretariat
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 10.47.0.1 255.255.254.0
 no shutdown
exit

! VLAN 20 - Kurikulum
interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 10.47.2.1 255.255.255.0
 no shutdown
exit

! VLAN 30 - Guru & Tendik
interface FastEthernet0/0.30
 encapsulation dot1Q 30
 ip address 10.47.3.1 255.255.255.128
 no shutdown
exit

! VLAN 40 - Sarpras
interface FastEthernet0/0.40
 encapsulation dot1Q 40
 ip address 10.47.3.129 255.255.255.192
 no shutdown
exit

! VLAN 50 - Pengawas Pusat
interface FastEthernet0/0.50
 encapsulation dot1Q 50
 ip address 10.47.3.193 255.255.255.224
 no shutdown
exit

! VLAN 60 - Server & Admin
interface FastEthernet0/0.60
 encapsulation dot1Q 60
 ip address 10.47.4.1 255.255.255.248
 no shutdown
exit

! Konfigurasi antar-router (Link ke Cabang)
interface FastEthernet0/1
 description Link-to-Router2
 ip address 10.47.4.9 255.255.255.252
 no shutdown
exit

! Routing statik (ke jaringan cabang)
ip route 10.47.3.224 255.255.255.224 10.47.4.10

end
write memory
```

**R2**
```
! Masuk ke mode konfigurasi
enable
configure terminal
hostname Router2

! Aktifkan interface fisik utama
interface FastEthernet0/0
 no ip address
 no shutdown
exit

interface FastEthernet0/1
 no shutdown
exit

! Buat Subinterface untuk VLAN Cabang
! VLAN 70 - Pengawas Cabang
interface FastEthernet0/0.70
 encapsulation dot1Q 70
 ip address 10.47.3.225 255.255.255.224
 no shutdown
exit

! Konfigurasi antar-router (Link ke Pusat)
interface FastEthernet0/1
 description Link-to-Router1
 ip address 10.47.4.10 255.255.255.252
 no shutdown
exit

! Routing statik (ke jaringan pusat)
ip route 10.47.0.0 255.255.248.0 10.47.4.9

end
write memory
```

**Switch 6**
```
enable
configure terminal

! VLAN untuk Server & Admin
vlan 60
 name SERVER_ADMIN
exit

! Port ke Server
interface FastEthernet0/1
 switchport mode access
 switchport access vlan 60
 no shutdown
exit

! Port ke Router1 (trunk)
interface FastEthernet0/24
 switchport mode trunk
 no shutdown
exit

end
write memory
```

---

## **IP PC**
| PC              | IP Address  | Subnet Mask     | Default Gateway |
| :-------------- | :---------- | :-------------- | :-------------- |
| Sekretariat     | 10.47.0.2   | 255.255.254.0   | 10.47.0.1       |
| Kurikulum       | 10.47.2.2   | 255.255.255.0   | 10.47.2.1       |
| Guru & Tendik   | 10.47.3.2   | 255.255.255.128 | 10.47.3.1       |
| Sarpras         | 10.47.3.130 | 255.255.255.192 | 10.47.3.129     |
| Pengawas Pusat  | 10.47.3.194 | 255.255.255.224 | 10.47.3.193     |
| Server          | 10.47.4.2   | 255.255.255.248 | 10.47.4.1       |
| Pengawas Cabang | 10.47.3.226 | 255.255.255.224 | 10.47.3.225     |

---

## Hasil akhir
