# Kebun Sawit - Web App (mandiri)

Halaman web (GitHub Pages) yang meniru aplikasi "Kebun Sawit" (AI Studio, by Harvin).
Berjalan penuh di browser HP/laptop: Terbaru, Riwayat, Banding, Animasi, tombol
Layar Penuh, ketuk gambar untuk zoom, dan tombol refresh.

Repo ini MANDIRI: ia mengambil datanya sendiri (tidak menumpang repo lain).

## Isi

- index.html ............. aplikasi (halaman utama GitHub Pages)
- sawit_satelit.py ....... script pengambil citra Sentinel-2
- .github/workflows/sawit.yml  workflow harian (otomatis)
- .nojekyll .............. agar GitHub Pages serve apa adanya
- dashboard.html ......... (dibuat otomatis) dashboard lama, tidak dipakai
- data.json, citra/ ...... (dibuat otomatis oleh workflow)

## Konfigurasi saat ini (di .github/workflows/sawit.yml)

- Jadwal  : setiap hari jam 14:00 (2 siang) waktu Anda  ->  cron "0 6 * * *" (06:00 UTC)
- Lintang : PLOT_LAT  = 0.81601
- Bujur   : PLOT_LON  = 101.97512
- Area    : BOX_HALF_M = 700  (700 m dari titik ke tiap sisi = kotak 1400 m)

Ubah nilai-nilai itu kapan saja lalu commit; halaman ikut berubah setelah workflow jalan.

## SECRET (WAJIB)

Workflow butuh kredensial Sentinel Hub. Secret TIDAK ikut pindah antar-repo,
jadi tambahkan lagi di repo ini (boleh pakai NILAI YANG SAMA dgn repo lama -
tidak perlu bikin kredensial baru):

1. Settings -> Secrets and variables -> Actions -> New repository secret
2. Buat: SH_CLIENT_ID       = (client id Sentinel Hub Anda)
3. Buat: SH_CLIENT_SECRET   = (client secret Sentinel Hub Anda)

## Cara publish (sekali saja)

1. Buat repo baru (mis. kebun-sawit-app), Public.
2. Upload SEMUA isi folder ini (termasuk folder .github).
3. Tambahkan 2 secret di atas.
4. Actions -> aktifkan workflow (klik "I understand... enable") -> pilih
   "Citra Sawit Harian" -> Run workflow (untuk isi data pertama kali).
   Catatan: run PERTAMA mengambil semua tanggal di lokasi baru, jadi agak lama.
5. Settings -> Pages -> Source: Deploy from a branch -> main / (root) -> Save.
6. Buka: https://<username>.github.io/kebun-sawit-app/

## Catatan

- Jangan buka index.html langsung dari komputer (file://) - browser memblokir
  pengambilan data. Harus lewat GitHub Pages (https).
- Sebelum workflow pertama selesai, halaman masih kosong (belum ada data.json).
