<h2>BAB III</h2>
<h2>METODOLOGI PENELITIAN</h2>

<h3>3.1 Tahapan Penelitian</h3>

<p>
Tahapan penelitian ini dirancang sebagai kerangka kerja sistematis (framework) yang memandu jalannya penelitian dari awal hingga akhir guna memastikan tujuan penelitian tercapai secara ilmiah. Alur penelitian mengadopsi metodologi standar pengembangan sistem berbasis pembelajaran mesin (Machine Learning Life Cycle). Secara detail, tahapan penelitian ini dibagi menjadi lima fase utama sebagai berikut:
</p>

<p><b>Fase Studi Literatur dan Eksplorasi Masalah</b></p>
<p>
Tahap ini merupakan fondasi teoretis penelitian. Kegiatan yang dilakukan meliputi identifikasi masalah klinis dengan mempelajari karakteristik visual penyakit Ringworm (Dermatophytosis) pada kucing melalui literatur kedokteran hewan. Pemahaman ini penting untuk membedakan fitur visual Ringworm dari penyakit kulit lain seperti Scabies atau Earmite. Selanjutnya, dilakukan analisis mendalam terhadap arsitektur MobileNetV3, khususnya mekanisme blok Squeeze-and-Excitation (SE) dan fungsi aktivasi Hard-Swish, dengan membedah paper asli "Searching for MobileNetV3" (Howard et al., 2019). Fase ini juga mencakup tinjauan strategi fine-tuning yang efektif pada dataset kecil melalui studi komparatif terhadap penelitian terdahulu (State of the Art) guna menemukan celah penelitian yang dapat diisi.
</p>

<p><b>Fase Pengumpulan dan Kurasi Data</b></p>
<p>
Fase ini berfokus pada penyediaan bahan baku penelitian yang berkualitas. Proses dimulai dengan akuisisi data, yaitu mengunduh dataset mentah berupa citra penyakit kulit kucing dari repositori publik terverifikasi seperti Roboflow (Feline DermaAid Dataset). Setelah data terkumpul, dilakukan pembersihan data (Data Cleaning) melalui inspeksi visual manual untuk menghapus data yang tidak relevan (seperti gambar buram atau resolusi rendah) dan memperbaiki label data yang salah (re-labeling) untuk memastikan Ground Truth yang akurat. Data yang bersih kemudian dipartisi (Data Splitting) secara acak namun proporsional menjadi tiga himpunan: Data Latih (70%) untuk pembelajaran bobot, Data Validasi (20%) untuk evaluasi selama pelatihan, dan Data Uji (10%) untuk pengujian akhir.
</p>

<p><b>Fase Pra-pemrosesan dan Rekayasa Data (Data Engineering)</b></p>
<p>
Fase ini bertujuan mentransformasi data mentah menjadi format yang siap diproses oleh model. Proses utamanya adalah Resizing dan Normalisasi, di mana dimensi seluruh citra diubah menjadi format standar input MobileNetV3 (224 × 224 piksel) dan nilai piksel dinormalisasi dari rentang [0, 255] menjadi [0, 1] guna mempercepat konvergensi gradien. Selain itu, teknik Augmentasi Data diterapkan pada data latih secara real-time (on-the-fly). Transformasi geometris acak seperti rotasi (±20°), pembalikan horizontal (flip), pergeseran (shift), dan zooming diterapkan untuk memperkaya variasi data latih secara artifisial dan mencegah model menghafal posisi objek (overfitting).
</p>

<p><b>Fase Pengembangan dan Pelatihan Model</b></p>
<p>
Ini adalah fase inti komputasi di mana arsitektur model dibangun. Dimulai dengan inisialisasi model MobileNetV3 sebagai backbone menggunakan bobot awal (pre-trained weights) dari ImageNet. Arsitektur kemudian dimodifikasi dengan memotong lapisan klasifikasi asli (Top Layer) dan menggantinya dengan lapisan Custom Head yang terdiri dari Global Average Pooling, Dense Layer (128 neuron), Dropout (rate 0.3–0.5), dan Output Layer (2 neuron dengan Softmax) untuk klasifikasi biner. Proses pelatihan (Training Loop) dilakukan menggunakan algoritma optimasi (Optimizer) dengan fungsi kerugian Categorical Crossentropy. Tahap ini juga mencakup Hyperparameter Tuning, yaitu eksperimen iteratif dengan mengubah parameter pelatihan (seperti Batch Size, Learning Rate, dan jenis Optimizer) untuk mencari konfigurasi yang menghasilkan akurasi validasi tertinggi.
</p>

<p><b>Fase Evaluasi dan Analisis Akhir</b></p>
<p>
Fase terakhir bertujuan memvalidasi keberhasilan penelitian. Model final diuji menggunakan Data Uji (Test Set) yang belum pernah dilihat sebelumnya (unseen data) untuk mengukur kinerja generalisasi yang objektif. Berdasarkan hasil prediksi, dihitung metrik Akurasi, Presisi, Recall, dan F1-Score melalui tabel Confusion Matrix. Dilakukan pula Analisis Kesalahan (Error Analysis) pada sampel data yang salah diprediksi (False Positive/False Negative) untuk memahami kelemahan model secara kualitatif, sebelum akhirnya ditarik kesimpulan untuk menjawab rumusan masalah.
</p>

<h3>3.2 Identifikasi Data</h3>

<p>
Data yang digunakan dalam penelitian ini merupakan dataset sekunder berupa citra digital penyakit kulit kucing yang diperoleh dari platform repositori dataset publik, Roboflow, dengan nama himpunan data Feline DermaAid. Pemilihan dataset ini didasarkan pada ketersediaan variasi citra klinis yang representatif terhadap kondisi lapangan.
</p>

<p>
Dataset ini secara spesifik difokuskan pada dua kelas label utama untuk keperluan klasifikasi biner, yaitu kelas Positif (Ringworm) dan kelas Negatif (Non-Ringworm). Kelas Positif berisi kumpulan citra kucing yang menunjukkan gejala klinis aktif berupa lesi melingkar (circular lesion), kerontokan bulu (alopecia), dan kemerahan (erythema). Sementara itu, kelas Negatif berisi citra kucing dengan kondisi kulit sehat atau citra kucing yang menderita penyakit kulit lain (seperti Scabies atau Earmite) namun tidak menunjukkan pola Ringworm, yang berfungsi sebagai pembanding (counter-example) agar model dapat belajar membedakan fitur penyakit secara spesifik.
</p>

<p>
Total volume data yang digunakan dalam penelitian ini diperkirakan berjumlah antara 1.500 hingga 2.000 citra dengan format file JPG atau PNG. Guna menjamin objektivitas evaluasi dan mencegah terjadinya data leakage (kebocoran data), dataset tersebut akan dipartisi menggunakan teknik Stratified Random Sampling. Skema pembagian data ditetapkan dengan rasio 70:20:10, di mana 70% dari total data dialokasikan sebagai Data Latih (Training Set), 20% sebagai Data Validasi (Validation Set), dan 10% sebagai Data Uji (Testing Set).
</p>

<h3>3.3 Lingkungan Implementasi</h3>

<h4>3.3.1 Perangkat Keras (Hardware)</h4>
<p>
Mengingat proses pelatihan model CNN melibatkan operasi perkalian matriks yang sangat intensif, penelitian ini memanfaatkan lingkungan komputasi hibrida. Untuk keperluan penulisan kode program, digunakan komputer lokal dengan spesifikasi minimal prosesor Intel Core i5 atau AMD Ryzen 5 dan memori RAM 8 GB. Untuk pelatihan model digunakan GPU cloud Google Colab dengan NVIDIA T4 Tensor Core berkapasitas VRAM 16 GB.
</p>

<h4>3.3.2 Perangkat Lunak (Software)</h4>
<p>
Implementasi sistem dibangun pada sistem operasi Windows 10/11 64-bit dengan bahasa pemrograman Python versi 3.8 atau lebih baru. Framework utama yang digunakan adalah TensorFlow 2.x dengan Keras. Pustaka pendukung meliputi NumPy, Pandas, Matplotlib, Seaborn, dan Scikit-Learn. Lingkungan pengembangan menggunakan Jupyter Notebook.
</p>

<h3>3.4 Perancangan Sistem</h3>

<h4>3.4.1 Pra-pemrosesan Data (Preprocessing)</h4>
<p>
Sebelum citra dimasukkan ke dalam model, dilakukan proses Resizing menjadi 224 × 224 piksel dan Normalisasi nilai piksel dari 0–255 menjadi 0–1. Teknik Augmentasi Data seperti rotasi acak (±20°), pembalikan horizontal, dan pergeseran diterapkan secara on-the-fly untuk meningkatkan robustnes model dan mencegah overfitting.
</p>

<h4>3.4.2 Perancangan Arsitektur Model (Proposed Method)</h4>
<p>
Arsitektur yang diusulkan menggunakan MobileNetV3 sebagai Base Model dengan bobot pre-trained ImageNet yang dibekukan. Lapisan klasifikasi asli dihapus dan diganti dengan Custom Classification Head yang terdiri dari Global Average Pooling, Dense Layer 128 neuron dengan aktivasi ReLU, Dropout 0.3–0.5, dan Output Layer Softmax dua kelas.
</p>

<h3>3.5 Skenario Pengujian</h3>

<h4>3.5.1 Skenario 1: Optimasi Hyperparameter</h4>
<p>
Pengujian dilakukan dengan memvariasikan Optimizer (Adam dan SGD) serta Learning Rate (0.001, 0.0001, dan 0.00001) untuk mendapatkan konfigurasi terbaik.
</p>

<h4>3.5.2 Skenario 2: Evaluasi Kinerja Model</h4>
<p>
Model terbaik diuji menggunakan Data Uji dan dievaluasi menggunakan Confusion Matrix untuk menghitung Akurasi, Presisi, Recall, dan F1-Score serta dianalisis melalui kurva pembelajaran.
</p>

<h3>3.6 Jadwal Penelitian</h3>

<p>
Penelitian ini direncanakan berlangsung selama satu semester (4 bulan) dengan rincian: Bulan ke-1 eksplorasi dan studi literatur, Bulan ke-2 desain dan preprocessing, Bulan ke-3 eksperimen dan optimasi, serta Bulan ke-4 evaluasi dan penulisan laporan akhir.
</p>
