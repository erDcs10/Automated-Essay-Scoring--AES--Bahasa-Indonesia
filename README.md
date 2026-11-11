## LAMPIRAN B. FORMULIR PENGAJUAN IDE (DIKUMPULKAN PADA CHECKPOINT 1)

| Komponen | Isian Mahasiswa |
|----------|-----------------|
| Nama / NIM | [ Erlangga Deanda Chandra Setya / 244311013, Muhammad Rofiqul Anam / 244311019] |
| Judul ide | [ Pengembangan Sistem Automated Essay Scoring (AES) Bahasa Indonesia untuk Evaluasi Pembelajaran Otomatis ] |
| SDG & target yang dipilih | [ 4 & 4.1] Quality Education|
| Masalah nyata yang diangkat | [ Ketimpangan rasio guru dan siswa di Indonesia, di mana pemeriksaan esai secara manual sering kali memakan waktu sangat lama ] |
| Tugas ML (Target & jenis tugas) | [ Jenis Tugas: Regresi / Klasifikasi Terurut (Ordinal Classification). Target: Memprediksi nilai/skor numerik (skala 0–100 atau 1–5) dari jawaban esai siswa berdasarkan tingkat kesesuaian makna (semantic similarity) dan kelengkapan konten terhadap kunci jawaban / rubrik penilaian guru.] |
| Objective & metrik utama | [ Membangun pipeline evaluasi jawaban esai Bahasa Indonesia yang presisi, obyektif, dan konsisten terhadap acuan skor guru. ] |
| Dataset (sumber, URL, ukuran, jenis data) | [ Sumber Data: Combined Public Dataset (Hugging Face Datasets: indolem/indobert-base-uncased benchmark & Ukara Enhanced Dataset Kaggle).Ukuran: ~12,173 sampel teks jawaban esai beserta kunci jawaban dan skor acuan manusia. Jenis Data: Teks (Unstructured Text) Bahasa Indonesia berupa jawaban siswa, kunci jawaban guru, dan skor numerik. ] |
| Risiko & pertimbangan etika (bias, privasi) | [ Bias Panjang Teks (Length Bias): Model berisiko memberikan nilai lebih tinggi pada jawaban yang lebih panjang meskipun pembahasannya tidak relevan. Bahasa Tidak Baku & Typo: Variasi bahasa gaul/singkatan siswa yang tidak terdaftar pada kosakata model. Privasi & Anonimisasi: Seluruh data teks siswa wajib di-anonimkan (menghapus nama, NIM, dan identitas sekolah) sebelum diproses oleh model. ] |
| Referensi awal (minimal 2) | [ Shermis, M. D., & Burstein, J. (2013). Handbook of Automated Essay Evaluation: Current Applications and New Directions. Routledge. Purwarianti, A., et al. (2020). IndoLEM and IndoBERT: A Benchmark Dataset and Pre-trained Language Model for Indonesian NLP. arXiv preprint arXiv:2011.00677. ] |

**Kriteria persetujuan dosen:**
- [ ] Ide berasal dari mahasiswa dan tidak duplikat
- [ ] Selaras jelas dengan satu SDG dan targetnya
- [ ] Dapat dirumuskan sebagai masalah ML dengan target yang jelas
- [ ] Dataset tersedia, legal/etis digunakan, dan cukup besar
- [ ] Layak untuk tiga model termasuk deep learning dalam 6 minggu
