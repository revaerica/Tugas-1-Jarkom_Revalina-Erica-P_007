# Tugas-1-Jarkom_Revalina-Erica-P_007

## Visualisasi

<img width="1067" height="682" alt="image" src="https://github.com/user-attachments/assets/915fb5a6-ac65-493b-be1e-c40557aed541" />

## Kofigurasi Router

**R1**
```
enable
configure terminal
hostname Router1

! Aktifkan port ke Switch Core (Router-on-a-Stick)
interface FastEthernet0/3/0
 no shutdown
exit

! Subinterface VLAN Sekretariat
interface FastEthernet0/3/0.10
 encapsulation dot1Q 10
 ip address 10.47.0.1 255.255.254.0
no shutdown
exit

! Subinterface VLAN Kurikulum
interface FastEthernet0/3/0.20
 encapsulation dot1Q 20
 ip address 10.47.2.1 255.255.255.0
 no shutdown
exit

! Subinterface VLAN Guru & Tendik
interface FastEthernet0/3/0.30
 encapsulation dot1Q 30
 ip address 10.47.3.1 255.255.255.128
 no shutdown
exit

! Subinterface VLAN Sarpras
interface FastEthernet0/3/0.40
 encapsulation dot1Q 40
 ip address 10.47.3.129 255.255.255.192
 no shutdown
exit

! Subinterface VLAN Pengawas Pusat
interface FastEthernet0/3/0.50
 encapsulation dot1Q 50
 ip address 10.47.3.193 255.255.255.224
 no shutdown
exit

! Subinterface VLAN Server & Admin
interface FastEthernet0/3/0.60
 encapsulation dot1Q 60
 ip address 10.47.4.1 255.255.255.248
 no shutdown
exit

! Serial link ke Router2 (Cabang)
interface Serial0/2/0
 ip address 10.47.4.9 255.255.255.252
 clock rate 64000
 no shutdown
exit

! Routing ke Cabang (Pengawas Cabang)
ip route 10.47.3.224 255.255.255.224 10.47.4.10

end
write memory
```

**R2**
```
enable
configure terminal
hostname Router2

! LAN Pengawas Cabang
interface FastEthernet0/1
 ip address 10.47.3.225 255.255.255.224
 no shutdown
exit

! --- Serial link ke Router1 (pastikan sisi R1 sudah 10.47.4.9 dan diberi clock rate)
interface Serial0/2/0
 description Link-to-Router1
 ip address 10.47.4.10 255.255.255.252
 no shutdown
exit

! --- LAN Pengawas Cabang ke Switch7
interface GigabitEthernet0/0
 description To-SW7-PengawasCabang
 ip address 10.47.3.225 255.255.255.224
 no shutdown
exit

! --- optional: jika ada interface gigabit lain jangan pakai sekarang
! --- Tambah routing statik kembali ke pusat (agregat /21)
ip route 10.47.0.0 255.255.248.0 10.47.4.9

end
write memory
```

**Switch Core**
```
enable
configure terminal
hostname SW-Core

! ==== VLAN Definition ====
vlan 10
 name Sekretariat
vlan 20
 name Kurikulum
vlan 30
 name GuruTendik
vlan 40
 name Sarpras
vlan 50
 name PengawasPusat
vlan 60
 name ServerAdmin
exit

! ==== Trunk ke Router1 ====
interface FastEthernet0/1
 description To-Router1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50,60
 no shutdown
exit

! ==== Access ke masing-masing switch ====
interface FastEthernet0/2
 description To-SW1-Sekretariat
 switchport mode access
 switchport access vlan 10
 no shutdown
exit

interface FastEthernet0/3
 description To-SW2-Kurikulum
 switchport mode access
 switchport access vlan 20
 no shutdown
exit

interface FastEthernet0/4
 description To-SW3-GuruTendik
 switchport mode access
 switchport access vlan 30
 no shutdown
exit

interface FastEthernet0/5
 description To-SW4-Sarpras
 switchport mode access
 switchport access vlan 40
 no shutdown
exit

interface FastEthernet0/6
 description To-SW5-PengawasPusat
 switchport mode access
 switchport access vlan 50
 no shutdown
exit

interface FastEthernet0/7
 description To-SW6-ServerAdmin
 switchport mode access
 switchport access vlan 60
 no shutdown
exit

end
write memory
```

**Switch 1**
```
enable
configure terminal
hostname SW-Sekretariat

! Hubungan ke Core
interface FastEthernet0/1
 switchport mode access
 switchport access vlan 10
 no shutdown
exit

! Hubungan ke PC
interface FastEthernet0/2
 switchport mode access
 switchport access vlan 10
 no shutdown
exit

end
write memory
```

**Switch 2**
```
enable
configure terminal
hostname SW-Kurikulum

interface FastEthernet0/1
 switchport mode access
 switchport access vlan 20
 no shutdown
exit
interface FastEthernet0/2
 switchport mode access
 switchport access vlan 20
 no shutdown
exit
end
write memory
```

**Switch 3**
```
enable
configure terminal
hostname SW-GuruTendik

interface FastEthernet0/1
 switchport mode access
 switchport access vlan 30
 no shutdown
exit
interface FastEthernet0/2
 switchport mode access
 switchport access vlan 30
 no shutdown
exit
end
write memory
```

**Switch 4**
```
enable
configure terminal
hostname SW-Sarpras

interface FastEthernet0/1
 switchport mode access
 switchport access vlan 40
 no shutdown
exit
interface FastEthernet0/2
 switchport mode access
 switchport access vlan 40
 no shutdown
exit
end
write memory
```

**Switch 5**
```
enable
configure terminal
hostname SW-PengawasPusat

interface FastEthernet0/1
 switchport mode access
 switchport access vlan 50
 no shutdown
exit
interface FastEthernet0/2
 switchport mode access
 switchport access vlan 50
 no shutdown
exit
end
write memory
```

**Switch 6**
```

```

---

## **IP Unit**

| Unit                | Device      | IP Address    | Subnet Mask       | Default Gateway |
| :------------------ | :---------- | :------------ | :---------------- | :-------------- |
| **Sekretariat**     | PC Sekre    | `10.47.0.2`   | `255.255.254.0`   | `10.47.0.1`     |
| **Kurikulum**       | PC Kur      | `10.47.2.2`   | `255.255.255.0`   | `10.47.2.1`     |
| **Guru & Tendik**   | PC Guru     | `10.47.3.2`   | `255.255.255.128` | `10.47.3.1`     |
| **Sarpras**         | PC Sarpras  | `10.47.3.130` | `255.255.255.192` | `10.47.3.129`   |
| **Pengawas Pusat**  | PC Pengawas | `10.47.3.194` | `255.255.255.224` | `10.47.3.193`   |
| **Server & Admin**  | Server      | `10.47.4.2`   | `255.255.255.248` | `10.47.4.1`     |
| **Pengawas Cabang** | PC Cabang   | `10.47.3.226` | `255.255.255.224` | `10.47.3.225`   |

---

## Hasil akhir

**PC Sekretariat**

<img width="1230" height="1066" alt="image" src="https://github.com/user-attachments/assets/a05cf4af-3191-4deb-9060-f790d751175a" />

- `ping 10.47.0.1`    (ke router1 gateway)
- `ping 10.47.4.2`    (ke server)
- `ping 10.47.3.226`  (ke PC cabang)

**PC Pengawas Cabang**
