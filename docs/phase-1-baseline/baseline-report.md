# Baseline Report — Kelompok 11 (Fase 1: Hardening)

## 1. Topologi Jaringan
[Embed/gambarkan ulang topologi: Attacker–Switch–Router–Target, Monitoring via mirror port]

## 2. Identitas Sistem
| Node | Hostname | IP | OS |
|---|---|---|---|
| Target | SRV-WEB-KEL11 | 192.168.11.5 | Ubuntu Server |
| Attacker | (isi) | 192.168.11.100 | Kali Linux |
| Monitoring | (isi) | 192.168.11.200 | Security Onion |

## 3. Network Hardening
[Screenshot `ufw status verbose`, jelaskan port yang dibuka dan alasannya]

## 4. System Hardening
[Screenshot service yang di-disable, bukti user non-root, bukti apt upgrade]

## 5. Logging Verification
[Screenshot Sguil/Squert menampilkan event ICMP dari attacker ke target]

## 6. Kesimpulan Hardening
[Ringkasan: sistem sudah siap diserang di fase berikutnya, karena firewall aktif, service dibatasi, dan monitoring bekerja]