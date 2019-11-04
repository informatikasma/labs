# Mario

## World 1-1

Menjelang akhir *World 1-1* di Super Mario Brothers Nintendo, Mario harus naik piramida balok yang menanjak ke kanan, a la di bawah.

![tangkapan layar Mario melompati piramida yang menanjak ke kanan](pyramid.png)

Mari kita buat ulang piramida itu di C, meskipun dalam teks, menggunakan hashes (`#`) untuk batu bata, a la di bawah ini.

```
       #
      ##
     ###
    ####
   #####
  ######
 #######
########
```

Program yang akan kita tulis akan disebut `mario`. Supaya lebih menarik, kita izinkan pengguna untuk memutuskan seberapa tinggi piramida dimana program kita hanya menerima bilangan bulat positif antara, katakanlah, 1 dan 8, inklusif.

Begini contoh program bekerja jika pengguna memasukkan `8` saat diminta:

<pre>
$ <u>./mario</u>
Tinggi: <u>8</u>
       #
      ##
     ###
    ####
   #####
  ######
 #######
########
</pre>

Begini contoh program bekerja jika pengguna memasukkan `4` saat diminta:

<pre>
$ <u>./mario</u>
Tinggi: <u>4</u>
   #
  ##
 ###
####
</pre>

Begini contoh program bekerja jika pengguna memasukkan `2` saat diminta:

<pre>
$ <u>./mario</u>
Tinggi: <u>2</u>
 #
##
</pre>

Dan begini contoh program bekerja jika pengguna memasukkan `1` saat diminta:

<pre>
$ <u>./mario</u>
Tinggi: <u>1</u>
#
</pre>

Jika pengguna tidak memasukkan bilangan bulat positif antara 1 dan 8, inklusif, ketika diminta, program harus meminta kembali pengguna sampai mereka bekerja sama:

<pre>
$ <u>./mario</u>
Tinggi: <u>-1</u>
Tinggi: <u>0</u>
Tinggi: <u>42</u>
Tinggi: <u>50</u>
Tinggi: <u>4</u>
   #
  ##
 ###
####
</pre>

Bagaimana memulainya? Mari kita mendekati masalah ini selangkah demi selangkah.

{% video https://youtu.be/Hi1KAN3jjuY %}

{% next %}

## Pseudocode

Pertama, tuliskan dalam `pseudocode.txt` di sebelah kanan beberapa pseudocode yang mengimplementasikan program ini, walaupun tidak (belum!) yakin bagaimana cara menuliskannya dalam kode. Tidak ada cara yang tepat untuk menulis pseudocode, tetapi kalimat bahasa Indonesia yang singkat sudah cukup.

Ingatlah bagaimana kita menulis pseudocode untuk menemukan Ucup. Kemungkinan pseudocode Anda akan menggunakan (atau Seakan menggunakan!) satu atau lebih fungsi, kondisi, ekspresi Boolean, loop, dan/atau variabel.

{% spoiler %}

Ada lebih dari satu cara untuk melakukan ini, ini hanya salah satunya!

1. Minta input pengguna berupa tinggi
2. Jika tinggi kurang dari 1 atau lebih dari 8 (atau bukan integer sama sekali), kembali ke tahap satu.
3. Ulangi dari 1 sampai tinggi:
    1. Untuk pengulangan *i*, cetak *i* pagar kemudian baris baru

Tidak masalah untuk mengedit sendiri setelah melihat pseudocode di sini, tetapi jangan hanya menyalin / menempelkan kode kami ke kode Anda sendiri!

{% endspoiler %}

{% next %}

## Struktur Dasar Program

Sebelum memulai, buatlah struktur dasar yang Anda perlukan dalam membuat program dalam bahasa C. Seperti yang Anda lihat di sebelah kanan, file `mario.c` masih kosong.

{% spoiler %}

Ingat bahwa kode yang kita buat harus dimasukkan dalam fungsi `main`.

```c
int main(void)
{

}
```

Kode Anda nantinya akan dituliskan di antara tanda kurung kurawal `{` dan `}`.

Anda juga mungkin harus memuat header `stdio.h`. Gunakan sintak berikut di bagian paling atas kode Anda.

```c
#include <stdio.h>
```

{% endspoiler %}

## Meminta Input

Apa pun pseudocode Anda, pertama-tama mari kita tuliskan hanya kode C yang meminta (dan meminta kembali, sesuai kebutuhan) pengguna untuk input.

Mintalah input pengguna, kemudian lakukan validasi untuk mengecek apakah bilangan yang dimasukkan oleh pengguna merupakan bilangan positif antara 1 dan 8, inklusif. Kemudian langsung cetak nilai variabel tersebut untuk memastikan (oleh diri Anda sendiri) bahwa Anda memang berhasil memvalidasi input pengguna, seperti di bawah ini.

<pre>
$ <u>./mario</u>
Tinggi: <u>-1</u>
Tinggi: <u>42</u>
Tinggi: <u>50</u>
Tinggi: <u>4</u>
Tersimpan: <u>4</u>
</pre>

{% spoiler "Petunjuk" %}

* Ingat bahwa Anda dapat mengkompilasi program Anda dengan `make`.
* Ingat bahwa Anda dapat mencetak `int` dengan` printf` menggunakan `%i`.
* Ingat bahwa Anda bisa mendapatkan integer dari pengguna dengan `get_int`.
* Ingat bahwa `get_int` ada dalam header `cs50.h`.
* Ingat bahwa kita meminta pengguna untuk bilangan bulat positif di kelas melalui [`positive.c`](https://sandbox.cs50.io/b56865fd-c861-425f-aad7-4adcf6831139).

{% endspoiler %}

## Membangun Kebalikannya

Sekarang program Anda (semoga!) menerima input seperti yang ditentukan, sekarang saatnya untuk langkah selanjutnya.

Ternyata sedikit lebih mudah untuk membangun piramida rata kiri daripada rata kanan, a la di bawah ini.

```
#
##
###
####
#####
######
#######
########
```

Jadi mari kita membangun piramida rata kiri terlebih dahulu dan kemudian, setelah itu berfungsi, rata kanan kan saja!

Modifikasi `mario.c` di kanan sedemikian rupa sehingga tidak lagi hanya mencetak input pengguna tetapi mencetak piramida rata kiri dengan ketinggian yang sesuai input pengguna.

{% spoiler "Petunjuk" %}

* Perlu diingat bahwa *hash* hanyalah karakter seperti yang lain, sehingga Anda dapat mencetaknya dengan `printf`.
* Sama seperti Scratch memiliki blok Repeat, begitu juga C memiliki loop `for`, di mana Anda dapat melakukan pengulangan beberapa kali. Mungkin pada setiap iterasi (pengulangan), *i*, Anda bisa mencetak hash dengan jumlah *i*?
* Loop Anda sebenarnya dapat "beranak", iterasi (pengulangan) dengan satu variabel (mis., `i`) di loop "luar" dan lainnya (mis., `j`) di loop "dalam". Sebagai contoh, ini adalah cara Anda mencetak balok persegi dengan tinggi dan lebar `n`, di bawah. Tentu saja, itu bukan piramida yang inginkan!

    ```
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            printf("#");
        }
        printf("\n");
    }
    ```

{% endspoiler %}

{% next %}

## Merata-kanan-kan dengan Titik

Sekarang mari kita buat piramida itu menjadi rata kanan dengan mendorong hashnya, tiap barisnya diawali menggunakan titik-titik, a la di bawah ini.

```
.......#
......##
.....###
....####
...#####
..######
.#######
########
```

Ubah `mario.c` sedemikian rupa sehingga dapat melakukan hal itu!

{% spoiler "Petunjuk" %}

Perhatikan bagaimana jumlah titik yang dibutuhkan pada setiap baris adalah "kebalikan" dari jumlah hash baris tersebut. Untuk piramida dengan tinggi 8, seperti di atas, baris pertama hanya memiliki 1 hash dan dengan demikian 7 titik. Baris terbawah, sementara itu, memiliki 8 hash dan dengan demikian 0 titik. Melalui rumus apa (atau aritmatika, sebenarnya) yang memungkinkan Anda mencetak titik sebanya itu?

{% endspoiler %}

### Cara Menguji Kode Anda

Apakah kode Anda berfungsi seperti yang ditentukan saat Anda input

* `-1` (atau angka negatif lainnya)?
* `0`?
* `1` hingga` 8`?
* `9` atau angka positif lainnya?
* huruf atau kata-kata?
* tidak ada input sama sekali, ketika Anda hanya menekan Enter?

{% next %}

## Menghapus Titik-titik

Yang tersisa sekarang hanyalah hiasan akhir! Ubah `mario.c` sedemikian rupa sehingga ia mencetak spasi alih-alih titik-titik itu!

## Pengujian
### Ketepatan

Jalankan di bawah ini untuk mengevaluasi ketepatan kode Anda menggunakan `check50`. Tapi pastikan untuk mengkompilasi dan mengujinya sendiri juga!

```
check50 informatikasma/problems/2019/mario
```

### Style

Jalankan di bawah ini untuk mengevaluasi gaya kode Anda menggunakan `style50`.

```
style50 mario.c
```

{% next %}

## How to Submit

Jalankan di bawah ini, masuk dengan nama pengguna dan kata sandi GitHub Anda saat diminta. Untuk keamanan, Anda akan melihat tanda bintang (`*`) alih-alih karakter sebenarnya dalam kata sandi Anda.

```bash
submit50 informatikasma/problems/2019/mario
```

Anda dapat mengulangi pengiriman sebanyak apapun yang Anda inginkan sebelum batas waktu pengumpulan.

Kiriman Anda akan dinilai kebenarannya dalam 2 menit, dimana skor Anda akan muncul di [https://submit.cs50.io](https://submit.cs50.io)!

Ini adalah Mario.