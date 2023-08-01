[TOC]

# <b>02.</b> Basic PHP

## Pengantar untuk Pengenalan Mengenai PHP

PHP (Hypertext Preprocessor) adalah bahasa pemrograman server-side yang banyak digunakan untuk pengembangan web. PHP sangat populer karena mudah dipelajari dan didukung oleh berbagai platform dan server web. Dengan PHP, Anda dapat membuat halaman web dinamis yang berinteraksi dengan pengguna dan database.

### Server-Side Scripting

PHP adalah bahasa pemrograman server-side, yang berarti kode PHP dijalankan di sisi server, bukan di sisi klien (browser pengguna). Ketika pengguna mengakses halaman web yang mengandung kode PHP, server akan memproses kode tersebut dan mengirimkan hasilnya (HTML yang telah di-generate) ke browser pengguna. Hal ini memungkinkan Anda untuk melakukan banyak hal, seperti memperoleh data dari database, memproses formulir, dan menghasilkan konten dinamis di halaman web.

### Tag PHP

Kode PHP dikelompokkan dalam tag PHP yang memungkinkan interpreter PHP mengidentifikasi kode yang harus dieksekusi. Tag PHP dapat dimulai dengan `<?php` dan diakhiri dengan `?>`. Seluruh kode PHP ditempatkan di antara tag ini:

```php
<?php
// Kode PHP di sini
?>
```


### Menampilkan Teks ke Browser

Anda dapat mengeluarkan teks atau konten lainnya ke browser menggunakan fungsi `echo` atau `print`. Teks yang dieluarkan akan menjadi bagian dari respons yang dikirimkan ke browser pengguna.


```php
<?php
echo "Hello, World!";
?>
```


### Variabel dan Tipe Data

Anda dapat menggunakan variabel dalam PHP untuk menyimpan data. Variabel diawali dengan tanda `$` diikuti dengan nama variabel. PHP adalah bahasa pemrograman yang lemah tipe, yang berarti Anda tidak perlu mendeklarasikan tipe data variabel sebelum digunakan.

```php
<?php
$nama = "John Doe";
$umur = 30;
$tinggi = 175.5;
?>
```


### Komentar

Anda dapat menambahkan komentar dalam kode PHP untuk memberikan penjelasan atau dokumentasi. Komentar tidak akan dieksekusi oleh interpreter PHP.

```php
<?php
// Ini adalah komentar satu baris

/*
Ini adalah komentar
lebih dari satu baris
*/
?>
```


### Mengaitkan dengan HTML

Kode PHP dapat disisipkan di dalam dokumen HTML. Saat server memproses halaman web, kode PHP akan dijalankan dan menghasilkan konten dinamis yang akan ditampilkan di halaman web.

```php
<!DOCTYPE html>
<html>
<head>
    <title>Contoh Halaman PHP</title>
</head>
<body>
    <h1><?php echo "Selamat Datang di Website Kami!"; ?></h1>
</body>
</html>
```

[Lanjut ke Git...](/basic/git)
