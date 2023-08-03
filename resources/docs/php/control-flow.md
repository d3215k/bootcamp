[TOC]

# <b>10.</b> Control Flow

Control flow adalah konsep dalam pemrograman yang mengatur urutan eksekusi dari pernyataan-pernyataan dalam kode. Dengan kontrol alur, Anda dapat mempengaruhi bagaimana kode dieksekusi berdasarkan kondisi tertentu atau pengulangan.

Dalam PHP, terdapat beberapa struktur kontrol yang umum digunakan:

1. Struktur Pemilihan (if, else, dan elseif)
2. Struktur Pengulangan (for, while, dan do-while)
3. Struktur Pemilihan Berganda (switch)

## Struktur Pemilihan (if, else, dan elseif)
Struktur pemilihan digunakan untuk memeriksa kondisi tertentu dan menjalankan blok kode yang sesuai berdasarkan kondisi tersebut.

```php
<?php
$nilai = 80;

if ($nilai >= 80) {
    echo "Nilai Anda A";
} elseif ($nilai >= 70) {
    echo "Nilai Anda B";
} elseif ($nilai >= 60) {
    echo "Nilai Anda C";
} else {
    echo "Nilai Anda D";
}
?>
```

### Ternary Operator
Ternary operator adalah operator khusus dalam PHP yang digunakan untuk menyederhanakan pernyataan `if...else`. Ternary operator memungkinkan Anda untuk menulis pernyataan kondisional dalam satu baris kode.

Struktur Ternary Operator:
```php
(condition) ? true_expression : false_expression;
```

Jika kondisi di dalam tanda kurung condition bernilai true, maka true_expression akan dieksekusi. Jika kondisi bernilai false, maka false_expression akan dieksekusi.

```php
<?php
$umur = 20;

// Menggunakan if...else
if ($umur >= 18) {
    $status = "Dewasa";
} else {
    $status = "Remaja";
}

echo $status; // Output: "Dewasa"
?>

<?php
$umur = 15;

// Menggunakan ternary operator
$status = ($umur >= 18) ? "Dewasa" : "Remaja";
echo $status; // Output: "Remaja"
?>
```

Dalam contoh pertama, kita menggunakan pernyataan `if...else` untuk menentukan apakah seseorang dewasa atau remaja berdasarkan usia. Sedangkan dalam contoh kedua, kita menggunakan ternary operator untuk melakukan hal yang sama dalam satu baris kode.

Ternary operator sangat berguna ketika Anda ingin menetapkan nilai variabel berdasarkan kondisi sederhana dan tidak memerlukan blok kode yang rumit untuk pernyataan `if...else`. Namun, perlu diingat untuk tidak terlalu memaksa penggunaan ternary operator jika kondisi menjadi terlalu kompleks, karena dapat mengurangi keterbacaan kode. Gunakan ternary operator dengan bijaksana dalam situasi yang sesuai.

## Struktur Pengulangan (for, while, dan do-while)
Struktur pengulangan digunakan untuk mengulangi blok kode selama kondisi tertentu terpenuhi.

Contoh for:

```php
<?php
for ($i = 1; $i <= 5; $i++) {
    echo "Iterasi ke-$i <br>";
}
?>
```

Contoh while:
```php
<?php
$i = 1;
while ($i <= 5) {
    echo "Iterasi ke-$i <br>";
    $i++;
}
?>
```

Contoh do-while:
```php
<?php
$i = 1;
do {
    echo "Iterasi ke-$i <br>";
    $i++;
} while ($i <= 5);
?>
```

## Struktur Pemilihan Berganda (switch)
Struktur pemilihan berganda digunakan untuk memeriksa nilai ekspresi dan menjalankan blok kode yang sesuai berdasarkan nilai ekspresi tersebut.

```php
<?php
$day = "Senin";

switch ($day) {
    case "Senin":
        echo "Hari ini adalah Senin";
        break;
    case "Selasa":
        echo "Hari ini adalah Selasa";
        break;
    case "Rabu":
        echo "Hari ini adalah Rabu";
        break;
    default:
        echo "Hari ini adalah hari lain";
}
?>
```

Dengan struktur kontrol ini, Anda dapat mengendalikan alur eksekusi kode dalam PHP berdasarkan kondisi atau pengulangan tertentu. Kontrol alur sangat penting dalam membuat aplikasi yang dapat menangani berbagai situasi dan menjalankan tindakan yang sesuai. 

[Lanjut ke Array di PHP...](/php/array)
