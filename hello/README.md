# Hello

<!-- TODO Introduction Video

{% video https://www.youtube.com/watch?v=sxXQ-jgUIg8 %}

{% next %} -->

## Mendaftar File

Hello, world! Di sebelah kanan, di *text editor*, adalah program pertama yang kita tulis dalam C, dalam file bernama `hello.c`.

Klik ikon folder di pojok kanan atas, dan Anda akan melihat bahwa `hello.c` adalah satu-satunya file yang ada saat ini. Klik ikon folder lagi untuk menyembunyikan semuanya.

Selanjutnya, di *terminal window* di kanan bawah, segera di sebelah kanan tanda dolar (`$`), atau dikenal sebagai *prompt*, ketikkan persis di bawah ini (dalam huruf kecil), lalu tekan Enter:

```bash
ls
```

Anda hanya melihat `hello.c` saja? Itu karena Anda baru saja mendaftarkan file di folder yang sama, kali ini menggunakan *command-line interface* (CLI), hanya menggunakan keyboard Anda, dibandingkan dengan *graphical user interface* (GUI) yang diwakili oleh ikon folder tadi. Secara khusus, Anda *mengeksekusi* (menjalankan) perintah yang disebut `ls`, yang merupakan singkatan untuk *"list."* (Ini adalah perintah yang sering digunakan sehingga pembuatnya menyebutnya dengan hanya `ls` untuk menghemat pengetikan.) Masuk akal?

Di sini, untuk mengeksekusi (menjalankan) perintah berarti mengetikkannya ke jendela terminal dan kemudian tekan Enter. Perintah sifatnya *"case-sensitive"* (kapitalisasi berpengaruh), jadi pastikan untuk tidak mengetikkan huruf kapital ketika maksud Anda huruf kecil atau sebaliknya.

{% next %}

## Compiling Program

Sekarang, sebelum kita dapat menjalankan program di sebelah kanan, ingat bahwa kita harus melakukan *compile* dengan *compiler* (misalnya, `clang`), menerjemahkannya dari *source code* ke *machine code* (yaitu, nol dan satu). Jalankan perintah di bawah ini untuk melakukannya:

```bash
clang hello.c
```

Dan kemudian jalankan yang ini lagi:

```bash
ls
```

Kali ini, Anda seharusnya melihat tidak hanya `hello.c` tetapi` a.out` terdaftar juga. (Anda dapat melihat hal yang sama secara grafis jika Anda mengklik ikon folder tadi lagi.) Itu karena `clang` telah menerjemahkan *source code* di `hello.c` ke dalam *machine code* di `a.out`, yang kebetulan merupakan singkatan dari *"assembler output,"* tetapi kita akan bahas tentang itu lain kali.

Sekarang jalankan program dengan mengeksekusi di bawah ini.

```bash
./a.out
```

*Hello, world*, tentunya!

{% next %}

## Memberi Nama Program

Sekarang, `a.out` bukan nama yang paling *user-friendly* untuk suatu program. Mari kita kompilasi `hello.c` lagi, kali ini menyimpan *machine code* dalam sebuah file bernama, lebih tepatnya, `hello`. Jalankan di bawah ini.

```bash
clang -o hello hello.c
```

Berhati-hatilah untuk tidak mengabaikan penulisan spasi perintah tersebut! Kemudian jalankan yang ini lagi:

```bash
ls
```

Anda seharusnya sekarang tidak hanya melihat `hello.c` (dan `a.out` dari sebelumnya) tetapi juga `hello`. Itu karena `-o` adalah argumen *command-line*, kadang-kadang dikenal sebagai *flag* atau *switch*, yang memberitahu `clang` untuk menghasilkan *output* (makanya `o`) sebuah file bernama `hello`. Jalankan di bawah ini untuk mencoba program yang baru saja diberi nama.

```bash
./hello
```

*Hello* lagi!

{% next %}

## Membuat Segala Sesuatu Lebih Mudah

Ingatlah bahwa kita dapat mengotomasikan proses eksekusi `clang`, memberikan `make` tugas mencari cara untuk melakukannya untuk kita, dengan demikian kita dapat menghemat beberapa ketikan. Jalankan di bawah ini untuk mengkompilasi program ini untuk yang terakhir kalinya.

```bash
make hello
```

Anda seharusnya melihat bahwa `make` mengeksekusi `clang` dengan lebih banyak *command-line arguments* untuk Anda. Bahasannya lebih lanjut, juga, di kesempatan yang lain!

Sekarang jalankan program itu sendiri untuk terakhir kalinya dengan mengeksekusi di bawah ini.

```bash
./hello
```

Fiuh!

{% next %}

## Mendapatkan Input Pengguna

Bisa dikatakan, tidak peduli bagaimana Anda mengkompilasi atau menjalankan program ini, ia hanya akan mencetak `hello, world`. Mari kita sedikit mempersonalisasikannya, sama seperti yang kita lakukan di kelas.

Ubah program `hello.c` sedemikian rupa sehingga di awal meminta pengguna siapa nama mereka dan kemudian mencetak `hello, begini-dan-begitu`, di mana `begini-dan-begitu` adalah nama pengguna.

Seperti sebelumnya, pastikan untuk mengkompilasi program Anda dengan:

```bash
make hello
```

Dan pastikan untuk menjalankan program Anda, mengujinya beberapa kali dengan input berbeda, dengan:

```bash
./hello
```

<!-- TODO Walkthrough Video

### Panduan

{% video https://www.youtube.com/watch?v=Y3nWGvqt_Cg %} -->

{% spoiler "Solusi Pengajar" %}

Untuk mencoba implementasi pengajar dari masalah ini, jalankan

```bash
./hello
```

dalam [sandbox ini](http://bit.ly/2Qp0a2g).

{% endspoiler %}

### Petunjuk

#### Tidak ingat bagaimana cara meminta nama kepada pengguna?

Ingatlah bahwa Anda dapat menggunakan `get_string` sebagai berikut, menyimpan *return value* atau jawaban pengguna dalam variabel yang disebut `nama` dengan tipe `string`.

```c
string nama = get_string("What is your nama?\n");
```

#### Tidak ingat cara memformat `string`?

Tidak ingat bagaimana cara *join* (menyatukan) nama pengguna dengan sebuah salam? Ingatlah bahwa Anda dapat menggunakan `printf` tidak hanya untuk mencetak tetapi juga untuk memformat *string* (karenanya,`f` dalam `printf`), seperti di bawah ini, di mana `nama` adalah sebuah variabel bertipe `string`.

```c
printf("hello, %s\n", nama);
```

#### *Use of undeclared identifier?*

Melihat tulisan seperti berikut, mungkin di atas error-error lainnya?

```bash
error: use of undeclared identifier 'string'; did you mean 'stdin'?
```

Ingat bahwa, untuk menggunakan `get_string`, Anda harus menyertakan `cs50.h` (di mana `get_string` *dideklarasikan*) di atas file, seperti dengan:

```c
#include <cs50.h>
```

### Cara Menguji Kode Anda

Jalankan di bawah ini untuk mengevaluasi kebenaran kode Anda menggunakan `check50`. Tapi pastikan untuk mengkompilasi dan mengujinya oleh Anda sendiri juga!

```bash
check50 informatikasma/problems/2019/hello
```

Jalankan di bawah ini untuk mengevaluasi gaya kode Anda menggunakan `style50`.

```bash
style50 hello.c
```

{% next "Siap Mengirim?" %}

## Cara Mengirim

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```bash
submit50 informatikasma/problems/2019/hello
```

Anda dapat mengulangi pengiriman sebanyak apapun yang Anda inginkan sebelum batas waktu pengumpulan.

Kiriman Anda akan dinilai kebenarannya dalam 2 menit, pada saat itu skor Anda akan muncul di [https://submit.cs50.io](https://submit.cs50.io)!

Ini adalah Hello.
