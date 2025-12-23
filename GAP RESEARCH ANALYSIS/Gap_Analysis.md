<h2>BAB II</h2>
<h2>TINJAUAN PUSTAKA</h2>

<h3>2.1 Landasan Teori</h3>

<h4>2.1.1 Penyakit Ringworm (Dermatophytosis) pada Kucing</h4>
<p>
Dermatophytosis, atau yang secara umum dikenal masyarakat sebagai <i>Ringworm</i> (kurap), merupakan infeksi jamur superfisial yang menyerang jaringan terkeratinisasi seperti lapisan tanduk kulit (<i>stratum corneum</i>), rambut, dan kuku. Pada spesies <i>Feline</i> (kucing), etiologi utama penyakit ini didominasi oleh jamur <i>Microsporum canis</i>, yang bertanggung jawab atas sebagian besar kasus klinis, diikuti oleh <i>Microsporum gypseum</i> dan <i>Trichophyton mentagrophytes</i>.
</p>

<p>
Penting untuk dicatat bahwa Ringworm dikategorikan sebagai penyakit zoonosis, yang berarti memiliki potensi transmisi yang tinggi dari hewan ke manusia (<i>animal-to-human transmission</i>). Risiko ini menjadikan deteksi dini dan akurat bukan hanya masalah kesehatan hewan, tetapi juga isu kesehatan masyarakat yang mendesak untuk mencegah wabah di lingkungan pemilik hewan peliharaan.
</p>

<p>
Secara manifestasi klinis, Ringworm menampilkan karakteristik visual yang cukup distingtif namun sering kali membingungkan bagi mata awam. Gejala patognomonik yang paling umum meliputi alopecia (kerontokan bulu) yang membentuk pola sirkular atau cincin, disertai dengan erythema (kemerahan pada kulit) dan pembentukan crust (kerak) atau sisik (<i>scaling</i>) di tepi lesi yang aktif.
</p>

<p>
Dalam konteks komputasi cerdas, keterbatasan metode konvensional mendorong penerapan teknologi pengolahan citra digital. Penelitian Taufiqoh dan Purnamasari (2025) menyebutkan bahwa tantangan utama diagnosis berbasis citra adalah kemiripan fitur visual antara Ringworm dan penyakit kulit lainnya, sehingga diperlukan algoritma <i>Deep Learning</i> yang mampu mengekstraksi fitur hirarkis secara robust dan objektif.
</p>

<h4>2.1.2 Pengolahan Citra Digital (<i>Digital Image Processing</i>)</h4>
<p>
Pengolahan citra digital merupakan disiplin ilmu yang mempelajari teknik manipulasi citra dua dimensi menggunakan komputer digital untuk memperbaiki kualitas visual atau mengekstraksi informasi yang relevan. Sebuah citra digital dinyatakan sebagai fungsi dua dimensi <i>I(x,y)</i> yang merepresentasikan intensitas cahaya pada koordinat spasial tertentu.
</p>

<p>
Dalam diagnosis medis, citra masukan umumnya berupa citra RGB (<i>Red, Green, Blue</i>) yang menyimpan informasi warna dan tekstur lesi kulit. Sebelum diproses oleh algoritma pembelajaran mesin, citra harus melalui tahap pra-pemrosesan (<i>preprocessing</i>) untuk menstandarisasi data.
</p>

<p>
Tahapan penting dalam pra-pemrosesan meliputi <i>resizing</i> dan normalisasi. Dimensi citra diseragamkan menjadi <i>224 × 224 piksel</i> agar sesuai dengan input CNN. Normalisasi dilakukan dengan mengubah rentang nilai piksel dari 0–255 menjadi 0–1 untuk mempercepat konvergensi algoritma optimasi dan menjaga stabilitas pelatihan.
</p>

<p>
Selain itu, teknik <i>Data Augmentation</i> berperan penting dalam mengatasi keterbatasan dataset. Menurut Dian Saputra Aji et al. (2025), augmentasi seperti rotasi dan pembalikan horizontal terbukti efektif dalam mencegah <i>overfitting</i> dengan memperkaya variasi data latih.
</p>

<h4>2.1.3 Convolutional Neural Network (CNN)</h4>
<p>
Convolutional Neural Network (CNN) merupakan arsitektur <i>Deep Learning</i> yang sangat dominan dalam bidang <i>Computer Vision</i>. CNN terinspirasi dari cara kerja korteks visual biologis yang memproses informasi visual secara hierarkis melalui medan reseptif lokal.
</p>

<p>
Lapisan utama CNN adalah <b>Convolutional Layer</b> yang berfungsi mengekstraksi fitur melalui operasi konvolusi menggunakan kernel terlatih. Lapisan awal mendeteksi fitur sederhana seperti tepi dan garis, sementara lapisan dalam mendeteksi pola kompleks seperti tekstur dan bentuk lesi.
</p>

<p>
Lapisan <b>Pooling</b>, khususnya <i>Max Pooling</i>, digunakan untuk mereduksi dimensi spasial fitur sehingga mengurangi beban komputasi serta memberikan ketahanan terhadap pergeseran posisi objek (<i>translation invariance</i>).
</p>

<p>
Lapisan terakhir adalah <b>Fully Connected Layer</b> yang bertindak sebagai pengklasifikasi. Fungsi aktivasi <i>Softmax</i> digunakan untuk menghasilkan probabilitas kelas keluaran, sebagaimana dijelaskan oleh Velasco et al. (2023).
</p>

<h4>2.1.4 Arsitektur MobileNetV3</h4>
<p>
MobileNetV3 merupakan arsitektur CNN ringan yang dikembangkan oleh Google Research untuk perangkat dengan sumber daya terbatas. Arsitektur ini dirancang menggunakan pendekatan <i>Automated Machine Learning</i> melalui <i>Neural Architecture Search</i> dan optimasi NetAdapt (Howard et al., 2019).
</p>

<p>
MobileNetV3 mengintegrasikan modul <i>Squeeze-and-Excitation</i> (SE) yang berfungsi sebagai mekanisme atensi saluran, sehingga model mampu memfokuskan perhatian pada fitur yang relevan seperti tepi dan tekstur lesi kulit.
</p>

<p>
Selain itu, MobileNetV3 memperkenalkan fungsi aktivasi <i>Hard-Swish</i> yang efisien secara komputasi, dirumuskan sebagai:
</p>

<p>
$$h\text{-}swish(x) = x \frac{ReLU6(x+3)}{6}$$
</p>

<p>
Studi Herimanto et al. (2024) membuktikan bahwa kombinasi SE-Block dan Hard-Swish memberikan performa superior dalam klasifikasi tekstur kulit.
</p>

<h4>2.1.5 Transfer Learning dan Fine-Tuning</h4>
<p>
Transfer Learning adalah teknik pembelajaran mesin yang memanfaatkan pengetahuan dari model yang telah dilatih sebelumnya pada dataset besar, seperti ImageNet. Dalam penelitian ini, MobileNetV3 digunakan dengan bobot pre-trained untuk mengatasi keterbatasan data.
</p>

<p>
Tahap pertama adalah <i>feature extraction</i>, di mana lapisan konvolusi dibekukan dan hanya lapisan klasifikasi yang dilatih. Tahap kedua adalah <i>fine-tuning</i>, yaitu melatih kembali beberapa lapisan atas dengan <i>learning rate</i> rendah untuk menyesuaikan fitur dengan karakteristik Ringworm.
</p>

<h4>2.1.6 Metrik Evaluasi Kinerja Model</h4>
<p>
Evaluasi kinerja model dilakukan menggunakan <i>Confusion Matrix</i> yang terdiri dari TP, TN, FP, dan FN. Berdasarkan parameter tersebut, metrik evaluasi yang digunakan adalah Akurasi, Presisi, Recall, dan F1-Score.
</p>

<p><b>Akurasi:</b></p>
<p>
$$Accuracy = \frac{TP + TN}{TP + TN + FP + FN}$$
</p>

<p><b>Presisi:</b></p>
<p>
$$Precision = \frac{TP}{TP + FP}$$
</p>

<p><b>Recall:</b></p>
<p>
$$Recall = \frac{TP}{TP + FN}$$
</p>

<p><b>F1-Score:</b></p>
<p>
$$F1\text{-}Score = 2 \times \frac{Precision \times Recall}{Precision + Recall}$$
</p>

<h3>2.2 Penelitian Terdahulu</h3>
<p>
Tinjauan penelitian terdahulu dilakukan untuk menentukan posisi penelitian dan mengidentifikasi celah riset. Penelitian oleh Taufiqoh dan Purnamasari (2025) menunjukkan keterbatasan arsitektur CNN berat pada dataset kecil. Dian Saputra Aji et al. (2025) membuktikan efektivitas Transfer Learning pada MobileNetV2, namun belum memanfaatkan fitur atensi modern.
</p>

<p>
Penelitian Herimanto et al. (2024) menunjukkan keunggulan MobileNetV3 dalam klasifikasi tekstur kulit, sehingga menjadi dasar kuat pemilihan arsitektur pada penelitian ini.
</p>

<h3>2.3 Kerangka Pemikiran</h3>
<p>
Kerangka pemikiran penelitian ini dimulai dari identifikasi masalah diagnosis Ringworm yang sulit dibedakan secara visual, dilanjutkan dengan pengumpulan data citra kulit kucing, tahap pra-pemrosesan, pengembangan model MobileNetV3 dengan Transfer Learning, evaluasi kinerja menggunakan metrik klasifikasi, hingga menghasilkan model diagnosis Ringworm yang akurat dan efisien secara komputasi.
</p>
