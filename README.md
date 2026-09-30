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

## Koreksi Otomatis (tab ✅ Koreksi Otomatis)

1. **Unggah kunci jawaban** — CSV, Excel, **Word (.docx)**, atau **PDF**.
   - CSV/Excel/tabel Word: kolom `no`, `kunci`, dan (opsional) `bobot`.
   - Teks Word/PDF: tulis per nomor, mis. `1. A`, `2. C`, … Bobot boleh ditulis `10. harga penetrasi (bobot 2)`.
   - Beberapa jawaban benar dipisah `|` atau ` / `, mis. `harga penetrasi / penetration pricing`.
   - Soal yang kuncinya dikosongkan (mis. esai) tidak ikut dinilai.
2. **Unggah jawaban mahasiswa** — boleh banyak file sekaligus, format campuran pun bisa:
   - **Satu file semua mahasiswa** (CSV/Excel): kolom `nim`, `nama`, lalu kolom soal `1`, `2`, `3`… Hasil ekspor **Google Form** langsung terbaca.
   - **Satu file per mahasiswa** (CSV/Excel/Word/PDF). Di Word/PDF, pola yang dikenali:
     - `1. A` · `1) A` · `2 - C` · beberapa per baris `1. A  2. C  3. B`
     - soal lengkap diikuti baris `Jawab: B`
     - tabel `No | Jawaban`
   - Identitas dibaca dari baris `Nama: …`, `NIM: …`, `Kelas: …`. Jika tidak ada, dari nama file `NIM_Nama.pdf` (mis. `2023010018_Siti Nurhaliza.pdf`).
   - PDF hasil **scan/foto** dan tulisan tangan tidak bisa dibaca. File `.doc` (Word lama) harus disimpan ulang sebagai `.docx`.
3. Nilai langsung muncul: jumlah benar/salah/kosong, nilai, analisis butir soal (soal sulit/mudah), dan detail jawaban per mahasiswa.
4. Pilih kolom tujuan (Tugas 1–N, kolom tugas baru, UTS, UAS) → **Masukkan ke Dashboard**. Nilai dicocokkan berdasarkan NIM (atau nama).
5. Klik **💾 Unduh Data** → unggah `mahasiswa.csv` yang baru ke folder `data` di GitHub agar tersimpan permanen.

### Penilaian esai dengan pedoman penskoran

Unggah **pedoman penskoran Word (.docx)** sebagai kunci jawaban, yaitu dokumen dengan tabel **Butir | Aspek / Konsep yang dinilai | Skor** (format lembar pedoman penskoran tugas tutorial). Mode esai aktif otomatis:

- Setiap butir dibaca beserta skor maksimalnya dan poin-poin kunci (daftar, tabel di dalam sel, dan paragraf penjelasan).
- Baris "Skor penggunaan bahasa" dan "Skor maksimal" dibaca otomatis. Contoh: nilai akhir = skor jawaban ÷ 100 × 90 + skor bahasa (maks 10).
- Jawaban mahasiswa (Word/PDF, satu file per mahasiswa) dipecah per butir menurut penanda **"Soal 1 / Nomor 1 / Butir 1"** atau penomoran "1.", "2." di awal baris. Jika tidak ada penanda, setiap butir dicocokkan dengan seluruh isi jawaban dan diberi tanda **cek**.
- Skor setiap butir adalah **saran otomatis** berdasarkan seberapa banyak poin kunci yang muncul dalam jawaban. Secara bawaan, skor penuh diberikan bila ≥ 60% poin kunci terpenuhi (dapat diubah).
- Klik nama mahasiswa untuk melihat poin kunci yang ✓ ditemukan, ◐ sebagian, atau ✗ tidak ditemukan, membaca jawabannya, **mengubah skor per butir**, dan mengisi **skor bahasa**.

Keterbatasan: pencocokan berbasis kata kunci tidak bisa menilai logika atau argumen, dan tidak mendeteksi jawaban yang **menyangkal** konsep (mis. "variabel internal **adalah** faktor utama" tetap dianggap menyebut konsep itu). Karena itu skor otomatis sebaiknya diperiksa, terutama untuk nilai yang mepet.

Catatan: pencocokan jawaban tidak membedakan huruf besar/kecil dan spasi. Untuk pilihan ganda, jawaban "B. Harga pokok" dianggap B. Jawaban uraian/esai bebas tetap perlu dinilai manual.
Contoh file untuk mencoba ada di folder `contoh/`.

## Aturan status

- **Berisiko** — kehadiran di bawah syarat, atau nilai akhir di bawah batas lulus.
- **Perlu Perhatian** — ada tugas kosong, alpa ≥ 3 kali, atau nilai akhir kurang dari 10 poin di atas batas lulus.
- **Aman** — selain itu.

## ⚠️ Privasi data mahasiswa

Repositori publik dan GitHub Pages **dapat dibuka siapa saja**. Jangan unggah data nilai asli dengan NIM dan nama lengkap ke repo publik. Pilihan yang lebih aman:

- Unggah ke GitHub **hanya `index.html`** (tanpa data asli), lalu gunakan tombol **Unggah CSV** saat membuka dashboard — data tetap di komputer Anda; atau
- Samarkan data (mis. hanya 4 digit akhir NIM, tanpa nama); atau
- Gunakan repo **Private** + GitHub Pages dari akun GitHub Pro/Education (dosen bisa mendaftar GitHub Education secara gratis).
