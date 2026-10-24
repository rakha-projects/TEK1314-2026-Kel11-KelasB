# Deklarasi Tech Stack — Kelompok 11 (BiliCheck)

| Komponen | Teknologi pada Proyek IoT Asli | Direplikasi sebagai (Target Node) |
|---|---|---|
| Sistem operasi backend | Ubuntu Server pada VPS AWS EC2 | Ubuntu Server `192.168.11.101` |
| Database/penyimpanan data | Firebase Firestore dan RTDB; backup CSV pada VPS | Firestore Emulator berisi data dummy; backup CSV lokal. RTDB belum dipakai skrip VPS |
| Protokol komunikasi sensor | ESP32 → Firebase RTDB melalui HTTPS (rancangan); VPS → Firestore melalui HTTPS | Alur sensor tidak diuji; skrip VPS mengakses Firestore Emulator melalui Firebase Admin SDK |
| Dashboard/monitoring | Aplikasi Flutter untuk pengguna; VPS tidak memiliki dashboard web | Tidak ada dashboard web pada Target Node; Security Onion untuk monitoring keamanan lab |

Target Node mereplikasi bagian VPS yang dikelola tim, bukan seluruh sistem BiliCheck. VPS asli dirancang untuk merelay FCM dan mengekspor CSV; pengujian lab berfokus pada ekspor CSV dari Firestore Emulator berisi data dummy. RTDB dan sensor tidak dijalankan pada Target Node karena skrip VPS saat ini hanya membaca Firestore. Firebase dan EC2 produksi tidak diuji.
