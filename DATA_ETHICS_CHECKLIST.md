# Data Ethics Checklist (9 Butir) — UTS Data Acquisition & Management

* **Nama Mahasiswa:** Yustina Dhambo
* **NIM:** 2501010337
* **Kelas:** F — Program Studi Informatika, INSTIKI
* **Email Kampus (`User-Agent`):** `2501010337@instiki.ac.id`
* **Topik Proyek:** Destinasi Wisata Nusantara (Kaggle), Kondisi Meteorologi & Elevasi Wilayah (Open-Meteo API), dan Administrasi Provinsi Indonesia (Wikipedia)

| No | Aspek Etika Data | Status | Bukti & Implementasi pada Proyek |
| :--- | :--- | :--- | :--- |
| 1 | **Informed Consent (Persetujuan)** | Terpenuhi | Seluruh objek data berupa destinasi wisata publik serta parameter cuaca dan geografis terbuka, bukan subjek manusia. |
| 2 | **Privasi & Anonimisasi (PII)** | Terpenuhi | Tidak terdapat nama individu, NIK, nomor telepon, alamat rumah pribadi, maupun akun media sosial (`0` kolom PII). |
| 3 | **Kepatuhan Lisensi & Hak Cipta** | Terpenuhi | Kaggle *Indonesia Tourism* (Academic Research), Open-Meteo Public API (CC BY 4.0), dan Wikipedia (CC BY-SA 4.0). |
| 4 | **Kepatuhan *Terms of Service* & `robots.txt`** | Terpenuhi | Bebas dari Google Maps, OTA komersial, dan media sosial; `robots.txt` diverifikasi via `RobotFileParser().can_fetch()`. |
| 5 | **Identitas *Crawler* (`User-Agent`)** | Terpenuhi | Setiap *request* HTTP menyertakan `User-Agent` resmi berisi email kampus (`2501010337@instiki.ac.id`). |
| 6 | **Pembatasan Laju (*Rate Limit*) & Stabilitas** | Terpenuhi | Menerapkan pengaturan `timeout`, jeda waktu `time.sleep()`, serta mekanisme `Retry` otomatis. |
| 7 | **Keamanan Kredensial** | Terpenuhi | Tidak ada API key, token akses, maupun kata sandi yang ditulis langsung (*hardcoded*) di dalam kode notebook. |
| 8 | **Integritas & *Provenance* Data** | Terpenuhi | Seluruh berkas mentah disimpan utuh di folder `data raw/` disertai URL lengkap, tanggal akses, lisensi, dan *hash* MD5. |
| 9 | **Transparansi & Reproduksibilitas** | Terpenuhi | Seluruh tahapan akuisisi, pembersihan, validasi anti-duplikasi, dan penggabungan data terdokumentasi rapi di notebook. |
