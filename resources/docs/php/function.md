[TOC]

# <b>02.</b> Fungsi dalam PHP

Dalam pengembangan web dengan PHP, terdapat banyak fungsi bawaan yang sangat bermanfaat untuk memanipulasi data, mengelola string, dan melakukan operasi lainnya.

### strlen()
Fungsi `strlen()` digunakan untuk menghitung jumlah karakter dalam sebuah string:
```php
<?php
$text = "Hello, World!";
$length = strlen($text); // Output: 13
?>
```

### strtolower() dan strtoupper()
Fungsi `strtolower()` digunakan untuk mengubah seluruh karakter dalam string menjadi huruf kecil, sementara strtoupper() digunakan untuk mengubah menjadi huruf besar:
```php
<?php
$text = "Hello, World!";
$lowercase = strtolower($text); // Output: "hello, world!"
$uppercase = strtoupper($text); // Output: "HELLO, WORLD!"
?>
```

### str_replace()
Fungsi `str_replace()` digunakan untuk mengganti semua kemunculan suatu string dengan string lain dalam sebuah string:
```php
<?php
$text = "Hello, World!";
$new_text = str_replace("Hello", "Hi", $text); // Output: "Hi, World!"
?>
```

### substr()
Fungsi `substr()` digunakan untuk mengambil sebagian dari string berdasarkan posisi awal dan panjang yang diinginkan:
```php
<?php
$text = "Hello, World!";
$substring = substr($text, 0, 5); // Output: "Hello"
?>
```

### explode() dan implode()
Fungsi `explode()` digunakan untuk memecah string menjadi array berdasarkan pemisah tertentu, sementara implode() digunakan untuk menggabungkan elemen array menjadi satu string dengan pemisah tertentu:
```php
<?php
$text = "apple,banana,orange";
$fruits_array = explode(",", $text); // Output: ["apple", "banana", "orange"]

$fruits_string = implode(", ", $fruits_array); // Output: "apple, banana, orange"
?>
```

### date()
Fungsi `date()` digunakan untuk mendapatkan tanggal dan waktu dalam format yang ditentukan:
```php
<?php
$date = date("Y-m-d"); // Output: "2023-08-01"
$time = date("H:i:s"); // Output: "10:30:45"
?>
```

### count()
Fungsi `count()` digunakan untuk menghitung jumlah elemen dalam array:
```php
<?php
$fruits = array("apple", "banana", "orange");
$jumlah_fruits = count($fruits); // Output: 3
?>
```

### empty()
Fungsi `empty()` digunakan untuk memeriksa apakah suatu variabel kosong atau tidak terdefinisi:
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
