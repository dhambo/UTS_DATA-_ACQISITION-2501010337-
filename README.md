# UTS Data Acquisition & Management — Pariwisata Nusantara, Meteorologi Wilayah, dan Administrasi Provinsi Indonesia

## Identitas Mahasiswa
* **Nama:** Yustina Dhambo
* **NIM:** 2501010337
* **Kelas:** F — Program Studi Informatika, INSTIKI
* **Email Kampus (`User-Agent`):** `2501010337@instiki.ac.id`
* **Tema Proyek:** Pariwisata dan Budaya (Destinasi Wisata Nusantara, Cuaca & Elevasi Wilayah, serta Administrasi Provinsi di Indonesia)

---

## Tabel Sumber Data & Provenance (`data raw`)

Seluruh berkas mentah hasil akuisisi disimpan utuh di dalam folder `data raw/` tanpa dilakukan perubahan isi maupun struktur aslinya.

| No | Sumber Data | Metode Akuisisi | Berkas Mentah (`data raw`) | URL Sumber | Tanggal Akses | Lisensi | MD5 Hash |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Kaggle — *Indonesia Tourism* (`sagitasantia`) | Unduh Dataset (`CSV`) | `data raw/wisata_nusantara.csv` | https://www.kaggle.com/datasets/sagitasantia/wisata-indonesia | 2026-11-24 | Academic Research & Non-Commercial Tourism Promotion (*Kaggle Data Card*) | `e02e743b15f22ce0b2d090e1e0846e00` |
| 2 | Open-Meteo Public API | REST API (`JSON`) | `data raw/api_cuaca_elevasi_raw.json` | https://open-meteo.com | 2026-11-27 | CC BY 4.0 (Open-Meteo) | `3b4f12702263b9b5e18feb6ed4def038` |
| 3 | Wikipedia Indonesia — *Provinsi di Indonesia* | *Ethical Web Scraping* (`HTML`) | `data raw/scraping_provinsi_indonesia_raw.html` | https://wikipedia.org | 2026-11-27 | CC BY-SA 4.0 (Wikipedia) | `7c13adad75af2654b35976ca96d23a8` |

---

## Ringkasan Alur Kerja & Hasil Perbaikan (Soal 1 – Soal 5)

1. **Akuisisi 1 — Unduhan Dataset & Estimasi Storage (Soal 1):**
   * Mengunduh dataset terbuka `wisata_nusantara.csv` (635 baris × 6 kolom: `nama_wisata`, `latitude`, `longitude`, `alamat`, `provinsi`, `kota_kabupaten`) dari halaman resmi Kaggle.
   * Menghitung kebutuhan penyimpanan 1 tahun dengan rumus `(ukuran berkas × 12 bulan) + cadangan 30%` = **1.620,60 KB (1,58 MB)**.
   * Membersihkan spasi berlebih pada kolom wilayah ke `process/wisata_nusantara_bersih.csv`.
2. **Etika Data, Lisensi, & Data Ethics Checklist (Soal 2):**
   * Memastikan seluruh sumber bebas dari Google Maps, OTA komersial, dan media sosial, serta bebas dari *Personal Identifiable Information* (PII).
   * Mendokumentasikan **Data Ethics Checklist (9 Butir)** di dalam notebook maupun berkas khusus [`DATA_ETHICS_CHECKLIST.md`](./DATA_ETHICS_CHECKLIST.md).
3. **Akuisisi 2 — Pengambilan Data via REST API (Soal 3):**
   * Menarik data numerik bernilai tinggi dari **Open-Meteo Public API** (elevasi ketinggian wilayah dalam mdpl, suhu udara °C, kelembapan %, dan kecepatan angin km/jam) untuk **40 kabupaten/kota wisata** (0 nilai kosong) menggunakan `User-Agent` email kampus (`2501010337@instiki.ac.id`), `timeout`, jeda waktu, dan *retry*.
4. **Akuisisi 3 — Web Scraping Etis (`RobotFileParser().can_fetch()`) (Soal 4):**
   * Memverifikasi izin akses `https://wikipedia.org` secara terprogram menggunakan `urllib.robotparser.RobotFileParser().can_fetch()` (`True`).
   * Mengekstrak tabel administratif **38 Provinsi di Indonesia** menggunakan `BeautifulSoup` dan `pandas` ke `process/scraping_provinsi_indonesia_bersih.csv`.
5. **Penggabungan Data / Merge Menyeluruh (Soal 5):**
   * Menggabungkan ketiga sumber data menggunakan `pd.merge()` dengan parameter `validate="many_to_one"` pada kunci wilayah (`kunci_wilayah`) dan kunci provinsi (`kunci_provinsi`).
   * Menghasilkan dataset terintegrasi lintas provinsi (**21 provinsi terisi merata**) yang terbukti **0 duplikasi** (`process/data_gabungan_wisata_final.csv`) beserta metadatanya (`process/metadata_data_gabungan.json`).

---

## Struktur Repositori

```text
UTS_DATA_ACQISITION_MANAGEMENT-2501010337-/
├── data raw/
│   ├── wisata_nusantara.csv                          # Sumber 1: Dataset mentah unduhan Kaggle
│   ├── api_cuaca_elevasi_raw.json                    # Sumber 2: Respons mentah Open-Meteo API
│   └── scraping_provinsi_indonesia_raw.html          # Sumber 3: Halaman mentah HTML Provinsi Indonesia
├── process/
│   ├── wisata_nusantara_bersih.csv                   # Hasil pembersihan Sumber 1
│   ├── api_cuaca_elevasi_bersih.csv                  # Hasil normalisasi Sumber 2 (40 wilayah, 0 null)
│   ├── scraping_provinsi_indonesia_bersih.csv        # Hasil ekstraksi Sumber 3 (38 Provinsi)
│   ├── data_gabungan_wisata_final.csv                # Hasil akhir penggabungan/merge (0 duplikat)
│   └── metadata_data_gabungan.json                   # Metadata dataset hasil penggabungan
├── DATA_ETHICS_CHECKLIST.md                          # Berkas khusus Data Ethics Checklist (9 Butir)
├── UTS_DATA_ACQISITION_MANAGEMENT_2501010337.ipynb   # Notebook utama lengkap (Soal 1 - Soal 5)
└── README.md                                         # Dokumentasi identitas, provenance, dan ringkasan proyek
```
