# Laporan Analisis Data Universities KNIME
## 💻Pendahuluan
Proyek ini mendemonstrasikan proses analisis data end-to-end (dari pembersihan data hingga visualisasi) menggunakan platform alur kerja KNIME Analytics Platform.

1. 📂 Data yang Digunakan
   Data yang dianalisis adalah Data Universitas di Amerika Serikat yang berasal dari file $\texttt{Universities.csv}$. Data ini berisi berbagai metrik kinerja dan biaya dari institusi pendidikan tinggi.Beberapa Kolom Utama dalam Dataset:
   - Informasi Sektor: Kolom Public (1)/ Private (2) untuk mengidentifikasi universitas negeri atau swasta.
   - Biaya Kuliah: Biaya kuliah per tahun (in-state dan out-of-state tuition).
   - Aplikasi: Jumlah aplikasi yang diterima dan yang masuk (penggunaan rumus appl. accepted / appl. rec'd).
   - Kinerja: Tingkat kelulusan (Graduation rate).

2. 🎯 Tujuan Analisis Data
    Tujuan utama dari proyek ini adalah untuk mendapatkan wawasan (insights) awal dari data universitas melalui pembuatan fitur baru dan agregasi statistik.
    Secara spesifik, analisis ini bertujuan untuk:
    - Pembuatan Metrik Selektivitas: Menghitung metrik penting Acceptance Rate (Tingkat Penerimaan) sebagai ukuran seberapa selektif suatu universitas.
    - Kategorisasi Data: Mengkonversi kolom Public (1)/ Private (2) menjadi kategori yang mudah diinterpretasi (Sector Type: Public/Private).
    - Analisis Agregasi: Menghitung rata-rata (Mean) dari biaya kuliah, biaya kamar/asrama, dan Acceptance Rate (tingkat penerimaan) untuk setiap Negara Bagian dan Sektor universitas.
    - Visualisasi Korelasi: Memvisualisasikan hubungan antara {Mean(Acceptance Rate)} (sebagai indikator selektivitas) dan {Mean(Graduation rate)} (sebagai indikator kualitas/efisiensi).
  

## 🛠️Workflow & Fungsi Node KNIME
1. CSV Reader: Ini adalah titik awal workflow Anda. Fungsinya adalah membaca file $\texttt{Universities.csv}$ dan memuat semua data mentah ke dalam lingkungan KNIME agar siap untuk diproses.Aksi: Membawa data ke dalam sistem.
2. Missing Value: Langkah pertama dalam pembersihan data. Node ini mengidentifikasi nilai-nilai yang hilang (null) dalam kolom numerik (seperti biaya dan graduation rate).Aksi: Mengisi nilai yang hilang tersebut (Imputasi) menggunakan nilai Median (nilai tengah) dari masing-masing kolom, memastikan perhitungan selanjutnya berjalan tanpa error.
3. Math Formula: Ini adalah langkah Feature Engineering yang krusial. Node ini digunakan untuk membuat kolom analitis baru yang tidak ada dalam data mentah.Aksi: Menghitung Acceptance Rate (Tingkat Penerimaan) dengan membagi kolom appl. accepted dengan appli. rec'd. Terakhir kolom Acceptance Rate akan ditambahkan ke dataset.
4. Rule Engine: Node ini digunakan untuk transformasi variabel kategori. Data mentah hanya menggunakan angka 1 dan 2 untuk sektor universitas. Aksi: Mengubah kolom Public (1)/ Private (2) menjadi kolom deskriptif baru bernama Sector Type dengan label "Public" atau "Private". Ini membuat data mudah dipahami dan dianalisis.
5. GroupBy: Ini adalah langkah inti Analisis dan Agregasi. Node ini meringkas data untuk menghasilkan insight awal. Aksi: Mengelompokkan universitas berdasarkan State dan Sector Type, lalu menghitung nilai Mean (Rata-rata) dari semua metrik penting (seperti biaya kuliah dan Acceptance Rate untuk setiap grup.
6. Scatter Plot (JavaScript...): Node ini digunakan untuk Visualisasi Data dan eksplorasi korelasi. Aksi: Memplot hasil rata-rata dari node GroupBy. Sumbu X diatur ke Mean(Acceptance Rate) dan Sumbu Y ke Mean(Graduation rate). Visualisasi ini bertujuan untuk menunjukkan hubungan (korelasi) antara selektivitas rata-rata dan tingkat kelulusan rata-rata per sektor.
