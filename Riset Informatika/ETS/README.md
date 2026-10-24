## Proposal Penelitian

## Judul: Pengembangan Model Klasifikasi Gejala GERD dan Anxiety Menggunakan Explainable Machine Learning

### 1. Latar Belakang

Gastroesophageal Reflux Disease (GERD) dan gangguan kecemasan (anxiety) sering muncul bersamaan. Gejala GERD seperti heartburn dan regurgitasi dapat meningkat saat cemas, sementara keluhan lambung yang menetap dapat memicu kecemasan. Tumpang tindih ini membuat penilaian awal berdasarkan gejala menjadi sulit.

Machine learning (ML) sudah dipakai untuk memprediksi GERD maupun anxiety dari data kuesioner dan faktor risiko, dan SHAP lazim dipakai untuk menjelaskan prediksinya. Namun sebagian besar penelitian memodelkan salah satu kondisi saja, sehingga kasus gejala campuran belum banyak ditangani. Di bidang kesehatan, model yang hanya akurat tetapi tidak dapat dijelaskan sulit dipercaya, sehingga explainability menjadi syarat.

### 2. Rumusan Masalah
Bagaimana membangun model ML yang mengklasifikasikan gejala menjadi normal, GERD, anxiety, dan GERD+anxiety?
Algoritma mana yang memberi kinerja terbaik, dengan memperhatikan ketidakseimbangan kelas?
Fitur gejala apa yang paling berpengaruh terhadap prediksi, menurut SHAP dan permutation importance, dan apakah masuk akal secara klinis?
### 3. Tujuan
Membangun dan membandingkan model klasifikasi (Logistic Regression, Random Forest, XGBoost).
Mengevaluasi model dengan metrik yang sesuai untuk data tidak seimbang.
Menjelaskan prediksi secara global dan lokal dengan SHAP.
### 4. Batasan Masalah
Menggunakan dataset publik anonim; tidak mengumpulkan data pasien.
Hasil adalah alat bantu skrining berbasis gejala, bukan alat diagnosis.
Label mengikuti definisi dataset (mis. cut-off GERD-Q dan GAD-7).
### 5. Manfaat

Akademis: perbandingan model dan analisis interpretabilitas untuk kasus gejala tumpang tindih. Praktis: dasar sistem skrining awal yang transparan.

### 6. Tinjauan Pustaka Singkat

Rujukan awal (verifikasi dan lengkapi sitasi sebelum dikirim):

Studi XAI untuk GERD dengan SHAP, Diagnostics 2022, 12(11):2740 (MDPI).
Model ML + SHAP untuk gejala anxiety pada lansia Tiongkok, GAD-7 cut-off >= 5, GBM terbaik (PMC13540043).
Model XGBoost + SHAP untuk risiko anxiety pada lansia dengan obesitas abdominal, Frontiers in Psychiatry 2024 (doi:10.3389/fpsyt.2024.1451703).
Geeraerts dkk., gejala psikologis tidak membedakan fenotipe refluks pada pasien GERD refrakter (Universitas Hasselt).

### 7. Research Gap
Ringkasan penelitian terdahulu

| Penelitian | Fokus | Metode | Catatan |
|---|---|---|---|
| Diagnostics 2022, 12(11):2740 | Prediktor GERD | 	ML + SHAP | Satu kondisi (GERD) |
| PMC13540043 | 	Anxiety pada lansia Tiongkok (GAD-7) | 	6 algoritma + SHAP + nomogram, GBM terbaik | + nomogram, GBM terbaik	Populasi lansia, satu kondisi |
| Front. Psychiatry 2024 (fpsyt.2024.1451703) | 	Anxiety pada lansia dengan obesitas abdominal | 	XGBoost + SHAP | 	Populasi sempit |
|Geeraerts dkk. (UHasselt) | 		Gejala psikologis vs fenotipe refluks | 	Statistik + ML | 	Model berkinerja buruk, misklasifikasi 67-68% |

## Gap yang diidentifikasi
1. Satu kondisi per model. Kebanyakan studi memodelkan GERD atau anxiety saja; kasus komorbid (GERD+anxiety) jarang diklasifikasikan sebagai kelas tersendiri.
2. Populasi terbatas. Banyak studi memakai populasi spesifik (lansia, kondisi khusus), sehingga kurang mewakili mahasiswa dan dewasa muda.
3. Interpretabilitas belum dikaitkan dengan klinis. SHAP sering hanya ditampilkan, belum dibandingkan dengan metode lain dan dengan pengetahuan klinis.
4. Ketidakseimbangan kelas sering tidak dibahas, padahal prevalensi anxiety/GERD pada sampel komunitas cenderung timpang.
5. Bukti hubungan lemah. Temuan Geeraerts dkk. menunjukkan gejala psikologis tidak membedakan fenotipe refluks, sehingga perlu diuji apakah klasifikasi gabungan memang feasible.

## Peluang pengembangan
* Klasifikasi 4 kelas (normal, GERD, anxiety, GERD+anxiety) atau multi-label.
* Perbandingan model sederhana vs ensemble dengan penanganan imbalance.
* Interpretabilitas ganda: SHAP + permutation importance, dan validasi terhadap literatur.
* Dasar untuk sistem skrining ringan berbasis kuesioner.

## Mind Map
<img width="2720" height="1800" alt="mind_map_klasifikasi_gerd_anxiety" src="https://github.com/user-attachments/assets/b0fa00ca-8a59-459a-bb96-a0b645727d81" /> 

## Rencana 
| Metrik | Alasan|
|---|---|
|Macro F1-score|Memperlakukan semua kelas setara; pembanding utama antar model|
|Recall per kelas (sensitivity) | Pada skrining, kasus yang terlewat (false negative) lebih merugikan|
|Precision per kelas| Mengukur false alarm|
|ROC-AUC (one-vs-rest, macro) | Kualitas pemisahan kelas lintas threshold|
|PR-AUC|	Lebih informatif saat kelas positif jarang|

## Rencana Model Singkat
|Tahap|Rencana|
|---|---|
|Baseline|Logistic Regression multinomial, dengan class_weight="balanced"|
|Model utama 1|Random Forest, tuning jumlah pohon, kedalaman, dan min_samples_leaf|
|Model utama 2|XGBoost, tuning learning_rate, max_depth, n_estimators, subsample|
|Imbalance|SMOTE di dalam fold training (pipeline imbalanced-learn), dibandingkan dengan class_weight saja|
|Tuning|GridSearchCV atau Optuna, 5-fold stratified, metrik Macro F1|
|Explainability|SHAP (TreeExplainer) untuk RF dan XGBoost; permutation importance sebagai pembanding|
|Implementasi	|Python, scikit-learn, xgboost, shap, imbalanced-learn|

## Referensi
1. Breiman, L. (2001). Random Forests. Machine Learning, 45(1), 5-32.
2. Chawla, N. V., Bowyer, K. W., Hall, L. O., & Kegelmeyer, W. P. (2002). SMOTE: Synthetic Minority Over-sampling Technique. Journal of Artificial Intelligence Research, 16, 321-357.
3. Chen, T., & Guestrin, C. (2016). XGBoost: A Scalable Tree Boosting System. Proceedings of KDD 2016, 785-794.
4. Lundberg, S. M., & Lee, S.-I. (2017). A Unified Approach to Interpreting Model Predictions. Advances in Neural Information Processing Systems 30 (NeurIPS 2017).
5. Pedregosa, F., dkk. (2011). Scikit-learn: Machine Learning in Python. Journal of Machine Learning Research, 12, 2825-2830.
6. Hosmer, D. W., Lemeshow, S., & Sturdivant, R. X. (2013). Applied Logistic Regression (3rd ed.). Wiley.
