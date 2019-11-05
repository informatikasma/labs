# ISBN

<!-- TODO Introduction Video

{% video https://www.youtube.com/watch?v=sxXQ-jgUIg8 %}

{% next %} -->

## Apa yang Harus Dilakukan

Terapkan program untuk memvalidasi nomor ISBN-10.

<pre>
$ <u>./isbn</u>
ISBN: <u>0307476464</u>
YES
</pre>

{% next %}

Seperti yang Anda ketahui, sebagian besar buku apa pun yang Anda pinjam atau beli memiliki International Standard Book Number, atau dikenal sebagai __ISBN__ atau ISBN-10, ["angka 10 digit yang secara unik mengidentifikasi buku dan produk seperti buku yang diterbitkan secara internasional."](http://www.isbn.org/standards/home/isbn/us/isbnqa.asp) Buku-buku yang diterbitkan sejak 2007 mungkin juga memiliki ISBN-13, angka 13 digit dengan tujuan yang sama, tetapi abaikan saja dulu.

Ternyata digit terakhir ISBN-10 adalah *"check digit"*, atau dikenal (dalam konteks biner) sebagai *"checksum,"* nomor yang terkait secara matematis dengan digit sebelumnya. Digit ISBN-10 diharuskan mematuhi suatu formula, mirip nomor kartu kredit, dan *check digit* ini memungkinkan Anda untuk memeriksa apakah sembilan digit ISBN-10 lainnya (kemungkinan besar) valid tanpa harus memeriksa, katakanlah, database buku.

Menurut Manual Pengguna ISBN Badan Internasional ISBN, ["*Check digit* adalah digit terakhir dari ISBN. Ini dihitung pada modulus 11 dengan bobot 10-2, menggunakan X sebagai pengganti 10 jika sepuluh muncul sebagai *check digit*."](http://www.isbn-international.org/en/userman/download/ISBNmanual.pdf)

![Rly?](orly.jpg)

{% next %}

*Yes rly*, tapi apa maksudnya? Manual tersebut menguraikan. "Ini berarti bahwa masing-masing dari sembilan digit pertama ISBN&mdash;tidak termasuk digit periksa itu sendiri&mdash;dikalikan dengan angka mulai dari 10 hingga 2 dan jumlah produk yang dihasilkan, ditambah digit periksa, harus dapat dibagi dengan 11 tanpa sisa."

Oke, lebih baik, tapi masih agak tidak jelas. Mari kita tentukan digit periksa dalam bentuk rumus. Untungnya, berkat "aritmatika modular," kita dapat menyederhanakan definisi formal tadi menggunakan bobot mulai dari 1 hingga 9 bukannya 10 hingga 2. Sebenarnya benar-benar sangat sederhana. Jika x<sub>1</sub> mewakili digit pertama ISBN-10 dan x<sub>10</sub> yang terakhir, itu menunjukkan bahwa:

x<sub>10</sub> = (1·x<sub>1</sub> + 2·x<sub>2</sub> + 3·x<sub>3</sub> + 4·<sub>x4</sub> + 5·x<sub>5</sub> + 6·x<sub>6</sub> + 7·x<sub>7</sub> + 8·x<sub>8</sub> + 9·x<sub>9</sub>) mod 11

Dengan kata lain, untuk menghitung digit kesepuluh ISBN-10, kalikan digit pertama dengan 1, digit kedua dengan 2, digit ketiga dengan 3, digit keempat dengan 4, digit kelima dengan 5, digit keenam dengan 6, digit ketujuh dengan 7, digit kedelapan dengan 8, dan digit kesembilan oleh 9. Ambil jumlah dari perhitungan-perhitungan itu dan kemudian bagi dengan 11. Sisa pembagiannya akan menjadi digit kesepuluh ISBN-10! Namun, jika sisanya 10, digit kesepuluh harus dicetak sebagai X agar jumlah digit tidak bertambah menjadi 11.

{% next %}

Mari kita coba. ISBN-10 untuk *Absolute Beginner's Guide to C*, salah satu buku yang direkomendasikan mata pelajaran, adalah 0-789-75198-4, digit kesepuluhnya, tentu saja, 4. Tetapi apakah perhitungannya benar? Baiklah, mari kita hitung jumlahnya menggunakan sembilan digit pertama ISBN-10 (disorot dengan huruf tebal):

1·**0** + 2·**7** + 3·**8** + 4·**9** + 5·**7** + 6·**5** + 7·**1** + 8·**9** + 9·**8** = 290

Jika kita sekarang membagi jumlah itu dengan 11, kita mendapatkan 290 ÷ 11 = 26 sisa 4. Bagus sekali, ISBN itu sah! Sebenarnya, juga berkat aritmatika modular, kita bisa memasukkan digit kesepuluh itu ke dalam jumlah kita dan mengalikannya dengan 10:


1·**0** + 2·**7** + 3·**8** + 4·**9** + 5·**7** + 6·**5** + 7·**1** + 8·**9** + 9·**8** + 10·**4** = 330

Jika kita sekarang membagi jumlah ini dengan 11, kita mendapatkan 330 ÷ 11 = 30 tanpa sisa sama sekali, yang merupakan cara yang setara dengan mengatakan ISBN-10 itu sah! Dinyatakan lebih formal, 0 ≡ 330 (mod 11).

Semoga formula terakhir tadi membuat matematika jadi lebih menarik.

Jadi, menghitung digit cek ini tidak sulit, tetapi sedikit membosankan dengan tangan. Mari kita menulis sebuah program.

{% next %}

# Detail Implementasi

Dalam file bernama `isbn.c`, tulis sebuah program yang meminta pengguna sebuah nomor ISBN-10 dan kemudian laporkan (melalui `printf`) apakah nomor itu sah. Agar kami dapat mengotomatiskan beberapa pengujian kode Anda, kami meminta agar *output* terakhir program Anda adalah `YA\n` atau `TIDAK\n`, tidak lebih, tidak kurang.

Untuk menyederhanakan, Anda dapat mengasumsikan bahwa input pengguna akan tepat sepuluh digit desimal (mis., Tanpa tanda hubung (-) dan X), digit pertama bahkan mungkin nol, seperti dalam kasus buku yang kami rekomendasikan.

Tapi jangan berasumsi bahwa input pengguna akan masuk dalam sebuah `int`! Ingat, bagaimanapun juga, bahwa nilai terbesar yang dapat ditampung dalam sebuah int adalah <code>2<sup>32</sup> - 1 = 4.294.967.295</code> (itupun jika dideklarasikan sebagai `unsigned`).

Angka 4.294.967.295 memang berjumlah 10 digit, tetapi ada kemungkinan masalah. (Apa kira-kira?) Lebih aman dan menggunakan `get_long` dari *library* CS50 untuk mendapatkan input pengguna. (Mengapa?)

Oke, jadi Anda sudah mendapat input. Apa yang harus kamu lakukan? Anggaplah bahwa suatu variabel `x` berisi 10 digit `long` (tanpa awalan nol). Bagaimana Anda bisa mendapatkan digit kesepuluh (mis., paling kanan)? Nah bagaimana dengan ini?

```c
int kesepuluh = x % 10;
```

Apakah Anda mengerti mengapa kode itu dapat mengambil digit ke sepuluh? Jangan melanjutkan sampai Anda sadar mengapa!

Bagaimana, sekarang, Anda bisa mendapatkan angka kesembilan variabel `x`? Nah, mengapa kita tidak pertama-tama menyingkirkan digit kesepuluh dengan menggeser setiap digit ke kanan?

```c
x = x / 10;
```

Bagaimana dengan trik itu? Apakah Anda mengerti mengapa itu berhasil? Digit kesembilan, sekarang, dapat diambil:

```c
int kesembilan = x % 10;
```

{% next %}

Ada pola di sini. Anda jangan menyalin / menempelkan baris seperti di atas sembilan atau sepuluh kali. Ingatlah bahwa Anda dapat menggunakan Loop.

Untuk mengkompilasi program Anda, ketik

```bash
make isbn
```

Dengan asumsi program Anda dikompilasi tanpa kesalahan, jalankan program Anda dengan perintah di bawah ini.

```bash
./isbn
```

Program Anda harus berperilaku seperti ini saat diberikan input ISBN-10 yang valid (tanpa tanda pemisah (-)); yang digarisbawahi adalah ketikan keyboard pengguna.

<pre>
$ <u>./isbn</u>
ISBN: <u>0789751984</u>
YES
</pre>

Tentu saja, `get_long("ISBN: ")` itu sendiri akan menolak tanda hubung (-) ISBN-10 (dan lebih banyak lagi):

<pre>
$ <u>./isbn</u>
ISBN: <u>0-789-75198-4</u>
ISBN: <u>foo</u>
ISBN: <u>0789751984</u>
YES
</pre>

Tetapi terserah kepada Anda untuk memberikan input yang bukan ISBN-10 (mis., nomor telepon [Sandy Canester](https://www.youtube.com/watch?v=lCqb3zDrtms)), meskipun panjangnya sepuluh digit.

<pre>
$ <u>./isbn</u>
ISBN: <u>6272777777</u>
NO
</pre>

{% next %}

## Pengujian

### Cara Menguji Kode Anda

Berikut adalah beberapa nilai yang dapat diperiksa:

* Beginners Guide (0789751984) valid
* Beginners Guide palsu (0789751985) invalid
* Programming in C (0321776410) valid
* Nomor Sandy Canester (6272777777) invalid

Apakah hasil Anda persis sama?

Uji program Anda dengan bermacam input, baik yang valid maupun yang tidak valid. Ada banyak ISBN-10 yang valid di gramedia.com.

{% next %}

### Ketepatan

Jalankan di bawah ini untuk mengevaluasi ketepatan kode Anda menggunakan `check50`. Tapi pastikan untuk mengkompilasi dan mengujinya sendiri juga!

```bash
check50 informatikasma/problems/2019/isbn
```

### Style

Jalankan di bawah ini untuk mengevaluasi gaya kode Anda menggunakan `style50`.

```bash
style50 isbn.c
```

{% next "Siap Mengirim?" %}

## Cara Mengirim

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```bash
submit50 informatikasma/problems/2019/isbn
```

Anda dapat mengulangi pengiriman sebanyak apapun yang Anda inginkan sebelum batas waktu pengumpulan.

Kiriman Anda akan dinilai kebenarannya dalam 2 menit, dimana skor Anda akan muncul di [https://submit.cs50.io](https://submit.cs50.io)!

Ini adalah ISBN.
