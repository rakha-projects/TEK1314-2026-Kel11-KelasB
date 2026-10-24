# Red Team Attack Plan — BiliCheck (Kelompok 11)

## 1. Tujuan dan ruang lingkup

Red Team menguji keamanan **VPS BiliCheck**, yaitu server Ubuntu yang menjalankan proses Node.js untuk membaca Firestore dan membuat cadangan CSV. VPS tidak berada di jalur pengukuran bilirubin; dampak yang diuji adalah akses tidak sah ke server, kebocoran data pemeriksaan, dan perubahan isi hasil ekspor.

Target pengujian adalah **Ubuntu lab `192.168.11.101`** dengan Firestore Emulator dan data dummy. Kali `192.168.11.100` menjadi Attacker Node. Firebase dan EC2 produksi tidak diuji. Tidak ada dashboard web atau API HTTP masuk pada VPS yang direplikasi.

## 2. Aset dan alur data

| Aset | Mengapa diuji |
|---|---|
| Akses SSH Ubuntu | Pintu administrasi ke skrip dan file backup |
| Data dummy pada Firestore Emulator | Sumber data yang diproses skrip ekspor |
| Skrip ekspor Node.js | Menentukan isi CSV yang dibuat VPS |
| Backup CSV | Berisi salinan data pemeriksaan dan pasien |

```text
Firestore Emulator (data dummy) → Node.js di Ubuntu → backup CSV
Kali → Ubuntu                         Security Onion memantau traffic lab
```

## 3. Aturan pengujian

1. Semua percobaan hanya pada Ubuntu lab dan data dummy.
2. Hardening Ubuntu yang sudah ada tetap menjadi kondisi awal; tidak dimatikan agar serangan berhasil.
3. Port SSH, layanan, dan lokasi CSV diperiksa di VM sebelum uji. Hasil serangan tidak diklaim sebelum ada bukti.

## 4. Skenario serangan

| ID | Kategori PBL | Target | Tools |
|---|---|---|---|
| S1 | Reconnaissance | Port dan layanan Ubuntu | Nmap |
| S2 | Exploitation/Akses | Login SSH akun dummy | SSH, Hydra |
| S3 | Web/API/Protokol IoT | Data Firestore dummy yang diekspor ke CSV | SSH, `curl`, LibreOffice Calc |

### S1 — Pemetaan port dan layanan

**Hipotesis:** Ubuntu mungkin masih menampilkan layanan yang tidak dibutuhkan oleh VPS tanpa web API.

**Langkah rencana:**
1. Pindai port dan identifikasi layanan pada `192.168.11.101` dari Kali.
2. Cocokkan hasil dengan layanan yang memang berjalan di Ubuntu.

**Temuan bila berhasil:** port atau layanan yang tidak diperlukan dapat diakses dari Kali. Hasil scan juga menjadi dasar memilih target uji berikutnya.

### S2 — Percobaan login SSH

**Hipotesis:** bila login password masih aktif pada akun dummy, percobaan berulang mungkin memperoleh akses atau tidak dibatasi.

**Langkah rencana:**
1. Periksa port SSH yang benar dan siapkan akun dummy khusus lab.
2. Coba daftar password kecil dengan Hydra dari Kali; hentikan setelah batas percobaan yang disepakati.
3. Catat apakah login berhasil, ditolak, atau sumber percobaan diblokir.

**Temuan bila berhasil:** akun dummy dapat dimasuki tanpa izin, atau percobaan berulang tetap diterima tanpa pembatasan.

### S3 — Formula pada hasil ekspor CSV

**Hipotesis:** nilai teks dari Firestore yang diawali `=` dapat ditulis apa adanya ke CSV dan dibaca spreadsheet sebagai formula.

**Langkah rencana:**
1. Melalui akun uji, masukkan nama pasien **dummy** `=1+1` ke Firestore Emulator memakai klien lokal. Akses dari Kali dilakukan lewat SSH; port emulator tidak dibuka ke Kali.
2. Jalankan proses ekspor dan ambil CSV hasilnya.
3. Buka CSV di LibreOffice Calc dan lihat apakah sel tersebut tampil sebagai teks `=1+1` atau dihitung menjadi `2`.

**Temuan bila berhasil:** nilai yang semestinya data pasien diproses sebagai formula. Uji memakai formula aritmetika ini saja, tanpa pengambilan data atau perintah lain.

## 5. Hal yang perlu dicek sebelum eksekusi

- Port dan metode autentikasi SSH yang sedang dipakai Ubuntu.
- Lokasi skrip ekspor serta file CSV setelah komponen lab dipasang.
- Cara akun uji menulis satu record dummy ke Firestore Emulator.

Ketiga skenario masih berupa **rencana**. Hasilnya baru diisi setelah pengujian pada VM.
