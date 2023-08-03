[TOC]

# <b>06.</b> Command Line

Command Line, atau sering disebut Terminal atau Command Prompt, adalah sebuah antarmuka teks yang memungkinkan pengguna untuk berinteraksi dengan sistem operasi melalui baris perintah.

> **Note**
> Jika sebelumnya Anda sudah install Laragon untuk setup perangkat. Laragon menyertakan aplikasi Terminal untuk menjalankan `command`.

### Menampilkan Direktori Saat Ini

Untuk menampilkan direktori saat ini, Anda bisa menggunakan perintah `pwd` (print working directory):
```shell
$ pwd
/home/user/documents
```


### Menampilkan Daftar File dan Direktori

Untuk melihat daftar file dan direktori di direktori saat ini, gunakan perintah `ls` (list):

```shell
$ ls
file1.txt file2.txt folder1 folder2
```


### Pindah ke Direktori Lain

Untuk berpindah ke direktori lain, gunakan perintah `cd` (change directory):
```shell
$ cd documents
```


### Membuat Direktori Baru

Untuk membuat direktori baru, gunakan perintah `mkdir` (make directory):

```shell
$ mkdir project_folder
```


### Membuat File Baru

Untuk membuat file baru, gunakan perintah `touch`:

```shell
$ touch new_file.txt
```


### Menghapus File

Untuk menghapus file, gunakan perintah `rm` (remove):

```shell
$ rm unwanted_file.txt
```

### Menghapus Direktori

Untuk menghapus direktori kosong, gunakan perintah `rmdir` (remove directory):

```shell
$ rmdir empty_folder
```

Untuk menghapus direktori beserta isi di dalamnya, gunakan perintah `rm` dengan opsi `-r` (recursive):

```shell
$ rm -r folder_to_remove
```


### Menampilkan Isi File

Untuk melihat isi dari sebuah file teks, gunakan perintah `cat`:

```shell
$ cat sample.txt
```


### Mengganti Nama File atau Direktori

Untuk mengganti nama file atau direktori, gunakan perintah `mv` (move):

```shell
$ mv old_name.txt new_name.txt
```


### Menyalin File atau Direktori

Untuk menyalin file atau direktori, gunakan perintah `cp` (copy):

```shell
$ cp source_file.txt destination_folder/
```


### Mencari Teks dalam File

Untuk mencari teks dalam file, gunakan perintah `grep`:

```shell
$ grep "keyword" file.txt
```


### Menampilkan Bantuan Perintah

Jika Anda membutuhkan bantuan mengenai suatu perintah, gunakan opsi `-h` atau `--help` setelah perintah:

```js
$ ls --help
```


### Keluar dari Terminal

Untuk keluar dari Terminal, gunakan perintah `exit`:

```js
$ exit
```

Selamat mencoba dan semoga tutorial dasar Command Line ini bermanfaat!


[Lanjut ke Git...](/basic/git)
