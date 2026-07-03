# Concrete Surface Crack Detection (CNN)

*Baca dalam bahasa [Inggris](README.md)*

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/achmadhadikurnia/concrete-crack-detection-cnn/blob/main/Proyek_S2_CNN_Keretakan_Beton.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Repositori ini berisi implementasi Deep Learning menggunakan *Convolutional Neural Network* (CNN) dengan arsitektur **MobileNetV2** untuk mendeteksi secara otomatis keretakan pada permukaan beton. Proyek ini ditujukan untuk mengotomatisasi inspeksi infrastruktur sipil berbasis citra visual (seperti dari *drone*).

## 📊 Deskripsi Dataset
Dataset yang digunakan adalah **Surface Crack Detection Dataset** yang bersumber dari [Kaggle](https://www.kaggle.com/datasets/arunrk7/surface-crack-detection). Dataset ini terdiri dari 40.000 citra berukuran 227x227 piksel yang terbagi menjadi dua kelas seimbang:
- `Positive` (Permukaan retak) - 20.000 citra
- `Negative` (Permukaan utuh/aman) - 20.000 citra

## ⚙️ Arsitektur Model
Pendekatan yang digunakan adalah **Transfer Learning** menggunakan **MobileNetV2** (pre-trained pada ImageNet). Arsitektur ini dipilih karena memiliki efisiensi komputasi yang tinggi (jumlah parameter sedikit), sehingga sangat ideal untuk dideploy pada perangkat tepi (*edge devices*).

* **Input Size:** 128 x 128 piksel
* **Base Model:** MobileNetV2 (Frozen weights)
* **Custom Head:** GlobalAveragePooling2D -> Dropout(0.2) -> Dense(1, Sigmoid)
* **Optimizer:** Adam (Learning Rate: 0.0005)
* **Loss Function:** Binary Crossentropy

## 🚀 Hasil Evaluasi (Model Performance)

Model dievaluasi menggunakan 8.000 citra validasi (*Validation Set*) yang belum pernah dilihat sebelumnya. Hasil menunjukkan performa klasifikasi yang sangat presisi.

### 1. Learning Curves (Akurasi & Loss)
Grafik di bawah ini menunjukkan proses konvergensi model selama pelatihan. Kurva *Validation Loss* terus menurun dan stabil mengikuti *Training Loss*, membuktikan bahwa model terhindar dari *Overfitting*.

![Grafik Akurasi dan Loss](img/5.%20Evaluation.png)

### 2. Confusion Matrix & Classification Report
Untuk inspeksi infrastruktur, metrik **Recall** pada deteksi retakan sangat krusial (untuk meminimalkan bahaya *False Negatives*). Model ini mencatatkan nilai metrik klasifikasi mendekati sempurna.

| Kelas | Precision | Recall | F1-Score | Support |
| :--- | :---: | :---: | :---: | :---: |
| **Negative (Aman)** | 1.00 | 1.00 | 1.00 | 4080 |
| **Positive (Retak)** | 1.00 | 1.00 | 1.00 | 3920 |
| *Accuracy* | | | *1.00* | *8000* |
| *Macro Avg* | 1.00 | 1.00 | 1.00 | 8000 |
| *Weighted Avg* | 1.00 | 1.00 | 1.00 | 8000 |

![Confusion Matrix](img/6.%20Confusion%20Matrix.png)
*(Catatan: Dari 8.000 data uji, model hanya keliru mendeteksi 6 gambar saja).*

### 3. Kurva ROC & AUC
Tingkat ketangguhan (*robustness*) model dalam membedakan dua kelas divisualisasikan menggunakan kurva ROC. Dengan skor AUC mencapai **1.000**, model diklasifikasikan sebagai *perfect classifier* pada kondisi lingkungan dataset ini.

![ROC Curve](img/7.%20ROC%20CURVE%20&%20AUC.png)

## 💻 Cara Penggunaan
1. Klik *badge* **Open In Colab** di atas untuk langsung membuka file proyek ini di Google Colab.
2. Pastikan *Runtime* Anda diatur ke GPU (T4 GPU).
3. Siapkan API Key Kaggle Anda (`kaggle.json`).
4. Jalankan sel kode (*Run All*) secara berurutan.

## 📄 Lisensi
Proyek ini dilisensikan di bawah **MIT License**. Silakan lihat file [LICENSE](LICENSE) untuk informasi lebih lanjut.
