# Eksperimen DBSCAN pada Data Meteorologi dengan Agregasi Temporal

## Identitas Kelompok

**Kelompok 6**

Anggota:
1. Nur Hikmah Salam
2. Rizal Alqadri
3. Naisya Nabila Pratiwi

## 1. Deskripsi Penelitian

Repositori ini berisi implementasi eksperimen penerapan algoritma Density-Based Spatial Clustering of Applications with Noise (DBSCAN) pada Data Meteorologi DKI Jakarta.

Penelitian ini bertujuan untuk menganalisis pengaruh agregasi temporal terhadap hasil clustering menggunakan algoritma DBSCAN.

Eksperimen dilakukan dengan membandingkan empat skenario agregasi temporal, yaitu tanpa agregasi, harian, tiga harian, dan mingguan.

Penelitian menggunakan parameter DBSCAN yang sama pada setiap skenario untuk mengetahui bagaimana perubahan resolusi waktu memengaruhi kualitas hasil clustering, jumlah cluster, persentase noise, dan waktu komputasi.

## 2. Tujuan Penelitian

Tujuan penelitian ini adalah:

1. Menerapkan algoritma DBSCAN pada data meteorologi.
2. Melakukan preprocessing terhadap data meteorologi.
3. Membandingkan hasil clustering pada empat skenario agregasi temporal.
4. Mengevaluasi kualitas clustering berdasarkan metrik evaluasi.
5. Menganalisis pengaruh agregasi temporal terhadap hasil clustering.

## 3. Sumber Dataset

Dataset yang digunakan adalah **Data Meteorologi Provinsi DKI Jakarta**.

**Sumber dataset:**  
https://data.go.id/dataset/dataset/data-meteorologi

**Produsen data:**  
Pemerintah Provinsi DKI Jakarta.

Dataset berisi pengukuran beberapa variabel meteorologi pada stasiun pengamatan di wilayah DKI Jakarta.

Variabel yang digunakan dalam penelitian:

| Variabel | Keterangan |
|---|---|
| grad | Radiasi matahari |
| temp_air | Temperatur udara |
| hum_air | Kelembapan udara |
| ff | Kecepatan angin |
| rain | Curah hujan |

Data yang digunakan dalam notebook terdiri dari 231.175 baris dan 8 kolom, dengan periode Januari 2024 sampai Agustus 2026.

Dataset disimpan dalam format CSV dan ditempatkan di dalam folder `data/` pada repositori.

## 4. Metodologi Penelitian

Penelitian dilakukan melalui tujuh tahapan utama.

### Tahap 1. Pengumpulan Data

Menggunakan dataset Data Meteorologi DKI Jakarta dalam format CSV.

### Tahap 2. Audit dan Eksplorasi Data

Melakukan pemeriksaan struktur data, identitas stasiun, validitas tanggal, duplikasi, missing value, nilai tidak wajar, statistik deskriptif, distribusi data, dan korelasi antarvariabel.

### Tahap 3. Preprocessing Data

Melakukan:
- Penyeragaman identitas stasiun.
- Pembentukan dan pemeriksaan tanggal.
- Penanganan duplikasi.
- Penanganan missing value.
- Pemeriksaan nilai tidak wajar.
- Pemilihan fitur.
- Transformasi log1p.
- Standardisasi Z-score per stasiun.

### Tahap 4. Agregasi Temporal

Penelitian membandingkan empat skenario:

| Skenario | Keterangan |
|---|---|
| S0 | Tanpa agregasi |
| S1 | Agregasi harian (1 hari) |
| S2 | Agregasi tiga harian (3 hari) |
| S3 | Agregasi mingguan (7 hari) |

Variabel `grad`, `temp_air`, `hum_air`, dan `ff` diagregasi menggunakan mean, sedangkan `rain` menggunakan sum.

Periode agregasi digunakan apabila memenuhi minimal 75% dari jumlah pengamatan acuan.

### Tahap 5. Penerapan DBSCAN

Algoritma DBSCAN diterapkan pada setiap skenario dan stasiun pengamatan.

Parameter yang digunakan:

- Epsilon (`eps`): 0.5
- Minimum Samples (`MinPts`): 5

Parameter dibuat sama pada seluruh skenario agar perbandingan berfokus pada pengaruh agregasi temporal.

### Tahap 6. Evaluasi Hasil Clustering

Evaluasi menggunakan:

1. Silhouette Score.
2. Davies-Bouldin Index.
3. Jumlah cluster.
4. Persentase noise.
5. Waktu komputasi.

Silhouette Score dan Davies-Bouldin Index dihitung pada data non-noise apabila terbentuk minimal dua cluster yang valid.

### Tahap 7. Analisis dan Perbandingan

Melakukan perbandingan hasil setiap skenario, menghitung perubahan terhadap baseline S0, menentukan skenario terbaik, serta menganalisis karakteristik cluster.

## 5. Struktur Repository

Struktur repositori GitHub disusun sebagai berikut:

```text
eksperimen-dbscan-meteorologi/
│
├── data/
│   ├── .gitkeep
│   └── Filedata_Data_Meteorologi.csv
│
├── hasil_eksperimen/
│   ├── .gitkeep
│   ├── delta_vs_baseline.csv
│   ├── evaluasi_per_skenario.csv
│   ├── evaluasi_per_stasiun.csv
│   ├── profil_cluster_S3.csv
│   └── tabel3_contoh_hasil_agregasi.csv
│
├── Eksperimen_DBSCAN_Agregasi_Temporal_revisi.ipynb
├── requirements.txt
├── README.md
└── .gitignore
```

## 6. Dependensi

Program dikembangkan menggunakan Python dengan beberapa library berikut:

- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook
- IPython

Seluruh dependensi yang diperlukan telah dicantumkan dalam file `requirements.txt`.

Instalasi seluruh dependensi dapat dilakukan menggunakan perintah:

```bash
pip install -r requirements.txt
```

## 7. Cara Menjalankan Program

### Persyaratan

Sebelum menjalankan program, pastikan perangkat telah memiliki:

- Python 3.
- Jupyter Notebook.
- Dataset Data Meteorologi dalam format CSV.
- Koneksi internet untuk mengunduh repositori dan menginstal dependensi.

### Langkah Menjalankan

**1. Clone repository**

Unduh repositori GitHub menggunakan perintah:

```bash
git clone https://github.com/tiwiyxz-web/eksperimen-dbscan-meteorologi.git
```

**2. Masuk ke direktori proyek**

```bash
cd eksperimen-dbscan-meteorologi
```

**3. Instal dependensi**

```bash
pip install -r requirements.txt
```

**4. Siapkan dataset CSV**

Pastikan file dataset `Filedata_Data_Meteorologi.csv` berada di dalam folder `data/` dengan struktur direktori:

```text
data/Filedata_Data_Meteorologi.csv
```

**5. Periksa konfigurasi lokasi dataset**

Pastikan konfigurasi `DATA_PATH` pada notebook telah sesuai dengan lokasi dataset yang digunakan.

Jika menggunakan lokasi relatif dari direktori utama repositori, format jalur yang digunakan adalah:

```python
DATA_PATH = "data/Filedata_Data_Meteorologi.csv"
```

**6. Jalankan Jupyter Notebook**

Gunakan perintah berikut untuk membuka Jupyter Notebook:

```bash
jupyter notebook
```

**7. Buka file notebook**

Pilih file:

`Eksperimen_DBSCAN_Agregasi_Temporal_revisi.ipynb`

**8. Jalankan seluruh cell**

Jalankan seluruh cell secara berurutan dari awal hingga akhir untuk melakukan pengumpulan dan preprocessing data, agregasi temporal, penerapan DBSCAN, evaluasi hasil clustering, serta menghasilkan file evaluasi secara otomatis.

Hasil eksperimen akan disimpan di dalam folder `hasil_eksperimen/`.

## 8. Output Penelitian

Hasil eksperimen disimpan secara otomatis dalam folder `hasil_eksperimen/`.

File hasil yang dihasilkan meliputi:

| Nama File | Keterangan |
|---|---|
| `tabel3_contoh_hasil_agregasi.csv` | Contoh hasil agregasi temporal |
| `evaluasi_per_stasiun.csv` | Hasil evaluasi clustering setiap stasiun |
| `evaluasi_per_skenario.csv` | Perbandingan hasil clustering setiap skenario |
| `delta_vs_baseline.csv` | Perubahan hasil dibandingkan skenario baseline S0 |
| `profil_cluster_S3.csv` | Profil cluster pada skenario S3 |

File tersebut digunakan untuk menganalisis hasil penerapan DBSCAN berdasarkan Silhouette Score, Davies-Bouldin Index, jumlah cluster, persentase noise, dan waktu komputasi.

Selain tabel evaluasi, visualisasi hasil eksperimen ditampilkan melalui notebook untuk membantu proses analisis dan perbandingan setiap skenario.

Seluruh file hasil evaluasi tersebut juga disertakan dalam repositori GitHub agar dapat diperiksa dan digunakan sebagai referensi dalam proses analisis penelitian.

## 9. Repository

**GitHub:**

https://github.com/tiwiyxz-web/eksperimen-dbscan-meteorologi

---

**Kelompok 6**

Penelitian ini disusun untuk keperluan akademik dan pembelajaran dalam penerapan data mining menggunakan algoritma DBSCAN pada data meteorologi.
