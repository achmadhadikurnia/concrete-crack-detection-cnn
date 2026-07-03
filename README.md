# Concrete Surface Crack Detection (CNN)

*Read this in [Indonesian](README_id.md)*

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/achmadhadikurnia/concrete-crack-detection-cnn/blob/main/Proyek_S2_CNN_Keretakan_Beton.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains a Deep Learning implementation using a *Convolutional Neural Network* (CNN) with the **MobileNetV2** architecture to automatically detect cracks on concrete surfaces. This project aims to automate visual-based civil infrastructure inspection (e.g., using *drones*).

## 📊 Dataset Description
The dataset used is the **Surface Crack Detection Dataset** sourced from [Kaggle](https://www.kaggle.com/datasets/arunrk7/surface-crack-detection). The dataset consists of 40,000 images of size 227x227 pixels, evenly distributed into two classes:
- `Positive` (Cracked surface) - 20,000 images
- `Negative` (Intact/safe surface) - 20,000 images

## ⚙️ Model Architecture
The approach used is **Transfer Learning** using **MobileNetV2** (pre-trained on ImageNet). This architecture was chosen due to its high computational efficiency (low parameter count), making it ideal for deployment on *edge devices*.

* **Input Size:** 128 x 128 pixels
* **Base Model:** MobileNetV2 (Frozen weights)
* **Custom Head:** GlobalAveragePooling2D -> Dropout(0.2) -> Dense(1, Sigmoid)
* **Optimizer:** Adam (Learning Rate: 0.0005)
* **Loss Function:** Binary Crossentropy

## 🚀 Evaluation Results (Model Performance)

The model was evaluated using 8,000 previously unseen validation images (*Validation Set*). The results demonstrate highly precise classification performance.

### 1. Learning Curves (Accuracy & Loss)
The graphs below illustrate the model's convergence process during training. The *Validation Loss* curve steadily decreases and closely follows the *Training Loss*, proving that the model successfully avoids *Overfitting*.

![Accuracy and Loss Graph](img/5.%20Evaluation.png)

### 2. Confusion Matrix & Classification Report
For infrastructure inspection, the **Recall** metric for crack detection is highly critical (to minimize the danger of *False Negatives*). This model achieved near-perfect classification metrics.

| Class | Precision | Recall | F1-Score | Support |
| :--- | :---: | :---: | :---: | :---: |
| **Negative (Safe)** | 1.00 | 1.00 | 1.00 | 4080 |
| **Positive (Crack)** | 1.00 | 1.00 | 1.00 | 3920 |
| *Accuracy* | | | *1.00* | *8000* |
| *Macro Avg* | 1.00 | 1.00 | 1.00 | 8000 |
| *Weighted Avg* | 1.00 | 1.00 | 1.00 | 8000 |

![Confusion Matrix](img/6.%20Confusion%20Matrix.png)
*(Note: Out of 8,000 validation images, the model only misclassified 6 images).*

### 3. ROC Curve & AUC
The model's *robustness* in distinguishing between the two classes is visualized using the ROC curve. With an AUC score reaching **1.000**, the model is classified as a *perfect classifier* under the idealized conditions of this dataset.

![ROC Curve](img/7.%20ROC%20CURVE%20&%20AUC.png)

## 💻 Usage Instructions
1. Click the **Open In Colab** badge above to directly open the project file in Google Colab.
2. Ensure your *Runtime* is set to GPU (T4 GPU).
3. Prepare your Kaggle API Key (`kaggle.json`).
4. Run all code cells (*Run All*) sequentially.

## 📄 License
This project is licensed under the **MIT License**. Please see the [LICENSE](LICENSE) file for more information.
