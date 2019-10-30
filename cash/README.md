# Cash

## Greedy Algorithms

<!-- Edited from: https://finance.detik.com/moneter/d-3374687/ini-11-uang-rupiah-desain-baru -->
![IDR coins](coins.png)

Saat memberikan kembalian, kemungkinan Anda ingin meminimalkan jumlah koin yang Anda keluarkan untuk setiap pelanggan, jangan sampai Anda kehabisan (atau membuat kesal pelanggan!). Untungnya, ilmu komputer telah memberi semua kasir cara untuk meminimalkan jumlah koin karena: algoritma serakah.

Anggaplah bahwa seorang kasir berhutang kepada pelanggan kembalian dan di laci kasir terdapat koin Rp1000, Rp500, Rp200, dan Rp100. Masalah yang harus dipecahkan adalah memutuskan koin mana dan berapa banyak masing-masing untuk diserahkan kepada pelanggan.

{% next %}

Jika seorang pelanggan terutang Rp1800, pecahan pertama terbesar yang dapat diambil adalah Rp1000. (Pecahan itu dianggap "terbaik" karena membuat kita lebih dekat ke Rp0 lebih cepat daripada koin lainnya.) Dengan demikian, jumlah masalah tinggal Rp1800 - Rp1000 = Rp800.

Dengan mengulangi cara yang sama, Rp1000 tentunya terlalu besar (kasir tidak ingin rugi!), sehingga kasir kita akan beralih ke pecahan Rp500, menyisakan masalah Rp300. Diikuti mengambil pecahan Rp200, dan terakhir Rp100, di mana masalah terselesaikan. Pelanggan menerima satu Rp1000, satu Rp500, satu Rp200, dan satu Rp100: total empat koin.

Selama seorang kasir memiliki cukup pecahan setiap koin, pendekatan terbesar ke terkecil ini akan menghasilkan jumlah koin sekecil mungkin. Seberapa kecil? Baiklah, beritahu kami!

{% next %}

## Detail Implementasi

Implementasikan, dalam `cash.c` di sebelah kanan, sebuah program yang pada awalnya menanyakan kepada pengguna berapa banyak kembalian yang terhutang dan kemudian mencetak jumlah minimum koin yang diperlukan.

* Gunakan `get_int` untuk mendapatkan input pengguna dan `printf` untuk menampilkan jawaban Anda. Asumsikan bahwa koin yang tersedia adalah Rp1000, Rp500, Rp200, dan Rp100.
* Pastikan *input* yang diberikan adalah bilangan bulat dan hanya bilangan positif.
* Jika pengguna gagal memberikan nilai positif, program Anda harus meminta kembali kepada pengguna angka yang valid berulang-ulang sampai pengguna mematuhinya.
* Anda tidak perlu menyebutkan jumlah masing-masing denominasi koin yang diberikan, cukup jumlah koin secara keseluruhan saja.

Program Anda harus berperilaku sesuai contoh di bawah ini.

<pre>
$ <u>./cash</u>
Kembalian: <u>1800</u>
4
</pre>

<pre>
$ <u>./cash</u>
Kembalian: <u>-1800</u>
Kembalian: <u>foo</u>
Kembalian: <u>1800</u>
4
</pre>

### Petunjuk

Pertama, Anda harus memvalidasi input pengguna, memastikan bahwa input yang diberikan adalah bilangan positif.

{% spoiler "Memvalidasi input pengguna" %}

Anda dapat menggunakan *loop* `do while`,

```c
do
{
    // Lakukan sesuatu
}
while (kondisi);
```

Buatlah kondisi yang mana jika kondisi tersebut terpenuhi, maka program akan bertanya kembali pada pengguna.

{% endspoiler %}

### Panduan

{% video https://www.youtube.com/watch?v=gm3_NTIo-VA %}

{% spoiler "Solusi Pengajar" %}

Untuk mencoba implementasi pengajar dari masalah ini, jalankan

```bash
./cash
```

dalam [sandbox ini](http://bit.ly/2o86JOt).

{% endspoiler %}

{% next %}

### Cara Menguji Kode Anda

Compile kode Anda, kemudian jalankan program.

{% spoiler "Lupa cara compile?" %}

Anda lupa cara compile kode?

```bash
make cash
```

Anda lupa cara menjalankan program?

```bash
./cash
```

Selalu uji program Anda secara mandiri sebelum menggunakan `check50`!

{% endspoiler %}

Apakah kode Anda berfungsi seperti yang ditentukan saat Anda memasukkan *input*:

* `-100` (atau bilangan negatif lainnya)?
* `0`?
* `100` (atau bilangan positif lainnya)?
* huruf atau kata?
* tidak ada input sama sekali, ketika Anda hanya menekan Enter?

Setelah mengujinya secara mandiri, jalankan `check50` dan `style50` dengan mengetik berikut ini di terminal:

```bash
check50 informatikasma/problems/2019/cash
```

dan akhirnya

```bash
style50 cash.c
```

untuk melihat apakah Anda dapat memformat kode Anda lebih baik. Blok merah berarti menghilangkan spasi, blok hijau berarti menambahkan spasi.

{% next "Siap Mengirim?" %}

## Cara Mengirimkan

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```bash
submit50 informatikasma/problems/2019/cash
```

Anda dapat mengulangi pengiriman sebanyak apapun yang Anda inginkan sebelum batas waktu pengumpulan.

Kiriman Anda akan dinilai kebenarannya dalam 2 menit, dimana skor Anda akan muncul di [https://submit.cs50.io](https://submit.cs50.io)!

Ini adalah Cash.
