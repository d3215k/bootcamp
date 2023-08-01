[TOC]

# <b>02.</b> Operator dalam PHP

Operator adalah simbol-simbol yang digunakan untuk melakukan operasi matematika, perbandingan, atau logika dalam pemrograman. Dalam PHP, terdapat berbagai jenis operator yang dapat Anda gunakan untuk melakukan berbagai tugas.

## Operator Aritmatika
Operator aritmatika digunakan untuk melakukan operasi matematika dasar seperti penjumlahan, pengurangan, perkalian, pembagian, dan sebagainya.

```php
<?php
$angka1 = 10;
$angka2 = 5;

$penjumlahan = $angka1 + $angka2; // Output: 15
$pengurangan = $angka1 - $angka2; // Output: 5
$perkalian = $angka1 * $angka2; // Output: 50
$pembagian = $angka1 / $angka2; // Output: 2
$sisa_bagi = $angka1 % $angka2; // Output: 0 (tidak ada sisa bagi)
?>
```

## Operator Assignment
Operator penugasan digunakan untuk memberikan nilai pada variabel.

```php
<?php
$nilai = 10; // Penugasan nilai 10 pada variabel $nilai
$nama = "John"; // Penugasan nilai "John" pada variabel $nama
?>
```

## Operator Perbandingan
Operator perbandingan digunakan untuk membandingkan nilai dari dua ekspresi.
```php
<?php
$angka1 = 10;
$angka2 = 5;

$hasil1 = $angka1 > $angka2; // Output: true (benar)
$hasil2 = $angka1 < $angka2; // Output: false (salah)
$hasil3 = $angka1 == $angka2; // Output: false (salah)
$hasil4 = $angka1 != $angka2; // Output: true (benar)
?>
```

## Operator Logika
Operator logika digunakan untuk menggabungkan atau membalikkan hasil dari ekspresi logika.
```php
<?php
$nilai1 = true;
$nilai2 = false;

$hasil1 = $nilai1 && $nilai2; // Output: false (salah)
$hasil2 = $nilai1 || $nilai2; // Output: true (benar)
$hasil3 = !$nilai1; // Output: false (salah)
?>
```

## Operator Increment dan Decrement
Operator increment dan decrement digunakan untuk menambah atau mengurangi nilai variabel dengan satu.

```php
<?php
$angka = 5;

$angka++; // Penambahan satu (increment), nilai menjadi 6
$angka--; // Pengurangan satu (decrement), nilai menjadi 5 kembali
?>
```

## Operator String Concatenation
Operator string concatenation (penggabung string) digunakan untuk menggabungkan dua atau lebih string.

```php
<?php
$nama_depan = "John";
$nama_belakang = "Doe";

$nama_lengkap = $nama_depan . " " . $nama_belakang; // Output: "John Doe"
?>
```

[Lanjut ke Git...](/basic/git)
