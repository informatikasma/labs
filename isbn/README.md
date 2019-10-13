# ISBN

<!-- TODO Introduction Video

{% video https://www.youtube.com/watch?v=sxXQ-jgUIg8 %}

{% next %} -->

## Apa yang Harus Dilakukan

Terapkan program untuk memvalidasi nomor ISBN-10.

```bash
./isbn
ISBN: 0307476464
YES
```

{% next %}

Seperti yang Anda ketahui, sebagian besar buku apa pun yang Anda pinjam atau beli memiliki International Standard Book Number, atau dikenal sebagai __ISBN__ atau ISBN-10, ["angka 10 digit yang secara unik mengidentifikasi buku dan produk seperti buku yang diterbitkan secara internasional."](http://www.isbn.org/standards/home/isbn/us/isbnqa.asp) Buku-buku yang diterbitkan sejak 2007 mungkin juga memiliki ISBN-13, angka 13 digit dengan tujuan yang sama, tetapi abaikan saja dulu.

Ternyata digit terakhir ISBN-10 adalah *"check digit"*, atau dikenal (dalam konteks biner) sebagai *"checksum,"* nomor yang terkait secara matematis dengan digit sebelumnya. Digit ISBN-10 diharuskan mematuhi suatu formula, mirip nomor kartu kredit, dan *check digit* ini memungkinkan Anda untuk memeriksa apakah sembilan digit ISBN-10 lainnya (kemungkinan besar) valid tanpa harus memeriksa, katakanlah, database buku.

Menurut Manual Pengguna ISBN Badan Internasional ISBN, ["*Check digit* adalah digit terakhir dari ISBN. Ini dihitung pada modulus 11 dengan bobot 10-2, menggunakan X sebagai pengganti 10 jika sepuluh muncul sebagai *check digit*."](http://www.isbn-international.org/en/userman/download/ISBNmanual.pdf)

![Rly?](orly.jpg)

{% next %}

Yes rly, tapi apa maksudnya? Manual tersebut menguraikan. "Ini berarti bahwa masing-masing dari sembilan digit pertama ISBN&mdash;tidak termasuk digit periksa itu sendiri&mdash;dikalikan dengan angka mulai dari 10 hingga 2 dan bahwa jumlah produk yang dihasilkan, ditambah digit periksa, harus dapat dibagi dengan 11 tanpa sisa."

Oke, lebih baik, tapi masih agak tidak jelas. Mari kita tentukan digit periksa dalam bentuk rumus. Untungnya, berkat "aritmatika modular," kita dapat menyederhanakan definisi formal tadi menggunakan bobot mulai dari 1 hingga 9 bukannya 10 hingga 2. Sebenarnya benar-benar sangat sederhana. Jika x<sub>1</sub> mewakili digit pertama ISBN-10 dan x<sub>10</sub> yang terakhir, itu menunjukkan bahwa:

x<sub>10</sub> = (1·x<sub>1</sub> + 2·x<sub>2</sub> + 3·x<sub>3</sub> + 4·<sub>x4</sub> + 5·x<sub>5</sub> + 6·x<sub>6</sub> + 7·x<sub>7</sub> + 8·x<sub>8</sub> + 9·x<sub>9</sub>) mod 11

Dengan kata lain, untuk menghitung digit kesepuluh ISBN-10, kalikan digit pertama dengan 1, digit kedua dengan 2, digit ketiga dengan 3, digit keempat dengan 4, digit kelima dengan 5, digit keenam dengan 6, digit ketujuh dengan 7, digit kedelapan dengan 8, dan digit kesembilan oleh 9. Ambil jumlah dari produk-produk itu dan kemudian bagi dengan 11. Sisanya pembagiannya akan menjadi digit kesepuluh ISBN-10! Namun, jika sisanya 10, digit kesepuluh harus dicetak sebagai X agar tidak dikacaukan dengan angka 1 diikuti oleh 0.

{% next %}

Mari kita coba. ISBN-10 untuk *Absolute Beginner's Guide to C*, salah satu buku yang direkomendasikan mata pelajaran, adalah 0-789-75198-4, digit kesepuluhnya, tentu saja, 4. Tetapi apakah perhitungannya benar? Baiklah, mari kita hitung jumlahnya menggunakan sembilan digit pertama ISBN-10 (disorot dengan huruf tebal):

1·**0** + 2·**7** + 3·**8** + 4·**9** + 5·**7** + 6·**5** + 7·**1** + 8·**9** + 9·**8** = 290

Jika kita sekarang membagi jumlah itu dengan 11, kita mendapatkan 290 ÷ 11 = 26 sisa 4! Bagus sekali, ISBN itu sah! Sebenarnya, juga berkat aritmatika modular, kita bisa memasukkan digit kesepuluh itu ke dalam jumlah kita dan mengalikannya dengan 10:

1·**0** + 2·**7** + 3·**8** + 4·**9** + 5·**7** + 6·**5** + 7·**1** + 8·**9** + 9·**8** + 10·**4** = 330

Jika kita sekarang membagi jumlah ini dengan 11, kita mendapatkan 330 ÷ 11 = 30 tanpa sisa sama sekali, yang merupakan cara yang setara dengan mengatakan ISBN-10 itu sah! Dinyatakan lebih formal, 0 ≡ 330 (mod 11)!

Semoga poin seru tersebut membuat matematika lebih menarik.

Jadi, menghitung digit cek ini tidak sulit, tetapi sedikit membosankan dengan tangan. Mari kita menulis sebuah program.


{% next %}