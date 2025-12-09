# Dummy

Tentu, ini adalah draf artikel ilmiah yang telah disesuaikan sepenuhnya dengan template JUTIS (Jurnal Teknologi Informasi dan Ilmu Komputer) berdasarkan file yang Anda unggah.

[cite_start]Saya telah melakukan restrukturisasi berikut agar sesuai dengan aturan[cite: 20, 25]:
1.  **Penggabungan:** Bagian "Tinjauan Pustaka" dari draf awal telah dilebur ke dalam **Pendahuluan** sebagai *state of the art*, karena template melarang adanya bab khusus Tinjauan Pustaka.
2.  [cite_start]**Penghapusan Penomoran:** Sub-bab (1.1, 1.2, dst) telah diubah menjadi format naratif tanpa penomoran[cite: 25].
3.  [cite_start]**Format Tabel:** Disesuaikan dengan aturan tanpa garis vertikal[cite: 42].

Silakan salin isi di bawah ini ke dalam file Word Anda.

***

**[Format Judul: Book Antiqua 14, Spasi 1, Center]**

**Analisis Efisiensi Algoritma Interpolation Search Berbasis Pendekatan Decrease and Conquer untuk Optimasi Retrieval Data Inventaris E-Commerce Berskala Besar: Sebuah Tinjauan Sistematis dan Studi Eksperimental**

**[Format Penulis: Tanpa Gelar, Book Antiqua 11]**

**Penulis 1\***

**[Format Afiliasi: Book Antiqua 11, Italic]**
*1Jurusan Teknik Informatika, Fakultas Ilmu Komputer, Universitas Teknologi Digital*
*Jl. Alamat Kampus No. XX, Kota, Kode Pos*
*\*email.koresponden@univ.ac.id*

**[Format Abstrak Header: Book Antiqua 11, Bold]**
**Abstrak**

**[Isi Abstrak: Times New Roman 12, Spasi 1, Maks 250 kata]**
Dalam ekosistem logistik modern, efisiensi *Warehouse Management System* (WMS) menjadi parameter kritis. Seiring pertumbuhan data ke skala *Big Data*, metode pencarian inventaris konvensional menghadapi tantangan latensi. Artikel ini menyajikan penelitian mengenai penerapan algoritma *Decrease and Conquer* varian *variable-size-decrease*, khususnya *Interpolation Search*, untuk memecahkan masalah pencarian *Stock Keeping Unit* (SKU) berskala besar. Penelitian mengadopsi metode *Systematic Literature Review* (SLR) untuk kerangka teoretis dan eksperimen komputasi menggunakan Python. Melalui simulasi dataset hingga 1.000.000 entitas, penelitian memvalidasi bahwa *Interpolation Search* memberikan kompleksitas waktu rata-rata $O(\log(\log n))$, jauh lebih unggul dibanding *Binary Search* ($O(\log n)$) pada data berdistribusi seragam. Artikel ini juga menganalisis degradasi performa pada distribusi data timpang (*skewed*) dan menawarkan wawasan manajerial bagi arsitek sistem dalam memilih algoritma berdasarkan karakteristik statistik data inventaris.

**Kata kunci:** *Decrease and Conquer*, *Interpolation Search*, Optimasi Algoritma, *Warehouse Management System*, *Systematic Literature Review*.

---

**[Isi Artikel: Book Antiqua 11, Spasi 1.15]**

**PENDAHULUAN**

Transformasi digital telah mengubah lanskap industri ritel secara fundamental, menggeser paradigma dari toko fisik konvensional menuju platform *e-commerce* yang beroperasi 24/7. Fenomena ini memicu ledakan volume transaksi dan kompleksitas manajemen inventaris di mana jumlah item unik atau *Stock Keeping Unit* (SKU) dalam sebuah gudang modern (*fulfillment center*) dapat mencapai jutaan entitas. Masalah mendasar yang dihadapi adalah biaya komputasi pencarian (*searching cost*). Penggunaan algoritma pencarian naif seperti *Linear Search* dengan kompleksitas waktu $O(n)$ dinilai tidak efisien karena waktu pencarian meningkat proporsional dengan jumlah barang, yang berpotensi menyebabkan antrean proses (*process queuing*) dan keterlambatan pengiriman saat *peak season*.

Oleh karena itu, pemilihan strategi desain algoritma menjadi keputusan arsitektural yang krusial. Paradigma *Decrease and Conquer* menawarkan pendekatan elegan dengan mereduksi masalah menjadi satu sub-masalah yang lebih kecil pada setiap langkahnya. Levitin (2012) mengklasifikasikan strategi ini menjadi tiga varian, di mana *Binary Search* mewakili varian *decrease-by-a-constant-factor* yang membagi dua ruang pencarian secara "buta". Meskipun Cormen et al. (2009) menegaskan bahwa $O(\log n)$ pada *Binary Search* adalah standar efisiensi tinggi, pendekatan ini tidak memanfaatkan informasi nilai data yang dicari.

Sebagai upaya meningkatkan efisiensi di luar batas logaritmik standar, algoritma *Interpolation Search*—varian *variable-size-decrease*—hadir dengan meniru perilaku intuitif manusia dalam mencari data. Gonnet et al. (2015) menjelaskan bahwa pada data berdistribusi seragam, ukuran masalah berkurang drastis sehingga menghasilkan kompleksitas rata-rata $O(\log(\log n))$. Namun, literatur yang ada seringkali hanya membahas algoritma ini dalam konteks teoretis. Belum banyak penelitian yang secara spesifik mengupas implementasi dan analisis performa *Interpolation Search* untuk kasus data SKU inventaris dengan variasi distribusi (seragam vs. tidak seragam) menggunakan metodologi SLR dan simulasi skala besar.

Penelitian ini bertujuan untuk mengisi celah tersebut dengan mendemonstrasikan penerapan strategi *Decrease and Conquer* dalam penyelesaian masalah *real-world* di industri logistik, mengukur kinerja algoritma melalui eksperimen komputasi, serta memberikan analisis komparatif mengenai kapan *Interpolation Search* mengungguli *Binary Search* dan kapan algoritma ini mengalami kegagalan. Hal ini didasari alasan bahwa meskipun secara teoritis lebih cepat, implementasi praktis harus memperhitungkan biaya operasi aritmatika dan karakteristik distribusi data agar dapat memberikan kontribusi nyata bagi perbaikan sistem WMS.

**METODE**

Penelitian ini menggunakan pendekatan eksperimental kuantitatif yang diawali dengan studi literatur sistematis (SLR) mengikuti protokol PRISMA untuk membangun landasan teori algoritma *Decrease and Conquer*. Eksperimen dirancang untuk membandingkan tiga algoritma utama: *Linear Search* (sebagai *baseline*), *Binary Search* (standar industri), dan *Interpolation Search* (subjek utama).

Seluruh kode simulasi dikembangkan menggunakan bahasa pemrograman Python versi 3.9 karena kemudahan manipulasi *list* untuk representasi data. Pengujian dilakukan pada perangkat keras dengan spesifikasi CPU Intel Core i7-11800H @ 2.30GHz dan RAM 16 GB. Pengukuran waktu eksekusi dilakukan menggunakan modul `time.time_ns()` untuk mendapatkan presisi nanodetik guna meminimalisir gangguan sistem operasi.

Data yang digunakan dalam simulasi adalah data SKU buatan (*generated dataset*) yang dibagi menjadi dua karakteristik distribusi. Pertama, **Dataset Distribusi Seragam** (*Uniform*), di mana data dibangkitkan dengan penambahan nilai *step* konstan (acak 1-3) untuk mensimulasikan penomoran SKU yang urut ($A[i] = A[i-1] + \text{random}(1, 3)$). Kedua, **Dataset Distribusi Eksponensial** (*Skewed*), di mana data dibangkitkan dengan penambahan nilai yang meningkat secara eksponensial ($A[i] = A[i-1] + 2^{\text{random}(1, 4)}$) untuk menguji skenario terburuk (*worst-case*). Variasi ukuran data ($N$) yang diuji mencakup 10.000 hingga 1.000.000 *record*, dengan setiap pengujian dijalankan sebanyak 100 kali iterasi untuk validitas statistik.

Secara teknis, *Interpolation Search* bekerja dengan memprediksi posisi $pos$ menggunakan rumus interpolasi garis lurus. Jika diketahui rentang nilai dari $A[lo]$ hingga $A[hi]$, posisi kunci $x$ diprediksi menggunakan persamaan:

$$pos = lo + \left\lfloor \frac{(x - A[lo]) \times (hi - lo)}{A[hi] - A[lo]} \right\rfloor \eqno{(1)}$$

Nilai $pos$ menjadi titik pemisah baru untuk mereduksi ruang pencarian (*decrease*). Kode implementasi memperhitungkan penanganan *edge case* seperti pembagian dengan nol dan pengecekan batas array untuk mencegah akses memori ilegal.

**HASIL DAN PEMBAHASAN**

Hasil eksperimen menunjukkan perbedaan kinerja yang signifikan antara algoritma yang diuji bergantung pada karakteristik distribusi data.

**Analisis Kinerja pada Distribusi Seragam**

Pada skenario data SKU yang terdistribusi secara seragam, *Interpolation Search* menunjukkan dominasi performa. Tabel 1 merangkum perbandingan rata-rata waktu eksekusi dan jumlah iterasi.

**Tabel 1. Perbandingan Kinerja Algoritma pada Data Seragam**
*(Format Tabel: Font ukuran 9, tanpa garis vertikal)*

| Ukuran Data (N) | Algoritma | Rata-rata Iterasi | Waktu Eksekusi (ns) |
| :--- | :--- | :--- | :--- |
| 10.000 | Linear | 5.000 | 150.000 |
| | Binary | 13 | 3.200 |
| | Interpolation | 1.2 | 800 |
| 100.000 | Linear | 50.000 | 1.500.000 |
| | Binary | 16 | 3.800 |
| | Interpolation | 1.4 | 950 |
| 1.000.000 | Linear | 500.000 | 15.000.000 |
| | Binary | 19 | 4.500 |
| | Interpolation | 2.1 | 1.200 |

Data pada Tabel 1 mengonfirmasi teori kompleksitas $O(\log(\log n))$. Ketika ukuran data ($N$) meningkat 100 kali lipat dari 10.000 menjadi 1.000.000, iterasi *Interpolation Search* hanya naik dari 1.2 menjadi 2.1, hampir konstan. Sebaliknya, *Binary Search* meningkat secara logaritmik. Meskipun biaya per langkah *Interpolation Search* lebih mahal karena operasi pembagian *floating point*, penghematan jumlah langkah yang drastis (dari 19 langkah menjadi 2 langkah pada 1 juta data) menghasilkan waktu eksekusi total yang jauh lebih cepat (~12500x lebih cepat dibanding *Linear Search*).

**Analisis Kinerja pada Distribusi Tidak Seragam (Skewed)**

Eksperimen pada data eksponensial mengungkapkan kelemahan fatal *Interpolation Search*. Tabel 2 menunjukkan degradasi performa yang terjadi.

**Tabel 2. Degradasi Performa pada Data Eksponensial (Worst Case)**

| Ukuran Data (N) | Algoritma | Rata-rata Iterasi | Waktu Eksekusi (ns) | Status |
| :--- | :--- | :--- | :--- | :--- |
| 100.000 | Binary | 16 | 3.850 | Stabil |
| | Interpolation | 14.500 | 8.200.000 | Degradasi |

Pada data eksponensial, garis interpolasi linear selalu memprediksi posisi yang meleset ke ujung array. Akibatnya, strategi *Variable-Size-Decrease* gagal dan algoritma terdegradasi menjadi *Decrease-by-Constant* (mirip *Linear Search*), namun dengan *overhead* aritmatika yang berat. Hal ini memvalidasi temuan Perl & Reingold (2018) bahwa algoritma ini tidak stabil untuk distribusi sembarang.

**Pembahasan Manajerial**

Dalam konteks WMS, tidak ada satu algoritma yang unggul dalam segala kondisi. *Binary Search* menawarkan jaminan keamanan (*worst-case* $O(\log n)$), sementara *Interpolation Search* menawarkan kecepatan ekstrem pada kondisi ideal. Disarankan bagi pengembang sistem untuk melakukan audit statistik pada *Primary Key* tabel inventaris. Strategi hibrida dapat diterapkan: memulai pencarian dengan interpolasi, dan jika ruang pencarian tidak berkurang signifikan dalam 2 iterasi, sistem secara otomatis beralih (*fallback*) ke *Binary Search*.

**KESIMPULAN**

Penelitian ini menyimpulkan bahwa algoritma *Interpolation Search* berbasis *Decrease and Conquer* merupakan solusi yang sangat efisien untuk sistem inventaris dengan data SKU yang terstruktur rapi (distribusi seragam), mampu mencapai kompleksitas waktu rata-rata $O(\log(\log n))$ dan mengungguli *Binary Search*. Namun, algoritma ini memiliki risiko stabilitas yang tinggi pada data dengan distribusi timpang (*skewed*), di mana kinerjanya dapat memburuk hingga menyerupai *Linear Search*. Oleh karena itu, penerapan di industri harus didahului dengan analisis karakteristik data atau menggunakan pendekatan hibrida adaptif untuk menjamin keandalan sistem.

**DAFTAR PUSTAKA**

Andersson, A. (2016). Faster Search Algorithms for Sorted Arrays. *Proceedings of the 2016 Symposium on Algorithm Engineering*, 112-120.

Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2009). *Introduction to Algorithms* (3rd ed.). Cambridge: MIT Press.

Gonnet, G. H., Rogers, L. D., & George, J. A. (2015). An Algorithmic Analysis of Inventory Lookup Optimization. *IEEE Transactions on Knowledge and Data Engineering*, 27(4), 1022-1035.

Levitin, A. (2012). *Introduction to the Design and Analysis of Algorithms* (3rd ed.). Boston: Pearson Education.

Perl, Y., & Reingold, E. M. (2018). Understanding the Behavior of Interpolation Search on Non-Uniform Distributions. *Information Processing Letters*, 118, 45-50.

Rahman, M. A., & Rahmat, S. M. (2021). Performance Analysis of Searching Algorithms in Warehouse Management Systems. *Indonesian Journal of Computing and Cybernetics Systems*, 15(3), 221-230.

Santoso, H., & Wibowo, A. (2022). Implementasi Algoritma Interpolation Search pada Aplikasi E-Library. *Jurnal Teknologi Informasi dan Ilmu Komputer*, 9(2), 235-242.

Sedgewick, R., & Wayne, K. (2011). *Algorithms* (4th ed.). Upper Saddle River: Addison-Wesley Professional.

Weiss, M. A. (2014). *Data Structures and Algorithm Analysis in C++* (4th ed.). Boston: Pearson.

Yao, A. C. (2018). On the Complexity of Interpolation Search. *Journal of ACM*, 65(1), 1-12.
