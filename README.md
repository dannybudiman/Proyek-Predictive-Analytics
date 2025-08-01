## 🌼 Proyek Klasifikasi Gambar Bunga - Dicoding Submission

### 🎯 Deskripsi Singkat
Proyek ini merupakan bagian dari *Submission Akhir* kelas Belajar Fundamental Deep Learning Dicoding. Model dikembangkan untuk mengklasifikasi gambar bunga, difokuskan pada dua kelas terfilter: **Sunflower** dan **Tulip**, menggunakan TensorFlow dan Keras.

### 📁 Struktur Folder

```
saved_models_filtered/              # Folder berisi SavedModel, TFLite, dan TFJS
sample_data_filtered/              # Contoh subset gambar terfilter (Sunflower, Tulip)
saved_models_filtered_zip.zip      # Arsip ZIP dari model
sample_data_filtered_zip.zip       # Arsip ZIP data contoh
```

### 🛠️ Arsitektur Model
Model Sequential dengan layer:
- `Rescaling` 0-255 → 0-1
- 2x `Conv2D` + `MaxPooling`
- `Flatten` + `Dense` layer
- `Dropout` (opsional) + `Dense` output (softmax)

Model dilatih menggunakan class_weight untuk menangani imbalance.

### 📦 Format Model yang Disertakan
| Format        | Keterangan                              |
|---------------|------------------------------------------|
| **SavedModel** | Digunakan untuk TF Serving dan TFLite   |
| **TFLite**     | Format ringan untuk perangkat mobile    |
| **TFJS**       | Format untuk deployment via Web         |

### 📉 Evaluasi dan Akurasi
Model dievaluasi pada validation split (20%). Penggunaan class weighting dan normalisasi gambar membantu meningkatkan generalisasi.

### ✅ Cara Menjalankan Model
```python
# Load SavedModel
model = tf.keras.models.load_model("saved_models_filtered/flower_model_filtered_saved")

# Load TFLite model (example)
interpreter = tf.lite.Interpreter(model_path="saved_models_filtered/flower_model_filtered.tflite")
interpreter.allocate_tensors()
```

### 📥 Unduh Model
- ZIP file dapat diunduh dari tab **Output → Files** di Kaggle setelah training selesai.

### 📓 Menjalankan Notebook di Kaggle

Untuk menjalankan proyek ini di [Kaggle Notebook](https://www.kaggle.com/), ikuti langkah-langkah berikut:

1. **Upload Dataset ke Kaggle sebagai Dataset Pribadi:**
   - Buka halaman **[My Datasets](https://www.kaggle.com/datasets)**.
   - Klik tombol **"New Dataset"** dan upload folder `flower_images/` dari repositori ini.

2. **Buat Notebook Baru dan Attach Dataset:**
   - Buka tab **Code** → **"New Notebook"**.
   - Klik ikon **"Add data"** di sidebar kanan, lalu pilih dataset pribadi berisi `flower_images`.

3. **Clone Repositori GitHub (Opsional):**
   Untuk menyalin kode sumber dari GitHub:
   ```python
   !git clone https://github.com/dannybudiman/Proyek-Klasifikasi-Gambar.git
