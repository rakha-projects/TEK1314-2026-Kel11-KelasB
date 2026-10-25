# Hardening Checklist — Target Node BiliCheck (`192.168.11.101`)


| ID | Kategori | Kontrol | Target layanan/file | Status | Bukti |
|---|---|---|---|---|---|
| A1 | Access & Authentication | Nonaktifkan login SSH langsung sebagai root | SSH (`/etc/ssh/sshd_config`) | Sudah | [Sebelum](evidence/A1_before.png) · [Sesudah](evidence/A1_after.png) |
| A2 | Access & Authentication | Ubah port standar SSH (`22` → `2222`) | SSH (`sshd_config`, `ssh.socket`) | Sudah | [Sebelum](evidence/A2_before.png) · [Sesudah](evidence/A2_after.png) |
| A3 | Access & Authentication | Fail2ban untuk percobaan SSH berulang | SSH, Fail2ban | Sudah | [Sebelum](evidence/A3_before.png) · [Sesudah](evidence/A3_after.png) |
| B1 | Service & Attack Surface | UFW default deny; buka hanya port SSH yang dipakai | UFW | Sudah | [Sebelum](evidence/B1_before.png) · [Sesudah](evidence/B1_after.png) |
| B2 | Service & Attack Surface | Firestore Emulator dan UI hanya bind ke `127.0.0.1` | Firestore Emulator | Sudah | [Sebelum](evidence/B2_before.png) · [Sesudah](evidence/B2_after.png) |
| B3 | Service & Attack Surface | Matikan layanan yang tidak dipakai | Layanan Ubuntu | Sudah | [Sebelum](evidence/B3_before.png) · [Sesudah](evidence/B3_after.png) |
| B4 | Service & Attack Surface | Perbarui Ubuntu, Node.js, dan dependensi | OS dan paket Node.js | SUdah | [Sebelum](evidence/B4_before.png) · [Sesudah](evidence/B4_after.png) |
| C1 | Data & Application | Jalankan ekspor sebagai akun `bilicheck` tanpa hak admin | Proses ekspor | Sudah | [C1](evidence/C1.png) |
| C2 | Data & Application | Folder backup `700`, file CSV `600` | Backup CSV | Sudah | [C2](evidence/C2.png) |
| C3 | Data & Application | Cegah nilai Firestore menjadi formula saat CSV dibuka | `export_csv.js` | Sudah | [C3](evidence/C3.png) |
| C4 | Data & Application | Catat kegagalan ekspor dan percobaan akses file | Log ekspor, audit Ubuntu | Sudah | [C4](evidence/C4.png) |
