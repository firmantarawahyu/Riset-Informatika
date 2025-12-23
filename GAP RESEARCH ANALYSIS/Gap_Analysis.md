<h2>BAB II</h2>
<h2>TINJAUAN PUSTAKA</h2>

<h3>2.1 Landasan Teori</h3>

<h4>2.1.1 Penyakit Ringworm (Dermatophytosis) pada Kucing</h4>

<p>
Dermatophytosis, atau yang secara umum dikenal masyarakat sebagai Ringworm (kurap), merupakan infeksi jamur superfisial yang menyerang jaringan terkeratinisasi seperti lapisan tanduk kulit (stratum corneum), rambut, dan kuku. Pada spesies Feline (kucing), etiologi utama penyakit ini didominasi oleh jamur Microsporum canis, yang bertanggung jawab atas sebagian besar kasus klinis, diikuti oleh Microsporum gypseum dan Trichophyton mentagrophytes.
</p>

<p>
Penting untuk dicatat bahwa Ringworm dikategorikan sebagai penyakit zoonosis, yang berarti memiliki potensi transmisi yang tinggi dari hewan ke manusia (animal-to-human transmission). Risiko ini menjadikan deteksi dini dan akurat bukan hanya masalah kesehatan hewan, tetapi juga isu kesehatan masyarakat yang mendesak untuk mencegah wabah di lingkungan pemilik hewan peliharaan.
</p>

<p>
Secara manifestasi klinis, Ringworm menampilkan karakteristik visual yang cukup distingtif namun sering kali membingungkan bagi mata awam. Gejala patognomonik yang paling umum meliputi alopecia (kerontokan bulu) yang membentuk pola sirkular atau cincin, disertai dengan erythema (kemerahan pada kulit) dan pembentukan crust (kerak) atau sisik (scaling) di tepi lesi yang aktif. Pola pertumbuhan jamur yang melingkar keluar dari pusat infeksi inilah yang menciptakan visual "cincin" tersebut. Namun, dalam banyak kasus, infeksi sekunder bakteri atau tahap penyembuhan dapat mengaburkan bentuk asli lesi, sehingga inspeksi visual semata sering kali tidak cukup untuk menegakkan diagnosis pasti.
</p>

<p>
Dalam konteks komputasi cerdas, keterbatasan metode konvensional mendorong penerapan teknologi pengolahan citra digital. Seperti yang diungkapkan dalam penelitian Taufiqoh dan Purnamasari (2025), tantangan utama dalam diagnosis berbasis citra adalah kemiripan fitur visual antara Ringworm dengan penyakit kulit lain seperti Scabies atau dermatitis alergi. Variasi warna bulu kucing, kondisi pencahayaan yang tidak merata, dan noise latar belakang semakin memperumit proses segmentasi lesi. Oleh karena itu, diperlukan algoritma Deep Learning yang mampu mengekstraksi fitur hirarkis yang kuat (robust) untuk membedakan pola morfologi cincin jamur dari gangguan kulit lainnya secara otomatis dan objektif.
</p>

<h4>2.1.2 Pengolahan Citra Digital (Digital Image Processing)</h4>

<p>
Pengolahan citra digital didefinisikan sebagai disiplin ilmu yang mempelajari teknik manipulasi citra dua dimensi menggunakan komputer digital untuk memperbaiki kualitas visual atau mengekstraksi informasi yang relevan. Sebuah citra digital I(x,y) dapat dipandang sebagai matriks diskrit dari intensitas cahaya, di mana x dan y merepresentasikan koordinat spasial, dan nilai pada koordinat tersebut mencerminkan tingkat kecerahan (gray level) atau warna. Dalam diagnosis medis, citra masukan umumnya berupa citra berwarna RGB (Red, Green, Blue) yang membawa informasi tekstur dan warna lesi kulit yang sangat kaya. Sebelum citra ini dapat diproses oleh algoritma pembelajaran mesin, serangkaian tahapan pra-pemrosesan (preprocessing) mutlak diperlukan untuk menstandarisasi data masukan.
</p>

<p>
Salah satu tahapan pra-pemrosesan yang paling krusial adalah resizing dan normalisasi. Citra yang diambil dari berbagai sumber kamera tentu memiliki resolusi yang beragam. Arsitektur Convolutional Neural Network (CNN) standar membutuhkan dimensi input yang tetap, misalnya 224 × 224 piksel, untuk menjaga konsistensi jumlah parameter pada lapisan fully connected. Selain itu, normalisasi nilai piksel dilakukan dengan mengubah rentang intensitas asli (0–255) menjadi rentang skalar (0–1). Langkah ini bertujuan untuk mempercepat proses konvergensi algoritma optimasi (Gradient Descent) selama pelatihan, mencegah masalah gradien yang meledak (exploding gradients), dan memastikan bahwa fitur dengan rentang nilai besar tidak mendominasi fitur lainnya.
</p>

<p>
Selain standarisasi, teknik Augmentasi Data (Data Augmentation) memegang peranan vital, terutama pada domain medis veteriner yang sering kali mengalami kelangkaan dataset (data scarcity). Augmentasi data adalah proses menghasilkan variasi data latih baru secara artifisial dari data yang sudah ada melalui transformasi geometris. Teknik ini ditegaskan urgensinya dalam penelitian Dian Saputra Aji et al. (2025), di mana penerapan augmentasi data seperti rotasi acak dan pembalikan horizontal terbukti mampu mencegah overfitting. Dengan memberikan variasi posisi dan orientasi lesi kulit pada model selama proses pelatihan, jaringan saraf dipaksa untuk mempelajari fitur intrinsik penyakit (seperti tekstur dan pola tepi lesi) alih-alih menghafal posisi atau orientasi lesi pada gambar.
</p>

<h4>2.1.3 Convolutional Neural Network (CNN)</h4>

<p>
Convolutional Neural Network (CNN) merupakan salah satu jenis arsitektur Deep Learning yang paling dominan dalam bidang Computer Vision. Struktur CNN terinspirasi secara biologis oleh organisasi korteks visual pada otak hewan, di mana neuron-neuron individual merespons rangsangan hanya di daerah terbatas dari bidang visual yang disebut medan reseptif (receptive field). Berbeda dengan Multilayer Perceptron (MLP) tradisional yang menghubungkan setiap neuron ke semua neuron di lapisan berikutnya (fully connected), CNN menggunakan prinsip konektivitas lokal dan pembagian bobot (weight sharing). Karakteristik ini membuat CNN jauh lebih efisien dalam memproses data berstruktur grid seperti gambar karena jumlah parameter yang harus dipelajari berkurang secara drastis.
</p>

<p>
Komponen fundamental pertama dari CNN adalah Lapisan Konvolusi (Convolutional Layer). Lapisan ini bertugas sebagai pengekstraksi fitur utama dengan cara melakukan operasi konvolusi matematis antara citra input dengan sekumpulan filter atau kernel yang dapat dipelajari. Setiap filter dirancang untuk mendeteksi pola spesifik: filter pada lapisan awal mungkin mendeteksi fitur sederhana seperti garis vertikal, tepi horizontal, atau perubahan warna, sedangkan filter pada lapisan yang lebih dalam dapat mendeteksi pola kompleks seperti bentuk lingkaran, mata, atau tekstur bulu kucing. Hasil dari operasi ini disebut sebagai peta fitur (feature map), yang merepresentasikan keberadaan fitur-fitur tersebut di berbagai lokasi dalam citra.
</p>

<p>
Komponen kedua yang tak kalah penting adalah Lapisan Pooling (Pooling Layer), yang biasanya disisipkan di antara lapisan konvolusi. Fungsi utama lapisan ini adalah untuk melakukan down-sampling atau reduksi dimensi spasial dari feature map. Teknik yang paling umum digunakan adalah Max Pooling, yang mengambil nilai maksimum dari suatu jendela area tertentu. Proses ini memberikan dua keuntungan: pertama, mengurangi beban komputasi dan penggunaan memori dengan memperkecil ukuran data; kedua, memberikan sifat invarian terhadap translasi (translation invariance), yang berarti model tetap dapat mengenali objek (misalnya lesi Ringworm) meskipun posisinya bergeser sedikit dalam gambar.
</p>

<p>
Komponen terakhir adalah Lapisan Terhubung Penuh (Fully Connected Layer) yang berada di bagian ujung arsitektur. Setelah melalui serangkaian lapisan konvolusi dan pooling, peta fitur 2D diratakan (flatten) menjadi vektor 1D. Lapisan ini kemudian bertindak sebagai pengklasifikasi (classifier) yang memetakan fitur-fitur visual yang telah diekstraksi menjadi probabilitas kelas akhir. Menurut Velasco et al. (2023), fungsi aktivasi Softmax biasanya digunakan pada neuron output terakhir untuk menghasilkan distribusi probabilitas, sehingga model dapat menentukan apakah sebuah citra termasuk dalam kategori penyakit tertentu atau sehat.
</p>

<h4>2.1.4 Arsitektur MobileNetV3</h4>

<p>
MobileNetV3 merepresentasikan evolusi terkini dalam desain arsitektur jaringan saraf yang efisien, yang dikembangkan oleh Google Research. Arsitektur ini dirancang khusus untuk menjembatani kesenjangan antara akurasi tinggi dan keterbatasan sumber daya komputasi pada perangkat seluler. Sebagaimana dijelaskan dalam literatur utama oleh Howard et al. (2019) berjudul "Searching for MobileNetV3", pengembangan arsitektur ini menggunakan pendekatan Automated Machine Learning (AutoML). Pendekatan ini menggabungkan Platform-Aware Neural Architecture Search (NAS) untuk menemukan struktur jaringan global, dan algoritma NetAdapt untuk mengoptimalkan jumlah filter di setiap lapisan.
</p>

<p>
MobileNetV3 mengintegrasikan modul Squeeze-and-Excitation (SE) ke dalam blok residual bottleneck-nya. Modul SE ini berfungsi sebagai mekanisme atensi saluran (channel attention mechanism). Secara sederhana, modul ini memungkinkan jaringan untuk "belajar" saluran fitur mana yang lebih penting melalui proses Squeeze (Global Average Pooling) dan Excitation. Dengan mekanisme ini, model dapat secara adaptif memberi bobot lebih besar pada fitur yang relevan dengan penyakit Ringworm (seperti pola tepi lesi) dan menekan fitur yang tidak relevan (seperti latar belakang kandang).
</p>

<p>
Selain itu, untuk mengatasi inefisiensi komputasi fungsi sigmoid pada perangkat mobile, MobileNetV3 memperkenalkan fungsi aktivasi Hard-Swish (h-swish). Fungsi ini merupakan aproksimasi linear dari fungsi Swish yang mempertahankan akurasi namun jauh lebih ringan untuk dihitung. Secara matematis, fungsi Hard-Swish dirumuskan dalam Persamaan (2.1):
</p>

<p>
$$h\text{-}swish(x) = x \frac{ReLU6(x+3)}{6}$$
</p>

<p>
Dimana:<br>
x : Nilai input fitur (input feature map).<br>
ReLU6 : Fungsi aktivasi yang membatasi nilai maksimal pada angka 6, didefinisikan sebagai min(max(0, x), 6).<br>
h-swish : Nilai output aktivasi.
</p>

<p>
Studi oleh Herimanto et al. (2024) memvalidasi bahwa kombinasi SE-Block dan h-swish pada MobileNetV3 menghasilkan akurasi klasifikasi tekstur kulit yang superior dibanding arsitektur ringan lainnya, menjadikannya kandidat ideal untuk penelitian ini.
</p>

<h4>2.1.5 Transfer Learning dan Fine-Tuning</h4>

<p>
Transfer Learning (pembelajaran transfer) adalah paradigma dalam pembelajaran mesin yang bertujuan untuk mentransfer pengetahuan yang diperoleh dari penyelesaian satu tugas ke tugas lain yang terkait. Dalam penelitian ini, model MobileNetV3 tidak dilatih dari awal (scratch), melainkan menggunakan bobot awal (pre-trained weights) dari dataset ImageNet. Menurut Dian Saputra Aji et al. (2025), metode ini adalah solusi paling efektif untuk mengatasi kelangkaan dataset pada domain medis veteriner, karena lapisan awal CNN cenderung mempelajari fitur visual universal (seperti garis dan tepi) yang relevan untuk semua tugas visi komputer.
</p>

<p>
Strategi Transfer Learning yang diterapkan terdiri dari dua fase utama. Fase pertama adalah Feature Extraction, di mana bobot lapisan konvolusi base model dibekukan (frozen). Model hanya melatih lapisan klasifikasi (head) baru yang disesuaikan dengan jumlah kelas target. Hal ini memungkinkan pemanfaatan fitur yang sudah matang tanpa waktu pelatihan yang lama. Teknik ini sangat krusial untuk mencegah overfitting pada dataset kecil.
</p>

<p>
Fase kedua adalah Fine-Tuning (penyesuaian halus), yang dilakukan setelah lapisan klasifikasi baru terkonvergensi. Beberapa lapisan atas (top layers) dari base model dicairkan (unfrozen) dan dilatih kembali dengan learning rate yang sangat rendah (misalnya 1e-5). Tujuannya adalah untuk sedikit memodifikasi representasi fitur abstrak tingkat tinggi agar lebih spesifik terhadap karakteristik unik penyakit Ringworm, tanpa merusak fitur dasar yang telah dipelajari sebelumnya.
</p>

<h4>2.1.6 Metrik Evaluasi Kinerja Model</h4>

<p>
Evaluasi kinerja model klasifikasi merupakan tahap krusial untuk memvalidasi efektivitas sistem. Instrumen dasar yang digunakan adalah Confusion Matrix, yang menghasilkan empat parameter utama: True Positive (TP), True Negative (TN), False Positive (FP), dan False Negative (FN).
</p>

<p>
a. Akurasi (Accuracy)<br>
Akurasi mengukur rasio prediksi benar terhadap keseluruhan data. Rumus akurasi ditunjukkan pada Persamaan (2.2):
</p>

<p>
$$Accuracy = \frac{TP + TN}{TP + TN + FP + FN}$$
</p>

<p>
Dimana:<br>
TP : Jumlah data positif (Ringworm) yang diprediksi benar.<br>
TN : Jumlah data negatif (Sehat) yang diprediksi benar.<br>
FP : Jumlah data negatif yang salah diprediksi sebagai positif.<br>
FN : Jumlah data positif yang salah diprediksi sebagai negatif.
</p>

<p>
b. Presisi (Precision)<br>
Presisi mengukur tingkat ketepatan model dalam memprediksi kelas positif. Nilai presisi dihitung menggunakan Persamaan (2.3):
</p>

<p>
$$Precision = \frac{TP}{TP + FP}$$
</p>

<p>
c. Recall (Sensitivitas)<br>
Recall mengukur kemampuan model untuk menemukan kembali seluruh data positif yang ada dalam dataset. Rumus Recall ditunjukkan pada Persamaan (2.4):
</p>

<p>
$$Recall = \frac{TP}{TP + FN}$$
</p>

<p>
d. F1-Score<br>
F1-Score adalah rata-rata harmonik antara Presisi dan Recall. Rumus F1-Score ditunjukkan pada Persamaan (2.5):
</p>

<p>
$$F1\text{-}Score = 2 \times \frac{Precision \times Recall}{Precision + Recall}$$
</p>

<h3>2.2 Penelitian Terdahulu</h3>

<p>
Tinjauan terhadap penelitian terdahulu dilakukan untuk memetakan posisi penelitian ini (State of the Art) dan mengidentifikasi celah yang masih perlu diisi.
</p>

<p>
Penelitian pertama yang menjadi rujukan adalah karya Taufiqoh dan Purnamasari (2025) berjudul "Development Of Detection Model For Skin Diseases In Pets". Penelitian ini berfokus pada deteksi tiga penyakit kulit (Earmite, Ringworm, Scabies) menggunakan tiga arsitektur berbeda: Custom CNN, ResNet-50, dan VGG16. Temuan penting dari studi ini adalah bahwa model Custom CNN yang lebih sederhana justru mencapai akurasi tertinggi sebesar 83%, mengungguli arsitektur Deep Learning yang lebih kompleks.
</p>

<p>
Penelitian kedua dilakukan oleh Dian Saputra Aji et al. (2025) dengan judul "Classification of Cat Skin Diseases Using MobileNetV2 Architecture with Transfer Learning".
</p>

<p>
Penelitian ketiga yang relevan adalah studi oleh Herimanto et al. (2024) mengenai "Performance Analysis of MobileNetV3-based CNN for Facial Skin Disorder Classification".
</p>

<p>
Analisis Research Gap:<br>
Berdasarkan literatur di atas, terlihat adanya evolusi metode dari model berat ke model ringan. Namun, belum ada penelitian yang secara spesifik menggabungkan arsitektur MobileNetV3 dengan Transfer Learning untuk mendeteksi Ringworm pada kucing.
</p>

<h3>2.3 Kerangka Pemikiran</h3>

<p>
Kerangka pemikiran penelitian ini dirancang sebagai alur logis sistematis untuk menyelesaikan permasalahan diagnosis Ringworm dari hulu ke hilir. Alur ini dimulai dari identifikasi masalah, pengumpulan data, pra-pemrosesan, pengembangan model, evaluasi, hingga menghasilkan model klasifikasi Ringworm yang akurat dan efisien.
</p>
