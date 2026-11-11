
# Laporan Proyek Machine Learning - Prediksi Risiko Diabetes

## 1. **Domain Proyek**

### 1.1 **Latar Belakang**
Diabetes adalah salah satu penyakit kronis yang banyak diderita oleh individu di seluruh dunia, dan prevalensinya semakin meningkat. Menurut World Health Organization (WHO), diabetes telah menjadi salah satu penyebab utama kematian di dunia. Oleh karena itu, penting untuk mengembangkan model prediktif yang dapat membantu dalam deteksi dini risiko diabetes, sehingga intervensi dan pencegahan dapat dilakukan lebih awal. Proyek ini bertujuan untuk mengembangkan model machine learning untuk memprediksi risiko diabetes berdasarkan sejumlah faktor seperti usia, indeks massa tubuh (BMI), kadar glukosa darah, kadar HbA1c, serta riwayat hipertensi dan penyakit jantung.

### 1.2 **Pentingnya Proyek**
Proyek ini memiliki beberapa alasan penting untuk dilaksanakan, antara lain:
1. Mengidentifikasi individu yang berisiko tinggi terkena diabetes sehingga dapat dilakukan intervensi lebih awal.
2. Menyediakan alat prediksi berbasis data yang dapat digunakan oleh tenaga medis untuk merencanakan pengelolaan kesehatan yang lebih baik.
3. Membantu dalam pemantauan kesehatan masyarakat dengan menyediakan sistem yang dapat mengklasifikasikan risiko diabetes.

### 1.3 **Hasil Riset dan Referensi**
Beberapa riset sebelumnya menunjukkan penggunaan algoritma machine learning, seperti Random Forest dan XGBoost, untuk memprediksi penyakit diabetes dengan hasil yang cukup akurat. Penelitian oleh [Delpino et al. (2024)](https://www.sciencedirect.com/science/article/pii/S0939475324002047) menyatakan bahwa algoritma klasifikasi dapat memprediksi diabetes dengan akurasi yang cukup tinggi.

## 2. **Business Understanding**

### 2.1 **Problem Statements**
Masalah yang ingin diselesaikan dalam proyek ini adalah:
- Bagaimana membangun model prediktif yang dapat mengklasifikasikan risiko diabetes pada individu?

### 2.2 **Goals**
Tujuan dari proyek ini adalah:
- Mengembangkan model prediktif dengan tingkat akurasi minimal 85% untuk mengklasifikasikan apakah seseorang berisiko diabetes atau tidak.

### 2.3 **Solution Statements**
Untuk mencapai tujuan di atas, kami mengusulkan beberapa solusi:
1. Mengembangkan dan membandingkan 6 model machine learning yang berbeda: Decision Tree, XGBoost, Random Forest, SVM, Logistic Regression, dan LightGBM.
2. Melakukan evaluasi terhadap setiap model menggunakan metrik evaluasi yang sesuai seperti akurasi, precision, recall, dan F1-score.
3. Memilih model terbaik berdasarkan hasil evaluasi yang diperoleh dari data testing.

## 3. **Data Understanding**

### 3.1 **Deskripsi Dataset**
Dataset yang digunakan dalam proyek ini diambil dari [Kaggle](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset). Dengan variabel-variabel sebagai berikut:
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

### 3.3 **Eksplorasi Data**
- **Correlation Matrix**: Menggambarkan hubungan antara fitur-fitur, di mana terdapat korelasi kuat antara **HbA1c Level** dan **Blood Glucose Level**.
- **Distribusi Data**: Distribusi **Age** cenderung skewed ke kiri, dengan sebagian besar data berada pada rentang usia 20-30 tahun.
  
## 4. **Data Preparation**

### 4.1 **Feature Engineering**
- Menambahkan fitur **BMI** sebagai indikator untuk mengukur obesitas, yang dihitung menggunakan rumus:  
  \[
  BMI = \frac{Weight}{Height^2}
  \]
- Membuat fitur interaksi **age_bmi_interaction** untuk melihat hubungan antara usia dan BMI dalam memprediksi risiko diabetes.

### 4.2 **Pembagian Data**
Dataset dibagi menjadi data pelatihan (80%) dan data pengujian (20%) menggunakan **train_test_split**.

### 4.3 **Standarisasi dan Encoding**
- **Standarisasi** fitur numerik menggunakan **StandardScaler**.
- **Encoding** variabel kategorikal seperti **Gender** dan **Smoking History** menggunakan **One-Hot Encoding**.

## 5. **Modeling**

### 5.1 **Algoritma yang Digunakan**
1. **Logistic Regression**: Model sederhana yang dapat mengklasifikasikan data dengan probabilitas.
2. **Random Forest**: Model berbasis ensemble yang menggunakan beberapa pohon keputusan untuk menghasilkan prediksi.
3. **XGBoost**: Model boosting yang menggunakan gradient descent untuk memperbaiki kesalahan model sebelumnya.
4. **SVM**: Model yang mencari hyperplane terbaik untuk memisahkan kelas-kelas data.

### 5.2 **Tahapan Pemodelan**
1. Inisialisasi setiap model dengan parameter default.
2. Melatih model menggunakan data pelatihan yang sudah diproses.
3. Melakukan prediksi pada data pengujian.
4. Menggunakan metrik evaluasi untuk mengevaluasi performa masing-masing model.

## 6. **Evaluation**

### 6.1 **Metrik Evaluasi**
1. **Akurasi**: Mengukur proporsi prediksi yang benar.
2. **Precision**: Mengukur proporsi prediksi positif yang benar.
3. **Recall**: Mengukur kemampuan model dalam mendeteksi hasil positif.
4. **F1-Score**: Mengukur keseimbangan antara precision dan recall.

### 6.2 **Hasil Evaluasi**
- **XGBoost** memberikan performa terbaik dengan akurasi 90%, diikuti oleh **Random Forest** (90%) dan **Logistic Regression** (87%).
- Semua model menunjukkan F1-score yang tinggi, dengan **XGBoost** mencatatkan skor terbaik.

## 7. **Kesimpulan**

### 7.1 **Pencapaian Tujuan**
- Model **XGBoost** berhasil mencapai akurasi lebih dari 85%, dengan hasil akurasi mencapai 90% pada data pengujian.
- Model ini memberikan solusi optimal untuk memprediksi risiko diabetes.

### 7.2 **Rekomendasi**
- Berdasarkan hasil evaluasi, disarankan untuk menggunakan model **XGBoost** dalam aplikasi prediksi risiko diabetes karena kinerjanya yang paling stabil dan akurat.

## 8. **Referensi**

1. Delpino, et al., "Does machine learning have a high performance to predict obesity among adults and older adults? A systematic review and meta-analysis." *Nutrition, Metabolism and Cardiovascular Diseases.*, 2024.  
2. Ferdowsy, et al., "Machine Learning Approaches for Obesity Prediction." *Current Research in Behavioral Sciences.*, 2021.  
3. M. Oyamada, "Extracting Feature Engineering Knowledge from Data Science Notebooks," 2019 IEEE International Conference on Big Data (Big Data), Los Angeles, CA, USA, 2019.  
4. T. Chen, C. Guestrin, "XGBoost: A Scalable Tree Boosting System," KDD, 2016.  

