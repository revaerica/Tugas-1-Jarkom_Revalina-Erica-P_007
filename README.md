# Tugas-1-Jarkom_Revalina-Erica-P_007

## Visualisasi

<img width="1358" height="597" alt="image" src="https://github.com/user-attachments/assets/7d716920-afa3-4761-a670-0bbac02a84ca" />

## Kofigurasi Router

**Route 1 (Route Pusat)**
```
enable
conf t
hostname Router1

! --- Link ke Router2 (Cabang)
interface serial0/2/0
 ip address 10.47.4.9 255.255.255.252
 clock rate 64000
 no shutdown

! --- Link ke Switch Core
interface gigabitEthernet0/0
 ip address 10.47.5.1 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
no network 10.0.0.0
 network 10.47.4.8
 network 10.47.5.0
 network 10.47.0.0
 network 10.47.2.0
 network 10.47.3.0
 network 10.47.4.0
end
write memory
```

**Route 2 (Route Cabang)**
```
enable
conf t
hostname Router2

interface gigabitEthernet0/0
 ip address 10.47.3.225 255.255.255.224
 no shutdown

interface serial0/2/0
 ip address 10.47.4.10 255.255.255.252
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.47.3.224
 network 10.47.4.8
end
write memory
```

**Route 0 (Sekretariat)**
```
enable
conf t
hostname Router0

interface gigabitEthernet0/0
 ip address 10.47.0.1 255.255.254.0
 no shutdown

interface gigabitEthernet0/1
 ip address 10.47.5.2 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.47.0.0
 network 10.47.5.0
end
write memory
```

**Route 3 (Kurikulum)**
```
enable
conf t
hostname Router3

interface gigabitEthernet0/0
 ip address 10.47.2.1 255.255.255.0
 no shutdown

interface gigabitEthernet0/1
 ip address 10.47.5.3 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.47.2.0
 network 10.47.5.0
end
write memory
```

**Route 4 (Guru & Tendik)**
```
enable
conf t
hostname Router4

interface gigabitEthernet0/0
 ip address 10.47.3.1 255.255.255.128
 no shutdown

interface gigabitEthernet0/1
 ip address 10.47.5.4 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.47.3.0
 network 10.47.5.0
end
write memory
```

**Route 5 (SarPras)**
```
enable
conf t
hostname Router5

interface gigabitEthernet0/0
 ip address 10.47.3.129 255.255.255.192
 no shutdown

interface gigabitEthernet0/1
 ip address 10.47.5.5 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.47.3.128
 network 10.47.5.0
end
write memory
```

**Route 6 (Pengawas Pusat)**
```
enable
conf t
hostname Router6

interface gigabitEthernet0/0
 ip address 10.47.3.193 255.255.255.224
 no shutdown

interface gigabitEthernet0/1
 ip address 10.47.5.6 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.47.3.192
 network 10.47.5.0
end
write memory
```

**Route 7 (Server & Admin)**
```
enable
conf t
hostname Router7

interface gigabitEthernet0/0
 ip address 10.47.4.1 255.255.255.248
 no shutdown

interface gigabitEthernet0/1
 ip address 10.47.5.7 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.47.4.0
 network 10.47.5.0
end
write memory
```

**Switch Core**
```
enable
conf t
hostname Switch-Core

interface range fa0/1 - 8
 description CONNECT-TO-ROUTERS
 switchport mode access
 switchport access vlan 1
 no shutdown
exit

interface range fa0/9 - 24
 description CONNECT-TO-ACCESS-SWITCHES
 switchport mode trunk
 no shutdown
exit

interface vlan 1
 ip address 10.47.5.100 255.255.255.0
 no shutdown
exit

end
write memory
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

<img width="1230" height="505" alt="Screenshot 2025-11-13 074326" src="https://github.com/user-attachments/assets/88aaa3fc-9f17-4afb-9c8b-6139daa6dd4e" />

**PC Pengawas Cabang**

<img width="1302" height="722" alt="image" src="https://github.com/user-attachments/assets/52392df4-fb24-492b-a201-d99c9ba2adae" />
