# Pennies

## Apa yang harus dilakukan

Implementasikan, dalam `pennies.c` di sebelah kanan, sebuah program yang menghitung total dari mendapatkan jumlah uang berlipat ganda setiap hari selama sebulan, seperti di bawah ini.

<pre>
$ <u>./pennies</u>
Jumlah hari dalam sebulan: <u>30</u>
Jumlah sen pada hari pertama: <u>1</u>
Rp10737418.23
</pre>

{% next %}

## Ganda atau Tidak Sama Sekali

Jika suatu saat diberikan pilihan antara Rp10.000.000 atau [uang sen](https://id.wikipedia.org/wiki/Sen_(mata_uang)) selama sebulan, di mana Anda menerima satu sen pada hari pertama, dua sen pada hari kedua, empat sen pada hari ketiga, dan seterusnya… ambil uang sen itu!

Bagaimanapun, mengapa uang sen? Eksponensial. Jumlah uang itu bertambah dua kali lipat setiap harinya. Pikirkan berapa banyak uang yang akan Anda terima pada hari ke-31 saja, belum lagi pada hari-hari setelahnya:

```
1 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2
  × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2
  × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2

  = 1073741824
```

Secara lebih ringkas, itu sama dengan `1 x 2`<sup>`30`</sup>. Konversikan uang itu menjadi Rupiah (dengan dibagi 100) dan Anda mendapatkan, apa, lebih dari Rp10.000.000? Hanya pada hari tersebut? Gila. 😲

Bagaimana jika Anda diberi lebih dari satu sen pada hari pertama? Atau bulan Februari, Anda akan kehilangan berapa juta? (Lebih baik untuk mengambil uang pada bulan Januari, Maret, Mei, Juli, Agustus, Oktober, atau Desember.) Mari kita cari tahu.

{% next %}

## Detail Implementasi

Implementasikan, dalam file bernama `pennies.c`, sebuah program yang pada awalnya menanyakan kepada pengguna berapa hari ada dalam sebulan dan kemudian bertanya kepada pengguna berapa banyak uang yang akan ia terima pada hari pertama bulan itu. Program kemudian harus menghitung jumlah yang akan diterima pengguna secara total pada akhir bulan (tidak hanya pada hari terakhir) jika uang yang diberikan itu digandakan setiap hari kecuali pada hari pertama, dinyatakan bukan sebagai sen saja, tetapi sebagai Rupiah dan sen . Jika pengguna tidak mengetikkan 28, 29, 30, atau 31 untuk jumlah hari dalam sebulan, program harus meminta pengguna untuk mencoba lagi. Jika pengguna tidak memasukkan bilangan bulat positif untuk jumlah uang hari pertama, program harus meminta pengguna untuk mencoba lagi.

Misalnya, program Anda mungkin berperilaku sebagai berikut.

<pre>
$ <u>./pennies</u>
Jumlah hari dalam sebulan: <u>32</u>
Jumlah hari dalam sebulan: <u>27</u>
Jumlah hari dalam sebulan: <u>31</u>
Jumlah sen pada hari pertama: <u>0</u>
Jumlah sen pada hari pertama: <u>-1</u>
Jumlah sen pada hari pertama: <u>1</u>
Rp21474836.47
</pre>

Perhatikan bagaimana output tersebut menunjukkan bahwa program harus meminta kembali pengguna sebuah input jika ia gagal untuk mematuhi aturan-aturan ini (seperti dengan memasukkan terlalu banyak hari dan uang negatif).

Bagaimana memulainya? Kemungkinannya adalah Anda akan membutuhkan beberapa loop, yang dapat digunakan untuk meminta (dan berpotensi meminta kembali) pengguna berapa jumlah hari, dan loop yang lainnya untuk meminta (dan berpotensi meminta kembali) pengguna jumlah sen pada hari pertama. Bagaimana cara mendapatkan kedua angka itu? Mungkin *Library CS50* menawarkan beberapa opsi?

Anda juga dapat menemukan fungsi dalam file header `math.h` yang dapat membantu saat menangani masalah ini. Lihat [CS50 Programmer's Manual] (https://man.cs50.io/) untuk melihat fungsi mana yang mungkin digunakan. Pastikan, jika Anda menggunakan salah satu dari fungsi itu, untuk menempatkan baris kodenya di bagian atas file `pennies.c` Anda:

```c
#include <math.h>
```

Tentu saja, jika Anda menyimpan jumlah uang yang diterima dalam `int` (yang hanya dapat menyimpan 32 bit), totalnya akan dibatasi oleh `2`<sup>`31`</sup>` - 1` sen. (Mengapa `2`<sup>`31`</sup> dan bukan `2`<sup>`32`</sup>? Dan mengapa `- 1` dari `2`<sup>`31`</sup>?) Karena itu, maka, lebih baik menyimpan total sen Anda dengan tipe `long long`, sehingga pengguna dapat menyimpan hingga 64 bit. (Jangan khawatir jika total hasil perhitungan meluap lebih dari 64 bit dan bahkan menjadi negatif; anggaplah itu hukuman akibat serakah!)

Pastikan untuk memformat total uang sebagai rupiah dan sen (dengan hanya 2 tempat desimal), diawali dengan tanda Rp, sama seperti output di atas. Anda tidak perlu memasukkan titik pemisah ribuan, seperti yang biasanya Anda lakukan.

Agar kami dapat mengotomatiskan beberapa pengujian kode Anda, kami meminta agar ouput terakhir program Anda adalah jumlah yang harus dibayarkan kepada pengguna, diikuti oleh `\n`. Sisa dari ciri khas program Anda, kami serahkan sepenuhnya kepada Anda!

{% next %}

### Petunjuk

Pertama, Anda harus meminta jumlah hari dalam sebulan. Jika pengguna tidak mengetikkan 28, 29, 30, atau 31, program harus meminta pengguna untuk mencoba lagi.

Selanjutnya Anda akan meminta jumlah sen pada hari pertama. Ini harus bilangan bulat positif.

Apakah Anda ingat cara memvalidasi input pengguna?

Ingat, Anda harus melacak total uang yang akan diterima dalam tipe `long long`, sesuai spesifikasi di atas. Anda bisa mendeklarasikan `long long` seperti ini:

```
long long total;
```

dan inisialisasi dengan menetapkan nilai awal.

Sekarang Anda harus menambahkan jumlah uang yang Anda dapatkan pada hari ke 2, hari ke 3, dan seterusnya hingga Anda menambahkan uang untuk setiap hari dalam sebulan. Anda dapat menggunakan fungsi ini:

```c
pow(2, n)
```

di *library* `math.h`. Fungsi tersebut sama seperti operasi matematika pangkat, seperti `2`<sup>`n`</sup>.

Dan tentu saja cetak total Anda sebagai rupiah dan sen, dengan tanda Rp di depan, dan tepat dua tempat desimal.

{% next %}

### Panduan

<!-- {% video https://www.youtube.com/watch?v=gm3_NTIo-VA %} -->

{% spoiler "Solusi Pengajar" %}

Untuk mencoba implementasi pengajar dari masalah ini, jalankan

```bash
./cash
```

dalam [sandbox ini](http://bit.ly/2o86JOt).

{% endspoiler %}

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

* `32` (atau hari lebih dari itu)?
* `27` (atau hari kurang dari itu)?
* `-1` (untuk sen pada hari pertama)?
* huruf atau kata?
* tidak ada input sama sekali, ketika Anda hanya menekan Enter?

Berikut adalah beberapa nilai yang perlu diperiksa:

* 28 hari, 1 sen pada hari pertama menghasilkan Rp2684354.55
* 31 hari, 1 sen pada hari pertama menghasilkan Rp21474836.47
* 29 hari, 2 sen pada hari pertama menghasilkan Rp10737418.22
* 30 hari, 30 sen pada hari pertama menghasilkan Rp322122546.90

Apakah hasil Anda sama persis?

{% next %}

### Pengujian Otomatis

Untuk menguji kebenaran program Anda, Anda dapat menjalankan perintah berikut di jendela terminal.

```
check50 cs50/informatikasma/problems/2019/pennies
```

Untuk memastikan Anda mendapatkan poin penuh untuk gaya kode, Anda mungkin ingin mengeksekusi `style50`!

```
style50 pennies.c
```

## Cara Mengirimkan

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```bash
submit50 informatikasma/problems/2019/pennies
```

Anda dapat mengulangi pengiriman sebanyak apapun yang Anda inginkan sebelum batas waktu pengumpulan.

Kiriman Anda akan dinilai kebenarannya dalam 2 menit, dimana skor Anda akan muncul di [https://submit.cs50.io](https://submit.cs50.io)!

Ini adalah Pennies.
