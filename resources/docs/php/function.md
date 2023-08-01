[TOC]

# <b>02.</b> Function dalam PHP

Function dalam PHP adalah blok kode yang dapat didefinisikan sekali dan digunakan berulang kali dalam program. Function dapat membantu mengorganisasi kode menjadi bagian-bagian yang dapat digunakan kembali, sehingga memudahkan dalam pengelolaan dan perbaikan kode. Function juga dapat menerima argumen (input) dan mengembalikan nilai (output) setelah dieksekusi.

## Membuat Function di PHP
Berikut adalah contoh cara membuat function di PHP:

```php
<?php
// Function tanpa argumen dan return value
function helloWorld() {
    echo "Hello, World!";
}

// Function dengan argumen dan return value
function add($a, $b) {
    $result = $a + $b;
    return $result;
}

// Function dengan argumen default
function greet($name = "Guest") {
    echo "Hello, $name!";
}
?>
```

## Memanggil Function
Setelah Anda mendefinisikan function, Anda dapat memanggilnya dengan menggunakan nama function dan argumen (jika ada). Berikut adalah contoh memanggil function yang telah didefinisikan di atas:

```php
<?php
helloWorld(); // Output: "Hello, World!"

$sum = add(5, 3); // $sum berisi 8
echo $sum;

greet(); // Output: "Hello, Guest!"
greet("John"); // Output: "Hello, John!"
?>
```

## Function dengan Return Value
Function juga dapat mengembalikan nilai dengan menggunakan pernyataan return. Nilai yang dikembalikan oleh function dapat digunakan atau ditangkap oleh variabel di luar function.
```php
<?php
function add($a, $b) {
    $result = $a + $b;
    return $result;
}

$sum = add(5, 3);
echo $sum; // Output: 8
?>
```

## Function dengan Argumen Default
Function dapat memiliki argumen default. Jika argumen tidak diberikan saat memanggil function, maka nilai default akan digunakan.

```php
<?php
function greet($name = "Guest") {
    echo "Hello, $name!";
}

greet(); // Output: "Hello, Guest!"
greet("John"); // Output: "Hello, John!"
?>
```

Dengan function, Anda dapat menyederhanakan kode, memecah logika program menjadi bagian-bagian yang lebih terkelola, dan meningkatkan keterbacaan dan keterorganisasian kode Anda. Function merupakan fitur yang sangat berguna dalam pengembangan aplikasi PHP.

## Function bawaan PHP
Dalam pengembangan web dengan PHP, terdapat banyak Function bawaan yang sangat bermanfaat untuk memanipulasi data, mengelola string, dan melakukan operasi lainnya.

### strlen()
Function `strlen()` digunakan untuk menghitung jumlah karakter dalam sebuah string:
```php
<?php
$text = "Hello, World!";
$length = strlen($text); // Output: 13
?>
```

### strtolower() dan strtoupper()
Function `strtolower()` digunakan untuk mengubah seluruh karakter dalam string menjadi huruf kecil, sementara strtoupper() digunakan untuk mengubah menjadi huruf besar:
```php
<?php
$text = "Hello, World!";
$lowercase = strtolower($text); // Output: "hello, world!"
$uppercase = strtoupper($text); // Output: "HELLO, WORLD!"
?>
```

### str_replace()
Function `str_replace()` digunakan untuk mengganti semua kemunculan suatu string dengan string lain dalam sebuah string:
```php
<?php
$text = "Hello, World!";
$new_text = str_replace("Hello", "Hi", $text); // Output: "Hi, World!"
?>
```

### substr()
Function `substr()` digunakan untuk mengambil sebagian dari string berdasarkan posisi awal dan panjang yang diinginkan:
```php
<?php
$text = "Hello, World!";
$substring = substr($text, 0, 5); // Output: "Hello"
?>
```

### explode() dan implode()
Function `explode()` digunakan untuk memecah string menjadi array berdasarkan pemisah tertentu, sementara implode() digunakan untuk menggabungkan elemen array menjadi satu string dengan pemisah tertentu:
```php
<?php
$text = "apple,banana,orange";
$fruits_array = explode(",", $text); // Output: ["apple", "banana", "orange"]

$fruits_string = implode(", ", $fruits_array); // Output: "apple, banana, orange"
?>
```

### date()
Function `date()` digunakan untuk mendapatkan tanggal dan waktu dalam format yang ditentukan:
```php
<?php
$date = date("Y-m-d"); // Output: "2023-08-01"
$time = date("H:i:s"); // Output: "10:30:45"
?>
```

### count()
Function `count()` digunakan untuk menghitung jumlah elemen dalam array:
```php
<?php
$fruits = array("apple", "banana", "orange");
$jumlah_fruits = count($fruits); // Output: 3
?>
```

### empty()
Function `empty()` digunakan untuk memeriksa apakah suatu variabel kosong atau tidak terdefinisi:
```php
<?php
$nama = "John";
if (empty($nama)) {
    echo "Variabel kosong atau tidak terdefinisi.";
} else {
    echo "Variabel tidak kosong.";
}
?>
```

[Lanjut ke Git...](/basic/git)
