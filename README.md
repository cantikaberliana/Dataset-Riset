# Riset Kecil: Pengembangan Model Klasifikasi Gejala GERD dan Anxiety Menggunakan Explainable Machine Learning
# 1. Rencana Topik
Topik yang dipilih adalah klasifikasi skrining GERD dan gejala kecemasan (anxiety) dari data kuesioner gejala, memakai model ML yang hasilnya dijelaskan dengan SHAP/LIME.
Menurut studi di Pakistan, kecemasan dan depresi berhubungan signifikan dengan GERD pada dewasa muda. Penulisnya menyarankan agar dewasa muda dengan GERD diskrining untuk kecemasan dan depresi (Association Between GERD Severity and Depression and Anxiety in Young Adults). Karena itu, model yang membaca kedua kelompok gejala sekaligus masuk akal sebagai alat bantu skrining awal. Model ini bukan alat diagnosis.
# 2. Formulasi Masalah
1. Seberapa baik algoritma ML (Random Forest, SVM, XGBoost, Logistic Regression) mengklasifikasikan status GERD dan anxiety dari data gejala?
2. Fitur gejala mana yang paling berpengaruh terhadap prediksi, dan apakah penjelasan model sejalan dengan literatur klinis?
3. Bagaimana menangani ketidakseimbangan kelas, misalnya dengan SMOTE atau class weight?
# 3. Riset Gap dari Penelitian Terdahulu
1. Hubungan GERD dan anxiety sudah terbukti, tetapi sebagian besar studinya statistik, bukan prediktif. Studi di Arab Saudi menemukan bahwa 31,4% peserta dengan anxiety mengalami GERD, dibanding 15,0% pada peserta tanpa anxiety (GAD-7 untuk anxiety dan GerdQ untuk GERD). Studi di India menemukan bahwa pasien dengan skor GERD-Q ≥ 8 punya peluang sekitar 3,5 kali lebih besar mengalami anxiety sedang sampai berat (Anxiety severity among adults having upper GI symptoms). Studi seperti ini menjelaskan hubungan, tetapi tidak membangun model klasifikasi.
2. Model ML yang menggabungkan gejala psikologis dan GERD masih lemah. Studi pada pasien refluks refrakter menemukan bahwa model ML-nya berkinerja buruk, dengan tingkat salah klasifikasi 67–68% (Geeraerts dkk., 2023). Ini menunjukkan masih ada ruang untuk perbaikan fitur dan algoritma.
3. ML untuk GERD berfokus pada citra endoskopi. Tinjauan literatur AI untuk GERD terutama membahas diagnosis dari citra endoskopi (Cureus, review AI untuk diagnosis GERD). Klasifikasi berbasis gejala dari kuesioner jauh lebih sedikit dibahas.
# 4. Peluang Pengembangan
1. Multi-label atau 4 kelas: normal, GERD saja, anxiety saja, GERD + anxiety.
2. Perbandingan model: Logistic Regression sebagai baseline, lalu Random Forest, SVM, dan XGBoost. Random Forest dengan LIME/SHAP sudah dipakai untuk data gejala di bidang kesehatan lain (Explainable AI for Healthcare using Random Forest with LIME and SHAP).
3. Penanganan imbalance: SMOTE vs class weight.
4. Evaluasi: macro-F1, recall (penting untuk skrining), PR-AUC, dan stratified cross-validation.
5. Validasi penjelasan: cocokkan fitur terpenting menurut SHAP dengan literatur klinis, misalnya nyeri dada dan heartburn.
# 5. Sumber Data dan Referensi
# a). Sumber Data
1. Data primer lewat Google Form dengan GERD-Q (6 item, ambang ≥ 8) dan GAD-7 (7 item, ambang umumnya ≥ 10), plus fitur demografi dan gaya hidup. Instrumen GERD-Q bebas dipakai (bioinformation.net). 
2. Dataset sekunder serupa (survei kesehatan nasional) di Kaggle, UCI, atau Zenodo.
# b). Referensi Jurnal
1. Geeraerts A. dkk. (2023). Psychological symptoms do not discriminate between reflux phenotypes along the organic-functional refractory GERD spectrum. https://documentserver.uhasselt.be/handle/1942/40712
2. Niu T. dkk. (2024). An explainable predictive model for anxiety symptoms risk among Chinese older adults with abdominal obesity using ML and SHAP. Frontiers in Psychiatry. https://pmc.ncbi.nlm.nih.gov/articles/pmid/39720434
3. ML-based identification of anxiety symptoms in Chinese community-dwelling older adults: six algorithms with SHAP and nomogram. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC13540043/
4. Association Between GERD Severity and Depression and Anxiety in Young Adults. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12547794/
5. Generalized Anxiety Disorder Associated With GERD Among the Saudi Population. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10771964/
6. Anxiety severity among adults having upper GI symptoms. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12859373/
