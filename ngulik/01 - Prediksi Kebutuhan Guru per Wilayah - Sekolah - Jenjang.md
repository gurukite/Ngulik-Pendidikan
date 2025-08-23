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


## Ngulik v.1

```python
# ===========================
# Prediksi Kebutuhan Guru 
# ===========================

# 1. Import Library
import pandas as pd
import numpy as np
from prophet import Prophet
import matplotlib.pyplot as plt
import seaborn as sns
import os
from io import StringIO

# ===========================
# 2. Load Data (CSV eksternal atau contoh internal)
# ===========================
csv_file = 'dataset_guru.csv'

try:
    df = pd.read_csv(csv_file)
    print(f"Dataset '{csv_file}' berhasil dimuat.")
except FileNotFoundError:
    print(f"Dataset '{csv_file}' tidak ditemukan. Menggunakan contoh dataset internal.")
    csv_data = StringIO("""
tahun,sekolah_id,sekolah_nama,kecamatan,desa,jenjang,jumlah_siswa,jumlah_guru_ada,mata_pelajaran,guru_ada_per_mapel,rasio_siswa_per_guru_ideal
2022,SDN001,SDN 1 Kecamatan A,Kecamatan A,Desa X,SD,120,10,Matematika,2,30
2022,SDN001,SDN 1 Kecamatan A,Kecamatan A,Desa X,SD,120,10,IPA,1,30
2022,SDN002,SDN 2 Kecamatan A,Kecamatan A,Desa Y,SD,150,12,Matematika,3,30
2022,SDN002,SDN 2 Kecamatan A,Kecamatan A,Desa Y,SD,150,12,IPA,2,30
2022,SMP001,SMP 1 Kecamatan B,Kecamatan B,Desa Z,SMP,200,8,Matematika,2,25
2022,SMP001,SMP 1 Kecamatan B,Kecamatan B,Desa Z,SMP,200,8,Bahasa Inggris,1,25
2022,SMP002,SMP 2 Kecamatan B,Kecamatan B,Desa W,SMP,180,9,Matematika,2,25
2022,SMP002,SMP 2 Kecamatan B,Kecamatan B,Desa W,SMP,180,9,Bahasa Inggris,2,25
""")
    df = pd.read_csv(csv_data)

# ===========================
# 3. Data Cleaning & Validasi
# ===========================
df.drop_duplicates(inplace=True)
numeric_cols = ['jumlah_siswa', 'jumlah_guru_ada', 'guru_ada_per_mapel', 'rasio_siswa_per_guru_ideal']
for col in numeric_cols:
    df[col] = pd.to_numeric(df[col], errors='coerce')
df.fillna(0, inplace=True)

# ===========================
# 4. Hitung Rasio Siswa/Guru
# ===========================
df['rasio_siswa_per_guru'] = df['jumlah_siswa'] / df['guru_ada_per_mapel']

# ===========================
# 5a. Forecast Pertumbuhan Siswa - 5% Growth
# ===========================
df['proyeksi_siswa'] = (df['jumlah_siswa'] * 1.05).round().astype(int)

# ===========================
# 5b. Forecast Pertumbuhan Siswa - Prophet per Sekolah
# ===========================
def forecast_siswa_prophet(school_id, periods=1):
    df_school = df[df['sekolah_id'] == school_id][['tahun', 'jumlah_siswa']].copy()
    if df_school.empty:
        return 0
    df_school.rename(columns={'tahun': 'ds', 'jumlah_siswa': 'y'}, inplace=True)
    model = Prophet(yearly_seasonality=True, daily_seasonality=False, weekly_seasonality=False)
    try:
        model.fit(df_school)
        future = model.make_future_dataframe(periods=periods, freq='Y')
        forecast = model.predict(future)
        return forecast[['ds', 'yhat']].tail(periods)['yhat'].values[0]
    except Exception as e:
        print(f"Forecast gagal untuk sekolah {school_id}: {e}")
        # fallback: growth 5%
        current_students = df_school['y'].iloc[-1] if not df_school.empty else 0
        return current_students * 1.05

df['proyeksi_siswa_prophet'] = df['sekolah_id'].apply(lambda x: forecast_siswa_prophet(x, periods=1))
df['proyeksi_siswa_prophet'] = df['proyeksi_siswa_prophet'].round().astype(int)

# ===========================
# 6. Hitung Kebutuhan Guru Masa Depan
# ===========================
df['jumlah_guru_dibutuhkan'] = np.ceil(df['proyeksi_siswa'] / df['rasio_siswa_per_guru_ideal'])
df['kekurangan_guru'] = df['jumlah_guru_dibutuhkan'] - df['guru_ada_per_mapel']
df['kekurangan_guru'] = df['kekurangan_guru'].apply(lambda x: max(x, 0))

df['jumlah_guru_dibutuhkan_prophet'] = np.ceil(df['proyeksi_siswa_prophet'] / df['rasio_siswa_per_guru_ideal'])
df['kekurangan_guru_prophet'] = df['jumlah_guru_dibutuhkan_prophet'] - df['guru_ada_per_mapel']
df['kekurangan_guru_prophet'] = df['kekurangan_guru_prophet'].apply(lambda x: max(x,0))

def prioritas(kekurangan):
    if kekurangan >= 3:
        return 'Tinggi'
    elif kekurangan == 2:
        return 'Sedang'
    elif kekurangan == 1:
        return 'Rendah'
    else:
        return 'Cukup'

df['prioritas'] = df['kekurangan_guru'].apply(prioritas)
df['rekomendasi_penempatan'] = df['prioritas'].apply(
    lambda x: 'Rekrut baru' if x in ['Tinggi','Sedang'] else 'Tidak perlu'
)
df['prioritas_prophet'] = df['kekurangan_guru_prophet'].apply(prioritas)
df['rekomendasi_penempatan_prophet'] = df['prioritas_prophet'].apply(
    lambda x: 'Rekrut baru' if x in ['Tinggi','Sedang'] else 'Tidak perlu'
)

# ===========================
# 7. Agregasi Per Jenjang & Kecamatan
# ===========================
agg_kecamatan = df.groupby(['kecamatan','jenjang']).agg({
    'jumlah_siswa':'sum',
    'jumlah_guru_ada':'sum',
    'jumlah_guru_dibutuhkan':'sum',
    'kekurangan_guru':'sum'
}).reset_index()

agg_kecamatan_prophet = df.groupby(['kecamatan','jenjang']).agg({
    'jumlah_siswa':'sum',
    'jumlah_guru_ada':'sum',
    'jumlah_guru_dibutuhkan_prophet':'sum',
    'kekurangan_guru_prophet':'sum'
}).reset_index()

# ===========================
# 8. Export Hasil
# ===========================
os.makedirs('output', exist_ok=True)
df.to_csv('output/hasil_prediksi_guru_per_sekolah.csv', index=False)
agg_kecamatan.to_csv('output/hasil_prediksi_guru_per_kecamatan.csv', index=False)
df.to_csv('output/hasil_prediksi_guru_prophet_per_sekolah.csv', index=False)
agg_kecamatan_prophet.to_csv('output/hasil_prediksi_guru_prophet_per_kecamatan.csv', index=False)
print("Prediksi kebutuhan guru berhasil dihitung dan diekspor di folder 'output/'.")

# ===========================
# 9. Visualisasi Distribusi Guru & Simpan Chart
# ===========================
os.makedirs('charts', exist_ok=True)

# a) Kekurangan Guru per Kecamatan (5% growth)
plt.figure(figsize=(10,6))
sns.barplot(data=agg_kecamatan, x='kecamatan', y='kekurangan_guru', hue='jenjang')
plt.title('Kekurangan Guru per Kecamatan dan Jenjang')
plt.ylabel('Kekurangan Guru')
plt.xlabel('Kecamatan')
plt.xticks(rotation=45)
plt.legend(title='Jenjang')
plt.tight_layout()
plt.savefig('charts/kekurangan_guru_per_kecamatan.png')
plt.close()

# b) Kekurangan Guru per Kecamatan (Prophet)
plt.figure(figsize=(10,6))
sns.barplot(data=agg_kecamatan_prophet, x='kecamatan', y='kekurangan_guru_prophet', hue='jenjang')
plt.title('Kekurangan Guru per Kecamatan dan Jenjang (Prophet Forecast)')
plt.ylabel('Kekurangan Guru')
plt.xlabel('Kecamatan')
plt.xticks(rotation=45)
plt.legend(title='Jenjang')
plt.tight_layout()
plt.savefig('charts/kekurangan_guru_prophet_per_kecamatan.png')
plt.close()

# c) Distribusi Guru per Mata Pelajaran
plt.figure(figsize=(12,6))
sns.barplot(data=df, x='mata_pelajaran', y='guru_ada_per_mapel', hue='jenjang')
plt.title('Distribusi Guru per Mata Pelajaran dan Jenjang')
plt.ylabel('Jumlah Guru')
plt.xlabel('Mata Pelajaran')
plt.xticks(rotation=45)
plt.legend(title='Jenjang')
plt.tight_layout()
plt.savefig('charts/distribusi_guru_per_mapel.png')
plt.close()

# d) Heatmap Kekurangan Guru per Sekolah (5% growth)
pivot = df.pivot_table(index='sekolah_nama', columns='mata_pelajaran', values='kekurangan_guru', fill_value=0)
plt.figure(figsize=(12,8))
sns.heatmap(pivot, annot=True, cmap='Reds')
plt.title('Heatmap Kekurangan Guru per Sekolah dan Mata Pelajaran')
plt.ylabel('Sekolah')
plt.xlabel('Mata Pelajaran')
plt.tight_layout()
plt.savefig('charts/heatmap_kekurangan_guru.png')
plt.close()

# e) Heatmap Kekurangan Guru per Sekolah (Prophet)
pivot_prophet = df.pivot_table(index='sekolah_nama', columns='mata_pelajaran', values='kekurangan_guru_prophet', fill_value=0)
plt.figure(figsize=(12,8))
sns.heatmap(pivot_prophet, annot=True, cmap='Reds')
plt.title('Heatmap Kekurangan Guru per Sekolah dan Mata Pelajaran (Prophet Forecast)')
plt.ylabel('Sekolah')
plt.xlabel('Mata Pelajaran')
plt.tight_layout()
plt.savefig('charts/heatmap_kekurangan_guru_prophet.png')
plt.close()

print("Semua chart berhasil disimpan di folder 'charts/'")

```

## Ngulik v.2

```python
# ===========================
# Enhanced Prediksi Kebutuhan Guru - Practical Version
# ===========================

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import os
from io import StringIO
import warnings
warnings.filterwarnings('ignore')

# ===========================
# 2. Enhanced Sample Dataset (Lebih Realistis)
# ===========================
csv_file = 'dataset_guru.csv'

try:
    df = pd.read_csv(csv_file)
    print(f"Dataset '{csv_file}' berhasil dimuat.")
except FileNotFoundError:
    print(f"Dataset '{csv_file}' tidak ditemukan. Menggunakan enhanced sample dataset.")
    csv_data = StringIO("""
tahun,sekolah_id,sekolah_nama,kecamatan,desa,jenjang,jumlah_siswa,jumlah_guru_ada,mata_pelajaran,guru_ada_per_mapel,rasio_siswa_per_guru_ideal,status_sekolah,akreditasi,jarak_ke_kota,tingkat_ekonomi
2020,SDN001,SDN 1 Kecamatan A,Kecamatan A,Desa X,SD,100,8,Matematika,2,30,Negeri,B,5,Menengah
2021,SDN001,SDN 1 Kecamatan A,Kecamatan A,Desa X,SD,110,9,Matematika,2,30,Negeri,B,5,Menengah
2022,SDN001,SDN 1 Kecamatan A,Kecamatan A,Desa X,SD,120,10,Matematika,2,30,Negeri,B,5,Menengah
2020,SDN001,SDN 1 Kecamatan A,Kecamatan A,Desa X,SD,100,8,IPA,1,30,Negeri,B,5,Menengah
2021,SDN001,SDN 1 Kecamatan A,Kecamatan A,Desa X,SD,110,9,IPA,1,30,Negeri,B,5,Menengah
2022,SDN001,SDN 1 Kecamatan A,Kecamatan A,Desa X,SD,120,10,IPA,1,30,Negeri,B,5,Menengah
2020,SDN002,SDN 2 Kecamatan A,Kecamatan A,Desa Y,SD,130,10,Matematika,2,30,Negeri,A,3,Tinggi
2021,SDN002,SDN 2 Kecamatan A,Kecamatan A,Desa Y,SD,140,11,Matematika,3,30,Negeri,A,3,Tinggi
2022,SDN002,SDN 2 Kecamatan A,Kecamatan A,Desa Y,SD,150,12,Matematika,3,30,Negeri,A,3,Tinggi
2020,SDN002,SDN 2 Kecamatan A,Kecamatan A,Desa Y,SD,130,10,IPA,1,30,Negeri,A,3,Tinggi
2021,SDN002,SDN 2 Kecamatan A,Kecamatan A,Desa Y,SD,140,11,IPA,2,30,Negeri,A,3,Tinggi
2022,SDN002,SDN 2 Kecamatan A,Kecamatan A,Desa Y,SD,150,12,IPA,2,30,Negeri,A,3,Tinggi
2020,SMP001,SMP 1 Kecamatan B,Kecamatan B,Desa Z,SMP,180,6,Matematika,1,25,Negeri,B,8,Rendah
2021,SMP001,SMP 1 Kecamatan B,Kecamatan B,Desa Z,SMP,190,7,Matematika,2,25,Negeri,B,8,Rendah
2022,SMP001,SMP 1 Kecamatan B,Kecamatan B,Desa Z,SMP,200,8,Matematika,2,25,Negeri,B,8,Rendah
2020,SMP001,SMP 1 Kecamatan B,Kecamatan B,Desa Z,SMP,180,6,Bahasa Inggris,1,25,Negeri,B,8,Rendah
2021,SMP001,SMP 1 Kecamatan B,Kecamatan B,Desa Z,SMP,190,7,Bahasa Inggris,1,25,Negeri,B,8,Rendah
2022,SMP001,SMP 1 Kecamatan B,Kecamatan B,Desa Z,SMP,200,8,Bahasa Inggris,1,25,Negeri,B,8,Rendah
2020,SMP002,SMP 2 Kecamatan B,Kecamatan B,Desa W,SMP,160,8,Matematika,2,25,Swasta,C,12,Rendah
2021,SMP002,SMP 2 Kecamatan B,Kecamatan B,Desa W,SMP,170,8,Matematika,2,25,Swasta,C,12,Rendah
2022,SMP002,SMP 2 Kecamatan B,Kecamatan B,Desa W,SMP,180,9,Matematika,2,25,Swasta,C,12,Rendah
2020,SMP002,SMP 2 Kecamatan B,Kecamatan B,Desa W,SMP,160,8,Bahasa Inggris,1,25,Swasta,C,12,Rendah
2021,SMP002,SMP 2 Kecamatan B,Kecamatan B,Desa W,SMP,170,8,Bahasa Inggris,2,25,Swasta,C,12,Rendah
2022,SMP002,SMP 2 Kecamatan B,Kecamatan B,Desa W,SMP,180,9,Bahasa Inggris,2,25,Swasta,C,12,Rendah
""")
    df = pd.read_csv(csv_data)

# ===========================
# 3. Enhanced Data Cleaning & Feature Engineering
# ===========================
df.drop_duplicates(inplace=True)

# Basic cleaning
numeric_cols = ['jumlah_siswa', 'jumlah_guru_ada', 'guru_ada_per_mapel', 'rasio_siswa_per_guru_ideal', 'jarak_ke_kota']
for col in numeric_cols:
    df[col] = pd.to_numeric(df[col], errors='coerce')
df.fillna(0, inplace=True)

# Feature Engineering - data yang mudah didapat dari DAPODIK
df['rasio_siswa_per_guru'] = df['jumlah_siswa'] / df['guru_ada_per_mapel'].replace(0, 1)

# Kategorisasi berdasarkan karakteristik sekolah
def kategori_lokasi(jarak):
    if jarak <= 5:
        return 'Kota'
    elif jarak <= 10:
        return 'Pinggiran'
    else:
        return 'Terpencil'

df['kategori_lokasi'] = df['jarak_ke_kota'].apply(kategori_lokasi)

# Skor prioritas berdasarkan multiple factors
def hitung_skor_prioritas(row):
    skor = 0
    
    # Faktor akreditasi
    if row['akreditasi'] == 'A': skor += 3
    elif row['akreditasi'] == 'B': skor += 2
    else: skor += 1
    
    # Faktor lokasi
    if row['kategori_lokasi'] == 'Terpencil': skor += 3
    elif row['kategori_lokasi'] == 'Pinggiran': skor += 2
    else: skor += 1
    
    # Faktor ekonomi
    if row['tingkat_ekonomi'] == 'Rendah': skor += 3
    elif row['tingkat_ekonomi'] == 'Menengah': skor += 2
    else: skor += 1
    
    return skor

df['skor_prioritas_sekolah'] = df.apply(hitung_skor_prioritas, axis=1)

# ===========================
# 4. Enhanced Growth Forecasting
# ===========================

# Simple growth berdasarkan historical trend per sekolah
def hitung_growth_rate(school_data):
    """Hitung growth rate berdasarkan data historis per sekolah"""
    if len(school_data) < 2:
        return 0.03  # default 3% jika tidak ada data historis
    
    # Hitung rata-rata growth rate
    growth_rates = []
    for i in range(1, len(school_data)):
        if school_data.iloc[i-1]['jumlah_siswa'] > 0:
            growth = (school_data.iloc[i]['jumlah_siswa'] - school_data.iloc[i-1]['jumlah_siswa']) / school_data.iloc[i-1]['jumlah_siswa']
            growth_rates.append(growth)
    
    return np.mean(growth_rates) if growth_rates else 0.03

# Hitung growth rate per sekolah dan mata pelajaran
growth_data = []
for (school_id, mapel), group in df.groupby(['sekolah_id', 'mata_pelajaran']):
    group_sorted = group.sort_values('tahun')
    growth_rate = hitung_growth_rate(group_sorted)
    
    latest_data = group_sorted.iloc[-1].copy()
    latest_data['growth_rate'] = growth_rate
    growth_data.append(latest_data)

df_latest = pd.DataFrame(growth_data)

# Proyeksi dengan growth rate yang dihitung
df_latest['proyeksi_siswa_2023'] = (df_latest['jumlah_siswa'] * (1 + df_latest['growth_rate'])).round().astype(int)
df_latest['proyeksi_siswa_2024'] = (df_latest['proyeksi_siswa_2023'] * (1 + df_latest['growth_rate'])).round().astype(int)

# ===========================
# 5. Enhanced Teacher Demand Calculation
# ===========================

# Hitung kebutuhan guru untuk 2023 dan 2024
df_latest['guru_dibutuhkan_2023'] = np.ceil(df_latest['proyeksi_siswa_2023'] / df_latest['rasio_siswa_per_guru_ideal'])
df_latest['guru_dibutuhkan_2024'] = np.ceil(df_latest['proyeksi_siswa_2024'] / df_latest['rasio_siswa_per_guru_ideal'])

df_latest['kekurangan_guru_2023'] = (df_latest['guru_dibutuhkan_2023'] - df_latest['guru_ada_per_mapel']).clip(lower=0)
df_latest['kekurangan_guru_2024'] = (df_latest['guru_dibutuhkan_2024'] - df_latest['guru_ada_per_mapel']).clip(lower=0)

# Enhanced prioritization dengan multiple criteria
def prioritas_enhanced(row):
    kekurangan = row['kekurangan_guru_2023']
    skor_sekolah = row['skor_prioritas_sekolah']
    
    if kekurangan >= 3 and skor_sekolah >= 7:
        return 'Sangat Tinggi'
    elif kekurangan >= 2 and skor_sekolah >= 6:
        return 'Tinggi'
    elif kekurangan >= 1 and skor_sekolah >= 5:
        return 'Sedang'
    elif kekurangan >= 1:
        return 'Rendah'
    else:
        return 'Cukup'

df_latest['prioritas_enhanced'] = df_latest.apply(prioritas_enhanced, axis=1)

# Rekomendasi yang lebih spesifik
def rekomendasi_enhanced(row):
    prioritas = row['prioritas_enhanced']
    lokasi = row['kategori_lokasi']
    
    if prioritas == 'Sangat Tinggi':
        return f'Rekrut SEGERA + Insentif Khusus ({lokasi})'
    elif prioritas == 'Tinggi':
        return f'Rekrut Prioritas + Tunjangan ({lokasi})'
    elif prioritas == 'Sedang':
        return f'Rekrut Normal ({lokasi})'
    elif prioritas == 'Rendah':
        return 'Mutasi Internal'
    else:
        return 'Tidak Ada Aksi'

df_latest['rekomendasi_enhanced'] = df_latest.apply(rekomendasi_enhanced, axis=1)

# ===========================
# 6. Comprehensive Analysis & Insights
# ===========================

# Analisis per kategori
analysis_results = {}

# 1. Total kebutuhan guru
total_kekurangan_2023 = df_latest['kekurangan_guru_2023'].sum()
total_kekurangan_2024 = df_latest['kekurangan_guru_2024'].sum()

# 2. Breakdown per jenjang
kekurangan_per_jenjang = df_latest.groupby('jenjang').agg({
    'kekurangan_guru_2023': 'sum',
    'kekurangan_guru_2024': 'sum',
    'skor_prioritas_sekolah': 'mean'
}).round(2)

# 3. Breakdown per mata pelajaran
kekurangan_per_mapel = df_latest.groupby('mata_pelajaran').agg({
    'kekurangan_guru_2023': 'sum',
    'kekurangan_guru_2024': 'sum',
    'guru_ada_per_mapel': 'sum'
}).round(2)

# 4. Analisis prioritas
prioritas_count = df_latest['prioritas_enhanced'].value_counts()

# 5. Estimasi budget (asumsi gaji guru 5 juta/bulan)
gaji_per_guru_tahunan = 5000000 * 12
budget_2023 = total_kekurangan_2023 * gaji_per_guru_tahunan
budget_2024 = total_kekurangan_2024 * gaji_per_guru_tahunan

# Store results
analysis_results.update({
    'total_kekurangan_2023': total_kekurangan_2023,
    'total_kekurangan_2024': total_kekurangan_2024,
    'budget_2023': budget_2023,
    'budget_2024': budget_2024,
    'kekurangan_per_jenjang': kekurangan_per_jenjang,
    'kekurangan_per_mapel': kekurangan_per_mapel,
    'prioritas_count': prioritas_count
})

# ===========================
# 7. Enhanced Visualizations
# ===========================
os.makedirs('enhanced_output', exist_ok=True)
os.makedirs('enhanced_charts', exist_ok=True)

# Set style
plt.style.use('seaborn-v0_8')
colors = ['#2E8B57', '#FF6347', '#4169E1', '#FF8C00', '#9932CC']

# 1. Dashboard Overview - Multiple Subplots
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(16, 12))

# Kekurangan guru per jenjang
kekurangan_per_jenjang[['kekurangan_guru_2023', 'kekurangan_guru_2024']].plot(kind='bar', ax=ax1, color=colors[:2])
ax1.set_title('Kekurangan Guru per Jenjang (2023 vs 2024)', fontsize=12, fontweight='bold')
ax1.set_ylabel('Jumlah Guru')
ax1.legend(['2023', '2024'])
ax1.tick_params(axis='x', rotation=45)

# Prioritas distribution
prioritas_count.plot(kind='pie', ax=ax2, autopct='%1.1f%%', colors=colors)
ax2.set_title('Distribusi Prioritas Sekolah', fontsize=12, fontweight='bold')
ax2.set_ylabel('')

# Kekurangan per mata pelajaran
kekurangan_per_mapel['kekurangan_guru_2023'].plot(kind='bar', ax=ax3, color=colors[2])
ax3.set_title('Kekurangan Guru per Mata Pelajaran (2023)', fontsize=12, fontweight='bold')
ax3.set_ylabel('Jumlah Guru')
ax3.tick_params(axis='x', rotation=45)

# Growth rate distribution
df_latest['growth_rate'].hist(ax=ax4, bins=10, color=colors[3], alpha=0.7)
ax4.set_title('Distribusi Growth Rate Siswa', fontsize=12, fontweight='bold')
ax4.set_xlabel('Growth Rate')
ax4.set_ylabel('Frequency')

plt.tight_layout()
plt.savefig('enhanced_charts/dashboard_overview.png', dpi=300, bbox_inches='tight')
plt.close()

# 2. Heatmap Enhanced
plt.figure(figsize=(14, 10))
pivot_enhanced = df_latest.pivot_table(
    index=['sekolah_nama', 'kategori_lokasi'], 
    columns='mata_pelajaran', 
    values='kekurangan_guru_2023', 
    fill_value=0
)
sns.heatmap(pivot_enhanced, annot=True, cmap='Reds', fmt='g', cbar_kws={'label': 'Kekurangan Guru'})
plt.title('Heatmap Kekurangan Guru 2023 (Enhanced)', fontsize=14, fontweight='bold')
plt.ylabel('Sekolah (Kategori Lokasi)')
plt.xlabel('Mata Pelajaran')
plt.tight_layout()
plt.savefig('enhanced_charts/heatmap_enhanced.png', dpi=300, bbox_inches='tight')
plt.close()

# 3. Scatter Plot: Prioritas vs Growth Rate
plt.figure(figsize=(12, 8))
colors_priority = {'Sangat Tinggi': '#FF0000', 'Tinggi': '#FF8C00', 'Sedang': '#FFD700', 'Rendah': '#90EE90', 'Cukup': '#87CEEB'}
for priority in df_latest['prioritas_enhanced'].unique():
    subset = df_latest[df_latest['prioritas_enhanced'] == priority]
    plt.scatter(subset['growth_rate'], subset['kekurangan_guru_2023'], 
               label=priority, c=colors_priority[priority], alpha=0.7, s=100)

plt.xlabel('Growth Rate Siswa')
plt.ylabel('Kekurangan Guru 2023')
plt.title('Hubungan Growth Rate vs Kekurangan Guru (berdasarkan Prioritas)', fontsize=14, fontweight='bold')
plt.legend()
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.savefig('enhanced_charts/scatter_growth_vs_shortage.png', dpi=300, bbox_inches='tight')
plt.close()

# ===========================
# 8. Export Enhanced Results
# ===========================

# Export detailed results
df_latest.to_csv('enhanced_output/prediksi_guru_enhanced_detail.csv', index=False)
kekurangan_per_jenjang.to_csv('enhanced_output/analisis_per_jenjang.csv')
kekurangan_per_mapel.to_csv('enhanced_output/analisis_per_mapel.csv')

# Create executive summary
summary_report = f"""
=== EXECUTIVE SUMMARY - PREDIKSI KEBUTUHAN GURU ===

1. TOTAL KEBUTUHAN GURU:
   - 2023: {total_kekurangan_2023} guru
   - 2024: {total_kekurangan_2024} guru
   - Peningkatan: {total_kekurangan_2024 - total_kekurangan_2023} guru

2. ESTIMASI BUDGET:
   - 2023: Rp {budget_2023:,.0f} ({budget_2023/1000000000:.1f} Miliar)
   - 2024: Rp {budget_2024:,.0f} ({budget_2024/1000000000:.1f} Miliar)

3. PRIORITAS SEKOLAH:
{prioritas_count.to_string()}

4. TOP 3 JENJANG YANG BUTUH PERHATIAN:
{kekurangan_per_jenjang['kekurangan_guru_2023'].sort_values(ascending=False).head(3).to_string()}

5. TOP 3 MATA PELAJARAN YANG KEKURANGAN:
{kekurangan_per_mapel['kekurangan_guru_2023'].sort_values(ascending=False).head(3).to_string()}

6. REKOMENDASI UTAMA:
   - Fokus rekrutmen pada sekolah kategori 'Sangat Tinggi' dan 'Tinggi'
   - Berikan insentif khusus untuk penempatan di daerah terpencil
   - Pertimbangkan program mutasi internal untuk efisiensi
   - Monitor pertumbuhan siswa secara berkala untuk updating proyeksi
"""

with open('enhanced_output/executive_summary.txt', 'w', encoding='utf-8') as f:
    f.write(summary_report)

print("=== ENHANCED ANALYSIS COMPLETED ===")
print(f"Total kekurangan guru 2023: {total_kekurangan_2023}")
print(f"Total kekurangan guru 2024: {total_kekurangan_2024}")
print(f"Budget estimate 2023: Rp {budget_2023/1000000000:.1f} Miliar")
print(f"Files saved in: enhanced_output/ and enhanced_charts/")
print("\nCheck 'executive_summary.txt' for detailed insights!")
```
