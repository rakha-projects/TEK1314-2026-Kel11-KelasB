# LOGBOOK — Kelompok 11 (TEK1314 Keamanan Siber)

**Skenario Proyek:** Simulasi serangan web server (SQL Injection & XSS) — Attacker Kali Linux vs Target Ubuntu Server, dipantau Security Onion. Target Node mereplikasi komponen backend self-hosted dari proyek IoT BiliCheck (VPS relay/ekspor).

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

## Minggu 8 — UTS Praktikum
- Tidak ada aktivitas proyek PBL (jadwal UTS).

## Minggu 9 — Case Study & Checkpoint
- Menyusun Deklarasi Tech Stack (`docs/presentation-minggu9/tech_stack_declaration.md`): memetakan backend self-hosted proyek IoT BiliCheck (VPS relay/ekspor: Ubuntu + HTTP + penyimpanan terstruktur) ke Target Node replika (DVWA untuk permukaan serangan web + komponen Flask tambahan untuk lapisan data/aplikasi).
- Menambahkan komponen replika VPS relay/ekspor berbasis Flask (`app/relay-export/`), terpisah dari DVWA, untuk memenuhi kontrol hardening kategori Data & Application.
- Menyusun checklist hardening terstruktur (`docs/blueteam/hardening_checklist.md`), 9 kontrol lintas kategori A/B/C.
- Menyusun Attack Plan Fase 2 (`docs/redteam/attack_plan.md`): 3 skenario lintas kategori (Reconnaissance, Exploitation/Akses, Web/API/Protokol IoT).
- Memperbaiki `baseline-report.md`: melengkapi daftar service yang dinonaktifkan, memperbaiki inkonsistensi IP target pada bagian Logging Verification.
- Persiapan slide presentasi checkpoint Minggu ke-9 (maks. 6–8 slide sesuai Bagian IV Panduan PBL).
