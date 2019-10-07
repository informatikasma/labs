# Hello

## Mendaftar File

Hello, world! Di sebelah kanan, di *text editor*, adalah program pertama yang kita tulis dalam C, dalam file bernama `hello.c`.

Klik ikon folder di pojok kanan atas, dan Anda akan melihat bahwa `hello.c` adalah satu-satunya file yang ada saat ini. Klik ikon folder lagi untuk menyembunyikan semuanya.

Selanjutnya, di *terminal window* di kanan bawah, segera di sebelah kanan tanda dolar (`$`), atau dikenal sebagai *prompt*, ketikkan persis di bawah ini (dalam huruf kecil), lalu tekan Enter:

```
ls
```

Anda seharusnya melihat `hello.c` saja? Itu karena Anda baru saja mendaftarkan file di folder yang sama, kali ini menggunakan *command-line interface* (CLI), hanya menggunakan keyboard Anda, dibandingkan dengan *graphical user interface* (GUI) yang diwakili oleh ikon folder itu. Secara khusus, Anda *mengeksekusi* (mis., menjalankan) perintah yang disebut `ls`, yang merupakan singkatan untuk *"list."* (Ini adalah perintah yang sering digunakan sehingga penulisnya menyebutnya hanya `ls` untuk menghemat penekanan tombol.) Masuk akal?

Di sini, untuk mengeksekusi (mis., menjalankan) perintah berarti mengetikkannya ke jendela terminal dan kemudian tekan Enter. Perintah sifatnya *"case-sensitive"* (kapitalisasi berpengaruh), jadi pastikan untuk tidak mengetikkan huruf kapital ketika maksud Anda huruf kecil atau sebaliknya.

{% next %}

## Compiling Program

Sekarang, sebelum kita dapat menjalankan program di sebelah kanan, ingat bahwa kita harus melakukan *compile* dengan *compiler* (misalnya, `clang`), menerjemahkannya dari *source code* ke *machine code* (yaitu, nol dan satu). Jalankan perintah di bawah ini untuk melakukannya:

```
clang hello.c
```

Dan kemudian jalankan yang ini lagi:

```
ls
```

Kali ini, Anda seharusnya melihat tidak hanya `hello.c` tetapi` a.out` terdaftar juga? (Anda dapat melihat hal yang sama secara grafis jika Anda mengklik ikon folder itu lagi.) Itu karena `clang` telah menerjemahkan *source code* di` hello.c` ke dalam *machine code* di `a.out`, yang kebetulan merupakan singkatan dari *"assembler output,"* tetapi kita akan bahas tentang itu lain kali.

Sekarang jalankan program dengan mengeksekusi di bawah ini.

```
./a.out
```

*Hello, world*, tentunya!

{% next %}

## Memberi Nama Program

Sekarang, `a.out` bukan nama yang paling *user-friendly* untuk suatu program. Mari kita kompilasi `hello.c` lagi, kali ini menyimpan *machine code* dalam sebuah file bernama, lebih tepatnya,` hello`. Jalankan di bawah ini.

```
clang -o hello hello.c
```

Berhati-hatilah untuk tidak mengabaikan penulisan spasi tersebut! Kemudian jalankan yang ini lagi:

```
ls
```

Anda seharusnya sekarang tidak hanya melihat `hello.c` (dan` a.out` dari sebelumnya) tetapi juga `hello` terdaftar juga? Itu karena `-o` adalah argumen *command-line*, kadang-kadang dikenal sebagai *flag* atau *switch*, yang memberitahu` clang` untuk menghasilkan *output* (makanya `o`) sebuah file bernama` hello`. Jalankan di bawah ini untuk mencoba program yang baru saja diberi nama.

```
./hello
```

*Hello* lagi!

{% next %}

## Membuat Segala Sesuatu Lebih Mudah

Ingatlah bahwa kita dapat mengotomasikan proses mengeksekusi `clang`, memberikan `make` tugas mencari cara untuk melakukannya bagi kita, dengan demikian kita dapat menghemat beberapa ketikan. Jalankan di bawah ini untuk mengkompilasi program ini untuk yang terakhir kalinya.

```
make hello
```

Anda seharusnya melihat bahwa `make` mengeksekusi `clang` dengan lebih banyak *command-line arguments* untuk Anda? Bahasannya lebih lanjut, juga, di kesempatan lain!

Sekarang jalankan program itu sendiri untuk terakhir kalinya dengan mengeksekusi di bawah ini.

```
./hello
```

Fiuh!

## Mendapatkan Input Pengguna

Bisa dikatakan, tidak peduli bagaimana Anda mengkompilasi atau menjalankan program ini, ia hanya akan mencetak `hello, world`. Mari kita sedikit mempersonalisasikannya, sama seperti yang kita lakukan di kelas.

Ubah program ini sedemikian rupa sehingga di awal meminta pengguna siapa nama mereka dan kemudian mencetak `hello, begini-dan-begitu`, di mana `begini-dan-begitu` adalah nama sebenarnya.

Seperti sebelumnya, pastikan untuk mengkompilasi program Anda dengan:

```
make hello
```

Dan pastikan untuk menjalankan program Anda, mengujinya beberapa kali dengan input berbeda, dengan:

```
./hello
```

### Solusi Pengajar

Untuk mencoba implementasi pengajar dari masalah ini, jalankan

```
./hello
```

dalam [sandbox ini](http://bit.ly/2Qp0a2g).

### Petunjuk

#### Tidak ingat bagaimana cara meminta nama kepada pengguna?

Ingatlah bahwa Anda dapat menggunakan `get_string` sebagai berikut, menyimpan *return value* dalam variabel yang disebut `nama` dari tipe `string`.

```c
string name = get_string("What is your name?\n");
```

#### Tidak ingat cara memformat `string`?

Tidak ingat bagaimana cara *join* (mis., menyatukan) nama pengguna dengan sebuah salam? Ingatlah bahwa Anda dapat menggunakan `printf` tidak hanya untuk mencetak tetapi juga untuk memformat *string* (karenanya,`f` dalam `printf`), seperti di bawah ini, di mana `name` adalah `string`.

```c
printf("hello, %s\n", name);
```

#### *Use of undeclared identifier?*

Melihat tulisan seperti berikut, mungkin di atas error-error lainnya?

```
error: use of undeclared identifier 'string'; did you mean 'stdin'?
```

Ingat bahwa, untuk menggunakan `get_string`, Anda harus menyertakan `cs50.h` (di mana `get_string` *dideklarasikan*) di atas file, seperti dengan:

```c
#include <cs50.h>
```

### Cara Menguji Kode Anda

Jalankan di bawah ini untuk mengevaluasi kebenaran kode Anda menggunakan `check50`. Tapi pastikan untuk mengkompilasi dan mengujinya oleh Anda sendiri juga!

```
check50 cs50/problems/2019/fall/hello
```

Jalankan di bawah ini untuk mengevaluasi gaya kode Anda menggunakan `style50`.

```
style50 hello.c
```

{% next %}

## Cara Mengirim

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```
submit50 informatikasma/problems/2019/hello
```
