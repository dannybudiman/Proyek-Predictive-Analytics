# 📘 Predictive Analytics Project: Churn Classification

---

## 1. 🧭 Domain Proyek

**Latar Belakang:**

Churn merupakan fenomena ketika pelanggan berhenti menggunakan layanan atau produk suatu perusahaan. Dalam industri telekomunikasi, identifikasi pelanggan yang berisiko churn sangat krusial agar perusahaan dapat merancang strategi retensi.

Menurut studi oleh [Gartner Research](https://www.gartner.com/en/newsroom), rata-rata perusahaan kehilangan hingga 10% pelanggannya setiap tahun karena churn. Deteksi churn yang akurat dapat menurunkan biaya akuisisi pelanggan baru dan meningkatkan lifetime value pelanggan yang ada. Oleh karena itu, proyek ini bertujuan membangun model prediksi churn berbasis machine learning.

---

## 2. 💼 Business Understanding

**Problem Statement:**

Bagaimana cara memprediksi pelanggan yang berpotensi melakukan churn berdasarkan atribut demografis dan penggunaan layanan agar perusahaan dapat mengambil keputusan preventif?

**Goals:**

- Membangun model klasifikasi untuk memprediksi churn pelanggan secara akurat.
- Meningkatkan f1-score pada kelas churn (label “Yes”) agar deteksi pelanggan yang akan keluar lebih efektif.

**Solution Statement:**

Proyek ini mengusulkan dua pendekatan sebagai solusi:

1. **Baseline Modeling:** Membangun model Logistic Regression dan Random Forest sebagai pembanding awal.
2. **Advanced Modeling (Improved):** Menerapkan algoritma XGBoost disertai:
   - Hyperparameter tuning menggunakan GridSearchCV
   - Penanganan imbalance data dengan SMOTE dan scale_pos_weight
   - Feature selection menggunakan SelectFromModel
   - Threshold tuning untuk mengoptimalkan recall dan f1-score pada kelas “Yes”

Seluruh solusi dievaluasi menggunakan metrik yang sesuai dengan konteks data imbalance dan mendukung tujuan bisnis.

---

## 3. 📊 Data Understanding

**Informasi Dataset:**

- Jumlah fitur: >20 kolom (numerik dan kategorikal)
- Jumlah observasi: 7043 data pelanggan
- Label target: `Churn` (Yes/No)

**Sumber Dataset:**

- [Kaggle - Telco Customer Churn Dataset](https://www.kaggle.com/blastchar/telco-customer-churn)

**Deskripsi Variabel Kunci:**

- `customerID`: ID pelanggan unik
- `gender`, `SeniorCitizen`, `Partner`, `Dependents`: demografi
- `tenure`, `MonthlyCharges`, `TotalCharges`: perilaku penggunaan
- `Contract`, `PaymentMethod`, `InternetService`: jenis layanan
- `Churn`: Target label (Yes/No)

---

## 4. 🧹 Data Preparation

**Teknik dan Urutan yang Dilakukan:**

1. **Train-test split (stratified)**: Menjaga distribusi churn di data latih dan uji.
2. **One-hot encoding**: Mengubah variabel kategorikal menjadi numerik agar dapat digunakan oleh algoritma.
3. **Sinkronisasi fitur**: Menyelaraskan dimensi train dan test dengan `.align(...)`.
4. **Label Encoding**: Mengonversi target `Churn` menjadi 0 dan 1.
5. **Standard Scaling**: Normalisasi fitur numerik untuk algoritma yang sensitif terhadap skala.
6. **SMOTE**: Mengatasi imbalance dengan oversampling kelas “Yes” secara sintetis.
7. **Feature Selection**: Menggunakan XGBoost untuk memilih fitur relevan saja.

**Alasan Tahapan:**

- **Scaling** membantu algoritma seperti Logistic Regression dan XGBoost berkonvergensi lebih cepat.
- **SMOTE** meningkatkan f1-score dan recall pada kelas minoritas.
- **Feature selection** mengurangi kompleksitas dan meningkatkan fokus pada atribut bermakna.

---

## 5. ⚙️ Modeling

**Model yang Dibangun:**

- Baseline:
  - Logistic Regression
  - Random Forest
- Model Utama:
  - XGBoost (Extreme Gradient Boosting)

**Parameter dan Tahapan:**

- Tuning XGBoost:
  - `GridSearchCV` dengan `StratifiedKFold`
  - Parameter grid: `n_estimators`, `max_depth`, `learning_rate`, `subsample`
  - Penanganan imbalance dengan `scale_pos_weight`

**Improvement yang Dilakukan:**

- Pemilihan fitur dengan `SelectFromModel(XGBoost)`
- Evaluasi probabilistik dengan threshold tuning (default 0.5 → disesuaikan ke 0.4)
- Fokus peningkatan pada f1-score dan recall kelas “Yes”

**Alasan Pemilihan XGBoost:**

- Menghasilkan performa terbaik dalam hal f1-score dan recall pada kelas churn setelah proses tuning dan balancing.
- Mendukung eksplorasi feature importance dan seleksi otomatis.
- Kompatibel dengan data besar dan tidak terlalu rentan terhadap noise hasil one-hot encoding.

---

## 6. 🧪 Evaluation

**Metrik Evaluasi:**

1. **Accuracy**: Proporsi prediksi yang benar dari seluruh data.
2. **Precision**: Kemampuan model memprediksi churn dengan akurat.
3. **Recall**: Kemampuan model menangkap pelanggan yang benar-benar churn.
4. **F1-Score**: Harmoni antara precision dan recall (penting untuk kelas minoritas).
5. **Confusion Matrix**: Visualisasi distribusi TP, FP, FN, TN
6. *(Opsional)*: ROC Curve dan Threshold Optimization

**Hasil Model Final (Threshold = 0.4):**


**Interpretasi:**

- F1-score kelas “Yes” sebesar 0.60 menunjukkan bahwa model cukup berhasil mendeteksi pelanggan churn.
- Recall kelas “Yes” sebesar 64% mengindikasikan sekitar 2/3 churn berhasil dikenali.
- Confusion Matrix menunjukkan model menyeimbangkan prediksi antar kelas dengan cukup baik.

**Formula:**

- `Recall = TP / (TP + FN)`
- `Precision = TP / (TP + FP)`
- `F1 = 2 * (Precision * Recall) / (Precision + Recall)`

Model memberikan trade-off yang sehat antara menghindari false positive dan berhasil menangkap churn aktual — cocok untuk intervensi bisnis.

---

