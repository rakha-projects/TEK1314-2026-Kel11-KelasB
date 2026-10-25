# TEK1314-2026-Kel11-KelasB
Kelompok 11 Siber Security TEK61-B

## Skenario Proyek

Proyek ini mensimulasikan SOC Engagement untuk mengamankan infrastruktur backend proyek IoT **BiliCheck/BILINOVA**, dengan tiga entitas utama:
- **Attacker Node** — Kali Linux, berperan sebagai penyerang.
- **Target Node (Korban)** — Ubuntu Server, replika VPS backend BiliCheck (Node.js export script + Firestore Emulator, menghasilkan backup CSV dari data pemeriksaan dummy).
- **Monitoring Node** — Security Onion, memantau seluruh segmen jaringan kelompok untuk mendeteksi aktivitas mencurigakan.

Detail pemetaan tech stack asli → replika ada di [`docs/presentation-minggu9/tech_stack_declaration.md`](docs/presentation-minggu9/tech_stack_declaration.md). Detail topologi jaringan dan skema IP tersedia di folder [`docs/design/`](docs/design/) (`topology.png` dan `ip_plan.md`).