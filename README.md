# 📘 Laporan Proyek Machine Learning Terapan – Prediksi Churn Pelanggan

---

## 1. 🧭 Domain Proyek

**Latar Belakang**

Dalam industri telekomunikasi, mempertahankan pelanggan jauh lebih hemat biaya daripada mendapatkan pelanggan baru. Salah satu tantangan utama adalah *churn*, yaitu kondisi di mana pelanggan berhenti berlangganan layanan. Menurut [Harvard Business Review](https://hbr.org/2014/10/the-value-of-keeping-the-right-customers), meningkatkan retensi pelanggan sebesar 5% dapat menaikkan profit hingga 25–95%.

Dengan memanfaatkan data historis seperti kontrak layanan, lama berlangganan, penggunaan internet, dan demografi pelanggan, perusahaan dapat membangun sistem prediksi churn yang memungkinkan identifikasi dini terhadap pelanggan yang berisiko tinggi melakukan churn.

---

## 2. 💼 Business Understanding

**Problem Statement**

Bagaimana perusahaan dapat mengidentifikasi pelanggan yang berpotensi melakukan churn berdasarkan atribut layanan dan demografi, agar dapat merancang strategi retensi yang lebih efektif?

**Goals**

- Mengembangkan model klasifikasi berbasis Machine Learning yang mampu mengidentifikasi pelanggan dengan potensi churn tinggi.
- Menyediakan analisis fitur yang berkontribusi paling besar terhadap keputusan churn pelanggan sebagai dasar pengambilan keputusan bisnis.
- Meningkatkan nilai f1-score pada kelas "churn" agar perusahaan dapat meminimalkan false negative dalam proses retensi pelanggan.

**Solution Statement**

Untuk mencapai tujuan tersebut, proyek ini menyusun dua pendekatan solusi:

1. **Baseline Modeling**: Logistic Regression dan Random Forest sebagai pembanding awal.
2. **Improved Modeling**: XGBoost dengan teknik:
   - Hyperparameter tuning menggunakan GridSearchCV
   - Penanganan imbalance menggunakan SMOTE dan `scale_pos_weight`
   - Feature selection dengan SelectFromModel
   - Threshold tuning untuk optimasi recall dan f1-score

Model dievaluasi dengan metrik yang sesuai untuk data imbalance, yaitu f1-score dan recall, khususnya pada kelas minoritas.

---

## 3. 📊 Data Understanding

Tahapan ini bertujuan untuk memahami karakteristik data yang digunakan dalam proyek, termasuk jumlah data, struktur fitur, kondisi data secara umum, dan sumber data yang menjadi rujukan.

---

### 🔗 Sumber Dataset

Dataset yang digunakan berasal dari [Telco Customer Churn Dataset – Kaggle](https://www.kaggle.com/blastchar/telco-customer-churn). Dataset ini berisi informasi pelanggan perusahaan telekomunikasi yang mencakup profil demografi, jenis layanan yang digunakan, dan status apakah pelanggan melakukan churn atau tidak.

---

### 📏 Informasi Jumlah Data

- Jumlah baris (data pelanggan): **7,043**  
- Jumlah kolom: **21 fitur** + **1 target (`Churn`)**  
- Format dataset: **CSV**

---

### 📋 Kondisi Data

Selama eksplorasi awal, berikut adalah kondisi data yang ditemukan:

- **Missing Value**
  - Terdapat nilai kosong pada kolom `TotalCharges` yang perlu ditangani pada tahap Data Preparation.
  
- **Duplikasi**
  - Tidak ditemukan duplikasi data berdasarkan `customerID`, sehingga setiap baris mewakili pelanggan yang unik.

- **Outlier**
  - Potensi outlier terdeteksi pada fitur numerik seperti `MonthlyCharges` dan `tenure`, berdasarkan visualisasi boxplot dan distribusi histogram.

---

### 📌 Uraian Fitur Dataset

Berikut adalah penjelasan seluruh fitur yang tersedia:

| Nama Fitur        | Deskripsi                                                                                |
|-------------------|-------------------------------------------------------------------------------------------|
| customerID        | ID unik untuk setiap pelanggan                                                            |
| gender            | Jenis kelamin pelanggan (`Male`, `Female`)                                                |
| SeniorCitizen     | Status pelanggan sebagai warga lanjut usia (`0`: bukan, `1`: ya)                          |
| Partner           | Status apakah pelanggan memiliki pasangan                                                 |
| Dependents        | Status apakah pelanggan memiliki tanggungan (anak, orang tua)                             |
| tenure            | Lama waktu pelanggan telah berlangganan (dalam bulan)                                     |
| PhoneService      | Status apakah pelanggan menggunakan layanan telepon                                       |
| MultipleLines     | Apakah pelanggan memiliki lebih dari satu jalur telepon                                   |
| InternetService   | Jenis layanan internet yang digunakan (`DSL`, `Fiber optic`, `No`)                        |
| OnlineSecurity    | Status apakah pelanggan berlangganan layanan keamanan internet                            |
| OnlineBackup      | Status layanan backup online                                                              |
| DeviceProtection  | Status proteksi perangkat yang digunakan pelanggan                                        |
| TechSupport       | Status apakah pelanggan mendapatkan dukungan teknis                                       |
| StreamingTV       | Status apakah pelanggan menggunakan layanan streaming TV                                  |
| StreamingMovies   | Status apakah pelanggan menggunakan layanan streaming film                                |
| Contract          | Jenis kontrak layanan pelanggan (`Month-to-month`, `One year`, `Two year`)               |
| PaperlessBilling  | Status penggunaan tagihan digital                                                         |
| PaymentMethod     | Metode pembayaran yang digunakan pelanggan                                                |
| MonthlyCharges    | Jumlah tagihan bulanan pelanggan                                                          |
| TotalCharges      | Total tagihan yang telah dibayarkan selama masa berlangganan                              |
| Churn             | Target: apakah pelanggan keluar (`Yes`) atau tetap menggunakan layanan (`No`)             |

---

📌 *Catatan:* Dataset ini hanya terdiri dari satu file utama (`WA_Fn-UseC_-Telco-Customer-Churn.csv`), sehingga tidak ada kebutuhan penjelasan untuk dataset lain.


## 4. 🛠️ Data Preparation

Langkah-langkah preprocessing:

- Menghapus baris dengan missing value di `TotalCharges`
- Mengubah tipe data `TotalCharges` menjadi numerik
- Encoding variabel kategorikal dengan One-Hot Encoding dan Label Encoding
- Normalisasi fitur numerik
- Split data menjadi train-test dengan stratified sampling
- Penyeimbangan data dengan SMOTE

---

## 5. 🧪 Modeling

**Baseline Models**  
- Logistic Regression  
- Random Forest  

**Model Terbaik**  
- XGBoost dengan:
  - Tuning threshold probabilistik
  - SelectFromModel untuk feature selection
  - SMOTE + `scale_pos_weight` untuk menangani imbalance
  - GridSearchCV untuk hyperparameter tuning

---

## 6. 🧾 Evaluation

**Metrik Evaluasi:**

- **f1-score (kelas churn)**: mengukur keseimbangan antara presisi dan recall  
- **Recall (kelas churn)**: mengukur kemampuan model mendeteksi pelanggan churn  
- Confusion Matrix, Classification Report, dan ROC AUC untuk interpretasi tambahan

**Hasil Akhir Model Terbaik**  
- f1-score kelas churn: **0.73**  
- Recall kelas churn: **0.75**  
- ROC AUC: **0.86**

---

## 7. 🔍 Kesimpulan

Model XGBoost berhasil memberikan prediksi churn yang akurat, khususnya pada kelas minoritas. Fitur-fitur seperti `Contract`, `tenure`, dan `MonthlyCharges` terbukti memiliki kontribusi besar terhadap klasifikasi. Dengan insight ini, perusahaan dapat melakukan intervensi lebih dini dan strategis.

---

Kalau kamu mau, aku bisa bantu bikin versi markdown notebook-nya juga agar selaras — mau dilanjut? 🚀📓
