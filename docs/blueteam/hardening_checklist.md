# Hardening Checklist — Target Node BiliCheck (`192.168.11.101`)


| ID | Kategori | Kontrol | Target layanan/file | Status sementara | Bukti |
|---|---|---|---|---|---|
| A1 | Access & Authentication | Admin memakai akun non-root | Akun Ubuntu, `sudo` | Selesai | [Sebelum](evidence/A1_before.png) · [Sesudah](evidence/A1_after.png) |
| A2 | Access & Authentication | SSH key; login password dimatikan setelah key teruji | SSH | Belum | [Sebelum](evidence/A2_before.png) · [Sesudah](evidence/A2_after.png) |
| A3 | Access & Authentication | Fail2ban untuk percobaan SSH berulang | SSH, Fail2ban | Belum | [Sebelum](evidence/A3_before.png) · [Sesudah](evidence/A3_after.png) |
| A4 | Access & Authentication | Login SSH langsung sebagai root dimatikan | SSH | Belum | [Sebelum](evidence/A4_before.png) · [Sesudah](evidence/A4_after.png) |
| B1 | Service & Attack Surface | UFW default deny; buka hanya port SSH yang dipakai | UFW | Sebagian | [Sebelum](evidence/B1_before.png) · [Sesudah](evidence/B1_after.png) |
| B2 | Service & Attack Surface | Firestore Emulator dan UI hanya bind ke `127.0.0.1` | Firestore Emulator | Belum | [Sebelum](evidence/B2_before.png) · [Sesudah](evidence/B2_after.png) |
| B3 | Service & Attack Surface | Matikan layanan yang tidak dipakai | Layanan Ubuntu | Sebagian | [Sebelum](evidence/B3_before.png) · [Sesudah](evidence/B3_after.png) |
| B4 | Service & Attack Surface | Perbarui Ubuntu, Node.js, dan dependensi | OS dan paket Node.js | Sebagian | [Sebelum](evidence/B4_before.png) · [Sesudah](evidence/B4_after.png) |
| C1 | Data & Application | Jalankan ekspor sebagai akun `bilicheck` tanpa hak admin | Proses ekspor | Belum | [Sebelum](evidence/C1_before.png) · [Sesudah](evidence/C1_after.png) |
| C2 | Data & Application | Folder backup `700`, file CSV `600` | Backup CSV | Belum | [Sebelum](evidence/C2_before.png) · [Sesudah](evidence/C2_after.png) |
| C3 | Data & Application | Cegah nilai Firestore menjadi formula saat CSV dibuka | `export_csv.js` | Belum | [Sebelum](evidence/C3_before.png) · [Sesudah](evidence/C3_after.png) |
| C4 | Data & Application | Catat kegagalan ekspor dan percobaan akses file | Log ekspor, audit Ubuntu | Belum | [Sebelum](evidence/C4_before.png) · [Sesudah](evidence/C4_after.png) |
