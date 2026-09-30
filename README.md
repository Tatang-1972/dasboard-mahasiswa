# Dashboard Pemeriksaan Mahasiswa

Dashboard HTML statis untuk memantau presensi, nilai tugas, UTS, UAS, nilai akhir, dan status risiko mahasiswa. Bisa di-hosting gratis di **GitHub Pages**.

## Isi folder

```
index.html            ← halaman dashboard
data/mahasiswa.csv    ← data mahasiswa (edit file ini)
README.md
```

## Cara publikasi di GitHub Pages

1. Masuk ke https://github.com → klik **New repository**.
2. Beri nama, misalnya `dashboard-kebijakan-harga`. Pilih **Public** (GitHub Pages gratis hanya untuk repo publik pada akun gratis).
3. Klik **Add file → Upload files**, lalu unggah `index.html`, `README.md`, dan folder `data` (seret seluruh folder ke jendela upload). Klik **Commit changes**.
4. Buka **Settings → Pages**. Pada *Source* pilih **Deploy from a branch**, branch **main**, folder **/ (root)**, lalu **Save**.
5. Tunggu 1–2 menit. Dashboard tampil di `https://<username>.github.io/<nama-repo>/`.

## Memperbarui data

1. Buka `data/mahasiswa.csv` di Excel / Google Sheets, isi data, simpan sebagai **CSV**.
2. Di GitHub, buka folder `data` → **Add file → Upload files** → unggah file baru dengan nama yang sama → **Commit changes**.
3. Dashboard otomatis terbarui dalam 1–2 menit.

Tanpa GitHub pun bisa: buka `index.html` di browser, lalu klik **Unggah CSV**. Data hanya dibaca di browser Anda.

## Format CSV

| Kolom | Isi |
|---|---|
| `nim`, `nama`, `kelas` | identitas mahasiswa |
| `p1` … `p14` | presensi: **H** hadir, **I** izin, **S** sakit, **A** alpa, kosong = belum ada pertemuan |
| `tugas1` … `tugasN` | nilai tugas 0–100 (jumlah kolom bebas) |
| `uts`, `uas` | nilai 0–100 |

Jumlah kolom pertemuan (`p…`) dan tugas (`tugas…`) boleh ditambah/dikurangi. Pemisah koma maupun titik koma (Excel Indonesia) sama-sama terbaca.

## Mengubah aturan penilaian

Buka `index.html`, cari bagian `CONFIG` di dekat bagian bawah:

- `mataKuliah`, `semester`, `dosen` — judul dashboard
- `bobot` — bobot tugas/UTS/UAS (default 30/30/40)
- `minKehadiran` — syarat kehadiran ikut UAS (default 75%)
- `batasLulus` — nilai akhir minimal lulus (default 60)
- `hitungIzinSakit` — apakah izin/sakit dihitung hadir
- `skalaNilai` — konversi nilai huruf (A, AB, B, BC, C, D, E)

Tombol **Pengaturan** di dashboard bisa dipakai untuk mencoba bobot lain secara sementara.

## Aturan status

- **Berisiko** — kehadiran di bawah syarat, atau nilai akhir di bawah batas lulus.
- **Perlu Perhatian** — ada tugas kosong, alpa ≥ 3 kali, atau nilai akhir kurang dari 10 poin di atas batas lulus.
- **Aman** — selain itu.

## ⚠️ Privasi data mahasiswa

Repositori publik dan GitHub Pages **dapat dibuka siapa saja**. Jangan unggah data nilai asli dengan NIM dan nama lengkap ke repo publik. Pilihan yang lebih aman:

- Unggah ke GitHub **hanya `index.html`** (tanpa data asli), lalu gunakan tombol **Unggah CSV** saat membuka dashboard — data tetap di komputer Anda; atau
- Samarkan data (mis. hanya 4 digit akhir NIM, tanpa nama); atau
- Gunakan repo **Private** + GitHub Pages dari akun GitHub Pro/Education (dosen bisa mendaftar GitHub Education secara gratis).
