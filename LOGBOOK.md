# LOGBOOK — Kelompok 11 (TEK1314 Keamanan Siber)

**Skenario Proyek:** Simulasi serangan web server (SQL Injection & XSS) — Attacker Kali Linux vs Target Ubuntu Server, dipantau Security Onion.

---

## Minggu 3 — Design Phase
- Merancang topologi logis (Attacker Node, Target Node, Monitoring Node).
- Menyusun skema IP Address: subnet `192.168.11.0/24`.
- Menentukan OS Target: Ubuntu Server dengan web app rentan (rekomendasi DVWA untuk demonstrasi SQLi/XSS).

## Minggu 5
- Instalasi dan konfigurasi Security Onion sebagai Monitoring Node (`192.168.11.200`).
- Verifikasi logging: pengujian ICMP dari Attacker ke Target, dikonfirmasi tercatat di dashboard Sguil/Squert.

## Minggu 6
- Hardening Target Node (Ubuntu Server):
  - Konfigurasi firewall UFW (buka port 22, 80, 443).
  - Menonaktifkan service yang tidak diperlukan.
  - Pembuatan user non-root (`analyst`) untuk administrasi.
  - Update security patch sistem.
- Penetapan hostname standar: `SRV-WEB-KEL11`.

## Minggu 7
- Finalisasi Baseline Report (`docs/phase-1-baseline/baseline-report.md`).
- Persiapan demo progres: topologi review, hardening walkthrough, logging verification live.
