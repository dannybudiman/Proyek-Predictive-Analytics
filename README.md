# 📘 Laporan Proyek Machine Learning Terapan – Prediksi Churn Pelanggan

---

## 1. 🧭 Domain Proyek

**Latar Belakang:**

Dalam industri telekomunikasi, mempertahankan pelanggan lebih murah daripada mendapatkan pelanggan baru. Salah satu tantangan utama adalah **churn**, yaitu kondisi ketika pelanggan berhenti berlangganan layanan. Menurut [Harvard Business Review](https://hbr.org/2014/10/the-value-of-keeping-the-right-customers), meningkatkan retensi pelanggan sebesar 5% dapat meningkatkan profit hingga 25–95%.

Dengan memanfaatkan data historis pelanggan seperti jenis kontrak, lama berlangganan, dan tagihan bulanan, perusahaan dapat membangun sistem prediksi churn untuk mengidentifikasi pelanggan yang berisiko tinggi dan melakukan intervensi lebih awal.

---

## 2. 💼 Business Understanding

**Problem Statement:**

Bagaimana perusahaan dapat mengidentifikasi pelanggan yang berpotensi melakukan churn berdasarkan atribut layanan dan demografi, agar dapat merancang strategi retensi yang lebih efektif?

**Goals:**

- Membangun model klasifikasi yang mampu memprediksi apakah pelanggan akan churn atau tidak.
- Meningkatkan f1-score pada kelas “Yes” (churn) agar deteksi pelanggan yang akan keluar lebih akurat.
- Memberikan insight fitur-fitur yang paling berpengaruh terhadap churn.

**Solution Statement:**

Untuk mencapai tujuan tersebut, proyek ini mengusulkan dua pendekatan:

1. **Baseline Modeling**: Menggunakan Logistic Regression dan Random Forest sebagai pembanding awal.
2. **Improved Modeling**: Menggunakan XGBoost dengan teknik:
   - Hyperparameter tuning menggunakan GridSearchCV
   - Penanganan imbalance dengan SMOTE dan `scale_pos_weight`
   - Feature selection menggunakan SelectFromModel
   - Threshold tuning untuk optimasi recall dan f1-score

Seluruh solusi dievaluasi menggunakan metrik yang relevan dengan data imbalance, yaitu f1-score dan recall.

---

## 3. 📊 Data Understanding

**Sumber Dataset:**

- [Telco Customer Churn Dataset – Kaggle](https://www.kaggle.com/blastchar/telco-customer-churn)

**Informasi Dataset:**

- Jumlah baris: 7043
- Jumlah kolom: 21 fitur + 1 target (`Churn`)
- Format: CSV
- Target: `Churn` (Yes/No)

**Kondisi Data:**

- Terdapat missing value pada kolom `TotalCharges`
- Tidak ditemukan duplikat berdasarkan `customerID`
- Outlier terdeteksi pada `MonthlyCharges` dan `tenure` melalui boxplot

**Uraian Fitur:**

| Fitur             | Deskripsi                                                                 |
|-------------------|---------------------------------------------------------------------------|
| customerID        | ID unik pelanggan                                                         |
| gender            | Jenis kelamin                                                             |
| SeniorCitizen     | Status lansia (0 = tidak, 1 = ya)                                         |
| Partner           | Memiliki pasangan                                                         |
| Dependents        | Memiliki tanggungan                                                       |
| tenure            | Lama berlangganan (bulan)                                                 |
| PhoneService      | Menggunakan layanan telepon                                               |
| MultipleLines     | Menggunakan lebih dari satu jalur telepon                                 |
| InternetService   | Jenis layanan internet                                                    |
| OnlineSecurity    | Layanan keamanan online                                                   |
| OnlineBackup      | Layanan backup online                                                     |
| DeviceProtection  | Proteksi perangkat                                                        |
| TechSupport       | Dukungan teknis                                                           |
| StreamingTV       | Layanan streaming TV                                                      |
| StreamingMovies   | Layanan streaming film                                                    |
| Contract          | Jenis kontrak (Bulanan, 1 tahun, 2 tahun)                                |
| PaperlessBilling  | Tagihan tanpa kertas                                                      |
| PaymentMethod     | Metode pembayaran                                                         |
| MonthlyCharges    | Biaya bulanan                                                             |
| TotalCharges      | Total biaya selama berlangganan                                           |
| Churn             | Target (Yes = churn, No = tidak churn)                                    |

---

## 4. 🧹 Data Preparation

**Langkah-langkah yang dilakukan:**

1. **Handling Missing Values**: Imputasi nilai kosong pada `TotalCharges` menggunakan median.
2. **One-Hot Encoding**: Mengubah fitur kategorikal menjadi numerik agar kompatibel dengan algoritma ML.
3. **Feature Alignment**: Menyamakan fitur antara train dan test set setelah encoding.
4. **Label Encoding**: Mengubah target `Churn` menjadi 0 (No) dan 1 (Yes).
5. **Scaling**: Normalisasi fitur numerik menggunakan `StandardScaler`.
6. **SMOTE**: Oversampling kelas minoritas untuk mengatasi imbalance.
7. **Feature Selection**: Menggunakan XGBoost untuk memilih fitur penting dan mengurangi noise.

**Alasan:**

- SMOTE dan `scale_pos_weight` digunakan karena distribusi label sangat tidak seimbang.
- Feature selection membantu meningkatkan performa dan efisiensi model.
- Threshold tuning digunakan untuk meningkatkan recall pada kelas “Yes”.

---

## 5. ⚙️ Modeling

**Model yang Dibangun:**

- Logistic Regression
- Random Forest
- XGBoost (model utama)

**Parameter Tuning:**

- GridSearchCV dengan parameter:
  - `n_estimators`: [100, 200]
  - `max_depth`: [3, 6]
  - `learning_rate`: [0.05, 0.1]
  - `subsample`: [0.8, 1.0]
- Validasi: StratifiedKFold (5 fold)
- Skor evaluasi: f1-score

**Improvement:**

- Penambahan `scale_pos_weight` untuk memperkuat perhatian pada kelas churn
- Feature selection dengan SelectFromModel
- Threshold tuning dari 0.5 → 0.4 untuk meningkatkan recall

**Kelebihan XGBoost:**

- Mendukung data imbalance
- Cepat dan akurat
- Dapat digunakan untuk feature importance dan seleksi otomatis

---

## 6. 🧪 Evaluation

**Metrik Evaluasi:**

1. **Accuracy**: Proporsi prediksi benar dari seluruh data
2. **Precision**: Akurasi prediksi churn
3. **Recall**: Kemampuan model menangkap churn aktual
4. **F1-Score**: Harmoni antara precision dan recall
5. **Confusion Matrix**: Visual distribusi TP, FP, FN, TN

**Hasil Evaluasi Model Final:**
Accuracy: 0.7761
precision recall f1-score support No 0.86 0.83 0.84 1033 Yes 0.57 0.64 0.60 374


**Interpretasi:**

- Recall kelas “Yes” sebesar 64% menunjukkan model berhasil mengenali sebagian besar pelanggan churn.
- F1-score kelas “Yes” sebesar 0.60 menunjukkan keseimbangan antara recall dan precision.
- Confusion matrix menunjukkan distribusi prediksi yang cukup seimbang.

---
