# Baseline Report — Kelompok 11 (Fase 1: Hardening)

**Mata Kuliah:** TEK1314 - Keamanan Siber
**Skenario:** Simulasi serangan web server (SQL Injection & XSS)
**Minggu:** 7 (Demo Progres — Hardening Review)

---

## 1. Topologi Jaringan

*(Sisipkan screenshot/gambar `topology.png` di sini)*

Topologi terdiri dari 3 entitas utama dalam satu subnet `192.168.11.0/24`, terhubung lewat Switch ke Router (gateway `192.168.11.1`):

- **Attacker Node** (Kali Linux) — `192.168.11.100`
- **Target Node** (Ubuntu Server, web app rentan SQLi/XSS) — `192.168.11.5`
- **Monitoring Node** (Security Onion) — `192.168.11.200`, terhubung via mirror port pada switch untuk memantau seluruh segmen jaringan.

---

## 2. Identitas Sistem

| Node | Hostname | IP Address | OS |
| --- | --- | --- | --- |
| Target | SRV-WEB-KEL11 | 192.168.11.5 | Ubuntu Server |
| Attacker | *(isi hostname)* | 192.168.11.100 | Kali Linux |
| Monitoring | *(isi hostname)* | 192.168.11.200 | Security Onion |

Verifikasi identitas dilakukan dengan:
```bash
hostnamectl
ip a
```
<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/b79dcc9e-282d-4bab-86e7-1b52acf36cea" />


---

## 3. Network Hardening

Firewall (UFW) dikonfigurasi pada Target Node dengan kebijakan default **deny incoming**, hanya membuka port yang diperlukan untuk operasional web server:

| Port | Layanan | Alasan Dibuka |
| --- | --- | --- |
| 22/tcp | SSH | Akses administrasi jarak jauh |
| 80/tcp | HTTP | Layanan web server utama |
| 443/tcp | HTTPS | Layanan web server terenkripsi |

Konfigurasi diverifikasi dengan:
```bash
sudo ufw status verbose
```
<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/11d9695b-9218-4360-b7ce-abd2341089e6" />


---

## 4. System Hardening

- **Penonaktifan service tidak perlu:** *(sebutkan service apa saja yang di-disable, misal: bluetooth, cups, avahi-daemon)*
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
   ping -c 5 192.168.11.5
   ```
2. Dashboard **Sguil/Squert** di Security Onion menampilkan event dengan:
   - Timestamp: *(isi)*
   - IP asal: `192.168.11.100`
   - IP tujuan: `192.168.11.5`

*(Sisipkan screenshot dashboard Sguil/Squert di sini)*

---

## 6. Kesimpulan Hardening

Berdasarkan hasil di atas, sistem Target Node (SRV-WEB-KEL11) telah diperkuat sebelum memasuki fase simulasi serangan: firewall aktif membatasi akses hanya pada port yang diperlukan, service yang tidak digunakan telah dinonaktifkan, akses administrasi menggunakan user non-root, dan Security Onion telah terverifikasi mampu merekam aktivitas jaringan secara real-time. Sistem dinyatakan siap untuk memasuki Fase 2 (Vulnerability Assessment).
