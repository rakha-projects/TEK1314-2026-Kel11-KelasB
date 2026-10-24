# Deklarasi Tech Stack — Kelompok 11 (BiliCheck)

| Komponen | Teknologi pada Proyek IoT Asli | Direplikasi sebagai (Target Node) |
|---|---|---|
| Sistem operasi backend | Firebase (backend cloud) dan Ubuntu Server 24.04 (AWS EC2) | Ubuntu Server 24.04 (VM lab) |
| Database/penyimpanan data | Firebase Firestore dan RTDB; CSV di VPS | Firestore Emulator dan CSV lokal |
| Protokol komunikasi sensor | ESP32 → Firebase Auth/RTDB (HTTPS/REST dan SSE) | HTTP REST (data dummy → Firestore Emulator) |
| Dashboard/monitoring | Aplikasi Flutter dan Firebase Console | Security Onion (monitoring keamanan) |

**Catatan:** BiliCheck memakai Firebase sebagai backend cloud dan VPS AWS EC2 untuk relay FCM serta ekspor CSV dari Firestore. Replika lab memakai data dummy; HTTP REST pada tabel hanya untuk pengisian data uji ke Firestore Emulator, bukan endpoint sensor pada VPS.
