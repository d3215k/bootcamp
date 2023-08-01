[TOC]

# <b>02.</b> Array Dalam PHP

Array adalah salah satu tipe data yang penting dalam pemrograman. Dalam PHP, array adalah struktur data yang digunakan untuk menyimpan kumpulan nilai (elemen) dalam satu variabel. Setiap elemen dalam array memiliki indeks yang unik, yang digunakan untuk mengakses nilai tersebut.

Array sangat berguna ketika Anda perlu menyimpan dan mengelola data dalam jumlah banyak. Misalnya, Anda dapat menggunakan array untuk menyimpan daftar nama, nilai-nilai dari formulir, data dari database, dan sebagainya.

Dalam PHP, ada dua jenis array yang umum digunakan:
## Array Indeks
Array indeks adalah array yang indeksnya berupa angka yang dimulai dari nol (0) dan seterusnya. Elemen-elemen dalam array indeks diakses berdasarkan indeksnya. Untuk membuat array indeks, Anda dapat menggunakan sintaks berikut:
```php
$buah = array("apel", "jeruk", "pisang");
```

Anda juga dapat menggunakan sintaks pendek untuk membuat array indeks:

```php
$buah = ["apel", "jeruk", "pisang"];
```

## Array Asosiatif
Array asosiatif adalah array yang indeksnya berupa string atau nama kunci yang ditentukan oleh pengguna. Setiap elemen dalam array asosiatif memiliki pasangan kunci-nilai, di mana kunci berfungsi sebagai nama indeks dan nilai adalah nilai dari elemen tersebut. Untuk membuat array asosiatif, Anda dapat menggunakan sintaks berikut:
```php
$student = array(
    "nama" => "John Doe",
    "umur" => 25,
    "jurusan" => "Informatika"
);
```

Anda juga dapat menggunakan sintaks pendek untuk membuat array asosiatif:
```php
$student = [
    "nama" => "John Doe",
    "umur" => 25,
    "jurusan" => "Informatika"
];
```

[Lanjut ke Git...](/basic/git)
