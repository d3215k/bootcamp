[TOC]

# <b>05.</b> Javascript

Setelah memahami dasar-dasar HTML dan CSS, saatnya untuk menambahkan interaktivitas ke halaman web Anda dengan menggunakan JavaScript. JavaScript adalah bahasa pemrograman yang kuat dan serbaguna, yang memungkinkan Anda untuk menangani peristiwa, memanipulasi elemen HTML, dan berkomunikasi dengan server untuk memberikan pengalaman yang dinamis kepada pengguna.

## Apa itu JavaScript

JavaScript adalah bahasa pemrograman yang berjalan di sisi klien (client-side) di browser pengguna. Ini memungkinkan Anda untuk mengendalikan perilaku dan interaksi elemen-elemen HTML di halaman web.

## Menyisipkan Skrip JavaScript

Anda dapat menyisipkan kode JavaScript di dalam elemen `<script>` di dalam elemen `<head>` atau `<body>` halaman HTML Anda.

```js
<script> // kode JavaScript Anda disini </script>
```

## Variabel dan Tipe Data

Dalam JavaScript, Anda dapat membuat variabel untuk menyimpan data. JavaScript memiliki beberapa tipe data seperti angka, string, boolean, array, dan objek.

```js
let nama = "John";
let umur = 30;
let statusMenikah = true;
```

## Komentar

Anda dapat menggunakan komentar dalam JavaScript untuk memberikan penjelasan atau catatan pada kode Anda. Komentar diawali dengan `//` untuk komentar satu baris atau diapit dengan `/* */` untuk komentar multi-baris.

## Event

JavaScript memungkinkan Anda menangani peristiwa yang terjadi di halaman web, seperti klik tombol, mengisi formulir, atau menggulir halaman.

```js
<button onclick="myFunction()">Klik Saya</button>
```

## Fungsi

Anda dapat membuat fungsi di JavaScript untuk menyimpan kode yang dapat dipanggil berulang kali.
Contoh: 
```js
function sapa(nama) {
    alert('Halo, ' + nama + '!');
}
```

## Manipulasi DOM (Document Object Model)

DOM adalah representasi struktur halaman web sebagai objek yang dapat diakses dan diubah oleh JavaScript. Anda dapat menggunakan JavaScript untuk memanipulasi elemen HTML, menambah atau menghapus elemen, mengubah konten, atau mengubah atribut elemen.

Contoh: 
```js
let judul = document.getElementById('judul-halaman');
judul.innerHTML = 'Halaman Baru';
```

## Penggunaan Kondisional

Anda dapat menggunakan pernyataan kondisional seperti `if`, `else`, dan `else if` untuk melakukan tindakan yang berbeda berdasarkan kondisi tertentu.

```js
let umur = 20;
if (umur >= 18) {
    console.log('Anda dewasa.');
} else {
    console.log('Anda masih anak-anak.');
}
```

## Looping

Looping memungkinkan Anda mengeksekusi blok kode berulang kali hingga kondisi tertentu terpenuhi.

```js
for (let i = 1; i <= 5; i++) {
    console.log('Nomor: ' + i);
}
```

Dengan memahami dasar-dasar JavaScript seperti di atas, Anda telah mempunyai gambaran untuk kedepannya memperkaya halaman web Anda dengan interaktivitas dan fungsionalitas yang menarik. JavaScript adalah bahasa pemrograman yang sangat penting dalam pengembangan web modern, dan Anda dapat mulai menggabungkannya dengan HTML dan CSS untuk menciptakan pengalaman web yang menakjubkan bagi pengguna.


[Lanjut ke Command Line...](/basic/cli)
