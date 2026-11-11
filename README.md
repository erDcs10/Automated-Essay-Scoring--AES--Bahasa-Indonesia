# README.md

---

## INFORMASI PROYEK

**Judul Proyek:**  
Automated Essay Scoring (AES) Evaluasi Otomatis Jawaban Esai

**Nama Mahasiswa:** Erlangga Deanda Chandra Setya, Muhammad Rofiqul Anam
**NIM:** 244311013, 244311019  
**Program Studi:** D4 Teknologi Rekayasa Perangkat Lunak  
**Mata Kuliah:** Machine Learning / Pembelajaran Mesin  
**Dosen Pengampu:** Gus Nanang Syaifuddin S.Kom M.Kom   
**Tahun Akademik:** 2026/2027 (Semester Ganjil)  
**Link GitHub Repository:** ``  
**Link Video Pembahasan:** ``  
**SDG yang Dipilih:** SDG 4 – Pendidikan Berkualitas  
**Target SDG yang Relevan:** Target 4.1 – Memastikan bahwa semua anak menyelesaikan pendidikan dasar dan menengah yang gratis, setara, dan berkualitas yang mengarah pada hasil belajar yang relevan dan efektif.

---

## 0. KERANGKA ML LIFECYCLE (L-M-O-P)

Laporan ini disusun mengikuti **ML Lifecycle** yang terdiri dari empat tahap berulang (iteratif):

| Tahap | Singkatan | Inti Pertanyaan | Bagian Laporan |
|-------|-----------|-----------------|----------------|
| **Learning Problem** | **L** | Apa target, objective, dan datanya? | Bab 2, 3, 4, 5 |
| **Model Design** | **M** | Model family/arsitektur apa, hypothesis space, dan inductive bias/asumsi apa? | Bab 6 (6.x.1 – 6.x.3) |
| **Optimization** | **O** | Bagaimana model dilatih: loss, optimizer, tuning, regularisasi, konvergensi? | Bab 6 (6.x.4 – 6.x.6) |
| **Predict & Evaluate** | **P** | Seberapa baik prediksi model berdasarkan metrik evaluasi? | Bab 7 |

---

## 1. LEARNING OUTCOMES

Pada proyek ini, mahasiswa telah berhasil:
1. **[L]** Merumuskan *problem statement* sistem koreksi esai otomatis dalam bahasa Indonesia yang mendukung pencapaian **SDG 4 (Pendidikan Berkualitas)**.
2. **[L]** Melakukan data preparation khusus NLP teks Bahasa Indonesia (cleansing, normalization slang/typo, tf-idf extraction, dan tokenization Transformer).
3. **[M]** Merancang 3 pendekatan model pembelajaran mesin dengan justifikasi *hypothesis space* dan *inductive bias*:
   - Baseline Model: Ridge Regression dengan TF-IDF N-grams
   - Advanced Model: Random Forest Regressor & Support Vector Regression (SVR)
   - Deep Learning Model (**WAJIB**): Fine-Tuned IndoBERT (`indobenchmark/indobert-base-p1`)
4. **[O]** Mengoptimasi hyperparameter, regularisasi (Dropout, Weight Decay), serta melakukan diagnosis konvergensi loss.
5. **[P]** Menganalisis hasil evaluasi menggunakan **Quadratic Weighted Kappa (QWK)**, **MAE**, dan **RMSE** sesuai standar evaluasi sistem AES global.
6. Menyusun repositori proyek yang terstruktur dan memenuhi kriteria *reproducibility*.

---

## 2. PROJECT OVERVIEW **[L]**

### 2.1 Latar Belakang
Pemberian umpan balik dan penilaian ujian esai secara manual di lembaga pendidikan memerlukan waktu yang lama serta rentan terhadap subjektivitas korektor (*inter-rater variability*). Dalam skala ujian masif, keterlambatan penilaian dapat menghambat efektivitas proses pembelajaran siswa. 

Sistem **Automated Essay Scoring (AES)** berbasis Machine Learning dan Natural Language Processing (NLP) hadir sebagai solusi untuk melakukan penilaian otomatis secara obyektif, konsisten, dan instan. Meskipun penelitian AES pada bahasa Inggris telah berkembang pesat (misalnya menggunakan dataset ASAP Kaggle), ketersediaan dan pengembangan AES untuk teks berbahasa Indonesia masih terbatas karena kompleksitas morfologi serta variasi bahasa informal yang tinggi dalam tulisan siswa. Proyek ini membangun pipeline AES otomatis menggunakan kombinasi fitur kebahasaan dan pemodelan representasi kontekstual transformer (*IndoBERT*).

**Referensi Ilmiah:**
1. Shermis, M. D., & Burstein, J. (2013). *Handbook of Automated Essay Evaluation: Current Applications and New Directions*. Routledge.
2. Bryan, N. A., et al. (2021). *IndoNLU: Benchmark and Resources for Indonesian Natural Language Understanding*. Proceedings of AACL-IJCNLP 2020.

### 2.2 Keterkaitan dengan SDGs (WAJIB)

| Komponen | Pertanyaan Panduan | Jawaban Anda |
|----------|--------------------|--------------|
| **SDG yang dipilih** | Goal nomor berapa dan apa namanya? | **SDG 4 – Pendidikan Berkualitas** |
| **Target SDG** | Target mana yang paling relevan? | **Target 4.1** (Meningkatkan mutu evaluasi pembelajaran secara efisien dan merata). |
| **Masalah nyata** | Masalah konkret apa yang diangkat? | Beban kerja pemeriksaan ujian esai yang tinggi pada pengajar, keterbatasan waktu koreksi, serta potensi bias subjektivitas penilaian. |
| **Peran ML** | Mengapa ML/DL cocok? | ML/DL dapat mempelajari pola hubungan spasial teks, kecocokan semantik dengan kunci jawaban, serta struktur tata bahasa untuk menghasilkan prediksi skor kontinu/kategori secara konsisten. |
| **Indikator kontribusi** | Bagaimana hasil model berkontribusi? | Mempercepat *feedback cycle* hasil ujian siswa dari hitungan hari menjadi hitungan detik dengan tingkat kesepakatan tinggi terhadap korektor manusia ($QWK > 0.75$). |
| **Pertimbangan etika** | Risiko bias, privasi, atau dampak salah prediksi? | Risiko penalaran salah pada esai yang menggunakan kata-kata unik (out-of-vocabulary) serta *algorithmic bias*. Oleh karena itu, AES dirancang sebagai *AI-assisted grading* (pembantu korektor), bukan pengganti penuh guru. |

**Sumber ide:** Pengalaman mengajar dan interaksi langsung dengan kebutuhan evaluasi pembelajaran berbasis kuis/esai di lingkungan pendidikan daerah.

### 2.3 Ringkasan Alur Lifecycle Proyek
Proyek diawali dengan perumusan masalah penilaian esai singkat/panjang (**L**), dilanjutkan pengolahan data teks UKARA/Indonesian AES. Pada tahap (**M**), tiga model dirancang dari regresi linier sederhana hingga arsitektur deep learning IndoBERT. Proses optimasi (**O**) dilakukan melalui pengaturan *learning rate*, *batch size*, dan *hyperparameter tuning* (GridSearch). Tahap evaluasi (**P**) mengukur metrik QWK dan MAE pada *test set*, yang kemudian memberikan masukan untuk iterasi pembersihan kata informal (*kamus alay*) dan penyesuaian augmentasi teks.

---

## 3. BUSINESS UNDERSTANDING / PROBLEM UNDERSTANDING **[L]**

### 3.1 Problem Statements
1. Bagaimana merancang pipeline preprocessing teks bahasa Indonesia yang efektif menangani *typo*, kata tidak baku, serta kompleksitas imbuhan pada jawaban esai siswa?
2. Seberapa akurat model machine learning konvensional (TF-IDF + Ridge/Random Forest) dibandingkan arsitektur deep learning (*IndoBERT*) dalam memprediksi nilai esai siswa?
3. Apakah model AES yang dikembangkan mampu mencapai tingkat kesepakatan yang setara dengan penilai manusia berdasarkan metrik *Quadratic Weighted Kappa (QWK)*?

### 3.2 Formulasi Learning Problem (WAJIB)

| Komponen | Pertanyaan Panduan | Jawaban Anda |
|----------|--------------------|--------------|
| **Target** | Apa yang diprediksi? Jenis tugas? | Prediksi skor numerik esai (skala 0–100 atau 0–5). **Tugas: Regresi Teks (Text Regression)** / Ordinal Classification. |
| **Objective** | Apa yang dioptimalkan secara matematis? | Meminimalkan *Mean Squared Error (MSE)* dan *Mean Absolute Error (MAE)*, serta memaksimalkan *Quadratic Weighted Kappa (QWK)*. |
| **Data** | Sumber, ukuran, jenis, dan asumsi data | Teks jawaban siswa (Bahasa Indonesia) beserta *prompt* dan kunci jawaban (reference answer). Jumlah data: ~3.000 sampel jawaban. Asumsi: Data bersifat i.i.d. setelah *stratified split* berdasarkan rentang skor. |

### 3.3 Goals
1. Membangun model AES berbahasa Indonesia yang mampu memprediksi skor esai dengan nilai $MAE < 5.0$ (skala 0–100) dan $QWK > 0.75$.
2. Mengembangkan baseline NLP konvensional dan membandingkannya secara empiris dengan model Deep Learning berbasis *IndoBERT*.
3. Menyediakan repositori eksperimen yang terstruktur, *reproducible*, dan mendukung efisiensi evaluasi pembelajaran untuk SDG 4 Target 4.1.

### 3.4 Solution Approach **[M]**

#### **Model 1 – Baseline Model**
* **Model:** TF-IDF Vectorizer + Ridge Regression.
* **Alasan Pemilihan:** Ridge Regression efisien menangani multikolinearitas pada matriks TF-IDF yang berdimensi tinggi, berfungsi sebagai batas performa minimum (*baseline speed & accuracy*).

#### **Model 2 – Advanced / ML Model**
* **Model:** Random Forest Regressor & Support Vector Regression (SVR - RBF Kernel).
* **Alasan Pemilihan:** SVR dengan kernel RBF mampu menangkap hubungan non-linear antar fitur frekuensi kata/N-gram, sedangkan Random Forest memberikan gambaran *feature importance* dari kata kunci esai.

#### **Model 3 – Deep Learning Model (WAJIB)**
* **Model:** Fine-Tuned IndoBERT (`indobenchmark/indobert-base-p1` + Mean Pooling + Dense Regression Layer).
* **Alasan Pemilihan:** Model berbasis Transformer mampu menangkap konteks semantik secara mendalam, tata bahasa, serta hubungan spasial antar kata tanpa bergantung semata-mata pada kecocokan kata kunci eksak (*exact keyword matching*).

---

## 4. DATA UNDERSTANDING **[L]**

### 4.1 Informasi Dataset
* **Sumber Dataset:** Dataset Publik UKARA AI Challenge / Dataset Penilaian Esai Bahasa Indonesia Terorientasi Akademik (Kaggle & Hugging Face).
* **Jumlah baris (rows):** 3.200 sampel jawaban esai
* **Jumlah kolom (columns):** 5 kolom
* **Tipe data:** Text & Numeric
* **Ukuran dataset:** ~8.5 MB
* **Format file:** `.csv`

### 4.2 Deskripsi Fitur

| Nama Fitur | Tipe Data | Deskripsi | Contoh Nilai |
|------------|-----------|-----------|--------------|
| `essay_id` | Integer | ID Unik Dokumen Esai | `101`, `102` |
| `prompt_text` | String | Soal/Instruksi Esai yang diberikan | `"Jelaskan fungsi Pancasila..."` |
| `reference_answer` | String | Kunci jawaban / Rubrik referensi | `"Pancasila berfungsi sebagai..."` |
| `student_essay` | String | Teks jawaban asli dari siswa | `"Peran pancasila dalam hdp..."` |
| `final_score` | Float/Int | Skor acuan dari penilai manusia (Ground Truth) | `85.0`, `60.0` |

