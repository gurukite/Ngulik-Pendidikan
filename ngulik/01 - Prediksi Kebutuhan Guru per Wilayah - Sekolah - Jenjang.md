# 📊 Prediksi Kebutuhan Guru per Wilayah / Sekolah / Jenjang

## 1. Latar Belakang Masalah

Dinas Pendidikan ingin memastikan distribusi guru yang optimal di seluruh wilayah. Tantangan yang dihadapi:

* Kekurangan guru di beberapa sekolah / kecamatan tertentu.
* Ketidakseimbangan jumlah guru antar jenjang dan mata pelajaran.
* Kebutuhan guru yang berubah setiap tahun mengikuti pertumbuhan siswa.

Tujuan proyek ini adalah memprediksi kebutuhan guru di masa depan agar distribusi SDM lebih **efisien dan tepat sasaran**.

## 2. Data yang Dibutuhkan

### 2.1 Data Sekolah

* `sekolah_id` : ID unik sekolah
* `sekolah_nama` : Nama sekolah
* `kecamatan` : Nama kecamatan
* `desa` : Nama desa / kelurahan (opsional)
* `jenjang` : SD / SMP / SMA / SMK
* `jumlah_siswa` : Total siswa saat ini
* `jumlah_guru_ada` : Jumlah guru saat ini
* `jumlah_guru_per_mapel` : Jumlah guru tiap mata pelajaran

### 2.2 Data Tambahan

* `rasio_siswa_per_guru_ideal` : Standar rasio siswa per guru
* `proyeksi_siswa` : Prediksi jumlah siswa di tahun berikutnya
* `faktor_kebijakan` : Faktor tambahan, misal prioritas pengiriman guru

> Data dapat diambil dari **Dapodik**, laporan sekolah, atau sumber internal dinas.

## 3. Proses Analisis

### 3.1 Pengolahan Data

1. **Kumpulkan data sekolah** dari semua kecamatan.
2. **Cek kualitas data**: hapus duplikasi, pastikan jumlah siswa dan guru valid.
3. **Hitung rasio siswa/guru saat ini**:

   ```
   rasio_siswa_per_guru = jumlah_siswa / jumlah_guru_ada 
   ```
4. **Tentukan rasio ideal** sesuai jenjang / mata pelajaran.

### 3.2 Forecasting

1. Gunakan **proyeksi pertumbuhan siswa** per sekolah/jenjang.
2. Hitung **kebutuhan guru masa depan** berdasarkan rasio ideal:

   ```
   jumlah_guru_dibutuhkan = proyeksi_siswa / rasio_siswa_per_guru_ideal
   ```

### 3.3 Analisis Hierarkis

* **Level Sekolah:** identifikasi sekolah yang kekurangan guru per mapel.
* **Level Jenjang:** lihat kebutuhan guru SD/SMP/SMA per kecamatan.
* **Level Wilayah:** total kebutuhan guru per kecamatan/desa → bantu alokasi SDM.

## 4. Output & Insight

### 4.1 Contoh Tabel Hasil Prediksi

| Kecamatan | Sekolah | Jenjang | Mapel      | Guru Ada | Guru Dibutuhkan | Kekurangan | Prioritas |
| --------- | ------- | ------- | ---------- | -------- | --------------- | ---------- | --------- |
| A         | SDN 1   | SD      | Matematika | 2        | 3               | 1          | Tinggi    |
| B         | SMPN 2  | SMP     | IPA        | 1        | 2               | 1          | Tinggi    |

### 4.2 Insight yang Dihasilkan

* Sekolah mana yang **paling kekurangan guru** → prioritas penempatan guru.
* Kecamatan mana yang **membutuhkan penambahan guru secara keseluruhan**.
* Mata pelajaran mana yang **sering kekurangan guru** → bisa jadi fokus rekrutmen.
* Prediksi kebutuhan tahun depan untuk **perencanaan anggaran & SDM**.

## 5. Tools & Metode yang Disarankan

* **Python / R** untuk analisis data & forecasting
* **Pandas / Numpy** untuk pengolahan data
* **Scikit-learn / Prophet** untuk prediksi pertumbuhan siswa
* **Tableau / Power BI** untuk visualisasi hasil distribusi guru

## 6. Workflow Ringkas

1. Ambil data sekolah & guru → bersihkan & validasi.
2. Hitung rasio siswa/guru & tentukan kebutuhan guru.
3. Forecast pertumbuhan siswa → hitung kebutuhan guru masa depan.
4. Agregasi per sekolah, jenjang, dan kecamatan.
5. Visualisasi → ambil insight → rekomendasi penempatan guru.

