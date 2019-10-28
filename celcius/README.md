# Celcius

## Awal yang Dingin

Di masa lalu, jika Anda ingin tahu suhu di luar ruangan, Anda harus melihat salah satu yang seperti ini, yang mungkin dipasang di luar di rumah Anda.

![Thermometer](thermometer.png)

Sebelum adanya alat tersebut, jika Anda ingin tahu suhu di luar, Anda harus berdiri di luar. Sekarang ini, cukup  membuka aplikasi cuaca di ponsel Anda atau mengunjungi situs web pelaporan cuaca untuk mendapatkan suhu saat ini dan ramalan lima hari kedepan. Tidak perlu dipusingkan dengan lingkarang angka di atas atau saudaranya, tabung merkuri.

Bergantung pada tempat Anda tinggal di dunia, negara Anda menggunakan salah satu dari dua skala suhu utama. Di hampir setiap negara di dunia, termasuk Indonesia, Anda mungkin paling akrab dengan skala Celcius, dan jika Anda mendengar bahwa suhu di luar 30&deg; Anda mungkin akan mencari-cari pakaian renang di lemari pakaian Anda dan mengenakan tabir surya, karena ini adalah hari pantai yang indah. Pada skala Celcius, 0&deg; adalah titik beku air, dan 100&deg; adalah titik didih.

{% next %}

Jika Anda tinggal di Amerika Serikat (dan tidak menghabiskan sebagian besar hari Anda bekerja di laboratorium sains), kemungkinan Anda terbiasa dengan skala Fahrenheit. Dalam hal ini, jika Anda mendengar bahwa suhu di luar 30&deg; Anda mungkin mengenakan mantel tebal dan celana hangat dan memepersiapkan diri untuk kemungkinan turunnya salju, karena suhu tersebut berarti cukup dingin, mengingat titik beku air adalah 32&deg;. Di sisi lain, air tidak akan mendidih sebelum mencapai 212&deg;.

Memang dengan sebagian besar aplikasi yang memberikan Anda laporan cuaca, cukup mudah untuk menekan tombol pilihan yang mengubah tampilan suhu dari Celsius ke Fahrenheit (atau sebaliknya), tetapi sebelum proses itu diotomatiskan untuk kita, orang harus menghafal sebagian titik konversi yang lebih umum atau harus menggunakan rumus matematika untuk mengkonversi dari satu skala ke skala lain, yang akan sangat dibutuhkan jika Anda berencana bepergian ke Amerika.

Untuk masalah ini, kita akan fokus pada konversi hanya dalam satu arah: _dari_ Fahrenheit _ke_ Celcius. Rumus untuk konversi ini tidak terlalu rumit. (Fiuh!) Seseorang cukup mengambil suhu saat ini dalam derajat Fahrenheit (&deg;F), menguranginya dengan 32, mengalikannya dengan 5, dan kemudian membaginya dengan 9. Hasilnya adalah suhu setara dalam derajat Celcius (&deg;C). Tidak sulit kan? Untuk yang lebih senang visual, cara tersebut dapat diterjemahkan ke dalam rumus ini:

```
C = (F - 32) * 5 / 9
```

Perlu diketaui, orang Amerika Serikat, dan juga komputer, menyatakan tanda desimal dengan simbol titik. Maka untuk sementara kita akan menggunakan tanda titik sebagai pembatas desimal.

Mari kita lakukan tes singkat untuk memastikan semuanya berjalan seperti yang diharapkan. Orang-orang di Amerika Serikat tahu suhu tubuh manusia normal adalah 98.6&deg;F (perhatikan tanda titik yang digunakan sebagai pembatas desimal). Jika kita memasukkan "98.6" ke dalam rumus menggantikan &deg;F dan melakukan perhitungan (98.6 dikurangi 32 adalah 66.6, 66.6 dikalikan dengan 5 adalah 333, 333 dibagi 9 adalah 37) kita mendapatkan 37&deg;C yang bagi orang-orang di seluruh dunia tahu bahwa itu suhu tubuh manusia normal. Jadi itu benar. Demikian pula jika kita memasukkan 32&deg;F (titik beku air) ke dalam formula yang dikonversi menjadi 0&deg;C, dan 212&deg;F (titik didih air) tampaknya setara dengan 100&deg;C. Sepertinya semuanya berjalan dengan baik.

{% next %}

## Semakin Hangat

Tulis program yang mengubah suhu dalam Fahrenheit menjadi Celcius, sesuai dengan sampel *output* di bawah ini, di mana teks yang digarisbawahi menunjukkan *input* pengguna.

<pre>
$ <u>./celcius</u>
F: <u>212</u>
C: 100.0
</pre>

## Pseudocode

Pertama, tulis di pseudocode.txt di sebelah kanan beberapa *pseudocode* yang mengimplementasikan program ini, walaupun tidak (belum!) yakin bagaimana cara menuliskannya dalam kode.

Kemungkinan *pseudocode* Anda akan menggunakan (atau seakan menggunakan!) satu atau lebih fungsi, operator, dan variabel.

{% spoiler %}

Ada lebih dari satu cara untuk melakukan ini, dan ini hanya salah satunya saja!

0. Minta pada pengguna suhu dalam Fahrenheit dan simpan ke sebuah variabel
1. Gunakan nilai tadi untuk menghitung derajat Celcius dan simpan dalam variabel lain
2. Cetak hasilnya

Tidak masalah untuk mengedit sendiri setelah melihat *pseudocode* di sini, tetapi jangan hanya menyalin / menempelkan kode ini ke kode Anda sendiri!

{% endspoiler %}

{% next %}

Apa pun *pseudocode* Anda, pertama-tama mari kita tuliskan hanya kode C yang meminta (dan meminta kembali, sesuai kebutuhan) pengguna untuk *input*.

Pertama, deklarasikan variabel floating point baru untuk menyimpan derajat Fahrenheit.

Ingat bahwa jika Anda memasukkan `<cs50.h>` di atas file `celcius.c` Anda, Anda akan memiliki akses ke fungsi yang disebut `get_float`, yang akan memungkinkan pengguna untuk memasukkan nilai *floating-point* (angka dengan titik desimal di dalamnya, juga dikenal sebagai __bilangan riil__). Parameter fungsi *get* akan menampilkan *prompt* pada pengguna.

Sekarang pastikan untuk menetapkan nilai fungsi input ini ke variabel Fahrenheit baru Anda.

Nyatakan *float* lain untuk menampung derajat Celcius, dan tetapkan hasil dari rumus konversi suhu (ada di atas).

Terakhir, cetak hasilnya dengan presisi satu tempat desimal.

{% spoiler "hint" %}

Printf dapat digunakan untuk menentukan berapa banyak tempat setelah titik desimal yang ingin Anda tampilkan kepada pengguna. Misalnya untuk mencetak *float* dengan 2 tempat desimal, ketikkan:

```c
printf("%.2f\n", number);
```

Dapatkah Anda melihat mengapa kode di atas akan mencetak 2 tempat desimal? Sekarang sesuaikan untuk mencetak derajat Celcius (jangan lupa untuk memulai keluaran dengan "C: ") tepat satu tempat desimal.

{% endspoiler %}

### Panduan

{% video https://www.youtube.com/watch?v=bVTp3vINuxk %}

### Solusi Pengajar

Untuk mencoba implementasi pengajar dari masalah ini, jalankan

```
./celcius
```

dalam [sandbox ini](http://bit.ly/2W3uR1t).

{% next %}

### Cara Menguji Kode Anda

Jalankan di bawah ini untuk mengevaluasi kebenaran kode Anda menggunakan `check50`. Tapi pastikan untuk mengkompilasi dan mengujinya oleh Anda sendiri juga!

{% spoiler "Lupa cara compile?" %}

Lupa cara menkompilasi sendiri kode Anda?

```bash
make celcius
```

Kemudian jalankan program Anda dengan mengetikkan nama program Anda, seperti:

```bash
./celcius
```

Selalu uji program Anda secara mandiri sebelum menggunakan `check50`!

{% endspoiler %}

```
check50 informatikasma/problems/2019/celcius
```

Jika Anda mendapatkan beberapa pesan kesalahan dan wajah merah sedih, tak perlu khawatir. Anda hanya perlu melakukan *debugging*, mencari letak kesalahan kemudian memperbaikinya.

Jalankan di bawah ini untuk mengevaluasi gaya kode Anda menggunakan `style50`.

```
style50 celcius.c
```

Blok merah berarti menghilangkan spasi, blok hijau berarti menambahkan spasi.

{% next "Siap Mengirim?" %}

## Cara Mengirim

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```bash
submit50 informatikasma/problems/2019/celcius
```

Anda dapat mengulangi pengiriman sebanyak apapun yang Anda inginkan sebelum batas waktu pengumpulan.

Kiriman Anda akan dinilai kebenarannya dalam 2 menit, pada saat itu skor Anda akan muncul di https://submit.cs50.io!

Ini adalah Celcius.