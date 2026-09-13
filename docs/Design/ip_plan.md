# IP Plan — Kelompok 11 (TEK1314 Keamanan Siber)

**Subnet Kelompok:** `192.168.11.0/24`

| Hostname | IP Address | OS Direncanakan |
| --- | --- | --- |
| Target Server (Korban) | 192.168.11.5 | Ubuntu Server |
| Attacker Node | 192.168.11.100 | Kali Linux |
| Monitoring Node | 192.168.11.200 | Security Onion |
| Gateway/Router | 192.168.11.1 | Router-PT (Cisco Packet Tracer) |

**Subnet Mask:** `255.255.255.0`

## Catatan Port & Potensi Celah (Riset Red Team — Skenario Web Server)

Target Server (192.168.11.5) direncanakan menjalankan web server dengan celah web-based (SQL Injection, XSS). Port yang berpotensi dibuka/dieksploitasi:

| Port | Layanan | Potensi Celah |
| --- | --- | --- |
| 80 | HTTP | SQL Injection pada form input, XSS (stored/reflected) |
| 443 | HTTPS | Sama seperti port 80, plus kemungkinan misconfigured SSL/TLS |
| 22 | SSH | Brute-force credential jika akses admin dibutuhkan untuk skenario tambahan |
| 3306 | MySQL | Terbuka jika database menjadi backend web app — rentan jika password default/lemah |

