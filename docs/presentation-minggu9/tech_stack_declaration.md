# Deklarasi Tech Stack — Kelompok 11 (BiliCheck)

| Komponen | Teknologi pada Proyek IoT Asli | Direplikasi sebagai (Target Node) |
|---|---|---|
| Sistem operasi backend | Firebase (backend cloud) dan Ubuntu Server 24.04 (AWS EC2) | Ubuntu Server 24.04 (VM lab) |
| Database/penyimpanan data | Firebase Firestore dan RTDB; CSV di VPS | Firestore Emulator dan CSV lokal |
| Protokol komunikasi sensor | ESP32 → Firebase Auth/RTDB (HTTPS/REST dan SSE) | HTTP REST (data dummy → Firestore Emulator) |
| Dashboard/monitoring | Tidak ada di VPS — backend VPS bersifat headless; monitoring data dilakukan lewat Firebase Console (cloud, tidak diuji) | Tidak direplikasi di Target Node (konsisten dengan tech stack asli yang juga tidak punya dashboard di VPS) |

**Catatan:** BiliCheck memakai Firebase sebagai backend cloud dan VPS AWS EC2 untuk relay FCM serta ekspor CSV dari Firestore. Replika lab memakai data dummy; HTTP REST pada tabel hanya untuk pengisian data uji ke Firestore Emulator, bukan endpoint sensor pada VPS.

Security Onion pada topologi lab berperan sebagai **Monitoring Node keamanan** (alat pemantauan lab, sesuai Bagian II Panduan PBL) — bukan replika dari komponen produk BiliCheck manapun.