# Deklarasi Tech Stack & Replikasi — Kelompok 11

**Proyek IoT Asli:** BiliCheck — alat pembaca kadar bilirubin non-invasif berbasis IoT (proyek mitra dosen, lintas mata kuliah).

**Catatan konteks:** mayoritas backend BiliCheck memakai Firebase (Firestore + Realtime Database + Cloud Messaging) sebagai layanan cloud terkelola pihak ketiga — bagian ini **tidak** direplikasi karena tim tidak mengoperasikan infrastrukturnya sendiri. Komponen yang benar-benar self-hosted dan menjadi dasar replikasi di bawah adalah **VPS relay/ekspor** milik tim (Ubuntu, AWS EC2) yang bertugas merelay notifikasi (Firebase Admin SDK) dan mengekspor data pemeriksaan secara berkala.

| Komponen | Pada Proyek IoT Asli (BiliCheck) | Direplikasi sebagai (Target Node) |
|---|---|---|
| Sistem Operasi backend | Ubuntu Server (VPS, AWS EC2) — menjalankan script relay & ekspor | Ubuntu Server — `SRV-WEB-KEL11` (`192.168.11.101`) |
| Database/penyimpanan data | Firebase Firestore + RTDB (cloud); data yang diekspor VPS disusun terstruktur sebelum dikirim | MySQL lokal di Target Node — merepresentasikan lapisan penyimpanan terstruktur pada sisi VPS |
| Protokol komunikasi | VPS berkomunikasi ke Firebase via HTTPS/REST (Admin SDK) dan menyajikan data ekspor lewat HTTP | HTTP pada port 80/443 (DVWA) dan port 5000 (REST endpoint Flask: `POST /pemeriksaan`, `GET /export.csv`) pada Target Node |
| Dashboard/monitoring | Firebase Console (monitor data) + endpoint ekspor CSV di VPS untuk tim | DVWA (port 80, permukaan serangan web) **+** app Flask (`app/relay-export/app.py`, port 5000) yang menjalankan fungsi ekspor data sebenarnya, merepresentasikan endpoint ekspor CSV di VPS asli |

**Alasan replikasi tidak 1:1 penuh:** backend produksi BiliCheck memang sudah bergeser ke arsitektur serverless (Firebase), sehingga permukaan backend yang masih *self-hosted dan layak diuji* hanya lapisan VPS relay/ekspor. Replika di atas memfokuskan simulasi pada lapisan itu: server Linux + database terstruktur + antarmuka web berbasis HTTP, yang secara prinsip sama dengan fungsi VPS asli meski implementasi teknisnya disederhanakan untuk kebutuhan lab 1 semester.

**Implikasi ke pembagian tim:**
- Kontrol hardening kategori **Data & Application** (lihat `docs/blueteam/hardening_checklist.md`) diterapkan pada komponen tambahan yang mereplikasi *script relay/ekspor* VPS asli — bukan pada DVWA itu sendiri.
