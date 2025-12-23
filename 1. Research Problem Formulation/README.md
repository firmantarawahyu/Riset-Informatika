<h1 align="center">Optimasi Model Convolutional Neural Network (CNN) Berbasis MobileNetV3 untuk Klasifikasi Penyakit Kulit Ringworm Pada Kucing Menggunakan Metode Transfer Learning</h1>

<h2>BAB I <br/> Pendahuluan</h2>

<h3>1.1 Latar Belakang</h3>
<p>
  Kucing merupakan salah satu hewan peliharaan yang paling populer di masyarakat, namun rentan terhadap berbagai gangguan kesehatan, khususnya penyakit kulit. Salah satu penyakit kulit yang paling umum dan persisten pada kucing adalah Dermatophytosis atau yang lebih dikenal sebagai Ringworm. Penyakit ini disebabkan oleh infeksi jamur yang bersifat zoonosis, artinya dapat menular dari hewan ke manusia melalui kontak langsung atau lingkungan yang terkontaminasi. Identifikasi dini terhadap Ringworm sangat krusial, namun diagnosis konvensional secara visual seringkali subjektif dan diagnosis pasti melalui kultur jamur membutuhkan waktu yang lama serta biaya yang relatif mahal.
</p>

<p>
  Perkembangan teknologi kecerdasan buatan, khususnya Deep Learning dengan metode Convolutional Neural Network (CNN), telah menawarkan solusi untuk otomatisasi diagnosis citra medis. Penelitian terkait deteksi penyakit kulit pada hewan peliharaan telah dilakukan oleh beberapa peneliti sebelumnya. Taufiqoh dan Purnamasari (2025) mengembangkan model deteksi penyakit kulit hewan (termasuk Ringworm) menggunakan arsitektur Custom CNN, ResNet-50, dan VGG16. Hasil penelitian mereka menunjukkan bahwa model Custom CNN mencapai akurasi 83%, namun model yang lebih kompleks seperti ResNet-50 dan VGG16 justru mengalami kesulitan konvergensi (overfitting) ketika dilatih pada dataset yang terbatas, serta memiliki ukuran model yang sangat besar sehingga membebani komputasi.
</p>

<p>
  Sebagai alternatif untuk efisiensi komputasi, penggunaan arsitektur yang lebih ringan (lightweight) mulai diterapkan. Dian Saputra Aji et al. (2025) berhasil menerapkan metode Transfer Learning menggunakan arsitektur MobileNetV2 untuk klasifikasi penyakit kulit kucing dengan hasil yang cukup baik. Hal serupa juga dilakukan oleh Idhawati Hestiningsih et al. (2023) yang memanfaatkan MobileNetV2 dan NASNetMobile untuk klasifikasi penyakit kulit. Meskipun MobileNetV2 terbukti ringan, arsitektur ini masih memiliki keterbatasan dalam menangkap fitur-fitur detail yang halus pada lesi kulit dibandingkan generasi penerusnya.
</p>

<p>
  Berdasarkan penelitian Howard et al. (2019), Google telah merilis MobileNetV3 yang merupakan penyempurnaan dari versi sebelumnya. MobileNetV3 mengintegrasikan blok Squeeze-and-Excitation (SE) dan fungsi aktivasi Hard-Swish yang terbukti mampu meningkatkan akurasi secara signifikan dengan latensi yang lebih rendah dibandingkan MobileNetV2. Efektivitas MobileNetV3 dalam domain dermatologi telah dibuktikan oleh Herimanto et al. (2024) yang menggunakannya untuk klasifikasi gangguan kulit pada wajah manusia dengan hasil performa tinggi. Namun, hingga saat ini, penerapan arsitektur MobileNetV3 secara spesifik untuk deteksi penyakit Ringworm pada kucing dengan pendekatan Transfer Learning belum banyak dieksplorasi secara mendalam.
</p>

<p>
  Berdasarkan celah penelitian (research gap) tersebut, di mana model berat (ResNet/VGG) tidak efisien dan model ringan versi lama (MobileNetV2) masih dapat dioptimalkan, penelitian ini mengusulkan penggunaan arsitektur MobileNetV3. Penelitian ini bertujuan untuk melakukan optimasi model CNN menggunakan metode Transfer Learning guna mendapatkan sistem klasifikasi Ringworm yang tidak hanya akurat dalam mengenali pola infeksi jamur, tetapi juga efisien dari segi komputasi.
</p>

<p>
  Oleh karena itu, penelitian ini mengangkat judul "Optimasi Model Convolutional Neural Network (CNN) Berbasis MobileNetV3 untuk Klasifikasi Penyakit Kulit Ringworm Pada Kucing Menggunakan Metode Transfer Learning".
</p>

<h3> 1.2 Rumusan Masalah </h3>
<p>
  Berdasarkan latar belakang yang telah diuraikan, rumusan masalah dalam penelitian ini adalah:
  <ol type=1>
  <li>Bagaimana menerapkan arsitektur MobileNetV3 dengan metode Transfer Learning untuk mengklasifikasikan penyakit Ringworm pada citra kulit kucing?
  </li>
  <li>Bagaimana pengaruh penggunaan pre-trained weights (Transfer Learning) terhadap kecepatan konvergensi dan stabilitas pelatihan model MobileNetV3 dibandingkan dengan pelatihan dari awal (scratch)?</li>
  <li>Berapa tingkat performa model yang dihasilkan berdasarkan parameter evaluasi Accuracy, Precision, Recall, dan F1-Score dalam mendeteksi penyakit Ringworm?</li>
  </ol>
</p>

<h3>1.3 Batasan Masalah</h3>
<p>
  Agar penelitian ini lebih terarah dan fokus pada tujuan utama, penulis menetapkan batasan masalah sebagai berikut:
<ol type=1>
<li>
  Dataset: Data yang digunakan adalah citra sekunder penyakit kulit kucing yang diperoleh dari repositori publik (Roboflow/Kaggle), difokuskan pada dua kelas utama: Ringworm dan Non-Ringworm (Sehat/Penyakit Lain).
</li> 

<li>Metode: Algoritma yang digunakan adalah MobileNetV3 (varian Small atau Large) dengan pendekatan Transfer Learning menggunakan bobot ImageNet.</li>

<li>Lingkup: Penelitian ini berfokus pada pembangunan, pelatihan, dan evaluasi kinerja model. Penelitian tidak mencakup pembuatan aplikasi antarmuka pengguna (user interface) berbasis Android ataupun Website.</li>

<li>Evaluasi: Metrik evaluasi kinerja model dibatasi pada penggunaan Confusion Matrix (Akurasi, Presisi, Recall, F1-Score) dan kurva Loss/Accuracy.</li>
</ol>
</p>

<h3>1.4 Tujuan Penelitian</h3>
<p>Tujuan yang ingin dicapai dalam penelitian ini adalah:
  <ol type=1>
    <li>Membangun model Deep Learning berbasis MobileNetV3 yang mampu mengenali karakteristik visual penyakit Ringworm pada kucing.</li>
    <li>Menganalisis efektivitas metode Fine-Tuning pada Transfer Learning dalam meningkatkan akurasi model pada dataset jumlah terbatas.</li>
    <li>Mengukur kinerja optimal model MobileNetV3 sebagai dasar pengembangan sistem diagnosis penyakit hewan yang efisien di masa depan.</li>
</p>

<h3>1.5 Manfaat Penelitian</h3>
<p>
  Penelitian ini diharapkan dapat memberikan manfaat sebagai berikut:
  <ol type=1>
    <li>Manfaat Teoretis: Memberikan kontribusi ilmiah mengenai perbandingan performa arsitektur lightweight (MobileNetV3) dibanding pendahulunya (MobileNetV2) dalam studi kasus dermatologi veteriner.</li>
    <li>Manfaat Praktis: Menghasilkan model klasifikasi yang siap guna dan efisien yang dapat menjadi rujukan bagi peneliti lain atau pengembang teknologi dalam menciptakan alat bantu diagnosis penyakit zoonosis pada hewan.</li>
  </ol>
</p>
