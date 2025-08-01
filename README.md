# 📊 Submission Proyek Predictive Analytics – Telco Customer Churn

## 🧭 Latar Belakang

Customer churn adalah masalah kritis bagi perusahaan telekomunikasi. Kehilangan pelanggan berdampak langsung pada pendapatan dan biaya akuisisi pelanggan baru bisa jauh lebih besar dibanding mempertahankan pelanggan lama (Frederick Reichheld, Bain & Company). Dengan memanfaatkan data historis, kita dapat membangun model prediksi yang membantu tim bisnis melakukan intervensi sebelum pelanggan benar-benar churn.

**Referensi:**
- [Harvard Business Review – The Value of Keeping the Right Customers](https://hbr.org/2014/10/the-value-of-keeping-the-right-customers)
- [IBM – Telco Churn Prediction Use Case](https://www.ibm.com/cloud/learn/telco-churn)

---

## 🔍 Klarifikasi Masalah

**Problem Statement:**
Bagaimana cara memprediksi pelanggan yang kemungkinan akan berhenti berlangganan?

**Goals:**
1. Membangun model machine learning untuk memprediksi churn.
2. Menyediakan insight bagi strategi retensi pelanggan.

---

## 📂 Informasi Dataset

- **Sumber:** [Kaggle Dataset – Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- **Versi GitHub:** [CSV File GitHub](https://raw.githubusercontent.com/dannybudiman/Proyek-Predictive-Analytics/main/WA_Fn-UseC_-Telco-Customer-Churn.csv)
- **Jumlah Baris:** 7043
- **Format:** CSV

### 🔎 Daftar Fitur:

| Fitur           | Deskripsi                                       |
|------------------|------------------------------------------------|
| `customerID`     | ID unik pelanggan                              |
| `gender`         | Jenis kelamin                                  |
| `SeniorCitizen`  | Status lansia                                  |
| `tenure`         | Lama berlangganan (bulan)                      |
| `Contract`       | Jenis kontrak                                  |
| `MonthlyCharges` | Biaya bulanan                                  |
| `TotalCharges`   | Total biaya selama langganan                   |
| `Churn`          | Target variabel – apakah pelanggan churn atau tidak |

---

## 🛠️ Teknik Data Preparation

1. Konversi nilai non-numerik di `TotalCharges`
2. Hapus missing value
3. Encoding semua fitur kategorikal menggunakan `LabelEncoder`
4. Scaling fitur numerik menggunakan `StandardScaler`
5. Split data menjadi training dan testing

---

## 🤖 Modeling

- Algoritma: `RandomForestClassifier`
- Parameter: default + `random_state=42`

Langkah:
1. Training model
2. Prediksi testing set
3. Evaluasi model

Alternatif: bisa menggunakan `XGBoost` untuk boosting atau `GridSearchCV` untuk tuning parameter.

---

## 📈 Evaluasi & Metrik

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix

Evaluasi dilakukan dengan `classification_report()` dan `confusion_matrix()` dari scikit-learn. Metrik seperti Recall dan F1 Score sangat relevan untuk kasus imbalance seperti churn prediction.
