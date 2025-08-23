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

## **Diagram Alur Prediksi Kebutuhan Guru**

```
+------------------+
| 1. Data Sekolah  |
|------------------|
| - ID Sekolah     |
| - Nama Sekolah   |
| - Kecamatan      |
| - Jenjang        |
| - Jumlah Siswa   |
| - Jumlah Guru    |
| - Mata Pelajaran |
+--------+---------+
         |
         v
+----------------------+
| 2. Data Cleaning &   |
|    Validasi          |
|----------------------|
| - Hapus duplikasi    |
| - Cek jumlah siswa   |
| - Cek jumlah guru    |
+--------+-------------+
         |
         v
+----------------------+
| 3. Hitung Rasio      |
|----------------------|
| rasio_siswa_per_guru |
| rasio_ideal_per_mapel|
+--------+-------------+
         |
         v
+----------------------+
| 4. Forecasting       |
|----------------------|
| - Proyeksi siswa     |
| - Kebutuhan guru     |
|   (jumlah_guru_dibutuhkan) |
+--------+-------------+
         |
         v
+------------------------+
| 5. Analisis Hierarkis  |
|------------------------|
| Level Sekolah           |
| Level Jenjang           |
| Level Kecamatan         |
+--------+---------------+
         |
         v
+------------------------+
| 6. Output & Insight    |
|------------------------|
| - Kekurangan guru      |
| - Prioritas penempatan |
| - Fokus mapel tertentu |
| - Prediksi tahun depan |
+------------------------+
```

---

### 🔹 Penjelasan Diagram

1. **Data Sekolah:** sumber data utama dari Dapodik atau laporan sekolah.
2. **Data Cleaning:** memastikan data valid dan siap diproses.
3. **Hitung Rasio:** mengetahui rasio siswa/guru saat ini dibandingkan standar ideal.
4. **Forecasting:** prediksi kebutuhan guru berdasarkan proyeksi siswa.
5. **Analisis Hierarkis:** bisa diturunkan sampai **per sekolah, per jenjang, atau per kecamatan**.
6. **Output & Insight:** hasil analisis berupa rekomendasi penempatan guru dan prioritas area/mata pelajaran.


## **1️⃣ Struktur Dataset Master**

| Kolom                          | Tipe Data | Deskripsi                                                          | Contoh                                          |
| ------------------------------ | --------- | ------------------------------------------------------------------ | ----------------------------------------------- |
| sekolah\_id                    | string    | ID unik sekolah                                                    | SDN001                                          |
| sekolah\_nama                  | string    | Nama sekolah                                                       | SDN 1 Kecamatan A                               |
| kecamatan                      | string    | Nama kecamatan                                                     | Kecamatan A                                     |
| desa                           | string    | Nama desa / kelurahan (opsional)                                   | Desa X                                          |
| jenjang                        | enum      | Jenjang sekolah                                                    | SD / SMP / SMA / SMK                            |
| jumlah\_siswa                  | integer   | Jumlah siswa saat ini                                              | 120                                             |
| jumlah\_guru\_ada              | integer   | Total guru saat ini                                                | 10                                              |
| mata\_pelajaran                | string    | Nama mapel                                                         | Matematika                                      |
| guru\_ada\_per\_mapel          | integer   | Jumlah guru per mata pelajaran                                     | 2                                               |
| rasio\_siswa\_per\_guru        | float     | Rasio siswa/guru saat ini                                          | 60.0                                            |
| rasio\_siswa\_per\_guru\_ideal | float     | Rasio ideal siswa/guru                                             | 30.0                                            |
| proyeksi\_siswa                | integer   | Prediksi jumlah siswa tahun depan                                  | 130                                             |
| jumlah\_guru\_dibutuhkan       | integer   | Hasil prediksi kebutuhan guru                                      | 5                                               |
| kekurangan\_guru               | integer   | kekurangan guru = jumlah\_guru\_dibutuhkan - guru\_ada\_per\_mapel | 3                                               |
| prioritas                      | enum      | Tingkat urgensi penempatan guru                                    | Tinggi / Sedang / Rendah                        |
| rekomendasi\_penempatan        | string    | Saran aksi                                                         | Rekrut baru / Mutasi / Pindah dari wilayah lain |


## **2️⃣ Contoh Data (Simulasi)**

| sekolah\_id | sekolah\_nama     | kecamatan   | desa   | jenjang | jumlah\_siswa | jumlah\_guru\_ada | mata\_pelajaran | guru\_ada\_per\_mapel | rasio\_siswa\_per\_guru | rasio\_siswa\_per\_guru\_ideal | proyeksi\_siswa | jumlah\_guru\_dibutuhkan | kekurangan\_guru | prioritas | rekomendasi\_penempatan |
| ----------- | ----------------- | ----------- | ------ | ------- | ------------- | ----------------- | --------------- | --------------------- | ----------------------- | ------------------------------ | --------------- | ------------------------ | ---------------- | --------- | ----------------------- |
| SDN001      | SDN 1 Kecamatan A | Kecamatan A | Desa X | SD      | 120           | 10                | Matematika      | 2                     | 60.0                    | 30.0                           | 130             | 5                        | 3                | Tinggi    | Rekrut baru             |
| SDN001      | SDN 1 Kecamatan A | Kecamatan A | Desa X | SD      | 120           | 10                | IPA             | 1                     | 120.0                   | 30.0                           | 130             | 5                        | 4                | Tinggi    | Rekrut baru             |
| SMP002      | SMP 2 Kecamatan B | Kecamatan B | Desa Y | SMP     | 200           | 8                 | Matematika      | 2                     | 100.0                   | 25.0                           | 210             | 8                        | 6                | Tinggi    | Rekrut baru             |
| SMP002      | SMP 2 Kecamatan B | Kecamatan B | Desa Y | SMP     | 200           | 8                 | Bahasa Inggris  | 1                     | 200.0                   | 25.0                           | 210             | 8                        | 7                | Tinggi    | Rekrut baru             |


## **3️⃣ Catatan Dataset**

1. **Granularitas:** Satu baris per sekolah per mata pelajaran → memudahkan analisis per mapel.
2. **Level Agregasi:** Bisa di-aggregate ke **jenjang atau kecamatan** menggunakan `groupby` di Python / R:

   ```python
   df.groupby(['kecamatan','jenjang']).sum()
   ```
3. **Forecasting:** kolom `proyeksi_siswa` bisa diisi menggunakan model prediksi pertumbuhan siswa.
4. **Insight:** kolom `kekurangan_guru`, `prioritas`, dan `rekomendasi_penempatan` adalah hasil analisis.

