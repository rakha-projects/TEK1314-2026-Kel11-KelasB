# Hardening Checklist — Target Node (SRV-WEB-KEL11, 192.168.11.101)

Status per kontrol: **Selesai** / **Sebagian** / **Belum**. Bukti before/after disimpan di `docs/blueteam/evidence/`.

## A. Access & Authentication

| # | Kontrol | Status | Bukti |
|---|---|---|---|
| A1 | User non-root (`analyst`, akses via `sudo`) untuk administrasi | Selesai | Screenshot `whoami` + `sudo -l` (sudah ada di baseline report) |
| A2 | SSH key-based authentication, `PasswordAuthentication no` di `sshd_config` | Belum — rencana sebelum demo | Screenshot `sshd_config` before/after + percobaan login password ditolak |

## B. Service & Attack Surface

| # | Kontrol | Status | Bukti |
|---|---|---|---|
| B1 | UFW default deny incoming, whitelist port 22/80/443 | Selesai | `sudo ufw status verbose` (sudah ada di baseline report) |
| B2 | Nonaktifkan service tidak dipakai (isi nama service aktual, mis. `bluetooth`, `cups`, `avahi-daemon`) | Sebagian — daftar service belum dikonfirmasi di baseline report, perlu dilengkapi | `systemctl list-unit-files --state=enabled` before/after |
| B3 | Update & patch OS (`apt update && apt upgrade`) | Selesai | Screenshot output upgrade (sudah ada di baseline report) |

## C. Data & Application

> Diterapkan pada script relay/ekspor (replika fungsi VPS BiliCheck) — bukan pada DVWA, yang sengaja dibiarkan *vulnerable* sebagai target Red Team.

| # | Kontrol | Status | Bukti |
|---|---|---|---|
| C1 | Kredensial database (MySQL) untuk script ekspor disimpan di `.env`, tidak hardcode di source | Belum | `app/relay-export/.env.example` + pemanggilan `load_dotenv()` di `app.py` |
| C2 | User MySQL `relay_user` khusus untuk script ekspor dengan least-privilege (bukan `root`) | Belum | `SHOW GRANTS FOR 'relay_user'@'localhost';` |
| C3 | Validasi input pada endpoint Flask `/pemeriksaan` (bukan form DVWA) | Belum | Blok validasi `pasien_id`/`hasil_bilirubin` di `app/relay-export/app.py` |
| C4 | Logging aktivitas mencurigakan (percobaan login gagal berulang, dsb.), terhubung ke Security Onion | Sebagian — Security Onion sudah memverifikasi capture traffic ICMP (Minggu 5), log aplikasi spesifik belum ditambahkan | Grep log + screenshot alert Security Onion |

**Ringkasan:** 2 kontrol kategori A, 3 kategori B, 4 kategori C — total 9 kontrol, memenuhi minimum 8 kontrol lintas 3 kategori (≥2 per kategori) sesuai Bagian VIII.

**TODO sebelum presentasi Minggu ke-9:** selesaikan A2 dan isi status B2 dengan daftar service aktual; C1–C4 cukup didemonstrasikan sebagai rencana/progres awal karena penilaian Minggu ke-9 berfokus pada kejelasan rencana, bukan eksekusi penuh (lihat Bagian VII Panduan).
