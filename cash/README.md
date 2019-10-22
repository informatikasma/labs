# Cash

{% video https://www.youtube.com/watch?v=AGrpmfxNYG8 %}

{% next %}

## Greedy Algorithms

<!-- Edited from: https://finance.detik.com/moneter/d-3374687/ini-11-uang-rupiah-desain-baru -->
![IDR coins](coins.png)

Saat memberikan kembalian, kemungkinan Anda ingin meminimalkan jumlah koin yang Anda keluarkan untuk setiap pelanggan, jangan sampai Anda kehabisan (atau membuat kesal pelanggan!). Untungnya, ilmu komputer telah memberi semua kasir cara untuk meminimalkan jumlah koin karena: algoritma serakah.

Menurut National Institute of Standards and Technology (NIST) di Amerika Serikat, algoritma serakah adalah salah satu "yang selalu mengambil solusi langsung, atau lokal, sembari mencari jawaban. Algoritma serakah menemukan solusi optimal secara keseluruhan, atau global, untuk beberapa masalah optimasi, tetapi mungkin menemukan solusi yang kurang optimal untuk beberapa contoh masalah lain."

Apa maksud semua itu? Nah, anggaplah bahwa seorang kasir berhutang kepada pelanggan beberapa kembalian dan di laci kasir terdapat koin Rp1000, Rp500, Rp200, dan Rp100. Masalah yang harus dipecahkan adalah memutuskan koin mana dan berapa banyak masing-masing untuk diserahkan kepada pelanggan.

{% next %}

Pikirkan seorang kasir "serakah" sebagai orang yang ingin mengambil pecahan terbesar dari masalah ini sebanyak mungkin dengan setiap koin yang mereka ambil dari laci. Jika seorang pelanggan terutang Rp1800, pecahan pertama (yaitu, langsung, atau lokal) terbesar yang dapat diambil adalah Rp1000. (Pecahan itu dianggap "terbaik" karena membuat kita lebih dekat ke Rp0 lebih cepat daripada koin lainnya.) Dengan demikian, jumlah masalah tinggal Rp1800 - Rp1000 = Rp800.

Dengan mengulangi cara yang sama, Rp1000 tentunya terlalu besar (kasir tidak ingin rugi!), sehingga kasir serakah kita akan beralih ke pecahan Rp500, menyisakan masalah Rp300. Diikuti mengambil pecahan Rp200, dan terakhir Rp100, di mana masalah terselesaikan. Pelanggan menerima satu Rp1000, satu Rp500, satu Rp200, dan satu Rp100: total empat koin.

Ternyata pendekatan serakah ini (mis., Algoritma) tidak hanya optimal secara lokal tetapi juga secara global untuk mata uang Indonesia (dan juga negara lainnya). Selama seorang kasir memiliki cukup pecahan setiap koin, pendekatan terbesar ke terkecil ini akan menghasilkan jumlah koin sekecil mungkin. Seberapa kecil? Baiklah, beritahu kami!

{% next %}

## Detil Implementasi

Implementasikan, dalam `cash.c` di sebelah kanan, sebuah program yang pertama kali menanyakan kepada pengguna berapa banyak kembalian yang terhutang dan kemudian mencetak jumlah minimum koin yang diperlukan.

* Gunakan `get_int` untuk mendapatkan input pengguna dan `printf` untuk menampilkan jawaban Anda. Asumsikan bahwa koin yang tersedia adalah Rp1000, Rp500, Rp200, dan Rp100.
* Anda tidak perlu mencoba memeriksa apakah input pengguna terlalu besar untuk masuk dalam `int`. Cukup pastikan saja *input* yang diberikan adalah bilangan bulat dan bukan bilangan negatif.
* Jika pengguna gagal memberikan nilai non-negatif, program Anda harus meminta kembali kepada pengguna angka yang valid berulang-ulang sampai pengguna mematuhinya.
* Agar kami dapat mengotomatisasi pengujian kode Anda, pastikan bahwa *output* program Anda hanyalah hasil perhitungan jumlah koin 
minimum: bilangan bulat diikuti oleh `\n`.

Program Anda harus berperilaku sesuai contoh di bawah ini.

```bash
$ ./cash
Change owed: 1800
4
```

```bash
$ ./cash
Change owed: -1800
Change owed: foo
Change owed: 1800
4
```

<!-- TODO Walkthrough Video

### Panduan

{% video https://www.youtube.com/watch?v=Y3nWGvqt_Cg %} -->

### Solusi Pengajar

Untuk mencoba implementasi pengajar dari masalah ini, jalankan

```bash
./cash
```

dalam [sandbox ini](http://bit.ly/2VAxlUr).

{% next %}

### Cara Menguji Kode Anda

Apakah kode Anda berfungsi seperti yang ditentukan saat Anda memasukkan *input*:

* `-100` (atau bilangan negatif lainnya)?
* `0`?
* `100` (atau bilangan positif lainnya)?
* huruf atau kata?
* tidak ada input sama sekali, ketika Anda hanya menekan Enter?

Kemudian jalankan `check50` dan `style50` dengan mengetik berikut ini di terminal:

```bash
check50 informatikasma/problems/2019/cash
```

dan akhirnya

```bash
style50 cash.c
```

untuk melihat apakah Anda dapat memformat kode Anda lebih baik. Blok merah berarti menghilangkan spasi, blok hijau berarti menambahkan spasi.

{% next "Siap Mengirim?" %}

## How to Submit

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```bash
submit50 informatikasma/problems/2019/cash
```

Anda dapat mengulangi pengiriman sebanyak apapun yang Anda inginkan sebelum batas waktu pengumpulan.

Kiriman Anda akan dinilai kebenarannya dalam 2 menit, pada saat itu skor Anda akan muncul di https://submit.cs50.io!

Ini adalah Cash.
