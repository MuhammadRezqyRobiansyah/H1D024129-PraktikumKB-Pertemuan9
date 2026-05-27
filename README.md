# Muhammad Rezqy Robiansyah-H1D024129-PraktikumKB-Pertemuan9
# Dokumentasi Program Algoritma Genetika (Knapsack Problem)

Folder ini berisi implementasi Algoritma Genetika (Genetic Algorithm) dalam bahasa Python untuk menyelesaikan masalah Knapsack (Knapsack Problem). Masalah Knapsack adalah masalah optimasi kombinatorial di mana kita harus memilih kombinasi barang dengan bobot dan nilai (harga) tertentu untuk dimasukkan ke dalam tas berkapasitas terbatas, sedemikian rupa sehingga total nilai barang yang dimasukkan mencapai maksimum tanpa melebihi kapasitas tas.

## Penjelasan File Program

Program dipecah menjadi beberapa modul (file) yang masing-masing menangani tahapan spesifik dalam Algoritma Genetika, serta satu file utama (`main.py`) yang menggabungkan seluruh tahapan tersebut.

### 1. `inisiasipopulasi.py`
File ini berisi fungsi untuk membangkitkan populasi awal secara acak.
- **Fungsi `inisialisasi_populasi(jumlah_populasi, jumlah_gen)`**: 
  Fungsi ini membuat sejumlah individu (kromosom) berdasarkan `jumlah_populasi`. Setiap kromosom direpresentasikan sebagai sebuah *list* biner (berisi 0 atau 1) dengan panjang `jumlah_gen` (mewakili jumlah total barang yang tersedia). 
  - `1` berarti barang pada indeks tersebut dipilih (dimasukkan ke dalam tas).
  - `0` berarti barang tidak dipilih.

### 2. `EvaluasiFitness.py`
File ini bertugas untuk menghitung nilai kelayakan (fitness) dari setiap individu di dalam populasi.
- Terdapat daftar `barang` dengan format `(Nama Barang, Harga, Bobot)`.
- **Fungsi `hitung_fitness(kromosom, barang, kapasitas_tas)`**:
  Menghitung total harga dan total bobot dari barang-barang yang direpresentasikan oleh kromosom (di mana gen bernilai 1). 
  - Jika total bobot melebihi `kapasitas_tas`, maka individu tersebut tidak valid atau terkena penalti sehingga nilai fitness dikembalikan sebagai `0`.
  - Jika total bobot masih di bawah atau sama dengan kapasitas, maka nilai fitness adalah total harga dari barang-barang tersebut.

### 3. `selection.py`
File ini menyediakan metode seleksi untuk memilih individu (parent/orang tua) yang akan bereproduksi menghasilkan keturunan (anak/offspring). Semakin tinggi nilai fitness suatu individu, semakin besar peluangnya untuk terpilih.
- **`roulette_wheel_selection`**: Metode seleksi yang menggunakan probabilitas proporsional berdasarkan nilai fitness. Individu dengan fitness besar memiliki "area" rolet yang lebih besar.
- **`tournament_selection`**: Metode seleksi dengan cara mengambil sejumlah individu secara acak (berdasarkan ukuran *k*), lalu memilih individu dengan nilai fitness terbaik di antara kelompok acak tersebut.

### 4. `crossover.py`
File ini menyediakan metode *crossover* (pindah silang) untuk menggabungkan gen dari dua parent (orang tua) untuk menghasilkan anak (keturunan) baru.
- **`one_point_crossover`**: Menentukan satu titik potong secara acak. Gen sebelum titik potong berasal dari parent 1, dan gen setelah titik potong berasal dari parent 2 (berlaku sebaliknya untuk anak kedua).
- **`two_point_crossover`**: Menentukan dua titik potong secara acak dan saling menukar gen di antara kedua titik tersebut antara parent 1 dan parent 2.
- **`uniform_crossover`**: Menggunakan mask (pola biner acak) untuk menentukan gen dari parent mana yang akan diwariskan pada setiap posisi ke masing-masing anak.

### 5. `mutation.py`
File ini menyediakan metode mutasi untuk mengubah sedikit struktur gen pada suatu kromosom secara acak guna menjaga keragaman populasi dan mencegah terjebak di optimum lokal.
- **`swap_mutation`**: Memilih dua posisi secara acak di dalam kromosom dan menukar nilai (gen) pada kedua posisi tersebut.
- **`inversion_mutation`**: Memilih sebuah segmen di dalam kromosom lalu membalikkan (reverse) urutan gen pada segmen tersebut.
- **`uniform_mutation`**: Mengubah setiap gen secara acak (dari 0 ke 1 atau 1 ke 0) berdasarkan nilai *mutation rate* (probabilitas mutasi).

### 6. `main.py`
File ini adalah modul utama yang mengimpor seluruh tahapan di atas dan menjalankan siklus Algoritma Genetika secara utuh.
- **Alur Kerja Utama**:
  1. Menginisialisasi parameter (jumlah generasi, jumlah populasi, probabilitas crossover, probabilitas mutasi, dan kapasitas tas).
  2. Menyiapkan daftar barang (total 9 barang).
  3. Membangkitkan populasi awal.
  4. Melakukan perulangan iterasi sebanyak generasi yang ditentukan (`jumlah_generasi` = 50).
     - Menghitung fitness dari seluruh individu.
     - Menyimpan data fitness terbaik, terendah, dan rata-rata.
     - Melakukan proses seleksi menggunakan *Roulette Wheel Selection*.
     - Melakukan persilangan (*crossover*) menggunakan *One-Point Crossover* sesuai dengan *crossover rate* (0.5).
     - Melakukan mutasi menggunakan *Swap Mutation* sesuai dengan *mutation rate* (0.1).
     - Mengganti populasi lama dengan populasi baru (*offspring*) untuk generasi berikutnya.
  5. Memvisualisasikan perkembangan nilai fitness (Grafik Garis/Scatter) menggunakan *library* `matplotlib`.
  6. Menampilkan hasil individu terbaik (barang apa saja yang terpilih, total harga, dan total bobot).

---

## Cara Pemakaian

### 1. Persyaratan Sistem
Pastikan Anda telah menginstal bahasa pemrograman Python di komputer Anda. Selain itu, Anda perlu menginstal *library* `matplotlib` dan `numpy` untuk keperluan visualisasi grafik data.

Buka terminal/command prompt dan jalankan perintah berikut untuk menginstal *library* yang dibutuhkan:
```bash
pip install matplotlib numpy
```

### 2. Menjalankan Program
Untuk menjalankan keseluruhan algoritma dan melihat hasil penyelesaian masalah Knapsack beserta visualisasinya, Anda hanya perlu menjalankan file `main.py`. 

Gunakan perintah berikut di terminal (pastikan direktori aktif Anda berada di folder `pertemuan9`):
```bash
python main.py
```

### 3. Memahami Output Program
Setelah `main.py` dijalankan, program akan memproses Algoritma Genetika dan:
1. **Menampilkan Grafik**: Sebuah jendela *figure matplotlib* akan muncul yang menunjukkan grafik pergerakan nilai fitness (Fitness Tertinggi, Terendah, dan Rata-rata) dari generasi pertama hingga terakhir.
2. **Menampilkan Hasil Akhir di Terminal**: Setelah Anda menutup grafik, terminal akan mencetak hasil solusi terbaik yang ditemukan oleh Algoritma Genetika, termasuk:
   - Nilai fitness terbaik (Total Harga maksimum).
   - Total bobot dari barang yang dipilih (dipastikan tidak melebihi batas kapasitas tas = 50).
   - Daftar barang yang terpilih masuk ke dalam tas.

### 4. Bereksperimen dengan Parameter
Anda dapat mengubah (modifikasi) performa Algoritma Genetika dengan mengganti parameter pada fungsi `run_ga()` yang berada di bagian paling bawah file `main.py`:
```python
run_ga(
    jumlah_generasi=50,    # Berapa lama siklus berulang, bisa ditambah untuk pencarian lebih mendalam
    jumlah_populasi=20,    # Jumlah individu dalam 1 generasi
    prob_crossover=0.5,    # Probabilitas / peluang gen orang tua disilangkan (0.0 s.d 1.0)
    prob_mutasi=0.1,       # Probabilitas / peluang gen anak mengalami mutasi (0.0 s.d 1.0)
    kapasitas_tas=50       # Batas maksimum beban knapsack
)
```
Anda juga bisa bereksperimen dengan mengganti metode *selection*, *crossover*, atau *mutation* di dalam loop utama pada `main.py` dengan metode lain yang telah tersedia (misalnya mengganti `one_point_crossover` menjadi `uniform_crossover`).