# Dummy

Berikut adalah **isi lengkap untuk bagian "Penjelasan"** pada laporan Anda. Teks ini disusun dengan gaya bahasa akademis laporan praktikum agar Anda tinggal menyalin (copy-paste) ke dalam file Microsoft Word Anda.

---

### **BAB I: ANALISIS SOURCE CODE**

#### **1. Analisis Source Code "Runge4_L0124144_WantechArofiqHudaFirdausyi.m"**

**Penjelasan:**
Kode ini merupakan implementasi fungsi (function) untuk menyelesaikan Persamaan Diferensial Biasa (PDB) menggunakan metode **Runge-Kutta Orde 4**. Fungsi ini menerima parameter berupa *handle* fungsi persamaan diferensial `f`, batas awal `a`, batas akhir `b`, nilai awal `y0`, dan jumlah langkah `N`.

Algoritma dimulai dengan menghitung ukuran langkah (step size) $h = (b-a)/N$. Proses utama terjadi di dalam loop `for` yang berjalan sebanyak $N$ kali. Pada setiap iterasi, program menghitung empat nilai kemiringan (slope), yaitu:
* `k1`: Kemiringan di awal interval.
* `k2` dan `k3`: Kemiringan di titik tengah interval.
* `k4`: Kemiringan di akhir interval.

Nilai estimasi fungsi untuk langkah selanjutnya ($y_{next}$) dihitung menggunakan rata-rata terbobot dari keempat slope tersebut dengan rumus: $y_{i+1} = y_i + \frac{h}{6}(k_1 + 2k_2 + 2k_3 + k_4)$. Selain melakukan perhitungan, kode ini juga menampilkan tabel iterasi yang rapi menggunakan `fprintf` dengan format *fixed-width* untuk memudahkan pemantauan nilai $t$, $k$, dan $T$ pada setiap langkah.

---

#### **2. Analisis Source Code "Kasus1_L0124144_WantechArofiqHudaFirdausyi.m"**

**Penjelasan:**
Kode ini adalah *main script* untuk menyelesaikan **Kasus 1** (Pendinginan Bola Aluminium).
1.  **Pendefinisian Parameter:** Program mendefinisikan konstanta fisika seperti massa ($m$), kalor jenis ($c$), suhu awal ($T0$), suhu lingkungan ($Tc$), serta dimensi dan konduktivitas batang ($l, A, k$). Konstanta-konstanta ini digabungkan menjadi satu nilai `Konstanta_K` sesuai persamaan hukum pendinginan Newton/Fourier yang disederhanakan.
2.  **Fungsi PDB:** Dibuat *function handle* `f` yang merepresentasikan persamaan diferensial $\frac{dT}{dt} = -K(T - Tc)$.
3.  **Metode Eksak:** Sebelum melakukan perhitungan numerik, program menghitung solusi analitik (eksak) menggunakan invers logaritma natural untuk mencari waktu ($t$) yang tepat saat suhu bola mencapai target $100^\circ C$.
4.  **Eksekusi Numerik:** Waktu yang didapat dari perhitungan eksak (`t_eksak`) kemudian digunakan sebagai batas akhir ($b$) untuk metode Runge-Kutta. Program memanggil fungsi `Runge4_...` dengan $N=64$ langkah.
5.  **Evaluasi:** Terakhir, program menghitung galat relatif (error) untuk membandingkan hasil numerik Runge-Kutta dengan target suhu yang diinginkan ($100^\circ C$).

---

#### **3. Analisis Source Code "Lagrange_L0124144_WantechArofiqHudaFirdausyi.m"**

**Penjelasan:**
Kode ini adalah fungsi untuk membentuk persamaan **Interpolasi Polinomial Lagrange** secara dinamis. Keunikan fungsi ini adalah tidak hanya menghitung nilai numerik secara langsung, melainkan membangun rumus polinomial dalam bentuk *string* terlebih dahulu.

Fungsi menerima input matriks `xy` yang berisi data titik. Algoritma menggunakan dua loop bersarang (nested loop):
* **Loop luar (`i`):** Bertanggung jawab untuk menjumlahkan suku-suku basis Lagrange dikalikan dengan nilai $y_i$.
* **Loop dalam (`j`):** Bertanggung jawab untuk membentuk perkalian produk basis Lagrange $L_i(x) = \prod \frac{(x-x_j)}{(x_i-x_j)}$.

Setelah *string* persamaan matematika terbentuk lengkap, fungsi `str2func` digunakan untuk mengonversi *string* tersebut menjadi *anonymous function* yang dapat dipanggil (`handle`). Hal ini memungkinkan fungsi hasil interpolasi digunakan berkali-kali untuk nilai $x$ yang berbeda atau digunakan sebagai input untuk integrasi numerik selanjutnya.

---

#### **4. Analisis Source Code "Simpson38_L0124144_WantechArofiqHudaFirdausyi.m"**

**Penjelasan:**
Fungsi ini mengimplementasikan metode **Integrasi Numerik Simpson 3/8**. Metode ini menghampiri luas di bawah kurva menggunakan polinomial orde 3 pada setiap segmen.
1.  **Validasi:** Kode diawali dengan pengecekan syarat utama Simpson 3/8, yaitu jumlah pias ($N$) harus habis dibagi 3 (`mod(n, 3) ~= 0`). Jika tidak memenuhi, program akan berhenti dan memberikan peringatan.
2.  **Perhitungan:** Lebar pias $h$ dihitung. Vektor $x$ dibuat dari batas bawah $a$ hingga batas atas $b$, dan nilai fungsi $y = f(x)$ dihitung untuk seluruh titik.
3.  **Rumus:** Perhitungan integral dilakukan secara vektorisasi (tanpa loop manual) untuk efisiensi, sesuai rumus Simpson 3/8:
    $$I = \frac{3h}{8} \left( f_0 + 3 \sum f_{i, i \equiv 1,2 \pmod 3} + 2 \sum f_{i, i \equiv 0 \pmod 3} + f_n \right)$$
    Kode menjumlahkan elemen dengan indeks tertentu (kelipatan 3 dikali 2, selain itu dikali 3) untuk mendapatkan hasil integral akhir $I$.

---

#### **5. Analisis Source Code "Kasus2_L0124144_WantechArofiqHudaFirdausyi.m"**

**Penjelasan:**
Kode ini adalah *main script* untuk menyelesaikan **Kasus 2** yang terdiri dari dua bagian: Interpolasi dan Integrasi.
1.  **Interpolasi Lagrange (Kasus 2a):** Program bertujuan mencari kalor jenis pada $T=90^\circ C$.
    * Untuk **Orde 3**, dipilih 4 titik data terdekat yang mengapit nilai 90 (indeks 2 hingga 5). Fungsi Lagrange dipanggil untuk membentuk polinomial dan nilai pada $T=90$ dihitung.
    * Untuk **Orde 2** (pembanding galat), dipilih 3 titik data terdekat.
    * Galat relatif dihitung untuk melihat seberapa besar perbedaan hasil antara penggunaan Orde 3 dan Orde 2.
2.  **Integrasi Simpson 3/8 (Kasus 2b):** Program bertujuan menghitung total kalor (luas di bawah kurva $C(T)$).
    * Fungsi polinomial dibuat menggunakan metode Lagrange dengan memasukkan **seluruh data (6 titik)**, sehingga menghasilkan polinomial orde 5 yang sangat akurat melewati semua titik data.
    * Integrasi dilakukan pada rentang suhu 20 hingga 145.
    * Jumlah pias $N$ ditetapkan sebesar **99**. Nilai ini dipilih karena harus memenuhi syarat Simpson 3/8 (habis dibagi 3) dan cukup besar untuk menghasilkan akurasi tinggi.

---

### **BAB II: ANALISIS HASIL PRAKTIKUM**

#### **1. Analisis "Hasil Kasus1_L0124144_WantechArofiqHudaFirdausyi.m"**

**Penjelasan:**
Hasil eksekusi menunjukkan penyelesaian masalah pendinginan bola aluminium.
1.  **Metode Eksak:** Perhitungan analitik menunjukkan bahwa waktu yang dibutuhkan agar suhu bola turun dari $350^\circ C$ menjadi $100^\circ C$ adalah **607.9303 detik**.
2.  **Metode Runge-Kutta Orde 4:**
    * Metode ini dijalankan dengan rentang waktu dari $t=0$ sampai $t=607.9303$ (hasil eksak) dengan 64 langkah iterasi.
    * Tabel output memperlihatkan penurunan suhu yang konsisten pada setiap iterasi.
    * Pada iterasi terakhir (ke-64), suhu yang dihasilkan adalah **100.0000 $^\circ C$**.
3.  **Kesimpulan Galat:** Galat relatif yang diperoleh adalah **0.000000%**. Hal ini menunjukkan bahwa metode Runge-Kutta Orde 4 sangat presisi dan stabil untuk menyelesaikan PDB linier orde satu seperti kasus pendinginan ini. Hasil numerik konvergen sempurna dengan solusi eksak pada jumlah langkah $N=64$.

---

#### **2. Analisis "Hasil Kasus2_L0124144_WantechArofiqHudaFirdausyi.m"**

**Penjelasan:**
Hasil eksekusi menampilkan solusi untuk pencarian nilai kalor jenis dan total kalor.
1.  **Interpolasi Lagrange:**
    * Nilai kalor jenis pada suhu $90^\circ C$ menggunakan pendekatan Orde 3 adalah **1938.5600 J/kg.C**.
    * Menggunakan pendekatan Orde 2, hasilnya adalah **1938.4000 J/kg.C**.
    * Perbedaan kedua hasil sangat kecil, ditunjukkan dengan estimasi galat relatif hanya sebesar **0.008254%**. Ini mengindikasikan bahwa data eksperimen memiliki tren yang cukup mulus (smooth), sehingga pendekatan polinomial orde rendah pun sudah memberikan hasil yang cukup akurat.
2.  **Integrasi Simpson 3/8:**
    * Program menghitung integral fungsi interpolasi polinomial (yang dibentuk dari semua titik data) pada rentang suhu $20 \le T \le 145$.
    * Dengan menggunakan $N=99$ (kelipatan 3), metode Simpson 3/8 menghasilkan total kalor sebesar **239,099.3923 Joule**.
    * Hasil ini merepresentasikan total energi yang dibutuhkan untuk memanaskan minyak dalam rentang suhu tersebut berdasarkan model data yang diberikan.
