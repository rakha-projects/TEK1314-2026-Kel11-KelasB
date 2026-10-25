# LOGBOOK — Kelompok 11 (TEK1314 Keamanan Siber)

**Skenario Proyek:** SOC Engagement — mengamankan VPS backend BiliCheck/BILINOVA (Node.js export script + Firestore Emulator) sebagai Target Node, diuji oleh Attacker Node (Kali Linux), dipantau Monitoring Node (Security Onion).

---

## Minggu 3 — Design Phase
- Merancang topologi logis (Attacker Node, Target Node, Monitoring Node).
- Menyusun skema IP Address: subnet `192.168.11.0/24`.
- Menentukan OS Target: Ubuntu Server, direncanakan sebagai replika VPS backend BiliCheck (Node.js export script + Firestore Emulator).

## Minggu 5
- Instalasi dan konfigurasi Security Onion sebagai Monitoring Node (`192.168.11.200`).
- Verifikasi logging: pengujian ICMP dari Attacker ke Target, dikonfirmasi tercatat di dashboard Sguil/Squert.

## Minggu 6
- Hardening Target Node (Ubuntu Server):
  - Konfigurasi firewall UFW.
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
- Finalisasi Deklarasi Tech Stack (`docs/presentation-minggu9/tech_stack_declaration.md`): memetakan backend self-hosted BiliCheck (VPS Node.js + Firestore Emulator + CSV backup) ke Target Node replika; VPS asli bersifat headless (tanpa dashboard), sehingga tidak ada komponen dashboard yang direplikasi.
- Menyusun checklist hardening (`docs/blueteam/hardening_checklist.md`), 12 kontrol lintas kategori A/B/C, termasuk pembatasan Firestore Emulator hanya bind ke `127.0.0.1`.
- Menyusun Attack Plan Fase 2 (`docs/redteam/attack_plan.md`): 3 skenario (Reconnaissance, Exploitation/Akses, formula injection pada ekspor CSV) beserta catatan jalur deteksi masing-masing — S1/S2 terdeteksi sebagai NIDS alert di Security Onion, S3 memerlukan deteksi berbasis log aplikasi/host karena dieksekusi lewat sesi SSH yang sah.
- Review arah proyek: skenario web app rentan (DVWA, SQLi/XSS) yang dipakai Minggu 3–7 digantikan dengan replika VPS BiliCheck yang lebih sesuai tech stack asli (Node.js + Firestore, tanpa dashboard web).
- Memperbaiki `baseline-report.md` dan `README.md` agar konsisten dengan skenario baru.
- Persiapan slide presentasi checkpoint Minggu ke-9.