# Laporan Proyek Machine Learning - Iqbal Alfaridzi Balman

## Domain Proyek
Diabetes merupakan salah satu penyakit kronis yang menjadi perhatian utama dalam sektor kesehatan global. Deteksi dini terhadap risiko diabetes sangat penting untuk mencegah komplikasi yang lebih serius. Di Indonesia sendiri, prevalensi penderita diabetes terus meningkat setiap tahun, sebagaimana dilaporkan oleh Kementerian Kesehatan RI. Oleh karena itu, dibutuhkan solusi berbasis teknologi untuk membantu proses diagnosis secara cepat dan akurat.

Pemanfaatan machine learning, khususnya klasifikasi berbasis data medis, memberikan peluang besar untuk mengembangkan sistem deteksi dini diabetes. Dengan menggunakan data kuantitatif seperti kadar glukosa, tekanan darah, dan indeks massa tubuh, model machine learning dapat memprediksi apakah seorang pasien berisiko menderita diabetes atau tidak. Solusi ini dapat digunakan oleh tenaga medis sebagai alat bantu pengambilan keputusan.

Referensi :
- Kementerian Kesehatan Republik Indonesia. "InfoDatin Diabetes Mellitus."
- Dataset: Kaggle - Pima Indians Diabetes Dataset.

## Business Understanding
### Problem Statements

- Banyak pasien tidak terdiagnosis diabetes secara dini karena keterbatasan skrining manual.
- Diperlukan sistem berbasis data untuk membantu klasifikasi risiko diabetes secara cepat dan akurat.

### Goals
- Membangun model klasifikasi dengan data kuantitatif untuk mendeteksi diabetes.
- Mencapai akurasi minimal 75% sebagai baseline untuk aplikasi praktis.

### Solution Statements
- Menggunakan algoritma klasifikasi (Random Forest) untuk membangun model prediktif.
- Menerapkan teknik evaluasi seperti confusion matrix dan classification report.

## Data Understanding
Dataset yang digunakan adalah Pima Indians Diabetes Dataset(https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database), terdiri dari 768 data pasien wanita dari kelompok etnis Pima Indian dengan fitur-fitur medis berikut:
- Pregnancies: Jumlah kehamilan yang pernah dialami
- Glucose: Konsentrasi glukosa plasma dua jam setelah tes toleransi glukosa oral
- BloodPressure: Tekanan darah
- SkinThickness: Ketebalan lipatan kulit
- Insulin: Kadar insulin
- BMI: Indeks massa tubuh
- DiabetesPedigreeFunction: Indikator riwayat keturunan diabetes
- Age: Usia pasien
- Target: Outcome (0 = negatif diabetes, 1 = positif diabetes)

## Data Preparation
Langkah-langkah yang dilakukan:
- Mengganti Nilai Tidak Valid dengan NaN, Nilai 0 pada fitur Glucose, BloodPressure, SkinThickness, Insulin, dan BMI dianggap tidak valid. Oleh karena itu, nilai-nilai ini diganti menjadi NaN untuk menandai data yang hilang.
- Imputasi Nilai yang Hilang, Nilai NaN yang muncul akibat langkah sebelumnya diimputasi menggunakan nilai median dari masing-masing kolom. Median dipilih karena lebih robust terhadap outlier dibandingkan mean.
- Pemisahan Fitur dan Target, Kolom Outcome dipisahkan sebagai label (target), sedangkan kolom lainnya menjadi fitur (X).
- Pembagian data → 80% data training, 20% data testing.

## Modeling
Pada tahap ini, model machine learning dibangun menggunakan algoritma Random Forest Classifier dari library scikit-learn.
Random Forest adalah metode ensemble learning berbasis decision tree. Algoritma ini membangun banyak decision tree pada data yang berbeda-beda dan menggabungkan prediksi dari semua pohon tersebut untuk menghasilkan prediksi akhir.
Parameter:
- n_estimators=100: Jumlah pohon dalam forest.
- criterion='gini': Digunakan untuk mengukur kualitas split.
- random_state=42: Supaya hasil dapat direproduksi.
## Evaluation
Model mencapai akurasi: 74.68%, cukup baik untuk baseline model klasifikasi medis.

![image](https://github.com/user-attachments/assets/c2d87722-0d18-4ed1-9ccb-cb00576369a1)

- Recall kelas 1 cukup tinggi (0.67), menunjukkan model cukup baik dalam mendeteksi pasien yang benar-benar diabetes.
- Precision kelas 1 masih rendah (0.64) → Model terkadang keliru memprediksi pasien tidak diabetes sebagai diabetes.

## Analisis dan Insight
Faktor-faktor yang memengaruhi performa model:
- Class imbalance → Masih ada ketimpangan antara jumlah data kelas 0 dan 1.
- Noise pada fitur medis, seperti insulin atau tekanan darah dengan nilai nol, bisa mengurangi kualitas input.
- Model baseline belum menggunakan tuning hyperparameter atau ensemble tambahan.
- Jumlah fitur terbatas → menambah fitur medis lain (misalnya HbA1c atau riwayat keluarga) dapat meningkatkan prediksi.
