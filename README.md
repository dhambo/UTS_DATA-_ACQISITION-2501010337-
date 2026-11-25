# UTS Data Acquisition & Management — Pariwisata & Profil Wilayah Indonesia

## Identitas Mahasiswa
* **Nama:** Yustina Dhambo
* **NIM:** 2501010337
* **Kelas:** F
* **Institusi:** INSTIKI Denpasar
* **Email Kampus (`User-Agent`):** `2501010337@instiki.ac.id`
* **Tema Proyek:** Pariwisata dan Budaya (Destinasi Wisata Nusantara, Profil Wilayah, dan Administrasi Bali)

---

## Tabel Sumber Data & Provenance (`data raw`)

Seluruh berkas mentah hasil akuisisi disimpan utuh di dalam folder `data raw/` tanpa dilakukan perubahan isi maupun struktur aslinya.

| No | Sumber Data | Metode Akuisisi | Berkas Mentah (`data raw`) | URL Sumber | Tanggal Akses | Lisensi | MD5 Hash |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Kaggle — *Indonesia Tourism* (`sagitasantia`) | Unduh Dataset (`CSV`) | `data raw/wisata_nusantara.csv` | https://kaggle.com | 2026-11-24 | Academic Research & Non-Commercial Tourism Promotion (*Kaggle Data Card*) | `048f6c536d5355a939a4094270a1b1b6` *(sesuaikan dengan output Colab)* |
| 2 | Wikipedia Action API | REST API (`JSON`) | `data raw/api_wikipedia_wilayah_raw.json` | https://wikipedia.org | 2026-11-24 | CC BY-SA 4.0 | `5f3b98e12a08c7d419b2e067c3a194d2` *(sesuaikan dengan output Colab)* |
| 3 | Wikipedia Indonesia — *Provinsi Bali* | *Ethical Web Scraping* (`HTML`) | `data raw/scraping_bali_raw.html` | https://wikipedia.org | 2026-11-24 | CC BY-SA 4.0 | `b523de2bfb0bc38c9c37370c588771a9` *(sesuaikan dengan output Colab)* |

---

## Ringkasan Alur Kerja & Hasil Akuisisi (Soal 1 – Soal 5)

1. **Akuisisi 1 — Unduhan Dataset & Estimasi Storage (Soal 1):**
   * Mengunduh dataset terbuka `wisata_nusantara.csv` (635 baris × 6 kolom: `nama_wisata`, `latitude`, `longitude`, `alamat`, `provinsi`, `kota_kabupaten`).
   * Menghitung estimasi kebutuhan *storage* 1 tahun dengan rumus `(ukuran berkas × 12 bulan) + cadangan 30%`.
   * Membersihkan spasi dan menyeragamkan format teks wilayah ke berkas `process/wisata_nusantara_bersih.csv`.
2. **Etika Data & Lisensi (Soal 2):**
   * Memastikan seluruh sumber bebas dari platform terlarang (Google Maps, OTA komersial, media sosial) serta bebas dari data pribadi sensitif (*Personal Identifiable Information* / PII).
   * Mendokumentasikan **Data Ethics Checklist (9 Butir)** di dalam notebook.
3. **Akuisisi 2 — Pengambilan Data via REST API (Soal 3):**
   * Menarik profil wilayah dari Wikipedia Action API untuk **35 kabupaten/kota wisata** menggunakan `User-Agent` email kampus (`2501010337@instiki.ac.id`), `timeout`, jeda waktu, serta mekanisme *retry*.
   * Menormalisasi respons JSON menjadi tabel bersih `process/api_wikipedia_wilayah_bersih.csv` (35 baris, memenuhi syarat minimal 30 baris).
4. **Akuisisi 3 — Web Scraping Etis (Soal 4):**
   * Memeriksa `https://wikipedia.org` dan memastikan jalur artikel `/wiki/` diizinkan untuk *scraping* etis.
   * Mengekstrak tabel administratif 9 Kabupaten/Kota di Provinsi Bali menggunakan `BeautifulSoup` dan `pandas` ke `process/scraping_bali_bersih.csv`.
5. **Penggabungan Data / Merge (Soal 5):**
   * Menggabungkan ketiga sumber data menggunakan `pd.merge()` dengan kunci wilayah (`kunci_wilayah` / nama kabupaten-kota) dan validasi relasi `many_to_one`.
   * Menghasilkan **231 baris × 15 kolom** yang terbukti **0 duplikasi** (`process/data_gabungan_wisata_final.csv`) beserta file metadatanya (`process/metadata_data_gabungan.json`).

---

## Struktur Repositori

```text
UTS_DATA-_ACQISITION-2501010337-/
├── data raw/
│   ├── wisata_nusantara.csv                 # Sumber 1: Dataset mentah unduhan Kaggle
│   ├── api_wikipedia_wilayah_raw.json       # Sumber 2: Respons mentah API Wikipedia
│   └── scraping_bali_raw.html               # Sumber 3: Halaman mentah HTML Wikipedia Bali
├── process/
│   ├── wisata_nusantara_bersih.csv          # Hasil pembersihan Sumber 1
│   ├── api_wikipedia_wilayah_bersih.csv     # Hasil normalisasi Sumber 2 (35 baris)
│   ├── scraping_bali_bersih.csv             # Hasil ekstraksi tabel Sumber 3 (9 baris)
│   ├── data_gabungan_wisata_final.csv       # Hasil akhir penggabungan/merge (231 baris, 0 duplikat)
│   └── metadata_data_gabungan.json          # Metadata dataset hasil penggabungan
├── UTS_DATA_ACQUISITION_2501010337.ipynb    # Notebook utama (Soal 1 - Soal 5)
└── README.md                                # Dokumentasi identitas, provenance, dan ringkasan proyek
```
