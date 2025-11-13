# Tugas-1-Jarkom_Revalina-Erica-P_007

## Visualisasi
<img width="957" height="584" alt="image" src="https://github.com/user-attachments/assets/a8a3a9b5-355a-4142-8cf0-d8e8ec0dce78" />

## Kofigurasi Router
**R1**
```
enable
configure terminal
hostname Router1

! LAN Guru & Tendik
interface FastEthernet0/3/0
 description To-SW3-GuruTendik
 ip address 10.47.3.1 255.255.255.128
 no shutdown
exit

! LAN Sarpras
interface FastEthernet0/3/1
 description To-SW4-Sarpras
 ip address 10.47.3.129 255.255.255.192
 no shutdown
exit

! LAN Pengawas Pusat
interface FastEthernet0/3/2
 description To-SW5-PengawasPusat
 ip address 10.47.3.193 255.255.255.224
 no shutdown
exit

! LAN Server & Admin
interface FastEthernet0/3/3
 description To-SW6-ServerAdmin
 ip address 10.47.4.1 255.255.255.248
 no shutdown
exit

! Serial Link ke Router2
interface Serial0/2/0
 description To-Router2
 ip address 10.47.4.9 255.255.255.252
 clock rate 64000
 no shutdown
exit

! Routing statik ke cabang
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

---

## **IP PC**

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

