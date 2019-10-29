# Pennies

## Apa yang Harus Dilakukan

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

Mengapa uang sen? Eksponensial. Jumlah uang itu bertambah dua kali lipat setiap harinya. Pikirkan berapa banyak uang yang akan Anda terima pada hari ke-31 saja, belum lagi pada hari-hari setelahnya:

```
1 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2
  × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2
  × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2

  = 1073741824
```

Secara lebih ringkas, itu sama dengan <code>1 x 2<sup>30</sup></code>. Konversikan uang itu menjadi Rupiah (dengan dibagi 100) dan Anda mendapatkan, apa, lebih dari Rp10.000.000? Hanya pada hari tersebut? Gila. 😲

Bagaimana jika Anda diberi lebih dari satu sen pada hari pertama? Atau pada bulan Februari, Anda akan kehilangan berapa juta? (Lebih baik untuk mengambil uang pada bulan Januari, Maret, Mei, Juli, Agustus, Oktober, atau Desember.) Mari kita cari tahu.

{% next %}

## Detail Implementasi

Implementasikan, dalam file bernama `pennies.c`, sebuah program yang pada awalnya menanyakan kepada pengguna berapa hari ada dalam sebulan dan kemudian bertanya kepada pengguna berapa banyak uang yang akan ia terima pada hari pertama bulan itu. Program kemudian harus menghitung jumlah yang akan diterima pengguna secara total pada akhir bulan (tidak hanya pada hari terakhir) jika uang yang diberikan itu digandakan setiap hari kecuali pada hari pertama, dinyatakan bukan sebagai sen saja, tetapi sebagai Rupiah dan sen. Jika pengguna tidak mengetikkan 28, 29, 30, atau 31 untuk jumlah hari dalam sebulan, program harus meminta pengguna untuk mencoba lagi. Jika pengguna tidak memasukkan bilangan bulat positif untuk jumlah uang hari pertama, program harus meminta pengguna untuk mencoba lagi.

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

Anda juga dapat menemukan fungsi dalam file header `math.h` yang dapat membantu saat menangani masalah ini. Lihat [CS50 Programmer's Manual](https://man.cs50.io/) untuk melihat fungsi mana yang mungkin digunakan. Pastikan, jika Anda menggunakan salah satu dari fungsi itu, untuk menempatkan baris kode berikut di bagian atas file `pennies.c` Anda:

```c
#include <math.h>
```

Tentu saja, jika Anda menyimpan jumlah uang yang diterima dalam `int` (yang hanya dapat menyimpan 32 bit), totalnya akan dibatasi oleh <code>2<sup>31</sup> - 1</code> sen. (Mengapa <code>2<sup>31</sup></code> dan bukan <code>2<sup>32</sup></code>? Dan mengapa `- 1` dari <code>2<sup>31</sup></code>?) Karena itu, maka, lebih baik menyimpan total sen Anda dengan tipe `long long`, sehingga pengguna dapat menyimpan hingga 64 bit. (Jangan khawatir jika total hasil perhitungan meluap lebih dari 64 bit dan bahkan menjadi negatif; anggaplah itu hukuman akibat serakah!)

Pastikan untuk memformat total uang sebagai rupiah dan sen (dengan hanya 2 tempat desimal), diawali dengan tanda Rp, sama seperti output di atas. Anda tidak perlu memasukkan titik pemisah ribuan, seperti yang biasanya Anda lakukan.

Agar kami dapat mengotomatiskan beberapa pengujian kode Anda, kami meminta agar ouput terakhir program Anda adalah jumlah yang harus dibayarkan kepada pengguna, diikuti oleh `\n`. Sisa dari ciri khas program Anda, kami serahkan sepenuhnya kepada Anda!

{% next %}

### Petunjuk

Pertama, Anda harus meminta jumlah hari dalam sebulan. Jika pengguna tidak mengetikkan 28, 29, 30, atau 31, program harus meminta pengguna untuk mencoba lagi.

Selanjutnya Anda akan meminta jumlah sen pada hari pertama. Ini harus bilangan bulat positif.

Apakah Anda ingat cara memvalidasi input pengguna?

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

Anda mungkin harus menggunakan gabungan dari dua *Boolean expression* pada kondisi validasi input jumlah hari.

{% spoiler "Menggabungkan dua *Boolean expression*%}

Untuk menggabungkan dua *Boolean expression*, Anda dapat menggunakan operator berikut:

* `&&`, operator AND, akan menghasilkan `true` jika *kedua ekspresi* sebelum dan sesudahnya bernilai `true`
* `||`, operator OR, akan menghasilkan `true` jika *salah satu ekspresi* sebelum dan sesudahnya bernilai `true`
* `!`. operator NOT, akan menghasilkan *kebalikan dari ekspresi* apapun setelahnya.

Sebagai contoh:

```c
bool a = 3 < 5;     // true
bool b = 2 >= 8;    // false
```

Variabel `a` berisi `true` karena `3 < 5` memang benar. Variabel `b` berisi `false` karena `2 >= 8` tentunya salah.

Sekarang, lihatlah kode berikut:

```c
bool c = a && b;    // false
```

Variabel `c` berisi `false` karena operator `&&` hanya akan menghasilkan `true` jika `a` dan `b` bernilai `true`.

```c
bool d = a || b;    // true
```

Variabel `d` berisi `true` karena operator `||` akan menghasilkan `true` jika salah satu dari `a` atau `b` bernilai `true`.

```c
bool e = !d;        // false
```

Variabel `e` berisi `false` karena operator `!` akan memberikan kebalikan dari nilai `d`.

Berdasarkan operator-operator tersebut, kira-kira operator apa yang cocok digunakan untuk mengevaluasi kondisi jumlah hari yang dapat diinputkan oleh pengguna?

{% endspoiler %}

Ingat, Anda harus melacak total uang yang akan diterima dalam tipe `long`, sesuai spesifikasi di atas. Anda bisa mendeklarasikan `long` seperti ini:

```
long total;
```

dan inisialisasi dengan menetapkan nilai awal.

Sekarang Anda harus menambahkan jumlah uang yang Anda dapatkan pada hari ke 2, hari ke 3, dan seterusnya hingga Anda menambahkan uang untuk setiap hari dalam sebulan. Anda dapat menggunakan fungsi ini:

```c
pow(2, n)
```

di *library* `math.h`. Fungsi tersebut sama seperti operasi matematika pangkat, seperti <code>2<sup>n</sup></code>.

Dan tentu saja cetak total Anda sebagai rupiah dan sen, dengan tanda Rp di depan, dan tepat dua tempat desimal.

{% spoiler "Output tidak menghasilkan bilangan desimal?" %}

Tipe data yang digunakan haruslah yang mendukung bilangan desimal. Tipe `long` hanya mendukung bilangan bulat. Anda membutuhkan tipe `double`, yang merupakan saudara dari `float` namun dapat menampung bilangan lebih besar, yaitu 8 byte (64 bit).

{% endspoiler %}

{% spoiler "Output selalu menghasilkan `.00`?" %}

Pada saat kita menghitung total uang kita menggunakan tipe `long`, sedangkan saat diubah ke rupiah kita menggunakan tipe `double`. Meskipun tidak akan menyebabkan *error* pada saat proses *compiling*, namun output tidak akan sesuai yang diharapkan.

Tipe `long` tidak dapat menyimpan bilangan desimal, sehingga kita harus menggunakan *type casting* seperti ini:

```c
long bilanganbulat = 1;
double hasil = (double) bilanganbulat / 10;
printf("%f", hasil);    // 0.100000
```

Perhatikan bahwa kita menggunakan `(double)` untuk mengkonversi variabel `bilanganbulat` yang awalnya bertipe `long` menjadi tipe `double`.

{% endspoiler %}

{% next %}

<!-- ### Panduan -->

<!-- {% video https://www.youtube.com/watch?v=gm3_NTIo-VA %} -->

<!-- {% spoiler "Solusi Pengajar" %}

Untuk mencoba implementasi pengajar dari masalah ini, jalankan

```bash
./pennies
```

dalam [sandbox ini](http://bit.ly/2o86JOt).

{% endspoiler %} -->

### Cara Menguji Kode Anda

Compile kode Anda, kemudian jalankan program.

{% spoiler "Lupa cara compile?" %}

Anda lupa cara compile kode?

```bash
make pennies
```

Anda lupa cara menjalankan program?

```bash
./pennies
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

{% next %}

## Cara Mengirimkan

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```bash
submit50 informatikasma/problems/2019/pennies
```

Anda dapat mengulangi pengiriman sebanyak apapun yang Anda inginkan sebelum batas waktu pengumpulan.

Kiriman Anda akan dinilai kebenarannya dalam 2 menit, dimana skor Anda akan muncul di [https://submit.cs50.io](https://submit.cs50.io)!

Ini adalah Pennies.
