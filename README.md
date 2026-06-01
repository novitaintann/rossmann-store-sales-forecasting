# Perbandingan Metode SARIMA, RNN, LSTM, dan GRU untuk Peramalan Penjualan Harian Toko (Rossmann Store Sales)

Project ini merupakan implementasi dan analisis komparatif antara metode statistik klasik (SARIMA) dengan arsitektur Deep Learning (Vanilla RNN, LSTM, dan GRU) untuk memprediksi nilai penjualan harian toko. Dataset yang digunakan berasal dari kompetisi legendaris Kaggle: **Rossmann Store Sales**.

## 🚀 Link Akses Kodingan Lengkap (Kaggle)
Seluruh proses *Exploratory Data Analysis* (EDA), pembersihan data, visualisasi, hingga pelatihan model dilakukan di Kaggle Notebook menggunakan akselerator GPU. Anda dapat melihat dan menjalankan ulang kode lengkapnya di sini:
👉 **[Kaggle Notebook: SARIMA vs Deep Learning Rossmann Sales](https://www.kaggle.com/code/brwnber/sarima-vs-deep-learning-rossmann-sales)**

---

## 📌 Deskripsi Masalah & Dataset
Rossmann mengoperasikan lebih dari 3.000 toko di beberapa negara Eropa. Tantangan utama dari project ini adalah memprediksi penjualan harian (*Sales*) untuk 6 minggu ke depan. Peramalan yang akurat sangat krusial bagi manajemen toko untuk mengatur logistik, stok barang, manajemen karyawan, dan strategi promosi harian.

Dataset yang digunakan dalam project ini bersifat publik dan diambil dari kompetisi Kaggle resmi:
👉 **[Dataset Rossmann Store Sales di Kaggle](https://www.kaggle.com/competitions/rossmann-store-sales/data)**

**Fitur utama yang digunakan dalam pemodelan meliputi:**
- Data Transaksi: `Sales`, `Customers`, `Promo`, `StateHoliday`, `SchoolHoliday`.
- Data Profil Toko: `StoreType`, `Assortment`, `CompetitionDistance`..

---

## 🛠️ Alur Metodologi & Preprocessing
Untuk memastikan model *Deep Learning* dan statistik berjalan optimal, alur data diatur sebagai berikut:
1. **Pembersihan Data:** Menangani data toko yang tutup (`Open == 0`) karena secara logis penjualannya bernilai 0.
2. **Feature Engineering:** Mengekstrak komponen waktu (`Month`, `DayOfWeek`) untuk menangkap pola musiman harian dan bulanan.
3. **Data Splitting:** Pembagian data dilakukan secara kronologis (bukan acak) untuk menghindari *look-ahead bias* pada data deret waktu.
4. **Scaling:** Menggunakan `MinMaxScaler` untuk mentransformasikan data ke rentang 0-1 sebelum dimasukkan ke jaringan saraf tiruan (RNN/LSTM/GRU).
5. **Sliding Window:** Mengubah struktur data harian menjadi sekuens waktu (*time steps*) untuk melatih memori model *Deep Learning*.

---

## 📊 Hasil Perbandingan Model

Eksperimen dilakukan secara terfokus pada data **Toko 1** untuk membandingkan performa terbaik dari keempat arsitektur. Berikut adalah hasil evaluasi komparatif berdasarkan metrik *Root Mean Squared Error* (RMSE) dan *Mean Absolute Error* (MAE):

| Metode / Model | Nilai RMSE | Nilai MAE | Karakteristik & Performa Model |
| :--- | :---: | :---: | :--- |
| **SARIMA** | **233.04** | **175.76** | **Terbaik (Sangat Akurat).** Sangat kuat dalam menangkap pola musiman (*seasonality*) harian dan mingguan secara linear. |
| **Simple RNN** | **2069.94** | **1748.51** | Performa paling rendah. Mengalami kendala *short-term memory* sehingga kesulitan mempelajari sekuens waktu yang panjang. |
| **LSTM** | **592.51** | **447.53** | Performa cukup baik. Jauh lebih optimal dibanding Simple RNN karena mampu menjaga informasi jangka panjang (*long-term dependencies*). |
| **GRU** | **519.82** | **377.10** | **Terbaik di kategori Deep Learning.** Memiliki performa di atas LSTM dan RNN dengan error yang lebih ditekan serta komputasi yang lebih efisien. |

---

## 💡 Kesimpulan Utama
Berdasarkan hasil pengujian pada Toko 1, metode statistik klasik **SARIMA** secara mengejutkan memberikan performa terbaik dengan nilai error terkecil (RMSE: 233.04, MAE: 175.76) dibandingkan ketiga metode *Deep Learning*. 

Hal ini mengindikasikan beberapa poin penting:
1. Data penjualan harian Rossmann (khususnya Toko 1) memiliki pola musiman (*seasonality*) yang sangat kuat, linear, dan berulang secara konsisten, sehingga pemodelan berbasis statistik linear seperti SARIMA bekerja dengan sangat efisien.
2. Di kategori jaringan saraf tiruan (*Deep Learning*), **GRU** (RMSE: 519.82) terbukti lebih unggul dan efisien dibandingkan LSTM dan Simple RNN dalam menangani sekuens data deret waktu ini.
3. Pendekatan *Deep Learning* kemungkinan membutuhkan data yang lebih masif (multivariat dari banyak toko sekaligus) atau *hyperparameter tuning* yang lebih mendalam untuk bisa mengungguli efisiensi model statistik klasik pada pola yang sangat musiman ini.

---

## 📁 Struktur Repository
```text
├── notebooks/
│   └── UTS_Statistika_Lanjut.ipynb   # File eksperimen utama (Jupyter Notebook)
├── README.md                          # Dokumentasi ringkas project
└── requirements.txt                   # Daftar library pendukung project
