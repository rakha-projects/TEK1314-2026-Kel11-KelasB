# Attack Plan — Fase 2 (Kelompok 11)

Target: `SRV-WEB-KEL11` (`192.168.11.101`). Dasar riset: `docs/Design/ip_plan.md` (Minggu ke-4).

## Skenario 1 — Reconnaissance

- **Teknik:** Port & service scanning, OS fingerprinting, banner grabbing
- **Tools:** `nmap -sV -O -p- 192.168.11.101`, Nikto (web recon tambahan)
- **Target:** seluruh port terbuka pada Target Node (fokus 22, 80, 443, 3306 sesuai temuan `ip_plan.md`)
- **Hasil diharapkan:** daftar port terbuka & versi service terkonfirmasi, jadi dasar validasi Skenario 2 dan 3; dibandingkan before/after hardening untuk bukti B2 di `hardening_checklist.md`

## Skenario 2 — Exploitation / Akses

- **Teknik:** Brute-force credential SSH
- **Tools:** Hydra (`hydra -l analyst -P wordlist.txt ssh://192.168.11.101`)
- **Target:** port 22/tcp, akun `analyst`
- **Hasil diharapkan:** sebelum kontrol A2 (SSH key-based auth) diterapkan, brute-force berpotensi berhasil; setelah diterapkan, percobaan harus gagal — jadi bukti verifikasi Purple Team Loop tahap 5

## Skenario 3 — Web/API/Protokol IoT

- **Teknik:** SQL Injection & XSS (stored/reflected) pada DVWA
- **Tools:** sqlmap, Burp Suite/OWASP ZAP, manual payload testing
- **Target:** form input DVWA pada port 80/443
- **Hasil diharapkan:** ekstraksi data via SQLi, eksekusi script via XSS; dicocokkan dengan deteksi Security Onion dan kontrol kategori C (validasi input) pada komponen replika VPS

**Catatan kategori:** 3 skenario di atas mencakup 3 kategori berbeda (Reconnaissance, Exploitation/Akses, Web/API/Protokol IoT) — memenuhi minimum 2 kategori berbeda sesuai Bagian IX. Tidak menyertakan skenario Availability/DoS.

**Rencana Purple Team Loop (Fase 2, s.d. Minggu ke-11):** setiap skenario di atas akan dijalankan mengikuti 5 tahap Bagian X (Serang → Deteksi → Analisis → Respons/Mitigasi → Verifikasi), dicatat di `docs/purple-team-log.md`.
