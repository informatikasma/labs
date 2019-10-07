# Hello

## Mendaftar File

Hello, world! Di sebelah kanan, di *text editor*, adalah program pertama yang kita tulis dalam C, dalam file bernama `hello.c`.

Klik ikon folder di pojok kanan atas, dan Anda akan melihat bahwa `hello.c` adalah satu-satunya file yang ada saat ini. Klik ikon folder lagi untuk menyembunyikan semuanya.

Selanjutnya, di *terminal window* di kanan bawah, segera di sebelah kanan tanda dolar (`$`), atau dikenal sebagai *prompt*, ketikkan persis di bawah ini (dalam huruf kecil), lalu tekan Enter:

```
ls
```

Anda seharusnya melihat `hello.c` saja? Itu karena Anda baru saja mendaftarkan file di folder yang sama, kali ini menggunakan *command-line interface* (CLI), hanya menggunakan keyboard Anda, dibandingkan dengan *graphical user interface* (GUI) yang diwakili oleh ikon folder itu. Secara khusus, Anda *mengeksekusi* (mis., menjalankan) perintah yang disebut `ls`, yang merupakan singkatan untuk "*list*." (Ini adalah perintah yang sering digunakan sehingga penulisnya menyebutnya hanya `ls` untuk menghemat penekanan tombol.) Masuk akal?

Di sini, untuk mengeksekusi (mis., menjalankan) perintah berarti mengetikkannya ke jendela terminal dan kemudian tekan Enter. Perintah sifatnya "*case-sensitive*" (kapitalisasi berpengaruh) jadi pastikan untuk tidak mengetikkan huruf kapital ketika maksud Anda huruf kecil atau sebaliknya.

{% next %}

## Compiling Programs

Now, before we can execute the program at right, recall that we must *compile* it with a *compiler* (e.g., `clang`), translating it from *source code* into *machine code* (i.e., zeroes and ones). Execute the command below to do just that:

```
clang hello.c
```

And then execute this one again:

```
ls
```

This time, you should see not only `hello.c` but `a.out` listed as well? (You can see the same graphically if you click that folder icon again.) That's because `clang` has translated the source code in `hello.c` into machine code in `a.out`, which happens to stand for "assembler output," but more on that another time.

Now run the program by executing the below.

```
./a.out
```

Hello, world, indeed!

{% next %}

## Naming Programs

Now, `a.out` isn't the most user-friendly name for a program. Let's compile `hello.c` again, this time saving the machine code in a file called, more aptly, `hello`. Execute the below.

```
clang -o hello hello.c
```

Take care not to overlook any of those spaces therein! Then execute this one again:

```
ls
```

You should now see not only `hello.c` (and `a.out` from before) but also `hello` listed as well? That's because `-o` is a *command-line argument*, sometimes known as a *flag* or a *switch*, that tells `clang` to output (hence the `o`) a file called `hello`. Execute the below to try out the newly named program.

```
./hello
```

Hello there again!

{% next %}

## Making Things Easier

Recall that we can automate the process of executing `clang`, letting `make` figure out how to do so for us, thereby saving us some keystrokes. Execute the below to compile this program one last time.

```
make hello
```

You should see that `make` executes `clang` with even more command-line arguments for you? More on those, too, another time!

Now execute the program itself one last time by executing the below.

```
./hello
```

Phew!

## Getting User Input

Suffice it to say, no matter how you compile or execute this program, it only ever prints `hello, world`. Let's personalize it a bit, just as we did in class.

Modify this program in such a way that it first prompts the user for their name and then prints `hello, so-and-so`, where `so-and-so` is their actual name.

As before, be sure to compile your program with:

```
make hello
```

And be sure to execute your program, testing it a few times with different inputs, with:

```
./hello
```

### Staff's Solution

To try out the staff's implementation of this problem, execute

<pre>
./hello
</pre>

within [this sandbox](http://bit.ly/2Qp0a2g).

### Walkthrough

{% video https://www.youtube.com/watch?v=wSk1KSDUEYA %}

### Hints

#### Don't recall how to prompt the user for their name?

Recall that you can use `get_string` as follows, storing its *return value* in a variable called `name` of type `string`.

```c
string name = get_string("What is your name?\n");
```

#### Don't recall how to format a string?

Don't recall how to join (i.e., concatenate) the user's name with a greeting? Recall that you can use `printf` not only to print but to format a string (hence, the `f` in `printf`), a la the below, wherein `name` is a `string`.

```c
printf("hello, %s\n", name);
```

#### Use of undeclared identifier?

Seeing the below, perhaps atop other errors?

```
error: use of undeclared identifier 'string'; did you mean 'stdin'?
```

Recall that, to use `get_string`, you need to include `cs50.h` (in which `get_string` is *declared*) atop a file, as with:

```c
#include <cs50.h>
```

### How to Test Your Code

Execute the below to evaluate the correctness of your code using `check50`. But be sure to compile and test it yourself as well!

```
check50 cs50/problems/2019/fall/hello
```

Execute the below to evaluate the style of your code using `style50`.

```
style50 hello.c
```

{% next %}

## How to Submit

Execute the below, logging in with your GitHub username and password when prompted. For security, you'll see asterisks (`*`) instead of the actual characters in your password.

```
submit50 cs50/problems/2019/fall/hello
```
