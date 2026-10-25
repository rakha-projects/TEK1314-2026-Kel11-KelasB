# Baseline Report — Kelompok 11 (Fase 1: Hardening)

**Mata Kuliah:** TEK1314 - Keamanan Siber
**Skenario:** SOC Engagement — replika VPS backend BiliCheck (Node.js export script + Firestore Emulator)
**Minggu:** 7 (Demo Progres — Hardening Review)

---

## 1. Topologi Jaringan

<img width="424" height="343" alt="image" src="https://github.com/user-attachments/assets/5e99c375-b2be-49ce-afd1-476679236789" />

Topologi terdiri dari 3 entitas utama dalam satu subnet `192.168.11.0/24`

- **Attacker Node** (Kali Linux) — `192.168.11.100`
- **Target Node** (Ubuntu Server, replika VPS BiliCheck: Node.js export script + Firestore Emulator) — `192.168.11.101`
- **Monitoring Node** (Security Onion) — `192.168.11.200`

---

## 2. Identitas Sistem

| Node | Hostname | IP Address | OS |
| --- | --- | --- | --- |
| Target | SRV-WEB-KEL11 | 192.168.11.101 | Ubuntu Server |
| Attacker | Attacker-KEL11 | 192.168.11.100 | Kali Linux |
| Monitoring | Defender-KEL11 | 192.168.11.200 | Security Onion |

Verifikasi identitas dilakukan dengan:
```bash
hostnamectl
ip a
```
<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/b79dcc9e-282d-4bab-86e7-1b52acf36cea" />

---

## 3. Network Hardening

Firewall (UFW) dikonfigurasi pada Target Node dengan kebijakan default **deny incoming**. Karena VPS BiliCheck asli bersifat headless (tanpa dashboard/API HTTP masuk), hanya SSH yang perlu dibuka dari luar; Firestore Emulator hanya bind ke `127.0.0.1` (lihat `docs/blueteam/hardening_checklist.md` kontrol B2), bukan port yang diizinkan UFW dari luar:

| Port | Layanan | Alasan Dibuka |
| --- | --- | --- |
| 22/tcp | SSH | Akses administrasi jarak jauh |

Konfigurasi diverifikasi dengan:
```bash
sudo ufw status verbose
```
<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/11d9695b-9218-4360-b7ce-abd2341089e6" />

---

## 4. System Hardening

- **Penonaktifan service tidak perlu:** dicek dengan `systemctl list-unit-files --type=service --state=enabled`, lalu dinonaktifkan jika ditemukan: `avahi-daemon`, `cups`, `bluetooth`, `ModemManager`, `motd-news.timer`/`apt-news.timer`. *(Sesuaikan dengan hasil aktual di VM kalian.)*
- **User non-root:** dibuat user `analyst` dengan hak akses sudo, bukan login langsung sebagai root.
- **Update security patch:**
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/04be2e3c-59ea-41cf-be86-287aeea0ee1d" />

<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/fc9da532-d6a8-4318-a5f8-53b014601473" />

---

## 5. Logging Verification

Bukti bahwa Security Onion aktif merekam traffic jaringan:

1. Traffic ICMP di-generate dari Attacker Node ke Target Node:
   ```bash
   ping -c 5 192.168.11.101
   ```
2. Dashboard **Sguil/Squert** di Security Onion menampilkan event dengan:
   - Timestamp: *(isi sesuai screenshot kalian)*
   - IP asal: `192.168.11.100`
   - IP tujuan: `192.168.11.101`

<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/abb04f8e-90ce-4c22-9e03-0801270f906e" />
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/d951a10c-ddf3-4809-b3be-6ab36c422ed6" />

---

## 6. Kesimpulan Hardening

Berdasarkan hasil di atas, sistem Target Node (SRV-WEB-KEL11) telah diperkuat sebelum memasuki fase simulasi serangan: firewall aktif hanya membuka SSH dari luar, Firestore Emulator dibatasi ke `localhost`, service yang tidak digunakan telah dinonaktifkan, akses administrasi menggunakan user non-root, dan Security Onion telah terverifikasi mampu merekam aktivitas jaringan secara real-time. Sistem dinyatakan siap untuk memasuki Fase 2 (Vulnerability Assessment).

**Catatan Minggu ke-9:** hardening kategori Data & Application (akun proses ekspor tanpa hak admin, permission file backup, pencegahan formula injection pada CSV, logging kegagalan ekspor) didetailkan di `docs/blueteam/hardening_checklist.md`. Skenario serangan terkait ada di `docs/redteam/attack_plan.md`, termasuk catatan bahwa skenario formula injection (S3) terdeteksi lewat log aplikasi/host, bukan NIDS Security Onion.