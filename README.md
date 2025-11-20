# Tugas-1-Jarkom_Revalina-Erica-P_007

## Visualisasi

<img width="1472" height="885" alt="image" src="https://github.com/user-attachments/assets/37a3e4d8-563a-4433-a7ac-fc4ac0c92378" />

## Konfigurasi Route

**Route 0 (Pusat)**
```
enable
conf t

interface fa0/0
 ip address 10.47.255.1 255.255.255.0
 no shutdown

interface se2/0
 ip address 10.47.4.9 255.255.255.252
 clock rate 64000
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.0.0.0

end
write
```

**Route 1**
```
enable
conf t

! LAN Sekretariat
interface FastEthernet0/0
 ip address 10.47.0.1 255.255.254.0
 no shutdown

! Ke Switch Backbone
interface FastEthernet1/0
 ip address 10.47.255.11 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.0.0.0

end
write
```

**Route 2**
```
enable
conf t

interface FastEthernet0/0
 ip address 10.47.2.1 255.255.255.0
 no shutdown

interface FastEthernet1/0
 ip address 10.47.255.12 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.0.0.0

end
write
```

**Route 3**
```
enable
conf t

interface FastEthernet0/0
 ip address 10.47.3.1 255.255.255.128
 no shutdown

interface FastEthernet1/0
 ip address 10.47.255.13 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.0.0.0

end
write
```

**Route 4**
```
enable
conf t

interface FastEthernet0/0
 ip address 10.47.3.129 255.255.255.192
 no shutdown

interface FastEthernet1/0
 ip address 10.47.255.14 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.0.0.0

end
write
```

**Route 5**
```
enable
conf t

interface FastEthernet0/0
 ip address 10.47.3.193 255.255.255.224
 no shutdown

interface FastEthernet1/0
 ip address 10.47.255.15 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.0.0.0

end
write
```

**Route 6**
```
enable
conf t

interface FastEthernet0/0
 ip address 10.47.4.1 255.255.255.248
 no shutdown

interface FastEthernet1/0
 ip address 10.47.255.16 255.255.255.0
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.0.0.0

end
write
```

**Route 7**
```
enable
conf t

interface FastEthernet0/0
 ip address 10.47.3.225 255.255.255.224
 no shutdown

interface FastEthernet1/0
 ip address 10.47.255.17 255.255.255.0
 no shutdown

interface Serial2/0
 ip address 10.47.4.10 255.255.255.252
 no shutdown

router rip
 version 2
 no auto-summary
 network 10.0.0.0

end
write
```

**Switch 0**
```
enable
conf t
interface range fa0/1 - 24
 no shutdown
end
write
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
