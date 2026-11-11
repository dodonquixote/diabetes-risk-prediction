# Laporan Proyek Machine Learning - Prediksi Risiko Diabetes

## 1. **Domain Proyek**

### 1.1 **Latar Belakang**
Diabetes adalah salah satu penyakit kronis yang paling umum di dunia dengan prevalensi yang terus meningkat. Deteksi dini risiko diabetes sangat penting untuk pencegahan dan pengelolaan yang efektif. Proyek ini bertujuan untuk mengembangkan model machine learning untuk memprediksi risiko diabetes berdasarkan sejumlah faktor seperti usia, indeks massa tubuh (BMI), kadar glukosa darah, kadar HbA1c, serta riwayat hipertensi dan penyakit jantung.

### 1.2 **Pentingnya Proyek**
Proyek ini bertujuan untuk memberikan alat prediktif berbasis data yang dapat digunakan oleh tenaga medis untuk merencanakan pengelolaan kesehatan yang lebih baik dan memantau kesehatan masyarakat.

### 1.3 **Sumber Data**
Pada proyek ini, dataset yang digunakan dihasilkan menggunakan fungsi **generate_sample_diabetes_data()**, yang menghasilkan 10.000 baris data dengan 9 fitur. Data sintetis ini meliputi variabel seperti **age**, **gender**, **bmi**, **hypertension**, **heart_disease**, **smoking_history**, **HbA1c_level**, **blood_glucose_level**, dan **diabetes** sebagai target variabel.

**Sumber Data**: Dataset sintetis yang dihasilkan secara internal, bukan dari Kaggle.

---

## 2. **Business Understanding**

### 2.1 **Problem Statements**
Masalah yang ingin diselesaikan dalam proyek ini adalah:
- Bagaimana membangun model prediktif yang dapat mengklasifikasikan risiko diabetes pada individu?

### 2.2 **Goals**
Tujuan dari proyek ini adalah:
- Mengembangkan model prediktif dengan tingkat akurasi minimal 85% untuk mengklasifikasikan apakah seseorang berisiko diabetes atau tidak.

### 2.3 **Solution Statements**
Untuk mencapai tujuan di atas, kami mengusulkan beberapa solusi:
1. Mengembangkan dan membandingkan beberapa model machine learning, termasuk **Logistic Regression**, **Random Forest**, **XGBoost**, **SVM**, dan **Gradient Boosting**.
2. Melakukan evaluasi terhadap setiap model menggunakan metrik evaluasi yang sesuai seperti akurasi, precision, recall, dan F1-score.
3. Memilih model terbaik berdasarkan hasil evaluasi yang diperoleh dari data testing.

---

## 3. **Data Understanding**

### 3.1 **Deskripsi Dataset**
Dataset yang digunakan dalam proyek ini diambil dari [Kaggle](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset) memiliki jumlah baris 100.000 (20.000 yang digunakan) dan 9 kolom. Dengan variabel-variabel sebagai berikut:
- **Age**: Usia (tahun)
- **Gender**: Jenis kelamin
- **BMI**: Indeks Massa Tubuh
- **Hypertension**: Riwayat hipertensi (1 = Ya, 0 = Tidak)
- **Heart Disease**: Riwayat penyakit jantung (1 = Ya, 0 = Tidak)
- **Smoking History**: Riwayat merokok
- **HbA1c Level**: Kadar HbA1c
- **Blood Glucose Level**: Kadar glukosa darah
- **Diabetes**: Target variabel, 1 = Diabetes, 0 = Tidak Diabetes

### 3.2 **Analisis Data**
- **Missing Value**: Tidak ada nilai yang hilang pada dataset.
- **Outlier**: Terdapat beberapa outlier pada variabel **Age** dan **Height**, namun tidak dihapus karena masih dalam rentang yang relevan untuk analisis.
- **Distribusi Kategorikal**: Sebagian besar data untuk **Gender** seimbang antara perempuan dan laki-laki (50.2% perempuan dan 49.8% laki-laki). Variabel **Smoking History** menunjukkan ketidakseimbangan, dengan lebih banyak non-perokok.

---

## 4. **Data Preparation**

### 4.1 **Feature Engineering**
Beberapa teknik feature engineering yang dilakukan:
- **BMI Category**: Mengklasifikasikan BMI ke dalam kategori sesuai standar WHO.
- **HbA1c Category**: Mengklasifikasikan kadar HbA1c menjadi kategori normal, prediabetes, dan diabetes.
- **Blood Glucose Category**: Mengklasifikasikan kadar glukosa darah menjadi kategori normal, prediabetes, dan diabetes.
- **Age Category**: Mengklasifikasikan usia menjadi kelompok (young, middle_aged, senior, elderly).
- **Risk Scores**: Menghitung skor risiko metabolik dan kardiovaskular berdasarkan BMI, HbA1c, blood glucose, hipertensi, dan penyakit jantung.
- **Interaction Features**: Menghitung interaksi antara fitur-fitur seperti **bmi_glucose_interaction** dan **age_bmi_interaction**.
- **Smoking Risk Score**: Mengubah kategori smoking_history ke skor biner/tingkat risiko (0–3).
- **hba1c_glucose_ratio**: Rasio antara HbA1c level dan blood glucose level, untuk menilai hubungan antara keduanya.

### 4.2 **Pembagian Data**
Dataset dibagi menjadi data pelatihan (80%) dan data pengujian (20%) menggunakan **train_test_split**.

### 4.3 **Preprocessing**
- **StandardScaler** digunakan untuk standarisasi fitur numerik.
- **OneHotEncoder** digunakan untuk encoding variabel kategorikal seperti **Gender** dan **Smoking History**.
- **SimpleImputer** digunakan untuk menangani missing values pada variabel numerik dan kategorikal.

---

## 5. **Modeling**

### 5.1 **Algoritma yang Digunakan**
1. **Logistic Regression**: Model yang menggunakan fungsi sigmoid untuk menghitung probabilitas dari masing-masing kelas.
2. **Random Forest**: Model berbasis ensemble yang menggunakan banyak pohon keputusan untuk menghasilkan prediksi.
3. **XGBoost**: Model boosting yang menggunakan gradient descent untuk memperbaiki kesalahan model sebelumnya.
4. **SVM**: Model yang mencari hyperplane terbaik untuk memisahkan kelas-kelas data.
5. **Gradient Boosting**: Model berbasis boosting yang memperbaiki kesalahan model sebelumnya dengan memperhatikan gradien.

### 5.2 **Penjelasan Cara Kerja Algoritma**
- **Logistic Regression**: Model ini mengestimasi probabilitas kelas menggunakan fungsi sigmoid dan memprediksi berdasarkan probabilitas tersebut.
- **Random Forest**: Algoritma ini membangun banyak pohon keputusan secara acak dengan menggunakan bootstrap sampling dan subset fitur, kemudian menggabungkan hasil voting untuk menghasilkan prediksi.
- **XGBoost**: Model ini menggunakan boosting untuk memperbaiki kesalahan model sebelumnya dan mengoptimalkan prediksi dengan teknik gradient descent.
- **SVM**: Model ini mencoba menemukan hyperplane yang memisahkan dua kelas dengan margin terbesar.
- **Gradient Boosting**: Ini adalah algoritma boosting yang membangun model secara bertahap dengan memperbaiki kesalahan model sebelumnya.

### 5.3 **Parameter yang Digunakan**
- **Logistic Regression**: `random_state=42`, `max_iter=1000`
- **Random Forest**: `random_state=42`, `n_estimators=100`
- **XGBoost**: `random_state=42`, `eval_metric='logloss'`
- **SVM**: `random_state=42`, `probability=True`
- **Gradient Boosting**: `random_state=42`

---

## 6. **Evaluation**

### 6.1 **Metrik Evaluasi**
1. **Akurasi**: Mengukur proporsi prediksi yang benar.
2. **Precision**: Mengukur proporsi prediksi positif yang benar.
3. **Recall**: Mengukur kemampuan model dalam mendeteksi hasil positif.
4. **F1-Score**: Mengukur keseimbangan antara precision dan recall.
5. **ROC AUC**: Mengukur kemampuan model dalam membedakan kelas positif dan negatif.

### 6.2 **Hasil Evaluasi**
Berikut adalah hasil evaluasi untuk setiap model yang dibandingkan:

| Model                | Accuracy  | Precision | Recall | F1-Score | ROC AUC |
|----------------------|-----------|-----------|--------|----------|---------|
| **Logistic Regression** | 96%       | 89.6%     | 65.5%  | 75.7%    | 96.8%   |
| **Random Forest**      | 97.1%     | 96.3%     | 68.4%  | 80.0%    | 96.7%   |
| **Gradient Boosting**  | 97.3%     | 99.2%     | 69.0%  | 81.4%    | 97.7%   |
| **SVM**                | 96.2%     | 95.3%     | 58.8%  | 72.7%    | 91.6%   |
| **XGBoost**            | 96.9%     | 90.6%     | 70.8%  | 79.5%    | 97.3%   |

---

## 7. **Kesimpulan**

### 7.1 **Pencapaian Tujuan**
- Model **Gradient Boosting** berhasil mencapai akurasi lebih dari 85%, dengan hasil akurasi mencapai 97% pada data pengujian.
- Model ini memberikan solusi optimal untuk memprediksi risiko diabetes.

### 7.2 **Rekomendasi**
- Berdasarkan hasil evaluasi, disarankan untuk menggunakan model **Gradient Boosting** dalam aplikasi prediksi risiko diabetes karena kinerjanya yang paling stabil dan akurat.

---

## 8. **Referensi**

1. Delpino, et al., "Does machine learning have a high performance to predict obesity among adults and older adults? A systematic review and meta-analysis." *Nutrition, Metabolism and Cardiovascular Diseases.*, 2024.  
2. Ferdowsy, et al., "Machine Learning Approaches for Obesity Prediction." *Current Research in Behavioral Sciences.*, 2021.  
3. M. Oyamada, "Extracting Feature Engineering Knowledge from Data Science Notebooks," 2019 IEEE International Conference on Big Data (Big Data), Los Angeles, CA, USA, 2019.  
4. T. Chen, C. Guestrin, "XGBoost: A Scalable Tree Boosting System," KDD, 2016.

---

Laporan ini telah diperbarui sesuai dengan catatan dari reviewer dan sekarang mencakup tambahan teknik yang digunakan dalam feature engineering, penjelasan parameter yang lebih jelas, serta hasil evaluasi yang lebih lengkap.
